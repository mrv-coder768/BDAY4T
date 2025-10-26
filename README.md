<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Happy Birthday Theerdhani 🎉</title>
<style>
html,body {margin:0;padding:0;height:100%;overflow:hidden;
  background: radial-gradient(circle at bottom,#000b18 0%,#00030a 100%);
  font-family:'Poppins',sans-serif;color:#fff;text-align:center;}
canvas{position:fixed;top:0;left:0;width:100%;height:100%;z-index:0;}
.content{position:relative;z-index:5;top:70%;
  transform:translateY(-50%);
  padding:0 20px;max-width:700px;margin:auto;transition: all 1s ease;opacity:1;}
h1{font-size:clamp(2em,5vw,3em);color:#ffcbf2;text-shadow:0 0 25px #ff1b8d,0 0 50px #ff66b3;
   animation:glow 2s ease-in-out infinite alternate;margin-bottom:10px;}
@keyframes glow{from{text-shadow:0 0 15px #ff66b3;}to{text-shadow:0 0 45px #ff1b8d;}}
h2{font-size:clamp(1.5em,4vw,2em);color:#ffd6ff;margin-top:10px;animation:jump 1s infinite alternate;}
@keyframes jump{0%{transform:translateY(0);}50%{transform:translateY(-10px);}100%{transform:translateY(0);}}
p{font-size:clamp(1em,3vw,1.2em);color:#fff0ff;margin-top:10px;line-height:1.5;}
.gift{font-size:1.5em;color:#ffd700;font-weight:bold;margin-top:20px;text-shadow:0 0 20px #ffdd33;}
.floating-photo{
  position:fixed;bottom:10%;left:50%;transform:translateX(-50%) translateY(50px);
  width:180px;height:180px;border-radius:50%;overflow:hidden;
  box-shadow:0 0 40px #ff66b3,0 0 80px #ff1b8d;
  opacity:0; transition: all 1.5s ease; z-index:3;
}
.floating-photo.show{opacity:1; transform:translateX(-50%) translateY(0);}
.hearts{position:fixed;top:0;left:0;width:100%;height:100%;pointer-events:none;overflow:hidden;z-index:2;}
.heart{position:absolute;bottom:0;width:20px;height:20px;background:#ff80c1;opacity:.7;
  clip-path:polygon(50% 0%,61% 15%,75% 15%,85% 25%,85% 40%,50% 75%,15% 40%,15% 25%,25% 15%,39% 15%);
  animation:floatHearts linear infinite;}
@keyframes floatHearts{0%{transform:translateY(0) scale(1);opacity:1;}100%{transform:translateY(-100vh) scale(1.5);opacity:0;}}
.confetti-piece{position:absolute;width:10px;height:10px;background:yellow;opacity:0.8;z-index:4; border-radius:50%;}
.countdown {display:flex; justify-content:center; gap:20px; margin-top:30px; flex-wrap:wrap;}
.time-box {background: linear-gradient(135deg, #6a82fb, #fc5c7d); border-radius: 20px; padding: 20px 25px; box-shadow: 0 0 25px rgba(106,130,251,0.8), 0 0 50px rgba(252,92,125,0.5); text-align: center;}
.time-box span {display: block; font-size: clamp(2em, 10vw, 3em); font-weight: bold; color: #fff; text-shadow: 0 0 20px #fff, 0 0 40px #6a82fb; animation: pulse 1s infinite alternate;}
.time-box small {display: block; font-size: clamp(0.8em, 3vw, 1em); color: #dcdcff; margin-top: 5px; text-shadow: 0 0 5px #6a82fb;}
@keyframes pulse {0%{transform:scale(1);}50%{transform:scale(1.1);}100%{transform:scale(1);}}
#overlay{
  position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.95);z-index:999;
  display:flex;justify-content:center;align-items:center;flex-direction:column;
}
#overlay button{padding:20px 40px;font-size:1.5em;border-radius:30px;border:none;background:linear-gradient(90deg,#ffcc66,#ff66b3);color:white;cursor:pointer;}
#overlay button:hover{transform:scale(1.08);transition:transform 0.2s;}
</style>
</head>
<body>

<div id="overlay">
  <h1>🎵 Tap to Start Music 🎵</h1>
  <button id="startBtn">Start</button>
</div>

<canvas id="fireworks"></canvas>
<div class="hearts" id="hearts"></div>

<div class="floating-photo" id="photo">
  <img src="bird1.PNG" alt="Theerdhani's Floating Photo" style="width:100%;height:100%;">
</div>

<div class="content" id="content">
  <h1>🎂 Countdown to Theerdhani’s Birthday 🎂</h1>
  <h2>Born in 2008 — Waiting for Nov 9 2025 🎉</h2>
  <div class="countdown" id="countdown">
    <div class="time-box"><span id="days">00</span><small>Days</small></div>
    <div class="time-box"><span id="hours">00</span><small>Hours</small></div>
    <div class="time-box"><span id="minutes">00</span><small>Minutes</small></div>
    <div class="time-box"><span id="seconds">00</span><small>Seconds</small></div>
  </div>
  <p id="msg">Get ready for the surprise 💫</p>
</div>

<!-- Audio -->
<audio id="bgmCountdown" loop>
  <source src="Liquid Time - Aakash Gandhi (mp3cut.net).mp3" type="audio/mp3">
</audio>
<audio id="bgmBirthday" loop>
  <source src="theuned_happy-birthday-crowd(chosic.com).mp3" type="audio/mp3">
</audio>

<script>
// ---------------- Countdown ----------------
const target=new Date("2025-11-08T23:59:59").getTime();
const daysEl=document.getElementById("days"), hoursEl=document.getElementById("hours");
const minutesEl=document.getElementById("minutes"), secondsEl=document.getElementById("seconds");

const countdownInterval=setInterval(()=>{
 const now=new Date().getTime();
 const diff=target-now;
 if(diff<=0){clearInterval(countdownInterval);fadeToBirthday();return;}
 const d=Math.floor(diff/(1000*60*60*24));
 const h=Math.floor((diff%(1000*60*60*24))/(1000*60*60));
 const m=Math.floor((diff%(1000*60*60))/(1000*60));
 const s=Math.floor((diff%(1000*60))/1000);
 daysEl.textContent=d.toString().padStart(2,'0');
 hoursEl.textContent=h.toString().padStart(2,'0');
 minutesEl.textContent=m.toString().padStart(2,'0');
 secondsEl.textContent=s.toString().padStart(2,'0');
},1000);

// ---------------- Fade and start Birthday ----------------
function fadeToBirthday(){
  const content=document.getElementById("content");
  content.style.transition="opacity 1s ease";
  content.style.opacity=0;
  setTimeout(startBirthday,1000);
}

// ---------------- Birthday ----------------
function startBirthday(){
  document.getElementById("bgmCountdown").pause(); 
  document.getElementById("bgmCountdown").currentTime=0;
  document.getElementById("bgmBirthday").play().catch(()=>{});

  const content = document.getElementById("content");
  content.innerHTML=`
    <h1>💖 Happy Birthday, Dear Theerdhani 💖</h1>
    <h2>Born in 2008 — Shine Bright Always! ✨🎉</h2>
    <p>Dear Theerdhani, today is your special day! 🌟 May your smile light up every corner of the world,  
       may laughter and joy follow you wherever you go, and may all your dreams turn into reality 💫.</p>
    <p>On this magical day, may happiness surround you, your heart be filled with love,  
       and every moment be more beautiful than the last. 💖🎂</p>
    <p>You are amazing, inspiring, and bring so much light to everyone around you.  
       Never stop dreaming, keep smiling, and enjoy every second of your birthday celebration! 🎉🎈</p>
    <p class="gift">🎁 Your Special Gift: Premium Watch ⌚ — A token of love and appreciation 💝</p>
    <p>With endless love, hugs, and blessings from Mourya 🤗💖 — Have the happiest birthday ever!</p>
  `;
  content.style.opacity=1;
  const photo=document.getElementById("photo");
  photo.style.display="block";
  photo.classList.add("show");
}

// ---------------- Overlay Start Music ----------------
document.getElementById("startBtn").addEventListener("click", ()=>{
  document.getElementById("bgmCountdown").play().catch(()=>{});
  document.getElementById("overlay").style.display="none";
});

// ---------------- Hearts ----------------
function createHeart(){
  const h=document.createElement("div");
  h.className="heart";
  h.style.left=Math.random()*100+"vw";
  h.style.animationDuration=3+Math.random()*4+"s";
  document.getElementById("hearts").appendChild(h);
  setTimeout(()=>h.remove(),7000);
}
setInterval(createHeart,400);

// ---------------- Confetti ----------------
function createConfetti(){
  const colors = ["#ff66b3", "#ffd700", "#ff80c1", "#6a82fb", "#fc5c7d"];
  const confetti=document.createElement("div");
  confetti.className="confetti-piece";
  confetti.style.background = colors[Math.floor(Math.random()*colors.length)];
  confetti.style.left = Math.random()*100 + "vw";
  confetti.style.top = "-10px";
  document.body.appendChild(confetti);
  let fall=0;
  const fallInterval=setInterval(()=>{
    fall+=5+Math.random()*5;
    confetti.style.top=fall+"px";
    confetti.style.transform=`rotate(${fall*3}deg)`;
    if(fall>window.innerHeight){confetti.remove(); clearInterval(fallInterval);}
  },30);
}
setInterval(createConfetti,200);

// ---------------- Fireworks ----------------
const canvas=document.getElementById("fireworks"),ctx=canvas.getContext("2d");
let w,h;
function resize(){w=canvas.width=innerWidth; h=canvas.height=innerHeight;}
window.addEventListener("resize",resize);resize();

let fireworks=[];
class Firework{
  constructor(){
    this.x=Math.random()*w;
    this.y=h;
    this.ty=Math.random()*h*0.5;
    this.color=`hsl(${Math.random()*360},100%,60%)`;
    this.speed=4+Math.random()*3;
    this.parts=[];
  }
  explode(){
    for(let i=0;i<50;i++){
      this.parts.push({x:this.x,y:this.y,vx:Math.cos(i*6)*Math.random()*4,vy:Math.sin(i*6)*Math.random()*4,a:1});
    }
  }
  update(){
    if(this.y>this.ty)this.y-=this.speed;
    else if(!this.parts.length)this.explode();
    this.parts.forEach(p=>{p.x+=p.vx; p.y+=p.vy; p.vy+=0.05; p.a-=0.01;});
    this.parts=this.parts.filter(p=>p.a>0);
  }
  draw(){
    ctx.beginPath();ctx.fillStyle=this.color;
    ctx.arc(this.x,this.y,3,0,Math.PI*2);ctx.fill();
    this.parts.forEach(p=>{ctx.fillStyle=this.color.replace("60%",`${p.a*100}%`);ctx.beginPath();ctx.arc(p.x,p.y,2,0,Math.PI*2);ctx.fill();});
  }
}
function animate(){
  ctx.fillStyle="rgba(0,0,0,0.2)";ctx.fillRect(0,0,w,h);
  if(Math.random()<0.05)fireworks.push(new Firework());
  fireworks.forEach((f,i)=>{f.update(); f.draw(); if(f.parts.length===0&&f.y<=f.ty)fireworks.splice(i,1);});
  requestAnimationFrame(animate);
}
animate();
</script>
</body>
</html>
