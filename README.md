<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>SURPRISE!! 🎁</title>
<meta name="description" content="A little surprise for my best friend ❤️">
<meta property="og:type" content="website">
<meta property="og:title" content="SURPRISE!! 🎁">
<meta property="og:description" content="A little surprise for my best friend ❤️">
<meta property="og:url" content="https://gamerrifat325-coder.github.io/Secret-box/">
<meta name="twitter:card" content="summary">
<meta name="twitter:title" content="SURPRISE!! 🎁">
<meta name="twitter:description" content="A little surprise for my best friend ❤️">

<style>
*{box-sizing:border-box}
body{
 margin:0;background:linear-gradient(135deg,#fff0f5,#ffe0eb);
 font-family:Arial,sans-serif;color:#35232c;text-align:center
}
main{max-width:600px;margin:auto;padding:18px 12px}
.card{
 background:white;border-radius:22px;padding:22px 15px;
 margin:12px 0;box-shadow:0 8px 30px #8f304015
}
h1{color:#e63946;font-size:25px}
p{line-height:1.5}
button{
 background:#e63946;color:white;border:0;border-radius:13px;
 padding:14px 18px;font-size:16px;font-weight:bold;
 box-shadow:0 4px 0 #b42332;cursor:pointer;margin:6px
}
button:active{transform:translateY(2px)}
.hidden{display:none!important}
#arena{height:210px;position:relative;margin:10px 0}
#runBtn{position:absolute;left:50%;top:65px;transform:translateX(-50%);white-space:nowrap}
.muted{font-size:13px;color:#888}
.stats{display:flex;justify-content:space-between;gap:8px;font-weight:bold}
.bar{height:13px;background:#eee;border-radius:10px;overflow:hidden;margin:8px 0}
.fill{height:100%;transition:width .15s}
#playerFill{background:#2ecc71;width:100%}
#enemyFill{background:#e63946;width:100%}
#healthPanel{padding:10px;border:1px solid #f1d9e1;border-radius:12px;cursor:pointer}
#game{display:block;width:100%;height:auto;background:#17192d;border-radius:15px;margin:12px 0;touch-action:manipulation}
#message{min-height:42px;color:#d63350;font-weight:bold}
#controls{display:flex;flex-wrap:wrap;justify-content:center}
#controls button{flex:1;min-width:90px}
#gift{font-size:90px;display:inline-block;cursor:pointer;transition:transform .2s}
#flash{position:fixed;inset:0;background:white;opacity:0;pointer-events:none;z-index:10}
#bear{font-size:110px;animation:pop .7s}
@keyframes pop{0%{transform:scale(0)}70%{transform:scale(1.2)}100%{transform:scale(1)}}
@keyframes flash{0%{opacity:0}20%{opacity:1}100%{opacity:0}}
</style>
</head>
<body>
<div id="flash"></div>
<main>

<section id="welcome" class="card">
 <h1>For You, My Best Friend ❤️</h1>
 <p>A tiny challenge awaits you... 👀</p>
 <div id="arena">
  <button id="runBtn" onclick="clickRun()">For You, My Best Friend ❤️</button>
 </div>
 <p id="clickInfo" class="muted">Click the button 5 times!</p>
</section>

<section id="ready" class="card hidden">
 <h1>🎉 Task Complete!</h1>
 <p>Well done! Ready for the real challenge?</p>
 <button onclick="startGame()">Are You Ready?</button>
</section>

<section id="battle" class="card hidden">
 <h1>⚔️ SURVIVAL GAME</h1>
 <div class="stats"><span id="wave">Enemy 1 / 11</span><span id="score">Defeated: 0</span></div>

 <div id="healthPanel" onclick="useMedkit()">
  <div class="stats"><span>❤️ Your Health</span><span id="hpText">10 / 10</span></div>
  <div class="bar"><div class="fill" id="playerFill"></div></div>
  <p class="muted">Tap your health bar to inspect it.</p>
 </div>

 <div class="stats"><span id="enemyName">Enemy</span><span id="enemyText">1 / 1 HP</span></div>
 <div class="bar"><div class="fill" id="enemyFill"></div></div>

 <canvas id="game" width="500" height="270"></canvas>
 <p id="message">Shoot the enemy to defeat it!</p>

 <div id="controls">
  <button onclick="shoot()">🔫 SHOOT</button>
  <button onclick="movePlayer(-1)">⬅️ MOVE</button>
  <button onclick="movePlayer(1)">MOVE ➡️</button>
 </div>
</section>

<section id="victory" class="card hidden">
 <h1>🏆 VICTORY!</h1>
 <p>You defeated all 11 enemies!</p>
 <button onclick="showGift()">Click Here Now!!</button>
</section>

<section id="giftSection" class="card hidden">
 <h1>Surprise Box 🎁</h1>
 <p id="giftPrompt">Click the box 3 times to open your surprise!</p>
 <div id="gift" onclick="clickGift()">🎁</div>
 <p id="giftClicks">Clicks: 0 / 3</p>
 <div id="final" class="hidden">
  <div id="bear">🐻🖕</div>
  <h1>Kaisa hai mere pyare dost bhangaar wala!! 😂</h1>
  <p>Best friends forever! ❤️</p>
  <button onclick="location.reload()">Play Again 🔄</button>
 </div>
</section>

</main>

<script>
const $=id=>document.getElementById(id);
let firstClicks=0;
let enemy=1,kills=0,playerHP=10,enemyHP=1,enemyMax=1;
let bossDeaths=0,medkitUsed=false,hintShown=false,gameOver=false;
let giftCount=0,playerX=250,invulnerable=false;

const canvas=$('game'),ctx=canvas.getContext('2d');

function clickRun(){
 firstClicks++;
 $('clickInfo').textContent=`Clicks: ${firstClicks} / 5`;
 const b=$('runBtn');

 if(firstClicks<5){
  b.textContent='Click 5 Times 😂';
  b.style.left=(3+Math.random()*68)+'%';
  b.style.top=(Math.random()*145)+'px';
  b.style.transform='none';
 }else{
  $('welcome').classList.add('hidden');
  $('ready').classList.remove('hidden');
 }
}

function startGame(){
 $('ready').classList.add('hidden');
 $('battle').classList.remove('hidden');
 enemy=1;kills=0;playerHP=10;bossDeaths=0;
 medkitUsed=false;hintShown=false;gameOver=false;
 invulnerable=false;playerX=250;
 nextEnemy();
}

function nextEnemy(){
 if(enemy>11){finishGame();return}
 enemyMax=enemy===11?100:1;
 enemyHP=enemyMax;
 $('message').textContent=enemy===11
  ?'FINAL BOSS! 100 HP. Each shot deals 1 damage to the boss and 0.1 damage to you.'
  :'Enemy incoming! One bullet defeats this enemy.';
 updateUI();drawGame();
}

function updateUI(){
 $('wave').textContent=`Enemy ${enemy} / 11`;
 $('score').textContent=`Defeated: ${kills}`;
 $('hpText').textContent=`${playerHP.toFixed(1)} / 10`;
 $('playerFill').style.width=(playerHP*10)+'%';
 $('enemyName').textContent=enemy===11?'👹 FINAL BOSS':'👾 Enemy '+enemy;
 $('enemyText').textContent=`${enemyHP} / ${enemyMax} HP`;
 $('enemyFill').style.width=(enemyHP/enemyMax*100)+'%';
}

function shoot(){
 if(gameOver||playerHP<=0)return;

 enemyHP=Math.max(0,enemyHP-1);

 // Only the boss deals damage
 if(enemy===11&&!invulnerable){
  playerHP=Math.max(0,Math.round((playerHP-.1)*10)/10);
 }

 if(enemy===11&&playerHP<=0){
  bossDeaths++;
  invulnerable=true;
  if(bossDeaths>=5&&!hintShown){
   hintShown=true;
   $('message').textContent='Hint: Click your health bar to recover your health!';
  }else{
   $('message').textContent='You got knocked out! Tap the health bar to recover.';
  }
  updateUI();drawGame();
  return;
 }

 if(enemyHP<=0){
  kills++;enemy++;
  nextEnemy();
 }else{
  $('message').textContent=enemy===11
   ?'Keep shooting! The boss is tough!'
   :'Nice shot!';
  updateUI();drawGame();
 }
}

function useMedkit(){
 if(enemy!==11||gameOver)return;

 if(invulnerable){
  invulnerable=false;
  playerHP=10;
  $('message').textContent='🩹 HEALTH RESTORED! Back to full health!';
 }else if(!medkitUsed){
  medkitUsed=true;
  playerHP=Math.min(10,playerHP+5);
  $('message').textContent='🩹 MEDKIT FOUND! 5 health restored!';
 }else{
  $('message').textContent='Your medkit has already been used!';
 }
 updateUI();drawGame();
}

function movePlayer(dir){
 if(gameOver||playerHP<=0)return;
 playerX=Math.max(25,Math.min(475,playerX+dir*25));
 drawGame();
}

function drawGame(){
 ctx.clearRect(0,0,500,270);
 ctx.fillStyle='#17192d';ctx.fillRect(0,0,500,270);

 ctx.strokeStyle='#292d49';
 for(let x=0;x<500;x+=25){
  ctx.beginPath();ctx.moveTo(x,0);ctx.lineTo(x,270);ctx.stroke();
 }
 for(let y=0;y<270;y+=25){
  ctx.beginPath();ctx.moveTo(0,y);ctx.lineTo(500,y);ctx.stroke();
 }

 // Player character and toy gun
 ctx.fillStyle='#55d8ff';ctx.fillRect(playerX-13,213,26,28);
 ctx.fillStyle='white';ctx.fillRect(playerX-8,219,5,5);ctx.fillRect(playerX+3,219,5,5);
 ctx.fillStyle='#ffda77';ctx.fillRect(playerX-3,198,6,15);
 ctx.fillStyle='#c8d2e8';ctx.fillRect(playerX-3,191,6,12);

 // Enemy
 ctx.fillStyle=enemy===11?'#ff385d':'#a78bfa';
 ctx.beginPath();ctx.arc(250,72,enemy===11?35:22,0,Math.PI*2);ctx.fill();
 ctx.fillStyle='white';ctx.fillRect(241,66,5,6);ctx.fillRect(254,66,5,6);
 ctx.fillStyle='#17192d';ctx.fillRect(242,81,16,4);
 ctx.fillStyle='white';ctx.textAlign='center';ctx.font='bold 14px Arial';
 ctx.fillText(enemy===11?'FINAL BOSS':'ENEMY '+enemy,250,124);
 if(enemy===11)ctx.fillText('HP: '+enemyHP,250,148);
}

function finishGame(){
 gameOver=true;
 $('battle').classList.add('hidden');
 $('victory').classList.remove('hidden');
}

function showGift(){
 $('victory').classList.add('hidden');
 $('giftSection').classList.remove('hidden');
}

function clickGift(){
 if(giftCount>=3)return;
 giftCount++;
 $('giftClicks').textContent=`Clicks: ${giftCount} / 3`;
 $('gift').style.transform=`scale(${1+giftCount*.12}) rotate(${giftCount%2?7:-7}deg)`;

 if(giftCount===3){
  $('giftPrompt').textContent='Opening your surprise...';
  $('flash').style.animation='none';
  void $('flash').offsetWidth;
  $('flash').style.animation='flash 1s';
  $('gift').textContent='✨🎁✨';

  setTimeout(()=>{
   $('gift').classList.add('hidden');
   $('giftPrompt').classList.add('hidden');
   $('giftClicks').classList.add('hidden');
   $('final').classList.remove('hidden');
  },850);
 }
}
</script>
</body>
</html>
