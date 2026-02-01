# BRXPORT
My portifolio
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>BRXQUEIROZ | CYBER WAR ROOM</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;700;900&display=swap" rel="stylesheet">

<style>
:root{
  --bg:#03060b;
  --neon:#00f5d4;
  --purple:#7c7cff;
  --text:#e5e7eb;
  --muted:#9ca3af;
  --red:#ff3b3b;
}

*{margin:0;padding:0;box-sizing:border-box;font-family:'Inter',sans-serif}

body{
  background:radial-gradient(circle at top,#0b1225,var(--bg));
  color:var(--text);
  overflow-x:hidden;
}

/* BACKGROUNDS */
canvas{position:fixed;inset:0;z-index:-3}

.scanlines{
  position:fixed;inset:0;pointer-events:none;
  background:repeating-linear-gradient(
    to bottom,
    rgba(255,255,255,.03),
    rgba(255,255,255,.03) 1px,
    transparent 2px,
    transparent 4px
  );
  z-index:10;
}

.cursor{
  position:fixed;width:22px;height:22px;border-radius:50%;
  background:rgba(0,245,212,.45);
  pointer-events:none;filter:blur(10px);z-index:999;
}

/* LOGIN */
#login{
  position:fixed;inset:0;
  background:#03060b;
  display:flex;align-items:center;justify-content:center;
  z-index:1000;
}

.login-box{
  border:1px solid rgba(0,245,212,.4);
  padding:45px;border-radius:16px;
  box-shadow:0 0 80px rgba(0,245,212,.35);
  width:320px;
}

.login-box h1{
  margin-bottom:25px;
  color:var(--neon);
  text-align:center;
  letter-spacing:2px;
}

.login-box input{
  width:100%;padding:12px;margin-bottom:15px;
  background:#01040a;color:var(--neon);
  border:1px solid rgba(0,245,212,.3);
}

.login-box button{
  width:100%;padding:12px;
  background:linear-gradient(90deg,var(--neon),var(--purple));
  border:none;color:#000;font-weight:800;
  cursor:pointer;
}

/* NAV */
nav{
  position:fixed;top:0;width:100%;
  padding:20px 60px;
  display:flex;justify-content:space-between;
  background:rgba(3,6,11,.7);
  backdrop-filter:blur(10px);
  z-index:20;
}

nav h1{
  font-weight:900;
  background:linear-gradient(90deg,var(--neon),var(--purple));
  -webkit-background-clip:text;
  -webkit-text-fill-color:transparent;
}

nav a{
  margin-left:25px;color:var(--muted);
  text-decoration:none;font-size:.9rem;
}

section{
  min-height:100vh;
  padding:140px 80px;
  display:flex;align-items:center;
}

.container{max-width:1150px;margin:auto}

/* GLITCH */
.glitch{
  font-size:4.5rem;font-weight:900;
  position:relative;text-transform:uppercase;
}

.glitch::before,.glitch::after{
  content:attr(data-text);position:absolute;left:0;width:100%;
}

.glitch::before{
  top:-2px;color:var(--neon);
  animation:g1 2s infinite;
}

.glitch::after{
  top:2px;color:var(--purple);
  animation:g2 1.5s infinite;
}

@keyframes g1{
  0%{clip-path:inset(10% 0 50% 0)}
  50%{clip-path:inset(30% 0 20% 0)}
}
@keyframes g2{
  0%{clip-path:inset(50% 0 10% 0)}
  50%{clip-path:inset(20% 0 40% 0)}
}

/* TERMINAL */
.terminal{
  background:#01040a;
  border:1px solid rgba(0,245,212,.35);
  padding:30px;border-radius:16px;
  font-family:monospace;
  box-shadow:0 0 60px rgba(0,245,212,.35);
}

.terminal-output{
  max-height:300px;
  overflow-y:auto;
  margin-bottom:15px;
}

.terminal-output p{color:var(--neon);margin-bottom:5px}

.terminal input{
  width:100%;
  background:#000;
  border:none;
  color:var(--neon);
  font-family:monospace;
  padding:10px;
}

/* MAP */
.map{
  position:relative;
  height:400px;
  background:radial-gradient(circle,#02050a,#000);
  border:1px solid rgba(0,245,212,.3);
  border-radius:16px;
  overflow:hidden;
}

.attack{
  position:absolute;
  width:8px;height:8px;
  background:var(--red);
  border-radius:50%;
  animation:pulse 1.5s infinite;
}

@keyframes pulse{
  0%{transform:scale(1);opacity:1}
  100%{transform:scale(3);opacity:0}
}

/* CARDS */
.grid{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(280px,1fr));
  gap:30px;margin-top:40px;
}

.card{
  background:#01040a;
  border:1px solid rgba(0,245,212,.3);
  padding:25px;border-radius:16px;
  box-shadow:0 0 50px rgba(0,245,212,.2);
}

.card h3{color:var(--neon);margin-bottom:12px}

footer{
  padding:40px;text-align:center;
  color:var(--muted);font-size:.8rem;
}
</style>
</head>

<body>

<canvas id="matrix"></canvas>
<div class="scanlines"></div>
<div class="cursor" id="cursor"></div>

<!-- LOGIN -->
<div id="login">
  <div class="login-box">
    <h1>SECURE ACCESS</h1>
    <input placeholder="user">
    <input placeholder="password" type="password">
    <button onclick="enter()">INITIALIZE</button>
  </div>
</div>

<nav>
  <h1>BRX WAR ROOM</h1>
  <div>
    <a href="#home">Dashboard</a>
    <a href="#terminal">Terminal</a>
    <a href="#map">Threat Map</a>
    <a href="#fichas">Fichas</a>
  </div>
</nav>

<section id="home">
  <div class="container">
    <div class="glitch" data-text="BrxQueiroz">BrxQueiroz</div>
    <p style="margin-top:25px;color:var(--muted);max-width:700px">
      Profissional de Tecnologia da Informação especializado em cibersegurança,
      arquitetura defensiva, análise profunda de sistemas e mitigação de riscos.
    </p>
  </div>
</section>

<section id="terminal">
  <div class="container terminal">
    <div class="terminal-output" id="out">
      <p>> system online</p>
      <p>> type 'help'</p>
    </div>
    <input id="cmd" placeholder="command">
  </div>
</section>

<section id="map">
  <div class="container">
    <h2 style="color:var(--neon)">Global Threat Map</h2>
    <div class="map" id="mapBox"></div>
  </div>
</section>

<section id="fichas">
  <div class="container">
    <h2 style="color:var(--neon)">Fichas Técnicas</h2>
    <div class="grid">
      <div class="card">
        <h3>Cybersegurança</h3>
        <p>• Análise de vulnerabilidades</p>
        <p>• Defesa em camadas</p>
        <p>• Threat modeling</p>
        <p>• Monitoramento contínuo</p>
      </div>
      <div class="card">
        <h3>Infraestrutura</h3>
        <p>• Redes e servidores</p>
        <p>• Ambientes resilientes</p>
        <p>• Segmentação e controle</p>
      </div>
      <div class="card">
        <h3>Análise Técnica</h3>
        <p>• Engenharia reversa conceitual</p>
        <p>• Mapeamento de falhas</p>
        <p>• Mitigação estratégica</p>
      </div>
      <div class="card">
        <h3>Perfil Profissional</h3>
        <p>• Mentalidade ofensiva/defensiva</p>
        <p>• Segurança realista</p>
        <p>• Evolução constante</p>
      </div>
    </div>
  </div>
</section>

<footer>
  © 2026 • BRXQUEIROZ • CYBER WAR ROOM
</footer>

<script>
// LOGIN + SOUND
const audio=new Audio("https://cdn.pixabay.com/audio/2022/10/19/audio_1b7b7c6f3a.mp3");
audio.loop=true;

function enter(){
  document.getElementById("login").style.display="none";
  audio.play();
}

// MATRIX
const c=document.getElementById("matrix"),x=c.getContext("2d");
c.width=innerWidth;c.height=innerHeight;
const letters="01",f=14,cols=c.width/f,drops=Array(cols).fill(1);
setInterval(()=>{
  x.fillStyle="rgba(3,6,11,.08)";
  x.fillRect(0,0,c.width,c.height);
  x.fillStyle="#00f5d4";
  x.font=f+"px monospace";
  drops.forEach((y,i)=>{
    x.fillText(letters[Math.random()*2|0],i*f,y*f);
    if(y*f>c.height&&Math.random()>.975)drops[i]=0;
    drops[i]++;
  });
},35);

// CURSOR
const cur=document.getElementById("cursor");
addEventListener("mousemove",e=>{
  cur.style.left=e.clientX+"px";
  cur.style.top=e.clientY+"px";
});

// TERMINAL COMMANDS
const cmd=document.getElementById("cmd");
const out=document.getElementById("out");

cmd.addEventListener("keydown",e=>{
  if(e.key==="Enter"){
    const v=cmd.value;
    out.innerHTML+=`<p>> ${v}</p>`;
    if(v==="help"){
      out.innerHTML+=`<p>commands: scan, status, clear</p>`;
    }
    if(v==="scan"){
      out.innerHTML+=`<p>scanning threats... none detected ✔</p>`;
    }
    if(v==="status"){
      out.innerHTML+=`<p>system stable | defenses active</p>`;
    }
    if(v==="clear"){out.innerHTML="";}
    cmd.value="";
    out.scrollTop=out.scrollHeight;
  }
});

// MAP ATTACKS
const map=document.getElementById("mapBox");
setInterval(()=>{
  const a=document.createElement("div");
  a.className="attack";
  a.style.left=Math.random()*100+"%";
  a.style.top=Math.random()*100+"%";
  map.appendChild(a);
  setTimeout(()=>a.remove(),1500);
},700);
</script>

</body>
</html>
