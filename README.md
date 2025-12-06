<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Para Mi Único Amor, Mi Princesa 👑</title>

    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@400;700&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">

    <style>
        /* --- VARIABLES DE DISEÑO --- */
        :root {
            --primary-color: #ff6f91; /* Rosa vibrante (Corazones, Títulos) */
            --secondary-color: #ff9aa2; /* Rosa suave (Caja de frases) */
            --accent-color: #f7a2a7; /* Rosa más intenso para brillo */
            --text-color: #4a4a4a;
            --light-text-color: #777;
            --bg-gradient-start: #ffebeb;
            --bg-gradient-end: #fddbdf;
            --box-shadow-light: 0 8px 25px rgba(0, 0, 0, 0.1);
            --box-shadow-hover: 0 12px 35px rgba(0, 0, 0, 0.15);
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, var(--bg-gradient-start) 0%, var(--bg-gradient-end) 100%);
            color: var(--text-color);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
            box-sizing: border-box;
            overflow-x: hidden;
            position: relative;
        }

        /* --- ANIMACIÓN DE FONDO (Corazones y Estrellas) --- */
        .background-animation {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            overflow: hidden;
            pointer-events: none;
            z-index: 0;
            opacity: 0.8;
        }
        .background-animation span {
            position: absolute;
            opacity: 0;
            animation: floatUp 15s infinite ease-in;
            background-size: contain;
            background-repeat: no-repeat;
        }
        .background-animation span.star {
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="%23ffffff"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.25l-6.18 3.25L7 14.14l-5-4.87 6.91-1.01L12 2z"/></svg>');
            width: 25px;
            height: 25px;
        }
        .background-animation span.heart {
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="%23ff4d4d"><path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/></svg>');
            width: 30px;
            height: 30px;
        }
        @keyframes floatUp {
            0% { transform: translateY(100vh) scale(0); opacity: 0; }
            10% { opacity: 0.8; }
            100% { transform: translateY(-100px) scale(1.2); opacity: 0; }
        }

        /* --- CONTENEDOR PRINCIPAL --- */
        .container {
            background-color: white;
            padding: 40px;
            border-radius: 25px;
            box-shadow: var(--box-shadow-light);
            max-width: 700px;
            width: 100%;
            text-align: center;
            position: relative;
            z-index: 1;
        }

        /* --- TÍTULOS Y CORAZÓN PULSANTE --- */
        h1 {
            font-family: 'Dancing Script', cursive;
            color: var(--primary-color);
            font-size: 3.5em;
            margin-bottom: 5px;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        h1 span {
            font-size: 0.8em;
            margin-left: 10px;
            color: #ff4d4d;
            animation: pulse 2s infinite alternate ease-in-out;
            display: inline-block;
        }
        @keyframes pulse {
            from { transform: scale(1); }
            to { transform: scale(1.1); }
        }
        h2 {
            font-family: 'Poppins', sans-serif;
            color: var(--primary-color);
            margin-top: 0;
            font-weight: 400;
            font-size: 1.5em;
        }

        /* --- SECCIÓN SNOOPY (IMAGEN GRANDE) --- */
        .snoopy-section {
            margin: 30px 0;
            position: relative;
        }
        .snoopy-section img {
            max-width: 90%;
            height: auto;
            border-radius: 15px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
            transition: transform 0.5s ease;
        }
        .snoopy-section img:hover {
            transform: scale(1.05);
        }
        .snoopy-section p {
            font-family: 'Dancing Script', cursive;
            font-size: 1.8em;
            color: var(--primary-color);
            margin-top: 20px;
        }

        /* --- FRASE INTERACTIVA CON EFECTO DE RESPLANDOR --- */
        .frase-box {
            background-color: var(--secondary-color);
            color: white;
            padding: 25px;
            border-radius: 18px;
            margin: 30px auto;
            cursor: pointer;
            transition: all 0.3s ease;
            max-width: 80%;
            position: relative;
            box-shadow: 0 0 10px var(--secondary-color), var(--box-shadow-light);
            animation: glow 3s infinite alternate;
        }
        @keyframes glow {
            from { box-shadow: 0 0 10px var(--accent-color), 0 0 20px var(--secondary-color); }
            to { box-shadow: 0 0 15px var(--primary-color), 0 0 25px var(--secondary-color); }
        }
        .frase-box:hover {
            transform: translateY(-8px) scale(1.02);
            box-shadow: 0 0 20px var(--primary-color), var(--box-shadow-hover);
        }
        .frase-box p {
            font-family: 'Dancing Script', cursive;
            font-size: 1.6em;
            margin: 0;
        }

        /* --- COSAS QUE ADORO DE TI (Con Emojis Estables) --- */
        .gustos h3 {
            font-family: 'Dancing Script', cursive;
            color: var(--primary-color);
            font-size: 2.5em;
            margin-top: 50px;
            margin-bottom: 25px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .gustos h3::before, .gustos h3::after {
            content: '✨';
            margin: 0 10px;
            font-size: 0.8em;
        }

        .gustos-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 20px;
            margin-top: 30px;
        }
        @media (min-width: 550px) {
            .gustos-grid {
                grid-template-columns: 1fr 1fr;
            }
        }
        .gusto-item {
            background-color: #fff0f3;
            padding: 15px;
            border-radius: 15px;
            text-align: left;
            display: flex;
            align-items: center;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
            transition: all 0.3s ease;
        }
        .gusto-item:hover {
            transform: scale(1.05);
            background-color: #ffcccc;
        }
        /* Estilo de los Emojis/Iconos que reemplazan las imágenes pequeñas */
        .gusto-item .gusto-icon {
            font-size: 2.5em; /* Tamaño grande para que parezca una imagen */
            line-height: 1;
            margin-right: 15px;
            flex-shrink: 0;
            width: 60px;
            text-align: center;
        }
        .gusto-item p {
            font-size: 1.1em;
            margin: 0;
            color: var(--text-color);
            line-height: 1.4;
        }

        .footer-text {
            font-size: 1em;
            color: var(--light-text-color);
            margin-top: 40px;
            padding-top: 20px;
            border-top: 1px dashed var(--secondary-color);
        }
    </style>
</head>
<body>

<div class="background-animation"></div>

<div class="container">
    <h1>¡Hola, Mi Vida! <span class="material-icons">favorite</span></h1>
    <h2>Te amo mi princesa</h2>

    <div class="snoopy-section">
        <img src="https://i.ibb.co/spLzN8HF/Whats-App-Image-2025-12-06-at-4-45-41-PM.jpg" alt="Snoopy con Corazón">
        <p>Con todo mi amor, tu novio. ❤️</p>
    </div>

    <hr style="border: 0; border-top: 1px dashed var(--secondary-color); margin: 30px auto; width: 80%;">

    <div class="frase-box" id="fraseBox">
        <p id="fraseTexto">Haz clic aquí para que te diga algo bonito. 😊</p>
    </div>
    <p class="frase-instruction">Toca el recuadro que brilla para leer otra frase.</p>

    <hr style="border: 0; border-top: 1px dashed var(--secondary-color); margin: 30px auto; width: 80%;">

    <div class="gustos">
        <h3>✨ Cosas que Adoro de Ti ✨</h3>
        <div class="gustos-grid">

            <div class="gusto-item">
                <span class="gusto-icon">⭐</span>
                <p>Tu sonrisa, que ilumina mis días.</p>
            </div>

            <div class="gusto-item">
                <span class="gusto-icon">🎶</span>
                <p>Tu voz, que es mi canción favorita.</p>
            </div>

            <div class="gusto-item">
                <span class="gusto-icon">💖</span>
                <p>La forma en que me haces sentir especial.</p>
            </div>

            <div class="gusto-item">
                <span class="gusto-icon">☕</span>
                <p>Nuestras pláticas juntas, mi momento favorito.</p>
            </div>

            <div class="gusto-item">
                <span class="gusto-icon">💡</span>
                <p>Tus ideas y la forma en que ves el mundo.</p>
            </div>

            <div class="gusto-item">
                <span class="gusto-icon">🌙</span>
                <p>Acurrucarme contigo es mi lugar seguro.</p>
            </div>
        </div>
    </div>

    <p class="footer-text">Con Amor, Tu Novio. 💖</p>
</div>

<script>
    const frases = [
        "Eres el sol que le hacía falta a mi universo.",
        "Mi lugar favorito en el mundo es a tu lado.",
        "Cada día contigo es mi día favorito.",
        "Tu voz es mi canción de cuna favorita.",
        "Si el amor fuera un viaje, contigo sería un vuelo sin escalas.",
        "Eres mi persona, mi hoy y mi para siempre.",
        "No necesito soñar, porque ya te tengo a ti.",
        "Tu risa es la melodía más hermosa que he escuchado.",
        "Eres la razón por la que creo en los cuentos de hadas.",
        "Contigo, cada momento es una aventura.",
        "Mi corazón te eligió y no se equivocó."
    ];

    let indiceActual = 0;
    const fraseBox = document.getElementById('fraseBox');
    const fraseTexto = document.getElementById('fraseTexto');

    function cambiarFrase() {
        if (fraseTexto.textContent.includes("Haz clic aquí")) {
             indiceActual = Math.floor(Math.random() * frases.length);
        }

        fraseTexto.textContent = frases[indiceActual];
        indiceActual = (indiceActual + 1) % frases.length;
    }

    fraseBox.addEventListener('click', cambiarFrase);


    // --- Script para la animación de fondo ---
    const backgroundAnimation = document.querySelector('.background-animation');
    const numParticles = 60;

    function createParticle() {
        const particle = document.createElement('span');
        const type = Math.random() > 0.5 ? 'star' : 'heart';
        particle.classList.add(type);

        particle.style.left = `${Math.random() * 100}%`;
        particle.style.animationDuration = `${Math.random() * 8 + 7}s`;
        particle.style.animationDelay = `${Math.random() * numParticles * 0.2}s`;
        particle.style.transform = `scale(${Math.random() * 0.6 + 0.4})`;

        backgroundAnimation.appendChild(particle);

        particle.addEventListener('animationend', () => {
            particle.remove();
        });
    }

    for (let i = 0; i < numParticles; i++) {
        createParticle();
    }
    setInterval(createParticle, 300);
</script>
</body>
</html>
