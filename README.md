<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Payal's Surprise 💖</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;600&display=swap" rel="stylesheet">
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Poppins',sans-serif;}
body{
  overflow:hidden;
  background:radial-gradient(circle at bottom,#1a1a2e,#000);
  color:white;
  text-align:center;
}
.section{
  position:absolute;
  width:100%;
  height:100vh;
  display:flex;
  flex-direction:column;
  justify-content:center;
  align-items:center;
  transition:1s;
}
.hidden{opacity:0;pointer-events:none;}
button{
  padding:12px 28px;
  border:none;
  border-radius:30px;
  cursor:pointer;
  margin-top:20px;
  font-size:16px;
  background:#ff4d88;
  color:white;
}
input{
  padding:12px;
  border-radius:25px;
  border:none;
  text-align:center;
  width:250px;
}
canvas{position:absolute;top:0;left:0;z-index:-1;}
.card{
  background:rgba(255,255,255,0.1);
  backdrop-filter:blur(12px);
  padding:40px;
  border-radius:20px;
  box-shadow:0 0 40px rgba(255,105,180,0.4);
  width:80%;
  max-width:600px;
}
img{
  width:200px;
  border-radius:20px;
  margin-top:20px;
}
.final-text{
  font-size:18px;
  line-height:1.7;
}
.glow{
  animation:glow 2s infinite alternate;
}
@keyframes glow{
  from{text-shadow:0 0 10px pink;}
  to{text-shadow:0 0 25px hotpink;}
}
</style>
</head>
<body>

<audio id="music" loop>
<source src="https://www.bensound.com/bensound-music/bensound-romantic.mp3">
</audio>

<canvas id="canvas"></canvas>

<!-- PASSWORD PAGE -->
<div class="section" id="page1">
<div class="card">
<h1 class="glow">Enter Secret Code 💌</h1>
<p style="font-size:14px;margin:10px 0;">Hint: its ___ birthday 😉</p>
<input type="password" id="pass" placeholder="Type here">
<br>
<button onclick="checkPass()">Unlock 💖</button>
</div>
</div>

<!-- PAGE 2 -->
<div class="section hidden" id="page2">
<div class="card">
<h1 class="glow">Hey Payal 💖</h1>
<p id="typing"></p>
<img src="https://i.imgur.com/8Km9tLL.png">
<button onclick="showFinal()">Final Surprise 🎂</button>
</div>
</div>

<!-- FINAL PAGE -->
<div class="section hidden" id="finalPage">
<div class="card">
<h1 class="glow">🎂 Happy Birthday Payal 🎂</h1>
<p class="final-text">
Payal, today is not just your birthday, it is a celebration of the beautiful soul you are. You bring warmth, laughter, and light wherever you go. From our silly conversations to our deep talks, every moment with you is something I truly value. You have this rare magic that makes people feel understood and appreciated.

Your smile has the power to brighten even the darkest days. Your kindness, your strength, and your positivity inspire everyone around you, especially me. I am genuinely grateful to have you as my best friend. Life feels lighter, happier, and more meaningful because you are in it.

On this special day, I wish you endless happiness, success in everything you dream of, and countless memories filled with laughter. May this new year of your life bring you growth, peace, and beautiful surprises.

Never forget how amazing, strong, and special you truly are.

Happy Birthday once again, Payal 💖  
— From Uwesh 💙
</p>
<button onclick="secretMsg()">Click for Secret Message 💌</button>
<p id="secret" style="margin-top:15px;"></p>
</div>
</div>

<script>
// Password
function checkPass(){
  let p=document.getElementById("pass").value;
  if(p.toLowerCase()=="its payal birthday"){
    document.getElementById("page1").classList.add("hidden");
    document.getElementById("page2").classList.remove("hidden");
    document.getElementById("music").play();
    type();
  }else{
    alert("Wrong password 😅 Try again!");
  }
}

// Typing Effect
let text="You are not just my best friend… you are my favorite notification, my happiness, and my biggest blessing ✨";
let i=0;
function type(){
  if(i<text.length){
    document.getElementById("typing").innerHTML+=text.charAt(i);
    i++;
    setTimeout(type,50);
  }
}

function showFinal(){
  document.getElementById("page2").classList.add("hidden");
  document.getElementById("finalPage").classList.remove("hidden");
}

function secretMsg(){
  document.getElementById("secret").innerHTML="No matter what happens, I will always be there for you 💖";
}

// Fireworks on click
const canvas=document.getElementById("canvas");
const ctx=canvas.getContext("2d");
canvas.width=window.innerWidth;
canvas.height=window.innerHeight;
let particles=[];

document.addEventListener("click",e=>{
  for(let i=0;i<60;i++){
    particles.push({
      x:e.clientX,
      y:e.clientY,
      angle:Math.random()*2*Math.PI,
      speed:Math.random()*5+2,
      life:100
    });
  }
});

function animate(){
  ctx.fillStyle="rgba(0,0,0,0.2)";
  ctx.fillRect(0,0,canvas.width,canvas.height);
  particles.forEach((p,index)=>{
    p.x+=Math.cos(p.angle)*p.speed;
    p.y+=Math.sin(p.angle)*p.speed;
    p.life--;
    ctx.beginPath();
    ctx.arc(p.x,p.y,2,0,2*Math.PI);
    ctx.fillStyle="hsl("+Math.random()*360+",100%,60%)";
    ctx.fill();
    if(p.life<=0) particles.splice(index,1);
  });
  requestAnimationFrame(animate);
}
animate();
</script>

</body>
</html>
