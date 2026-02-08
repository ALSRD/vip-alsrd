<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>ALSRD - Asistente VIP</title>
    <style>
        :root { --azul: #003366; --dorado: #d4af37; --fondo: #f4f4f9; }
        * { box-sizing: border-box; }
        body { font-family: 'Segoe UI', sans-serif; background-color: var(--fondo); margin: 0; padding: 0; height: 100vh; height: -webkit-fill-available; display: flex; flex-direction: column; overflow: hidden; }
        .header { background: linear-gradient(135deg, var(--azul) 0%, #001f3f 100%); color: white; padding: 12px; display: flex; align-items: center; border-bottom: 4px solid var(--dorado); flex-shrink: 0; }
        .header-icon { background: var(--dorado); width: 40px; height: 40px; border-radius: 50%; margin-right: 12px; display: flex; align-items: center; justify-content: center; color: var(--azul); font-weight: 900; }
        .messages { flex: 1; padding: 15px; overflow-y: auto; background-color: #e5ddd5; display: flex; flex-direction: column; }
        .message { margin-bottom: 12px; padding: 12px; border-radius: 12px; max-width: 85%; font-size: 14px; line-height: 1.4; position: relative; }
        .bot { background: white; align-self: flex-start; border-left: 4px solid var(--dorado); border-radius: 0 12px 12px 12px; }
        .user { background: #d1e7dd; align-self: flex-end; border-right: 4px solid var(--azul); border-radius: 12px 0 12px 12px; }
        .plan-card { background: #fff; padding: 10px; margin: 6px 0; border-radius: 8px; border: 1px solid #ddd; cursor: pointer; border-left: 4px solid var(--dorado); }
        .input-area { padding: 10px; background: #fff; display: flex; border-top: 1px solid #ccc; flex-shrink: 0; padding-bottom: calc(10px + env(safe-area-inset-bottom)); }
        input { flex: 1; padding: 12px 15px; border: 1px solid #bbb; border-radius: 25px; outline: none; font-size: 16px; /* Evita zoom en iPhone */ }
        button#mainSend { background: var(--azul); color: white; border: none; padding: 10px 15px; margin-left: 8px; border-radius: 50%; cursor: pointer; font-size: 18px; }
        .wa-btn { display: block; background: #25D366; color: white; text-decoration: none; padding: 12px; border-radius: 8px; text-align: center; margin-top: 10px; font-weight: bold; border-bottom: 3px solid #128C7E; }
        .confirm-btns { display: flex; flex-direction: column; gap: 6px; margin-top: 10px; }
        .btn-opt { padding: 10px; border-radius: 6px; border: none; cursor: pointer; font-weight: bold; color: white; text-align: center; }
    </style>
</head>
<body>
    <div class="header">
        <div class="header-icon">#</div>
        <div><h1 style="font-size: 14px; margin: 0;">ALSRD • Maestro de los Números</h1><span style="font-size: 10px;">Asistente Comercial Oficial</span></div>
    </div>
    <div class="messages" id="chatBox"></div>
    <div class="input-area">
        <input type="text" id="userInput" placeholder="Escribe un mensaje..." autocomplete="off">
        <button id="mainSend" onclick="sendMessage()">➤</button>
    </div>

<script>
    const planesVIP = [
        { id: 1, nombre: 'VIP EXTRA', precio: '5,000', desc: '15 días. Loterías Nacionales y Leidsa.' },
        { id: 2, nombre: 'VIP GOLD', precio: '10,000', desc: '1 mes. Nacionales cada 3 días.' },
        { id: 3, nombre: 'VIP SIMPLE', precio: '3,000', desc: 'Según ciclo activo.' },
        { id: 4, nombre: 'SOLO ANGUILAS', precio: '1,800', desc: 'Cada 3 días.' },
        { id: 5, nombre: 'OFERTA SOLO PALES', precio: '4,500', desc: '15 días.' },
        { id: 6, nombre: 'FIN DE SEMANA', precio: '1,500', desc: 'Vie-Sab-Dom (1 palé + 2 fuertes).' },
        { id: 7, nombre: 'NY Y FLORIDA', precio: '2,000', desc: '15 días.' },
        { id: 8, nombre: 'SOLO PAREJAS', precio: '500', desc: '2 y 3 parejas.' },
        { id: 9, nombre: 'EL QUE MÁS SALE', precio: '15,000', desc: '1 semana (Lun-Lun).' },
        { id: 10, nombre: 'PALÉ SÁBADOS', precio: '1,000', desc: 'Solo sábados.' },
        { id: 11, nombre: 'UN SOLO MIÉRCOLES', precio: '1,000', desc: 'Solo miércoles.' }
    ];

    const chatBox = document.getElementById('chatBox');
    const userInput = document.getElementById('userInput');

    function addMessage(text, type) {
        const div = document.createElement('div');
        div.className = `message ${type}`;
        div.innerHTML = text;
        chatBox.appendChild(div);
        chatBox.scrollTop = chatBox.scrollHeight;
    }

    function sendMessage() {
        const text = userInput.value.trim();
        if(!text) return;
        addMessage(text, 'user');
        userInput.value = '';
        
        setTimeout(() => {
            if(text.toLowerCase().includes('hola') || text.toLowerCase().includes('si')) {
                addMessage("¡Excelente! Aquí tienes nuestros planes VIP. Toca el que te interese:", 'bot');
                let cat = "";
                planesVIP.forEach(p => {
                    cat += `<div class="plan-card" onclick="verPlan(${p.id})"><b>${p.nombre}</b> - RD$${p.precio}</div>`;
                });
                addMessage(cat, 'bot');
            }
        }, 800);
    }

    window.verPlan = function(id) {
        const p = planesVIP.find(x => x.id === id);
        addMessage(`Elegí ${p.nombre}`, 'user');
        setTimeout(() => {
            addMessage(`<b>${p.nombre}</b><br>💰 RD$${p.precio}<br>📝 ${p.desc}<br><br>🏦 <b>César Saviñón:</b><br>Popular: 807385729<br>BHD: 17071310013<br>Reservas: 9605441241`, 'bot');
            addMessage(`<a href="https://wa.me/18493182005?text=Hola, elegí el ${p.nombre}" class="wa-btn">✅ ENVIAR BAUCHE AHORA</a>`, 'bot');
        }, 600);
    }

    window.onload = () => addMessage("👋 Hola, soy el asistente de ALSRD. Escribe <b>'Hola'</b> para ver los planes.", 'bot');
    userInput.addEventListener("keypress", (e) => { if(e.key === "Enter") sendMessage(); });
</script>
</body>
</html>
