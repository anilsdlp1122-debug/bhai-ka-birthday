<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Happy Birthday Brother</title>

<style>
*{
  margin:0;
  padding:0;
  box-sizing:border-box;
  font-family:sans-serif;
}

body{
  color:white;
  text-align:center;
  background:black;
  overflow-x:hidden;   /* allow vertical scroll */
}

/* Pages */
.page{
  width:100%;
  min-height:100vh;        /* allows scroll if content more */
  display:none;
  flex-direction:column;
  justify-content:center;
  align-items:center;
  padding:20px;
  position:relative;
}

.page.active{
  display:flex;
}

/* Responsive Images */
img{
  width:100%;
  max-width:300px;
  border-radius:20px;
  margin:12px 0;
  box-shadow:0 10px 30px rgba(0,0,0,0.6);
}

/* Buttons */
button{
  padding:14px 30px;
  margin:12px;
  border:none;
  border-radius:30px;
  background:#ff2e63;
  color:white;
  font-size:18px;
  cursor:pointer;
  transition:0.3s;
}

button:hover{
  transform:scale(1.05);
  background:#ff0055;
}

h1{
  margin-bottom:20px;
  font-size:clamp(20px,5vw,32px); /* auto responsive text */
}

/* Typing Effect */
.typing{
  font-size:clamp(16px,4vw,24px);
  border-right:2px solid white;
  white-space:nowrap;
  overflow:hidden;
  width:0;
  animation:typing 4s steps(40,end) forwards, blink 1s infinite;
}

@keyframes typing{ to{width:100%;} }
@keyframes blink{ 50%{border-color:transparent;} }

/* Balloons */
.balloon{
  position:fixed;
  bottom:-100px;
  width:35px;
  height:55px;
  border-radius:50%;
  animation:float 10s linear infinite;
  z-index:-1;
}

@keyframes float{
  from{transform:translateY(0);}
  to{transform:translateY(-110vh);}
}

/* Hearts */
.heart{
  position:fixed;
  animation:fall 5s linear infinite;
  z-index:-1;
}

@keyframes fall{
  from{transform:translateY(-10vh);}
  to{transform:translateY(110vh);}
}

/* Fireworks */
canvas{
  position:fixed;
  top:0;
  left:0;
  z-index:-2;
}
</style>
</head>

<body>

<canvas id="fireworks"></canvas>

<!-- PAGE 1 -->
<div id="page1" class="page active">
  <h1>🎉 Happy Birthday Brother 🎂</h1>
  <div class="typing">You are hero ❤️</div>
  <img src="bro1.jpg.jpeg">
  <button onclick="playMusic(1)">▶ Play Song</button>
  <button onclick="nextPage(2)">Next ➜</button>
  <audio id="audio1" src="song1.mp3.mp3"></audio>
</div>

<!-- PAGE 2 -->
<div id="page2" class="page">
  <h1>💙 Memories 💙</h1>
  <img src="bro2.jpg.jpeg">
  <img src="bro3.jpg.jpeg">
  <img src="bro4.jpg.jpeg">
  <button onclick="playMusic(2)">▶ Play Song</button>
  <button onclick="nextPage(3)">Next ➜</button>
  <audio id="audio2" src="song2.mp3.mp3"></audio>
</div>

<!-- PAGE 3 -->
<div id="page3" class="page">
  <h1>🌟 Best Brother Forever 🌟</h1>
  <img src="bro5.jpg.jpeg">
  <button onclick="playMusic(3)">▶ Play Song</button>
  <audio id="audio3" src="song3.mp3.mp3"></audio>
</div>

<script>

/* MUSIC CONTROL */
function playMusic(num){
  stopAll();
  document.getElementById("audio"+num).play();
}

function stopAll(){
  for(let i=1;i<=3;i++){
    let a=document.getElementById("audio"+i);
    if(a){
      a.pause();
      a.currentTime=0;
    }
  }
}

/* PAGE SWITCH */
function nextPage(page){
  stopAll();
  document.querySelectorAll(".page").forEach(p=>{
    p.classList.remove("active");
  });
  document.getElementById("page"+page).classList.add("active");
  window.scrollTo(0,0);   // scroll top on page change
}

/* Balloons */
for(let i=0;i<8;i++){
  let b=document.createElement("div");
  b.className="balloon";
  b.style.left=Math.random()*100+"vw";
  b.style.background=`hsl(${Math.random()*360},70%,60%)`;
  b.style.animationDuration=(6+Math.random()*4)+"s";
  document.body.appendChild(b);
}

/* Heart Rain */
setInterval(()=>{
  let h=document.createElement("div");
  h.className="heart";
  h.innerHTML="💖";
  h.style.left=Math.random()*100+"vw";
  h.style.fontSize=(15+Math.random()*20)+"px";
  document.body.appendChild(h);
  setTimeout(()=>h.remove(),5000);
},500);

/* Fireworks */
const canvas=document.getElementById("fireworks");
const ctx=canvas.getContext("2d");

function resizeCanvas(){
  canvas.width=window.innerWidth;
  canvas.height=window.innerHeight;
}
resizeCanvas();
window.addEventListener("resize", resizeCanvas);

function firework(){
  let x=Math.random()*canvas.width;
  let y=Math.random()*canvas.height/2;
  for(let i=0;i<40;i++){
    let angle=Math.random()*2*Math.PI;
    let speed=Math.random()*4;
    let dx=Math.cos(angle)*speed;
    let dy=Math.sin(angle)*speed;
    ctx.fillStyle=`hsl(${Math.random()*360},100%,50%)`;
    ctx.fillRect(x+dx*10,y+dy*10,3,3);
  }
}
setInterval(firework,800);

</script>

</body>
</html>
