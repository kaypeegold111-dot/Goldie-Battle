
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no">
<title>Goldie Battle</title>
<style>
*{box-sizing:border-box}
body{margin:0;overflow:hidden;background:#142437;color:white;font-family:Arial;touch-action:none}
canvas{display:block}
#menu{position:fixed;inset:0;z-index:5;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:16px;text-align:center;background:linear-gradient(145deg,#101b30,#344c65);padding:20px}
.logo{font-size:38px;font-weight:900;color:#ffd34e;text-shadow:0 0 18px #e6a700}
.sub{color:#d2e0ed;font-size:13px}
.mode{width:260px;padding:15px;border:2px solid #66809a;border-radius:12px;background:#263d59;color:white;font-weight:bold;font-size:17px}
.mode.selected{border-color:#ffd34e;background:#40516b}
#start{padding:15px 45px;border:0;border-radius:12px;background:#ffd34e;color:#172437;font-size:19px;font-weight:bold}
#hud{display:none;position:fixed;inset:0;pointer-events:none}
#top{position:absolute;top:12px;left:12px;right:12px;display:flex;justify-content:space-between;gap:8px;font-size:13px}
.panel{background:#101a2ddd;padding:10px;border-radius:9px}
#health{color:#76f5a1}
#joystick{position:absolute;bottom:30px;left:25px;width:116px;height:116px;border:2px solid #ffffff80;border-radius:50%;background:#ffffff30;pointer-events:auto}
#stick{position:absolute;left:32px;top:32px;width:48px;height:48px;border-radius:50%;background:#ffd34e}
#pulse{position:absolute;right:25px;bottom:45px;width:86px;height:86px;border-radius:50%;background:#c89aff;color:#25153c;border:3px solid white;font-weight:bold;pointer-events:auto}
#message{position:absolute;top:42%;width:100%;text-align:center;font-size:30px;font-weight:bold;text-shadow:2px 2px 5px black}
#again{display:none;position:absolute;top:57%;left:50%;transform:translateX(-50%);padding:14px 25px;background:#ffd34e;border:0;border-radius:10px;font-weight:bold;pointer-events:auto}
</style>
</head>
<body>

<div id="menu">
 <div class="logo">GOLDIE BATTLE</div>
 <div class="sub">YOUR BATTLE. YOUR LEGEND.</div>
 <button class="mode selected" data-mode="survival">SURVIVAL MODE</button>
 <button class="mode" data-mode="team">TEAM ARENA</button>
 <div class="sub">Choose a mode and enter the arena.</div>
 <button id="start">START GAME</button>
</div>

<div id="hud">
 <div id="top">
  <div class="panel">
   <div id="modeLabel">SURVIVAL</div>
   <div>Health: <span id="health">100</span></div>
  </div>
  <div class="panel">
   <div id="score">Score: 0</div>
   <div id="remaining">Opponents: 6</div>
  </div>
 </div>
 <div id="message"></div>
 <button id="again">PLAY AGAIN</button>
 <div id="joystick"><div id="stick"></div></div>
 <button id="pulse">ENERGY<br>PULSE</button>
</div>

<script type="module">
import * as THREE from
"https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js";

let scene,camera,renderer,player,clock;
let bots=[],effects=[];
let mode="survival",playing=false;
let health=100,score=0;
let moveX=0,moveZ=0;
let lastPulse=0;
let pointerId=null;
let keys={};

const $=id=>document.getElementById(id);
const menu=$("menu"),hud=$("hud");

document.querySelectorAll(".mode").forEach(button=>{
 button.onclick=()=>{
  document.querySelectorAll(".mode").forEach(b=>b.classList.remove("selected"));
  button.classList.add("selected");
  mode=button.dataset.mode;
 };
});

function character(color,x,z,team){
 const group=new THREE.Group();

 const body=new THREE.Mesh(
  new THREE.CylinderGeometry(.45,.55,1.2,10),
  new THREE.MeshStandardMaterial({color,roughness:.8})
 );
 body.position.y=.85;
 group.add(body);

 const head=new THREE.Mesh(
  new THREE.SphereGeometry(.32,12,12),
  new THREE.MeshStandardMaterial({color:0xf0c49c})
 );
 head.position.y=1.65;
 group.add(head);

 const ring=new THREE.Mesh(
  new THREE.TorusGeometry(.62,.045,8,24),
  new THREE.MeshBasicMaterial({color})
 );
 ring.rotation.x=Math.PI/2;
 ring.position.y=.08;
 group.add(ring);

 group.position.set(x,0,z);
 scene.add(group);

 return {mesh:group,team,hp:100,alive:true,cool:Math.random(),speed:2.2};
}

function makeWorld(){
 scene=new THREE.Scene();
 scene.background=new THREE.Color(0x9cc9df);
 scene.fog=new THREE.Fog(0x9cc9df,35,85);

 camera=new THREE.PerspectiveCamera(65,innerWidth/innerHeight,.1,120);

 renderer=new THREE.WebGLRenderer({antialias:true});
 renderer.setSize(innerWidth,innerHeight);
 renderer.setPixelRatio(Math.min(devicePixelRatio,1.5));
 document.body.appendChild(renderer.domElement);

 scene.add(new THREE.HemisphereLight(0xffffff,0x53634b,2));

 const sun=new THREE.DirectionalLight(0xffffff,1.5);
 sun.position.set(15,25,10);
 scene.add(sun);

 const ground=new THREE.Mesh(
  new THREE.PlaneGeometry(84,84),
  new THREE.MeshStandardMaterial({color:0x538553})
 );
 ground.rotation.x=-Math.PI/2;
 ground.position.y=-.1;
 scene.add(ground);

 // Arena walls
 const wallMat=new THREE.MeshStandardMaterial({color:0x45576a});
 for(let i=0;i<4;i++){
  const horizontal=i<2;
  const wall=new THREE.Mesh(
   new THREE.BoxGeometry(horizontal?84:1,2,horizontal?1:84),
   wallMat
  );
  wall.position.set(
   horizontal?0:(i===2?-42:42),
   1,
   horizontal?(i===0?-42:42):0
  );
  scene.add(wall);
 }

 // Buildings
 for(let i=0;i<18;i++){
  const x=Math.random()*60-30;
  const z=Math.random()*60-30;
  if(Math.hypot(x,z)<7)continue;

  const h=2+Math.random()*3;
  const building=new THREE.Mesh(
   new THREE.BoxGeometry(3,h,3),
   new THREE.MeshStandardMaterial({color:0x9baeb1})
  );
  building.position.set(x,h/2,z);
  scene.add(building);
 }

 // Trees
 for(let i=0;i<18;i++){
  const x=Math.random()*68-34;
  const z=Math.random()*68-34;

  const trunk=new THREE.Mesh(
   new THREE.CylinderGeometry(.18,.25,1.5,7),
   new THREE.MeshStandardMaterial({color:0x785238})
  );
  trunk.position.set(x,.75,z);
  scene.add(trunk);

  const leaves=new THREE.Mesh(
   new THREE.SphereGeometry(1,8,8),
   new THREE.MeshStandardMaterial({color:0x276c42})
  );
  leaves.position.set(x,1.8,z);
  scene.add(leaves);
 }

 player=character(0xffca35,0,0,"player");
 camera.position.set(0,12,16);
}

function startGame(){
 if(renderer){
  renderer.domElement.remove();
  renderer.dispose();
 }

 bots.forEach(b=>scene&&scene.remove(b.mesh));
 bots=[];
 effects=[];
 health=100;
 score=0;
 lastPulse=0;
 playing=true;
 $("message").textContent="";
 $("again").style.display="none";

 makeWorld();

 if(mode==="survival"){
  for(let i=0;i<6;i++){
   const a=i*Math.PI/3;
   bots.push(character(0xff6262,Math.cos(a)*16,Math.sin(a)*16,"enemy"));
  }
  $("modeLabel").textContent="SURVIVAL";
 }else{
  bots.push(character(0x4aaaff,-8,6,"ally"));
  bots.push(character(0x4aaaff,-10,8,"ally"));
  for(let i=0;i<4;i++){
   bots.push(character(0xff6262,8+i*2,-8+i*3,"enemy"));
  }
  $("modeLabel").textContent="TEAM ARENA";
 }

 menu.style.display="none";
 hud.style.display="block";
 clock=new THREE.Clock();
 updateHUD();
 animate();
}

function updateHUD(){
 $("health").textContent=Math.max(0,Math.ceil(health));
 $("score").textContent="Score: "+score;
 const enemies=bots.filter(b=>b.alive&&b.team==="enemy").length;
 $("remaining").textContent=mode==="survival"?
  "Opponents: "+enemies:"Enemies: "+enemies;
}

function firePulse(){
 if(!playing||performance.now()-lastPulse<500)return;
 lastPulse=performance.now();

 let target=null,best=10;

 bots.forEach(b=>{
  if(!b.alive||b.team!=="enemy")return;
  const d=player.mesh.position.distanceTo(b.mesh.position);
  if(d<best){best=d;target=b;}
 });

 if(target){
  const from=player.mesh.position.clone();
  from.y=1.2;
  const to=target.mesh.position.clone();
  to.y=1;
  const ball=new THREE.Mesh(
   new THREE.SphereGeometry(.23,10,10),
   new THREE.MeshBasicMaterial({color:0xe8b4ff})
  );
  ball.position.copy(from);
  scene.add(ball);
  effects.push({mesh:ball,from,to,t:0});

  target.hp-=50;
  if(target.hp<=0){
   target.alive=false;
   scene.remove(target.mesh);
   score++;
  }
 }
 updateHUD();
 checkEnd();
}

function moveToward(bot,target,dt){
 const dx=target.x-bot.mesh.position.x;
 const dz=target.z-bot.mesh.position.z;
 const d=Math.hypot(dx,dz);
 if(d>.15){
  bot.mesh.position.x+=dx/d*bot.speed*dt;
  bot.mesh.position.z+=dz/d*bot.speed*dt;
  bot.mesh.rotation.y=Math.atan2(dx,dz);
 }
}

function animate(){
 if(!playing)return;
 requestAnimationFrame(animate);

 const dt=Math.min(clock.getDelta(),.04);

 let x=moveX,z=moveZ;
 if(keys.ArrowLeft||keys.a)x--;
 if(keys.ArrowRight||keys.d)x++;
 if(keys.ArrowUp||keys.w)z--;
 if(keys.ArrowDown||keys.s)z++;

 const len=Math.hypot(x,z);
 if(len>1){x/=len;z/=len;}

 player.mesh.position.x+=x*8*dt;
 player.mesh.position.z+=z*8*dt;
 player.mesh.position.x=THREE.MathUtils.clamp(player.mesh.position.x,-39,39);
 player.mesh.position.z=THREE.MathUtils.clamp(player.mesh.position.z,-39,39);

 if(Math.hypot(x,z)>.1)player.mesh.rotation.y=Math.atan2(x,z);

 bots.forEach(bot=>{
  if(!bot.alive)return;

  let target=player;

  if(bot.team==="ally"){
   const enemies=bots.filter(b=>b.alive&&b.team==="enemy");
   if(!enemies.length)return;
   target=enemies.reduce((a,b)=>
    bot.mesh.position.distanceTo(a.mesh.position)<
    bot.mesh.position.distanceTo(b.mesh.position)?a:b
   );
  }else if(mode==="team"){
   const allies=bots.filter(b=>b.alive&&b.team==="ally");
   if(allies.length){
    target=allies.reduce((a,b)=>
     bot.mesh.position.distanceTo(a.mesh.position)<
     bot.mesh.position.distanceTo(b.mesh.position)?a:b
    );
   }
  }

  moveToward(bot,target,dt);
  bot.cool-=dt;

  if(bot.mesh.position.distanceTo(target.mesh.position)<1.6&&bot.cool<=0){
   if(target===player)health-=7;
   else{
    target.hp-=15;
    if(target.hp<=0){
     target.alive=false;
     scene.remove(target.mesh);
     score++;
    }
   }
   bot.cool=1.3;
  }
 });

 effects.forEach(e=>{
  e.t+=dt*3;
  e.mesh.position.lerpVectors(e.from,e.to,Math.min(e.t,1));
 });
 effects=effects.filter(e=>{
  if(e.t>=1){scene.remove(e.mesh);return false;}
  return true;
 });

 const desired=new THREE.Vector3(
  player.mesh.position.x,
  11,
  player.mesh.position.z+15
 );
 camera.position.lerp(desired,.1);
 camera.lookAt(player.mesh.position.x,0,player.mesh.position.z);

 updateHUD();
 checkEnd();
 renderer.render(scene,camera);
}

function checkEnd(){
 if(!playing)return;
 if(health<=0){finish("GAME OVER!");return;}

 const enemies=bots.filter(b=>b.alive&&b.team==="enemy");
 if(enemies.length===0){
  finish(mode==="survival"?"YOU WIN!":"TEAM BLUE WINS!");
 }
}

function finish(text){
 playing=false;
 $("message").textContent=text;
 $("again").style.display="block";
}

$("start").onclick=startGame;
$("again").onclick=startGame;
$("pulse").addEventListener("pointerdown",e=>{
 e.preventDefault();firePulse();
});

// Joystick
const joystick=$("joystick"),stick=$("stick");

joystick.addEventListener("pointerdown",e=>{
 pointerId=e.pointerId;
 joystick.setPointerCapture(pointerId);
 joystickMove(e);
});

joystick.addEventListener("pointermove",e=>{
 if(e.pointerId===pointerId)joystickMove(e);
});

function joystickMove(e){
 const r=joystick.getBoundingClientRect();
 const dx=e.clientX-r.left-r.width/2;
 const dy=e.clientY-r.top-r.height/2;
 const d=Math.hypot(dx,dy);
 const s=d>34?34/d:1;
 const px=dx*s,py=dy*s;
 stick.style.transform=`translate(${px}px,${py}px)`;
 moveX=px/34;
 moveZ=py/34;
}

function release(e){
 if(e.pointerId!==pointerId)return;
 pointerId=null;
 moveX=moveZ=0;
 stick.style.transform="translate(0,0)";
}
joystick.addEventListener("pointerup",release);
joystick.addEventListener("pointercancel",release);

window.addEventListener("keydown",e=>keys[e.key]=true);
window.addEventListener("keyup",e=>keys[e.key]=false);

window.addEventListener("resize",()=>{
 if(!camera||!renderer)return;
 camera.aspect=innerWidth/innerHeight;
 camera.updateProjectionMatrix();
 renderer.setSize(innerWidth,innerHeight);
});
</script>
</body>
</html>
