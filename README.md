# Secret-box-
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>A Birthday Surprise</title>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    background: #fff5f8;
    color: #d63384;
    min-height: 100vh;
    overflow-x: hidden;
}

.screen {
    display: none;
    min-height: 100vh;
    padding: 24px;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    text-align: center;
}

.screen.active {
    display: flex;
    animation: fade .6s ease;
}

@keyframes fade {
    from { opacity: 0; transform: translateY(12px); }
    to { opacity: 1; transform: translateY(0); }
}

.card {
    width: 100%;
    max-width: 380px;
    padding: 35px 24px;
    background: white;
    border-radius: 24px;
    box-shadow: 0 10px 40px #e7548015;
}

.emoji {
    font-size: 60px;
    margin-bottom: 22px;
}

h1 {
    font-size: 32px;
    margin-bottom: 16px;
    color: #e84393;
}

p {
    font-size: 16px;
    line-height: 1.8;
    color: #8f526d;
    white-space: pre-line;
}

button {
    border: none;
    background: #f45b9a;
    color: white;
    padding: 14px 22px;
    border-radius: 30px;
    font-size: 15px;
    cursor: pointer;
    margin-top: 24px;
    transition: .2s;
}

button:hover {
    background: #e84393;
    transform: translateY(-2px);
}

.options {
    display: flex;
    flex-direction: column;
    gap: 12px;
    margin-top: 20px;
}

.options button {
    width: 100%;
    margin: 0;
}

#effects {
    position: fixed;
    inset: 0;
    pointer-events: none;
    overflow: hidden;
    z-index: 10;
}

.spark {
    position: absolute;
    font-size: 24px;
    animation: explode 1.8s ease-out forwards;
}

@keyframes explode {
    0% {
        transform: scale(.2);
        opacity: 0;
    }
    30% { opacity: 1; }
    100% {
        transform: scale(2) rotate(160deg);
        opacity: 0;
    }
}

.confetti {
    position: fixed;
    top: -30px;
    pointer-events: none;
    animation: fall 3s linear forwards;
}

@keyframes fall {
    to {
        transform: translateY(110vh) rotate(600deg);
        opacity: 0;
    }
}

.heart {
    position: fixed;
    bottom: -30px;
    pointer-events: none;
    animation: float 6s linear forwards;
}

@keyframes float {
    to {
        transform: translateY(-110vh);
        opacity: 0;
    }
}

</style>
</head>

<body>

<div id="effects"></div>

<!-- FIRST PAGE -->
<section class="screen active" id="first">
    <div class="card">
        <div class="emoji">🎀</div>
        <h1>A Little Surprise</h1>
        <p>Someone has something special for you.</p>
        <button onclick="celebrate()">Do you want to see this?</button>
    </div>
</section>

<!-- BIRTHDAY PAGE -->
<section class="screen" id="birthday">
    <div class="card">
        <div class="emoji">🎂</div>
        <h1>Happy Birthday!</h1>
        <p>Today is your special day. 💗

May your life be filled with love,
happiness and beautiful memories.</p>
        <button onclick="openOptions()">Open Your Surprise</button>
    </div>
</section>

<!-- OPTIONS PAGE -->
<section class="screen" id="options">
    <div class="card">
        <div class="emoji">💌</div>
        <h1>Choose One</h1>
        <p>A little message, just for you.</p>

        <div class="options">
            <button onclick="showWish(0)">A Special Wish 💗</button>
            <button onclick="showWish(1)">From My Heart 💌</button>
            <button onclick="showWish(2)">One More Surprise 🎀</button>
        </div>
    </div>
</section>

<!-- WISH PAGE -->
<section class="screen" id="wish">
    <div class="card">
        <div class="emoji" id="wishEmoji">💗</div>
        <h1 id="wishTitle">A Special Wish</h1>
        <p id="wishText"></p>
        <button onclick="back()">Go Back</button>
    </div>
</section>

<script>
const messages = [
    {
        emoji: "💗",
        title: "A Special Wish",
        text: `Happy Birthday! 🎂

May every day of your life bring you
new reasons to smile. May your dreams
come true and your heart always be
filled with happiness.

You deserve all the beautiful things
life has to offer. Stay happy, keep
smiling and always shine. 💕`
    },
    {
        emoji: "💌",
        title: "From My Heart",
        text: `Today is all about you. 🌸

I hope this new chapter brings you
peace, happiness and countless
beautiful memories.

May you always be surrounded by
people who appreciate you, moments
that make you smile, and dreams
that inspire you.

Happy Birthday, once again! 💗`
    },
    {
        emoji: "🎀",
        title: "One More Surprise",
        text: `Here's a little reminder for you. 💖

You deserve happiness not just today,
but every single day of the year.

May your life be full of laughter,
wonderful surprises and lovely
memories that stay with you forever.

Have the most beautiful birthday! 🎂`
    }
];

function changePage(id) {
    document.querySelectorAll(".screen").forEach(page => {
        page.classList.remove("active");
    });
    document.getElementById(id).classList.add("active");
}

function celebrate() {
    changePage("birthday");

    for (let i = 0; i < 45; i++) {
        setTimeout(makeSpark, i * 70);
    }

    for (let i = 0; i < 65; i++) {
        setTimeout(makeConfetti, i * 40);
    }
}

function makeSpark() {
    const el = document.createElement("div");
    el.className = "spark";
    el.textContent = ["🎆", "✨", "💖", "🎉"][
        Math.floor(Math.random() * 4)
    ];
    el.style.left = Math.random() * 95 + "vw";
    el.style.top = Math.random() * 85 + "vh";

    document.getElementById("effects").appendChild(el);
    setTimeout(() => el.remove(), 1900);
}

function makeConfetti() {
    const el = document.createElement("div");
    el.className = "confetti";
    el.textContent = ["🎊", "✨", "💕", "🎉"][
        Math.floor(Math.random() * 4)
    ];
    el.style.left = Math.random() * 100 + "vw";
    el.style.animationDuration = (2 + Math.random() * 2) + "s";

    document.body.appendChild(el);
    setTimeout(() => el.remove(), 4500);
}

function openOptions() {
    changePage("options");
}

function showWish(index) {
    document.getElementById("wishEmoji").textContent =
        messages[index].emoji;
    document.getElementById("wishTitle").textContent =
        messages[index].title;
    document.getElementById("wishText").textContent =
        messages[index].text;

    changePage("wish");
}

function back() {
    changePage("options");
}

// Subtle floating hearts
setInterval(() => {
    const heart = document.createElement("div");
    heart.className = "heart";
    heart.textContent = "♡";
    heart.style.left = Math.random() * 100 + "vw";
    heart.style.fontSize = (18 + Math.random() * 12) + "px";
    heart.style.color = "#f45b9a";

    document.body.appendChild(heart);
    setTimeout(() => heart.remove(), 6500);
}, 1200);
</script>

</body>
</html>
