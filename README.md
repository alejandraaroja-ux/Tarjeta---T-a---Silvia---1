# Tarjeta---T-a---Silvia---1
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Tarjeta para Tía Silvia</title>

<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #111, #222);
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    text-align: center;
    overflow: hidden;
}

#cover {
    cursor: pointer;
}

#card {
    display: none;
    position: relative;
    animation: fadeIn 1.5s ease;
}

img {
    max-width: 90vw;
    max-height: 90vh;
    border-radius: 15px;
    box-shadow: 0 0 25px rgba(0,0,0,0.7);
}

@keyframes fadeIn {
    from { opacity: 0; transform: scale(0.8); }
    to { opacity: 1; transform: scale(1); }
}

/* Stickers */
.sticker {
    position: absolute;
    font-size: 40px;
    animation: float 3s infinite ease-in-out;
}

.ball1 { top: 10%; left: 5%; }
.ball2 { bottom: 10%; right: 5%; }
.ball3 { top: 20%; right: 10%; }

@keyframes float {
    0% { transform: translateY(0px) rotate(0deg); }
    50% { transform: translateY(-20px) rotate(20deg); }
    100% { transform: translateY(0px) rotate(0deg); }
}

/* Canvas */
#basketCanvas {
    position: fixed;
    top: 0;
    left: 0;
    pointer-events: none;
}
</style>
</head>

<body>

<canvas id="basketCanvas"></canvas>

<div id="cover" onclick="showCard()">
    <h1>🎉 Para Mi Tía Silvia 🎉</h1>
    <p>(Haz clic para ver tu sorpresa)</p>
</div>

<div id="card">
    <img src="card.jpg" alt="Tarjeta de cumpleaños">

    <div class="sticker ball1">🏀</div>
    <div class="sticker ball2">🏀</div>
    <div class="sticker ball3">🏀</div>
</div>

<script>
function showCard() {
    document.getElementById('cover').style.display = 'none';
    document.getElementById('card').style.display = 'block';
}

/* BALONES */
const canvas = document.getElementById('basketCanvas');
const ctx = canvas.getContext('2d');

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let balls = [];

for (let i = 0; i < 25; i++) {
    balls.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        size: Math.random() * 25 + 20,
        speedY: Math.random() * 3 + 2,
        speedX: (Math.random() - 0.5) * 2
    });
}

function drawBall(x, y, size) {
    ctx.font = size + "px Arial";
    ctx.fillText("🏀", x, y);
}

function update() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    balls.forEach(b => {
        b.y += b.speedY;
        b.x += b.speedX;

        // Rebote en el suelo
        if (b.y > canvas.height) {
            b.y = canvas.height;
            b.speedY *= -0.7;
        }

        // Gravedad
        b.speedY += 0.1;

        drawBall(b.x, b.y, b.size);
    });

    requestAnimationFrame(update);
}

update();
</script>

</body>
</html>
