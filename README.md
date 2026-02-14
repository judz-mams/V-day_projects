<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Valentines Surprise</title>
<style>
    body {
        margin: 0;
        padding: 0;
        font-family: Arial, sans-serif;
        background: linear-gradient(135deg, #ff4e50, #fc913a);
        overflow: hidden;
        text-align: center;
        color: white;
    }

    h1 {
        margin-top: 100px;
        font-size: 40px;
        animation: pulse 1.5s infinite;
    }

    @keyframes pulse {
        0% { transform: scale(1); }
        50% { transform: scale(1.1); }
        100% { transform: scale(1); }
    }

    .buttons {
        margin-top: 40px;
        position: relative;
    }

    button {
        padding: 15px 30px;
        font-size: 18px;
        border: none;
        border-radius: 30px;
        cursor: pointer;
        transition: 0.3s;
        position: absolute;
    }

    #yesBtn {
        background-color: #00ff88;
        left: 40%;
    }

    #noBtn {
        background-color: #ff0033;
        left: 55%;
    }

    .hidden {
        display: none;
    }

    #fireworks {
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        pointer-events: none;
    }

    .center {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }

    .error {
        font-size: 50px;
        color: black;
    }

</style>
</head>
<body>

<h1 id="question">Can you be my Valentines? 💖</h1>

<div class="buttons">
    <button id="yesBtn">YES ❤️</button>
    <button id="noBtn">NO 💀</button>
</div>

<canvas id="fireworks" class="hidden"></canvas>

<div id="result" class="hidden center"></div>

<script>
const noBtn = document.getElementById("noBtn");
const yesBtn = document.getElementById("yesBtn");
const question = document.getElementById("question");
const result = document.getElementById("result");
const canvas = document.getElementById("fireworks");
const ctx = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

// Make NO button move when hovered
noBtn.addEventListener("mouseover", function() {
    const x = Math.random() * (window.innerWidth - 100);
    const y = Math.random() * (window.innerHeight - 50);
    noBtn.style.left = x + "px";
    noBtn.style.top = y + "px";
});

// YES button action
yesBtn.addEventListener("click", function() {
    question.classList.add("hidden");
    yesBtn.classList.add("hidden");
    noBtn.classList.add("hidden");

    result.classList.remove("hidden");
    result.innerHTML = `
        <h1>🎆 HAPPY VALENTINES DAY RINKY 🎆</h1>
        <img src="https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExczR4YWZyNnkwbGFkdG5xOWowM3d5dWhnZ3draTBnZWVkbTN2OHE2NSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/jyYLZNC0smvFiNZur9/giphy.gif" width="300">
    `;

    canvas.classList.remove("hidden");
    launchFireworks();
});

// If NO is somehow clicked
noBtn.addEventListener("click", function() {
    question.classList.add("hidden");
    yesBtn.classList.add("hidden");
    noBtn.classList.add("hidden");

    result.classList.remove("hidden");
    result.innerHTML = `
        <div class="error">ERROR 201 💔</div>
        <div style="font-size:60px;">💀❤️</div>
    `;
});

// Simple Fireworks
let particles = [];

function launchFireworks() {
    setInterval(() => {
        for (let i = 0; i < 50; i++) {
            particles.push({
                x: canvas.width / 2,
                y: canvas.height / 2,
                radius: Math.random() * 3 + 2,
                color: `hsl(${Math.random()*360}, 100%, 50%)`,
                speedX: (Math.random() - 0.5) * 10,
                speedY: (Math.random() - 0.5) * 10,
                life: 100
            });
        }
    }, 500);

    animate();
}

function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    particles.forEach((p, index) => {
        ctx.beginPath();
        ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
        ctx.fillStyle = p.color;
        ctx.fill();

        p.x += p.speedX;
        p.y += p.speedY;
        p.life--;

        if (p.life <= 0) particles.splice(index, 1);
    });

    requestAnimationFrame(animate);
}
</script>

</body>
</html>
