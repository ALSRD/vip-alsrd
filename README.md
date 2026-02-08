<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>ALSRD VIP</title>
    <style>
        :root { --azul: #003366; --dorado: #d4af37; }
        * { box-sizing: border-box; margin: 0; padding: 0; }
        html, body { height: 100%; overflow: hidden; background: #f4f4f9; }
        body { display: flex; flex-direction: column; font-family: sans-serif; }
        .header { background: var(--azul); color: white; padding: 15px; border-bottom: 3px solid var(--dorado); flex-shrink: 0; }
        .messages { flex: 1; overflow-y: auto; background: #e5ddd5; padding: 15px; display: flex; flex-direction: column; }
        .bot { background: white; padding: 10px; border-radius: 10px; margin-bottom: 10px; align-self: flex-start; border-left: 4px solid var(--dorado); max-width: 85%; font-size: 14px; }
        .user { background: #d1e7dd; padding: 10px; border-radius: 10px; margin-bottom: 10px; align-self: flex-end; max-width: 85%; font-size: 14px; }
        .input-area { background: white; padding: 15px; display: flex; border-top: 1px solid #ccc; flex-shrink: 0; }
        input { flex: 1; padding: 12px; border: 1px solid #ccc; border-radius: 20px; font-size: 16px; outline: none; }
        button { background: var(--azul); color: white; border: none; padding: 10px 15px; margin-left: 10px; border-radius: 50%; font-size: 18px; }
        .plan-card { background: #fff; padding: 10px; margin: 5px 0; border: 1px solid #ddd; border-left: 4px solid var(--dorado); border-radius: 5px; cursor: pointer; }
        .wa-btn { display: block; background: #25D366; color: white; text-align: center; padding: 12px; border-radius: 8px; text-decoration: none; font-weight: bold; margin-top: 10px; }
    </style>
</head>
<body>
    <div class="header"><b>ALSRD • Maestro</b></div>
    <div class="messages" id="chatBox"></div>
    <div class="input-area">
        <input type="text" id="userInput" placeholder="Escribe 'Hola'...">
        <button onclick="sendMessage()">➤</button>
    </div>
<script>
    const planes = [
        { n: 'VIP EXTRA', p: '5,000' }, { n: 'VIP GOLD', p: '10,000' }, { n: 'VIP SIMPLE', p: '3,000' },
        { n: 'SOLO ANGUILAS', p: '1,800' }, { n: 'SOLO PALES', p: '4,500' }, { n: 'FIN DE SEMANA', p: '1,500' }
    ];
    const box = document.getElementById('chatBox');
    const input = document.getElementById('userInput');
    function msg(txt, type) {
        const d = document.createElement('div'); d.className = type; d.innerHTML = txt;
        box.appendChild(d); box.scrollTop = box.scrollHeight;
    }
    function sendMessage() {
        const val = input.value.trim(); if(!val) return;
        msg(val, 'user'); input.value = '';
        setTimeout(() => {
            msg("¡Hola! Toca un plan para ver detalles:", 'bot');
            let h = ""; planes.forEach(p => { h += `<div class="plan-card" onclick="ver('${p.n}','${p.p}')">${p.n} - RD$${p.p}</div>`; });
            msg(h, 'bot');
        }, 500);
    }
    window.ver = (n, p) => {
        msg(`Elegí ${n}`, 'user');
        setTimeout(() => {
            msg(`<b>${n}</b><br>Precio: RD$${p}<br><br>🏦 <b>César Saviñón:</b><br>Popular: 807385729<br>BHD: 17071310013`, 'bot');
            msg(`<a href="https://wa.me/18493182005?text=Elegí el ${n}" class="wa-btn">✅ PAGAR AHORA</a>`, 'bot');
        }, 500);
    }
    window.onload = () => msg("👋 ¡Hola! Escribe <b>'Hola'</b> para empezar.", "bot");
</script>
</body>
</html>
