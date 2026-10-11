<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">

<title>SURPRISE!! 🎁</title>
<meta name="description" content="A little surprise for you ❤️">

<meta property="og:type" content="website">
<meta property="og:title" content="SURPRISE!! 🎁">
<meta property="og:description" content="A little surprise for you ❤️">
<meta property="og:url" content="https://gamerrifat325-coder.github.io/Secret-box/">

<meta name="twitter:card" content="summary">
<meta name="twitter:title" content="SURPRISE!! 🎁">
<meta name="twitter:description" content="A little surprise for you ❤️">

<style>
*{box-sizing:border-box}
body{margin:0;background:linear-gradient(135deg,#fff0f4,#f9dce7);font-family:Arial,sans-serif;color:#30212a;text-align:center}
main{max-width:600px;margin:auto;padding:22px 14px}
.card{background:#fff;padding:22px 15px;border-radius:22px;margin:14px 0;box-shadow:0 8px 30px #a52b4915}
h1{color:#e63946;font-size:26px}
button{border:0;border-radius:13px;background:#e63946;color:white;padding:14px 20px;font-size:16px;font-weight:bold;cursor:pointer;margin:7px;box-shadow:0 4px 0 #ad2430}
button:active{transform:translateY(2px)}
.hidden{display:none!important}
#stage{height:200px;position:relative;margin-top:15px}
#startBtn{position:absolute;left:50%;top:55px;transform:translateX(-50%);white-space:nowrap}
.bar{height:14px;background:#e6e6e6;border-radius:10px;overflow:hidden;margin:8px 0}
.fill{height:100%;transition:width .15s}
#playerFill{background:#2ecc71;width:100%}
#enemyFill{background:#e63946;width:100%}
#healthPanel{padding:10px;border-radius:12px;text-align:left;cursor:pointer}
.stats{display:flex;justify-content:space-between;font-weight:bold;gap:8px}
#game{width:100%;background:#17192d;border-radius:14px;margin:12px 0;touch-action:manipulation}
#msg{min-height:40px;color:#d63350;font-weight:bold;line-height:1.4}
.small{color:#888;font-size:13px}
#gift{font-size:90px;cursor:pointer;display:inline-block}
#reveal{font-size:80px;animation:pop .7s}
#flash{position:fixed;inset:0;background:white;pointer-events:none;opacity:0;z-index:9}
@keyframes pop{0%{transform:scale(0)}70%{transform:scale(1.2)}100%{transform:scale(1)}}
@keyframes flash{0%{opacity:0}25%{opacity:1}100%{opacity:0}}
</style>
</head>
<body>
<div id="flash"></div>
<main>
<section id="welcome" class="card">
<h1>For You, My Best Friend ❤️</h1>
<p>A little challenge, just for you! 👀</p>
<div id="stage">
<button id="startBtn" onclick="firstClick()">For You, My Best Friend ❤️</button>
</div>
<p id="clickCount" class="small">Click 5 times to continue.</p>
</section>

<section id="ready" class="card hidden">
<h1>🎉 Task Complete!</h1>
<p>Impressive! But there's one more challenge...</p>
<button onclick="startGame()">Are You Ready?</button>
</section>

<section id="battle" class="card hidden">
<h1>⚔️ BEST FRIEND SURVIVAL</h1>
<div class="stats"><span id="wave">Enemy 1 / 11</span><span id="score">Defeated: 0</span></div>

<div id="healthPanel" onclick="useMedkit()">
<div class="stats"><span>❤️ Your Health</span><span id="hpText">10 / 10</span></div>
<div class="bar"><div class="fill" id="playerFill"></div></div>
<p class="small">Your health bar — tap to inspect.</p>
</div>

<div class="stats"><span id="enemyName">Enemy</span><span id="enemyText">1 HP</span></div>
<div class="bar"><div class="fill" id="enemyFill"></div></div>
<canvas id="game" width="500" height="270"></canvas>
<p id="msg">Shoot the enemy to defeat it!</p>
<button onclick="shoot()">🔫 SHOOT</button>
<button onclick="move(-1)">⬅️ MOVE</button>
<button onclick="move(1)">MOVE ➡️</button>
</section>

<section id="win" class="card hidden">
<h1>🏆 VICTORY!</h1>
<p>You defeated every enemy!</p>
<button onclick="openGift()">Click Here Now!!</button>
</section>

<section id="giftSection" class="card hidden">
<h1>🎁 Surprise Box</h1>
<p>Click the box 3 times to open your gift!</p>
<div id="gift" onclick="clickGift()">🎁</div>
<p id="giftCount">Clicks: 0 / 3</p>
<div id="final" class="hidden">
<div id="reveal">🐻</div>
<h1>KAISA HAI MERE PYARE DOST, BHANGAAR WALA!! 😂🖕</h1>
<p>Best friends forever, unfortunately! ❤️💀</p>
<button onclick="location.reload()">Play Again 🔄</button>
</div>
</section>
</main>

<script>
const $=id=>document.getElementById(id);
let clicks=0,enemy=1,kills=0,playerHP=10,enemyHP=1,enemyMax=1;
let deaths=0,medkit=false,hintShown=false,gameEnded=false,giftClicks=0;
let px=250,shots=[];

function firstClick(){
 clicks++;
 $('clickCount').textContent=`Clicks: ${clicks} / 5`;
 const b=$('startBtn');
 if(clicks<5){
  b.textContent='Click 5 Times 😂';
  b.style.left=(8+Math.random()*65)+'%';
  b.style.top=(Math.random()*125)+'px';
  b.style.transform='none';
 }else{
  $('welcome').classList.add('hidden');
  $('ready').classList.remove('hidden');
 }
}

const canvas=$('game'),ctx=canvas.getContext('2d');

function startGame(){
 $('ready').classList.add('hidden');
 $('battle').classList.remove('hidden');
 enemy=1;kills=0;playerHP=10;deaths=0;
 medkit=false;hintShown=false;gameEnded=false;px=250;
 nextEnemy();
}

function nextEnemy(){
 if(enemy>11){finish();return}
 enemyMax=enemy===11?100:1;
 enemyHP=enemyMax;
 $('msg').textContent=enemy===11?
 'THE FINAL BOSS! It has 100 HP. Keep shooting!':
 'Enemy approaching! One hit should do it.';
 update();draw();
}

function update(){
 $('wave').textContent=`Enemy ${enemy} / 11`;
 $('score').textContent=`Defeated: ${kills}`;
 $('hpText').textContent=`${Math.max(0,playerHP).toFixed(1)} / 10`;
 $('playerFill').style.width=Math.max(0,playerHP)*10+'%';
 $('enemyName').textContent=enemy===11?'👹 FINAL BOSS':'👾 Enemy '+enemy;
 $('enemyText').textContent=`${enemyHP} / ${enemyMax} HP`;
 $('enemyFill').style.width=(enemyHP/enemyMax*100)+'%';
}

function shoot(){
 if(gameEnded)return;
 enemyHP--;

 if(enemy===11){
  playerHP=Math.max(0,playerHP-0.1);
  if(playerHP<=0){
   deaths++;
   playerHP=10;
   $('msg').textContent='You were defeated! Try again!';
   if(deaths>=5&&!hintShown){
    hintShown=true;
    $('msg').textContent='Hint: Click your health bar to recover your health!';
   }
  }else if(!hintShown&&playerHP<=5){
   hintShown=true;
   $('msg').textContent='Hint: Click your health bar to recover your health!';
  }else if(enemyHP>0){
   $('msg').textContent='The boss is still standing! Keep firing!';
  }
 }

 if(enemyHP<=0){
  kills++;enemy++;
  nextEnemy();
 }else update();
 draw();
}

function useMedkit(){
 if(enemy!==11||gameEnded)return;
 if(!medkit){
  medkit=true;
  playerHP=Math.min(10,playerHP+5);
  $('msg').textContent='🩹 MEDKIT FOUND! 5 health restored!';
 }else{
  $('msg').textContent='Your medkit has already been used!';
 }
 update();
}

function move(dir){
 if(gameEnded)return;
 px=Math.max(25,Math.min(475,px+dir*25));
 draw();
}

function draw(){
 ctx.clearRect(0,0,500,270);
 ctx.fillStyle='#17192d';
 ctx.fillRect(0,0,500,270);
 ctx.strokeStyle='#292d49';

 for(let x=0;x<500;x+=25){
  ctx.beginPath();ctx.moveTo(x,0);ctx.lineTo(x,270);ctx.stroke();
 }
 for(let y=0;y<270;y+=25){
  ctx.beginPath();ctx.moveTo(0,y);ctx.lineTo(500,y);ctx.stroke();
 }

 ctx.fillStyle='#55d8ff';
 ctx.fillRect(px-13,213,26,28);
 ctx.fillStyle='#fff';
 ctx.fillRect(px-8,219,5,5);
 ctx.fillRect(px+3,219,5,5);
 ctx.fillStyle='#ffda77';
 ctx.fillRect(px-3,198,6,16);

 ctx.fillStyle=enemy===11?'#ff385d':'#a78bfa';
 ctx.beginPath();
 ctx.arc(250,72,enemy===11?35:22,0,Math.PI*2);
 ctx.fill();
 ctx.fillStyle='white';
 ctx.fillRect(241,66,5,6);
 ctx.fillRect(254,66,5,6);
 ctx.fillStyle='#17192d';
 ctx.fillRect(242,81,16,4);
 ctx.fillStyle='#fff';
 ctx.textAlign='center';
 ctx.font='bold 14px Arial';
 ctx.fillText(enemy===11?'FINAL BOSS':'ENEMY '+enemy,250,124);
}

function finish(){
 gameEnded=true;
 $('battle').classList.add('hidden');
 $('win').classList.remove('hidden');
}

function openGift(){
 $('win').classList.add('hidden');
 $('giftSection').classList.remove('hidden');
}

function clickGift(){
 if(giftClicks>=3)return;
 giftClicks++;
 $('giftCount').textContent=`Clicks: ${giftClicks} / 3`;
 $('gift').style.transform=`scale(${1+giftClicks*.1}) rotate(${giftClicks%2?8:-8}deg)`;

 if(giftClicks>=3){
  $('flash').style.animation='flash .8s';
  $('gift').textContent='✨🎁✨';
  $('giftCount').textContent='SURPRISE UNLOCKED!';
  setTimeout(()=>{
   $('gift').classList.add('hidden');
   $('final').classList.remove('hidden');
  },650);
 }
}
</script>
</body>
</html>
