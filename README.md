<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no,viewport-fit=cover">
<title>Sprout: A Gardener's Journey</title>
<style>
:root{--wood3:#3a2110;--leaf:#7fd13b;--cream:#fbeec1;--glow:#ffe45c}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{margin:0;height:100%;background:#07140b;overflow:hidden;touch-action:none;-webkit-user-select:none;user-select:none;font-family:"Trebuchet MS","Segoe UI",Verdana,sans-serif;color:var(--cream)}
#menu{position:fixed;left:50%;top:50%;transform:translate(-50%,-50%);background:#0d2414 center/cover no-repeat;animation:fin .8s ease-out;border-radius:20px;overflow:hidden;box-shadow:0 20px 60px #000a}
#menu .hot{position:absolute;display:flex;align-items:center;border-radius:14px;cursor:pointer;background:transparent;border:0;outline:0;padding:0;transition:box-shadow .15s,background .15s,transform .12s}
#menu .hot:hover,#menu .hot:focus-visible{box-shadow:0 0 0 3px rgba(255,235,120,.9),0 0 22px rgba(190,255,90,.7);background:rgba(255,255,160,.08);transform:translateX(6px)}
#menu .hot:active{background:rgba(255,255,160,.22)}
#menu .hot span{display:block;width:100%;padding-left:26%;padding-right:4%;text-align:center;font-weight:800;color:#f6e2b0;text-shadow:0 2px 0 #4a2a10,0 0 8px #0006;letter-spacing:.03em;font-size:var(--fs,18px);pointer-events:none;white-space:nowrap}
#cv{position:fixed;left:50%;top:50%;transform:translate(-50%,-50%);display:none;background:#0c1d12;touch-action:none;border-radius:14px;box-shadow:0 20px 60px #0008}
#panel{position:fixed;inset:0;display:none;align-items:center;justify-content:center;background:rgba(5,15,8,.72);z-index:20;padding:10px;backdrop-filter:blur(2px)}
#panel .box{width:min(94vw,660px);max-height:96vh;overflow:auto;background:linear-gradient(#80502d,#5a351b);border:4px solid var(--wood3);border-radius:16px;box-shadow:inset 0 0 0 2px #a8713f,0 12px 40px #000a;padding:12px 18px;text-align:center;animation:pop .18s ease-out}
#panel h2{margin:0 0 4px;font-size:clamp(20px,4.6vh,30px);color:var(--glow);text-shadow:0 2px 0 var(--wood3)}
#panel p{margin:6px 0;font-size:clamp(12px,2.7vh,16px);line-height:1.4}
#panel small{opacity:.85}
.btn{display:block;width:100%;margin:6px 0;padding:8px 14px;font:inherit;font-weight:700;font-size:clamp(14px,3vh,18px);color:var(--cream);background:linear-gradient(#9a6236,#6a3f20);border:3px solid var(--wood3);border-radius:12px;cursor:pointer;box-shadow:0 3px 0 #2a1608;transition:filter .1s,transform .06s}
.btn:hover{filter:brightness(1.15)}
.btn:active{transform:translateY(2px);box-shadow:0 1px 0 #2a1608}
.btn.green{background:linear-gradient(#58a52c,#357a1b)}
.btn[disabled]{opacity:.45;cursor:default;filter:none}
.row{display:flex;gap:10px;flex-wrap:wrap}
.row .btn{flex:1 1 140px}
.stat{display:flex;justify-content:space-between;gap:12px;padding:3px 8px;background:#0002;border-radius:8px;margin:3px 0;font-size:clamp(12px,2.7vh,15px);align-items:center}
.sw{min-width:64px;padding:4px 10px;font:inherit;font-weight:700;font-size:inherit;color:var(--cream);background:#2a1608;border:2px solid var(--wood3);border-radius:14px;cursor:pointer}
.sw.on{background:#4a9a26}
.seg{display:flex;gap:4px;flex-wrap:wrap;justify-content:flex-end}
.seg .sw{min-width:0;padding:4px 9px;border-radius:9px}
input[type=range]{-webkit-appearance:none;appearance:none;width:44%;height:7px;border-radius:5px;background:#2a1608;outline:none;margin:0}
input[type=range]::-webkit-slider-thumb{-webkit-appearance:none;width:22px;height:22px;border-radius:50%;background:#8fd14f;border:3px solid var(--wood3);cursor:pointer}
input[type=range]::-moz-range-thumb{width:18px;height:18px;border-radius:50%;background:#8fd14f;border:3px solid var(--wood3);cursor:pointer}
#touch{--ts:1;--to:.6;position:fixed;inset:0;pointer-events:none;display:none;z-index:10}
#touch .grp{position:absolute;bottom:calc(16px*var(--ts));display:grid;gap:calc(10px*var(--ts));pointer-events:none}
#touch .A{left:16px;grid-template-columns:auto auto}
#touch .B{right:16px;grid-template-columns:auto auto}
#touch.lefty .A{left:auto;right:16px}
#touch.lefty .B{right:auto;left:16px}
#touch .tb{pointer-events:auto;width:calc(74px*var(--ts));height:calc(74px*var(--ts));border-radius:50%;background:rgba(20,50,20,.55);border:3px solid rgba(255,240,150,.7);color:#fff;font-size:calc(28px*var(--ts));font-weight:700;display:flex;align-items:center;justify-content:center;touch-action:none;-webkit-user-select:none;user-select:none;opacity:var(--to);transition:background .06s,transform .06s}
#touch .tb.on{background:rgba(140,220,60,.7);transform:scale(.93)}
#touch .tb.atk{background:rgba(150,60,20,.6)}
#touch .tb.cyc{grid-column:2;grid-row:1;width:calc(56px*var(--ts));height:calc(56px*var(--ts));justify-self:end;font-size:calc(22px*var(--ts))}
#touch .tb#tdash{grid-column:1;grid-row:1;width:calc(60px*var(--ts));height:calc(60px*var(--ts));justify-self:end;font-size:calc(24px*var(--ts));background:rgba(30,80,30,.55)}
#pauseBtn{position:fixed;top:8px;left:50%;margin-left:-18px;width:36px;height:36px;border-radius:50%;display:none;z-index:11;background:rgba(20,30,15,.75);border:2px solid #cdb36a;color:var(--cream);font-weight:700;font-size:15px;cursor:pointer;padding:0;transition:transform .1s}
#pauseBtn:active{transform:scale(.92)}
#langBtn{position:fixed;top:8px;right:8px;z-index:12;padding:5px 11px;border-radius:14px;border:2px solid #cdb36a;background:rgba(20,30,15,.75);color:var(--cream);font:700 13px inherit;cursor:pointer}
#toast{position:fixed;top:58px;left:50%;transform:translateX(-50%);background:#000b;color:#fff3c0;padding:6px 14px;border-radius:14px;opacity:0;transition:opacity .3s;z-index:30;pointer-events:none;font-size:14px}
#rot{position:fixed;inset:0;background:#07140bf2;z-index:100;display:none;align-items:center;justify-content:center;text-align:center;font-size:20px;padding:30px}
@media(orientation:portrait){body.touch #rot{display:flex}}
#pbox.bookbox{width:min(96vw,800px);background:linear-gradient(#5a3419,#3f2310);padding:10px 12px}
.book{display:flex;background:linear-gradient(90deg,#d9c08a,#ecdcae 48%,#d3b87c 50%,#ecdcae 52%,#d9c08a);border-radius:8px;box-shadow:0 6px 18px #000a,inset 0 0 40px #8a6a30aa;color:#3a2a14;min-height:min(56vh,300px);perspective:1200px;overflow:hidden}
.bpage{flex:1;padding:12px 16px;text-align:left;font-size:clamp(11px,2.5vh,14px);line-height:1.4;overflow:auto;max-height:60vh;min-width:0}
.bspine{width:6px;background:linear-gradient(90deg,#00000030,#ffffff30,#00000030);flex:none}
.bpage h3{margin:0 0 4px;color:#5a3412;font-size:clamp(15px,3.4vh,20px)}
.bgrid{display:grid;grid-template-columns:repeat(auto-fill,minmax(112px,1fr));gap:8px}
.bcard{background:#fff3;border:1px solid #8a6a3055;border-radius:8px;padding:6px;text-align:center}
.bcard img{height:clamp(44px,12vh,72px);max-width:100%;object-fit:contain}
.bcard b{display:block;font-size:.95em}
.bcard small{display:block;opacity:.85;font-size:.8em;line-height:1.25}
@keyframes fin{from{opacity:0}to{opacity:1}}
@keyframes pop{from{transform:scale(.92);opacity:0}to{transform:none;opacity:1}}
</style>
</head>
<body>
<div id="menu"></div>
<canvas id="cv"></canvas>
<div id="touch">
  <div class="grp A"><div class="tb" data-k="left">◀</div><div class="tb" data-k="right">▶</div></div>
  <div class="grp B"><div class="tb" id="tdash" data-k="dash" style="display:none">⚡</div><div class="tb cyc" data-k="cycle">⟳</div><div class="tb atk" data-k="attack">✦</div><div class="tb" data-k="jump">⤒</div></div>
</div>
<button id="langBtn">RU · EN</button>
<button id="pauseBtn">II</button>
<div id="panel"><div class="box" id="pbox"></div></div>
<div id="toast"></div>
<div id="rot">Поверните телефон горизонтально, чтобы играть</div>
<script>
(()=>{
'use strict';

/* ========== АССЕТЫ (заглушки SVG, заменяемы на base64) ========== */
const S=(w,h,body)=>'data:image/svg+xml;utf8,'+encodeURIComponent('<svg xmlns="http://www.w3.org/2000/svg" width="'+w+'" height="'+h+'" viewBox="0 0 '+w+' '+h+'">'+body+'</svg>');
const SRC={
  bg:S(800,400,'<defs><linearGradient id="g" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#87ceeb"/><stop offset="1" stop-color="#b8e0a0"/></linearGradient></defs><rect width="800" height="400" fill="url(#g)"/>'),
  menu:S(800,600,'<defs><radialGradient id="g" cx=".3" cy=".2" r=".9"><stop offset="0" stop-color="#2a5a24"/><stop offset="1" stop-color="#07140b"/></radialGradient></defs><rect width="800" height="600" fill="url(#g)"/><circle cx="140" cy="120" r="90" fill="#7fd13b" opacity=".18"/><circle cx="660" cy="180" r="140" fill="#7fd13b" opacity=".12"/><circle cx="400" cy="540" r="180" fill="#4a9a26" opacity=".15"/>'),
  beetle:S(60,50,'<ellipse cx="30" cy="30" rx="26" ry="18" fill="#3a2010"/>'),
  fly:S(50,40,'<ellipse cx="25" cy="22" rx="11" ry="12" fill="#222"/>'),
  hatlas:S(64,64,'<circle cx="32" cy="32" r="28" fill="#7fd13b"/>')
};

/* ========== КОНСТАНТЫ ========== */
const W=960,H=540;
const $=id=>document.getElementById(id);
const TAU=Math.PI*2;
const rand=(a,b)=>a+Math.random()*(b-a);
const clamp=(v,a,b)=>v<a?a:v>b?b:v;
const lerp=(a,b,t)=>a+(b-a)*t;

/* ========== ДИКТ ========== */
const DICT={
  ru:{play:'Играть',settings:'Настройки',collection:'Коллекция',more:'Ещё',back:'Назад',resume:'Продолжить',restart:'Заново',toMenu:'В меню',paused:'Пауза',gameOver:'Игра окончена',youWin:'Победа!',coins:'Монеты',music:'Музыка',sfx:'Звуки',quality:'Качество',auto:'Авто',high:'Высокое',med:'Среднее',low:'Ниже',lefty:'Левша',exit:'Ещё',fullscreen:'Полный экран',levels:'Уровни',info:'Растения и враги',stats:'Статистика',sprout:'Росток',sprout_d:'Игрок',beetle:'Жук',beetle_d:'Ходун',fly:'Муха',fly_d:'Летун',locked:'Закрыто',unlocked:'Открыто',ability:'Умение ⚡',rotate:'Поверните телефон горизонтально',graphics:'Графика снижена',hint:'← → движение · ↑ прыжок · X удар',garden:'Сад',forest:'Лес',pond:'Пруд'},
  en:{play:'Play',settings:'Settings',collection:'Collection',more:'More',back:'Back',resume:'Resume',restart:'Restart',toMenu:'To menu',paused:'Paused',gameOver:'Game Over',youWin:'You Win!',coins:'Coins',music:'Music',sfx:'SFX',quality:'Quality',auto:'Auto',high:'High',med:'Medium',low:'Low',lefty:'Lefty',exit:'More',fullscreen:'Fullscreen',levels:'Levels',info:'Plants & Foes',stats:'Stats',sprout:'Sprout',sprout_d:'Hero',beetle:'Beetle',beetle_d:'Walker',fly:'Fly',fly_d:'Flyer',locked:'Locked',unlocked:'Unlocked',ability:'Ability ⚡',rotate:'Rotate your phone to landscape',graphics:'Graphics reduced',hint:'← → move · ↑ jump · X hit',garden:'Garden',forest:'Forest',pond:'Pond'}
};
const L=k=>(DICT[CFG.lang]||DICT.ru)[k]||k;

/* ========== КОНФИГ / ПРОГРЕСС ========== */
let CFG={lang:'ru',quality:'auto',audio:{music:.5,sfx:.7},lefty:false};
let PROG={levels:0,coins:0,ability:false};
function loadCfg(){try{Object.assign(CFG,JSON.parse(localStorage.getItem('sprout_cfg')||'{}'))}catch(e){}}
function saveCfg(){try{localStorage.setItem('sprout_cfg',JSON.stringify(CFG))}catch(e){}}
function loadProg(){try{Object.assign(PROG,JSON.parse(localStorage.getItem('sprout_prog')||'{}'))}catch(e){}}
function saveProg(){try{localStorage.setItem('sprout_prog',JSON.stringify(PROG))}catch(e){}}

/* ========== СОСТОЯНИЕ ========== */
let mode='boot';
let LV=null,P=null,enemies=[],haz=[],AC=[],cam={x:0,y:0,tx:0};
let G={time:0,overT:0,hitstop:0,slow:0,coins:0,won:false,levelBanner:0};
const Qe={dpr:1,tier:'high'};
const SX={x:0,y:0,mag:0};
let isTouch=('ontouchstart'in window)||navigator.maxTouchPoints>0;
const particles=[],floaters=[],ambient=[];

/* ========== AUDIO ========== */
let AU=null;
function initAudio(){if(AU)return;try{AU=new (window.AudioContext||window.webkitAudioContext)()}catch(e){}}
function audioSuspend(){if(AU&&AU.state==='running')AU.suspend()}
function audioResume(){if(AU&&AU.state==='suspended')AU.resume()}
function sfx(kind){
  if(!AU)return;
  const o=AU.createOscillator(),g=AU.createGain(),t=AU.currentTime;
  o.connect(g);g.connect(AU.destination);
  g.gain.value=CFG.audio.sfx*.12;
  const f={click:660,swap:440,jump:520,hit:160,coin:880,win:1040}[kind]||600;
  o.type=kind==='hit'?'sawtooth':'square';
  o.frequency.setValueAtTime(f,t);
  o.frequency.exponentialRampToValueAtTime(f*.7,t+.1);
  g.gain.exponentialRampToValueAtTime(.001,t+.15);
  o.start(t);o.stop(t+.16);
}

/* ========== CANVAS ========== */
let cv=$('cv'),ctx=cv.getContext('2d');
let CW=0,CH=0,K=1,BUFS=null,IMG={};
function mkBuf(w,h){const c=document.createElement('canvas');c.width=w;c.height=h;return c}
function layout(){
  const vw=innerWidth,vh=innerHeight;
  let cw,ch;
  if(vw/vh>W/H){ch=vh;cw=ch*W/H;}
  else{cw=vw;ch=cw*H/W;}
  CW=cw;CH=ch;
  cv.style.width=cw+'px';cv.style.height=ch+'px';
  const pw=Math.max(480,Math.round(cw*(Qe.dpr||1))),nk=pw/W;
  if(cv.width!==pw||nk!==K||!BUFS){
    cv.width=pw;cv.height=Math.round(pw*H/W);K=nk;
    BUFS={s:mkBuf(170,190),l:mkBuf(340,260),xl:mkBuf(470,430)};
  }
  ctx.imageSmoothingEnabled=true;
  ctx.imageSmoothingQuality=Qe.tier==='low'?'low':'high';
}
addEventListener('resize',layout);

/* ========== ВВОД ========== */
const inp={left:false,right:false,jump:false,jumpPressed:false};
const keys={};
function onKey(c,down){
  if(c==='ArrowLeft'||c==='KeyA')inp.left=down;
  else if(c==='ArrowRight'||c==='KeyD')inp.right=down;
  else if(c==='ArrowUp'||c==='KeyW'||c==='Space'){inp.jump=down;if(down)inp.jumpPressed=true}
  else if((c==='KeyJ'||c==='KeyX')&&down&&P)P.attackT=Math.max(P.attackT,.22);
  else if((c==='Escape'||c==='KeyP')&&down&&mode==='play')pauseGame();
}
addEventListener('keydown',e=>{if(keys[e.code])return;keys[e.code]=true;onKey(e.code,true)});
addEventListener('keyup',e=>{keys[e.code]=false;onKey(e.code,false)});

/* ========== TOUCH ========== */
function applyTouch(){
  const t=$('touch');
  t.style.display=isTouch?'block':'none';
  t.classList.toggle('lefty',!!CFG.lefty);
  document.body.classList.toggle('touch',isTouch);
  t.querySelectorAll('.tb').forEach(b=>{
    if(b.dataset.bound)return;
    b.dataset.bound='1';
    const k=b.dataset.k;
    const set=v=>{
      b.classList.toggle('on',v);
      if(k==='left'||k==='right'||k==='jump')inp[k]=v;
      if(k==='jump'&&v)inp.jumpPressed=true;
      if(k==='attack'&&v&&P)P.attackT=Math.max(P.attackT,.22);
      if(k==='dash'&&v&&P){P.vx+=P.face*12;P.inv=Math.max(P.inv,.4);burstDust(P.x,P.y,P.face)}
    };
    b.addEventListener('touchstart',e=>{e.preventDefault();set(true)},{passive:false});
    b.addEventListener('touchend',e=>{e.preventDefault();set(false)},{passive:false});
    b.addEventListener('touchcancel',()=>set(false));
    b.addEventListener('mousedown',()=>set(true));
    b.addEventListener('mouseup',()=>set(false));
    b.addEventListener('mouseleave',()=>set(false));
  });
}

/* ========== QUALITY / TOAST ========== */
function applyQuality(){Qe.dpr=Math.min(window.devicePixelRatio||1,2);Qe.tier=CFG.quality==='auto'?'high':CFG.quality;layout()}
let toastT;
function toast(msg){const t=$('toast');t.textContent=msg;t.style.opacity=1;clearTimeout(toastT);toastT=setTimeout(()=>t.style.opacity=0,2200)}

/* ========== ЧАСТИЦЫ / FLOATERS / AMBIENT ========== */
function spawnParticle(x,y,o={}){
  const a=o.angle!==undefined?o.angle:rand(0,TAU);
  const sp=rand(o.spdMin??40,o.spdMax??140);
  particles.push({
    x,y,
    vx:Math.cos(a)*sp,
    vy:Math.sin(a)*sp,
    life:rand(o.lifeMin??.4,o.lifeMax??.8),
    max:o.lifeMax??.8,
    color:o.color||'#fff',
    size:rand(o.sizeMin??2,o.sizeMax??5),
    gravity:o.gravity??400,
    drag:o.drag??.94,
    rot:rand(0,TAU),
    rotV:rand(-8,8),
    shape:o.shape||'circle'
  });
}
function burstDust(x,y,dir){
  for(let i=0;i<6;i++)spawnParticle(x+rand(-6,6),y+10,{
    angle:dir>0?Math.PI-rand(0,Math.PI/2):rand(-Math.PI/2,0),
    spdMin:30,spdMax:100,
    color:'rgba(200,180,140,.9)',
    sizeMin:2,sizeMax:4,
    lifeMax:.5,gravity:80
  });
}
function burstLeaves(x,y,color){
  for(let i=0;i<8;i++)spawnParticle(x,y,{
    spdMin:60,spdMax:180,color,sizeMin:3,sizeMax:6,lifeMax:.7,gravity:500,shape:'leaf'
  });
}
function burstDamage(x,y){
  for(let i=0;i<10;i++)spawnParticle(x,y,{
    spdMin:80,spdMax:260,color:i%2?'#ff4b4b':'#ffb04b',
    sizeMin:2,sizeMax:5,lifeMax:.6,gravity:500
  });
}
function spawnFloater(x,y,text,color){floaters.push({x,y,text,color:color||'#ffe45c',life:1.1,max:1.1})}

function updateParticles(dt){
  for(let i=particles.length-1;i>=0;i--){
    const p=particles[i];
    p.life-=dt;
    if(p.life<=0){particles.splice(i,1);continue}
    p.vy+=p.gravity*dt;
    p.vx*=Math.pow(p.drag,dt*60);
    p.vy*=Math.pow(p.drag,dt*60);
    p.x+=p.vx*dt;p.y+=p.vy*dt;
    p.rot+=p.rotV*dt;
  }
  for(let i=floaters.length-1;i>=0;i--){
    const f=floaters[i];
    f.life-=dt;f.y-=50*dt;
    if(f.life<=0)floaters.splice(i,1);
  }
}
function drawParticles(){
  for(const p of particles){
    const a=p.life/p.max;
    ctx.save();
    ctx.globalAlpha=a;
    ctx.translate(p.x,p.y);
    ctx.rotate(p.rot);
    ctx.fillStyle=p.color;
    if(p.shape==='leaf'){
      ctx.beginPath();ctx.ellipse(0,0,p.size*1.6,p.size*.8,0,0,TAU);ctx.fill();
    }else{
      ctx.beginPath();ctx.arc(0,0,p.size,0,TAU);ctx.fill();
    }
    ctx.restore();
  }
}
function drawFloaters(s){
  ctx.setTransform(s,0,0,s,-cam.x*s,-cam.y*s);
  for(const f of floaters){
    ctx.globalAlpha=Math.min(1,f.life/f.max*1.4);
    ctx.fillStyle=f.color;
    ctx.font='bold 20px sans-serif';
    ctx.textAlign='center';
    ctx.strokeStyle='rgba(0,0,0,.7)';
    ctx.lineWidth=4;
    ctx.strokeText(f.text,f.x,f.y);
    ctx.fillText(f.text,f.x,f.y);
  }
  ctx.globalAlpha=1;
}

/* ========== AMBIENT (пыльца/светлячки) ========== */
function initAmbient(){
  ambient.length=0;
  for(let i=0;i<28;i++)ambient.push({
    x:rand(0,LV.width),y:rand(60,380),
    ph:rand(0,TAU),amp:rand(4,14),sp:rand(.3,1),
    r:rand(1,2.5),a:rand(.3,.7)
  });
}
function drawAmbient(dt){
  for(const p of ambient){
    p.ph+=dt*p.sp;
    const y=p.y+Math.sin(p.ph)*p.amp;
    const x=p.x+Math.cos(p.ph*.7)*p.amp*.5;
    ctx.globalAlpha=p.a*(0.5+0.5*Math.sin(p.ph*1.3));
    ctx.fillStyle='#fff8c0';
    ctx.beginPath();ctx.arc(x,y,p.r,0,TAU);ctx.fill();
  }
  ctx.globalAlpha=1;
}

/* ========== УРОВНИ ========== */
const LEVELS=[
  {index:0,width:1800,sky:['#7ec0e8','#b8e0a0'],sun:'#ffe45c',hills:['#4a7a2a','#3a5a1e'],
   ground:[[0,420,1800,120]],plats:[[300,330,140,20],[540,260,120,20],[820,330,140,20]],
   enemies:[[640,380,'beetle'],[1050,380,'beetle'],[1250,220,'fly']],
   haz:[[460,400,60,20]],
   coins:[[340,300],[580,230],[860,300],[1080,340],[1320,180]],
   exit:[1650,320,80,100],name:'garden'},
  {index:1,width:2000,sky:['#5a8a6a','#8fb87a'],sun:'#ffd84b',hills:['#2a5a34','#1e3a22'],
   ground:[[0,420,2000,120]],plats:[[260,340,120,20],[500,270,100,20],[740,340,100,20],[980,260,120,20],[1280,340,100,20]],
   enemies:[[600,380,'beetle'],[900,380,'beetle'],[1150,220,'fly'],[1500,380,'beetle']],
   haz:[[420,400,50,20],[860,400,50,20]],
   coins:[[300,310],[540,240],[780,310],[1020,230],[1320,310],[1600,340]],
   exit:[1850,320,80,100],name:'forest'},
  {index:2,width:2200,sky:['#6a9ec4','#a8d4e8'],sun:'#ffe0a0',hills:['#3a6a5a','#2a4a40'],
   ground:[[0,420,2200,120]],plats:[[300,330,120,20],[600,260,120,20],[900,330,120,20],[1200,260,120,20],[1500,330,120,20]],
   enemies:[[700,380,'beetle'],[900,240,'fly'],[1200,380,'beetle'],[1600,380,'beetle'],[1800,240,'fly']],
   haz:[[500,400,60,20],[1100,400,60,20],[1700,400,60,20]],
   coins:[[340,300],[640,230],[940,300],[1240,230],[1540,300],[1750,180]],
   exit:[2050,320,80,100],name:'pond'}
];

/* ========== START / END ========== */
function startLevel(i){
  LV={...LEVELS[i]};
  mode='play';G.time=0;G.overT=0;G.coins=0;G.hitstop=0;G.slow=0;G.won=false;G.levelBanner=2.5;
  P={x:80,y:340,vx:0,vy:0,w:36,h:48,onG:false,face:1,hp:3,inv:0,attackT:0,alive:true,
     sx:1,sy:1,blink:0,stepT:0,bob:0,wasOnG:false,trail:[]};
  enemies=LV.enemies.map(([x,y,t])=>({x,y,vx:t==='fly'?-40:-50,type:t,w:40,h:32,hp:2,anim:rand(0,10),dir:-1,dead:false,y0:y,dieT:0}));
  haz=LV.haz.map(([x,y,w,h])=>({x,y,w,h}));
  AC=LV.coins.map(([x,y])=>({x,y,r:12,got:false,t:rand(0,TAU),spin:0}));
  particles.length=0;floaters.length=0;
  cam.x=0;cam.tx=0;cam.y=0;SX.mag=0;
  initAmbient();
  $('menu').style.display='none';
  $('cv').style.display='block';
  $('pauseBtn').style.display='block';
  $('tdash').style.display=PROG.ability?'flex':'none';
  hidePanel();
}
function go(i){startLevel(i)}
function toMenu(){
  mode='menu';LV=null;P=null;
  $('panel').style.display='none';
  $('pauseBtn').style.display='none';
  $('cv').style.display='none';
  $('menu').style.display='block';
  ctx.setTransform(1,0,0,1,0,0);ctx.clearRect(0,0,cv.width,cv.height);
}
function win(){
  G.won=true;
  PROG.coins+=G.coins;
  if(PROG.levels<LV.index+1)PROG.levels=LV.index+1;
  if(LV.index>=1)PROG.ability=true;
  saveProg();
  mode='over';G.overT=0;
  sfx('win');
  for(let i=0;i<40;i++)spawnParticle(P.x,P.y-20,{color:i%2?'#ffe45c':'#7fd13b',spdMin:80,spdMax:280,lifeMax:1.2,gravity:300,sizeMin:3,sizeMax:7});
}
function gameOver(){mode='over';G.overT=0;G.won=false}
function damage(n){
  if(!P||P.inv>0||!P.alive)return;
  P.hp-=n;P.inv=1.1;SX.mag=14;
  burstDamage(P.x,P.y);
  if(P.hp<=0){P.hp=0;P.alive=false;gameOver();for(let i=0;i<20;i++)spawnParticle(P.x,P.y,{color:'#7fd13b',spdMin:60,spdMax:240,lifeMax:.9,gravity:400});}
  else sfx('hit');
}

/* ========== UPDATE ========== */
function update(dt){
  if(!P||!P.alive)return;
  G.time+=dt;
  if(G.levelBanner>0)G.levelBanner-=dt;

  // dust trail while running
  if(P.onG&&Math.abs(P.vx)>120){
    P.stepT+=dt*Math.abs(P.vx)/300;
    if(P.stepT>.12){P.stepT=0;burstDust(P.x,P.y,P.face)}
  }

  // physics
  const acc=2600,max=290,fr=0.0006;
  if(inp.left&&!inp.right){P.vx-=acc*dt;P.face=-1}
  else if(inp.right&&!inp.left){P.vx+=acc*dt;P.face=1}
  else P.vx*=Math.pow(fr,dt);
  P.vx=clamp(P.vx,-max,max);
  if(inp.jumpPressed&&P.onG){
    P.vy=-680;P.onG=false;P.sx=.75;P.sy=1.25;
    for(let i=0;i<6;i++)spawnParticle(P.x+rand(-8,8),P.y+18,{color:'rgba(200,180,140,.8)',angle:Math.PI/2+rand(-.6,.6),spdMin:30,spdMax:90,lifeMax:.4,gravity:200,sizeMin:2,sizeMax:4});
    sfx('jump');
  }
  P.vy+=1900*dt;
  P.x+=P.vx*dt;P.y+=P.vy*dt;
  const wasOnG=P.onG;
  P.onG=false;

  // collisions
  const rects=[...LV.ground,...(LV.plats||[])];
  for(const [rx,ry,rw,rh] of rects){
    if(P.x+P.w/2>rx&&P.x-P.w/2<rx+rw&&P.y+P.h>ry&&P.y-P.h<ry+rh){
      if(P.vy>0&&P.y-P.vy*dt+P.h<=ry+8){
        P.y=ry;P.vy=0;P.onG=true;
      }
    }
  }
  if(P.onG&&!wasOnG){ // landing
    P.sx=1.35;P.sy=.68;
    for(let i=0;i<8;i++)spawnParticle(P.x+rand(-10,10),P.y+20,{color:'rgba(200,180,140,.85)',angle:-Math.PI/2+rand(-.8,.8),spdMin:60,spdMax:160,lifeMax:.5,gravity:600,sizeMin:2,sizeMax:4});
    burstDust(P.x,P.y,P.face);
  }

  // squash/stretch relax
  P.sx=lerp(P.sx,1,Math.min(1,dt*14));
  P.sy=lerp(P.sy,1,Math.min(1,dt*14));

  // blink
  P.blink-=dt;
  if(P.blink<0)P.blink=rand(2,5);
  P.bob=Math.sin(G.time*3)*1.2;

  if(P.y>H+300){damage(1);P.y=200;P.vy=0;P.x=Math.max(80,P.x-40)}
  if(P.attackT>0){
    P.attackT-=dt;
    // spawn attack trail particles
    if(Math.random()<.5){
      spawnParticle(P.x+P.face*22,P.y+rand(-14,4),{
        color:'#ffe45c',spdMin:10,spdMax:40,lifeMax:.25,gravity:0,sizeMin:2,sizeMax:4
      });
    }
  }
  if(P.inv>0)P.inv-=dt;

  // coins
  for(const c of AC){
    if(c.got)continue;
    c.t+=dt*3;c.spin+=dt*6;
    if(Math.hypot(c.x-P.x,c.y-P.y)<32){
      c.got=true;G.coins++;sfx('coin');
      spawnFloater(c.x,c.y-10,'+1','#ffe45c');
      for(let i=0;i<8;i++)spawnParticle(c.x,c.y,{color:i%2?'#ffe45c':'#ffb400',spdMin:60,spdMax:180,lifeMax:.6,gravity:300,sizeMin:2,sizeMax:4});
    }
  }

  // hazards
  for(const h of haz){
    if(P.x+P.w/2>h.x&&P.x-P.w/2<h.x+h.w&&P.y+P.h>h.y&&P.y-P.h<h.y+h.h){
      if(P.inv<=0){damage(1);P.vy=-460;P.vx=-P.face*300}
    }
  }

  // enemies
  for(const e of enemies){
    if(e.dead){e.dieT+=dt;continue}
    e.anim+=dt;
    if(e.type==='fly'){
      e.x+=Math.sin(e.anim*1.5+e.y0*.02)*dt*140;
      e.y=e.y0+Math.sin(e.anim*3)*32;
    }else{
      e.x+=e.vx*dt;
      if(e.x<20||e.x>LV.width-60)e.vx*=-1;
    }
    if(Math.abs(e.x-P.x)<(e.w+P.w)/2-8&&Math.abs(e.y-P.y)<(e.h+P.h)/2-8){
      if(P.attackT>0){
        e.hp--;G.hitstop=.08;SX.mag=8;
        burstLeaves(e.x,e.y,e.type==='fly'?'#888':'#8a4a1a');
        if(e.hp<=0){
          e.dead=true;e.dieT=0;
          G.coins+=2;spawnFloater(e.x,e.y-15,'+2','#7fd13b');
          for(let i=0;i<14;i++)spawnParticle(e.x,e.y,{color:e.type==='fly'?'#444':'#5a3010',spdMin:80,spdMax:260,lifeMax:.8,gravity:600,sizeMin:3,sizeMax:6,shape:'leaf'});
        }
        P.attackT=0;
      }else{
        damage(1);
        P.vx=-P.face*300;P.vy=-240;P.sx=.7;P.sy=1.3;
      }
    }
  }

  // exit
  if(LV.exit){
    const [ex,ey,ew,eh]=LV.exit;
    if(P.x>ex&&P.x<ex+ew&&P.y>ey&&P.y<ey+eh)win();
  }

  // camera target with lookahead
  const look=P.vx*0.18;
  const tx=clamp(P.x-W*.4+look,0,LV.width-W);
  cam.tx=tx;
  cam.x=lerp(cam.x,tx,Math.min(1,dt*5));

  updateParticles(dt);

  // screen shake decay
  if(SX.mag>0){
    SX.mag=Math.max(0,SX.mag-dt*40);
    SX.x=rand(-SX.mag,SX.mag);
    SX.y=rand(-SX.mag,SX.mag);
  }else{SX.x=0;SX.y=0}
}

/* ========== RENDER ========== */
function render(dt){
  if(!LV||!P)return;
  const s=cv.width/W;
  ctx.setTransform(1,0,0,1,0,0);
  // sky
  const sky=ctx.createLinearGradient(0,0,0,cv.height);
  sky.addColorStop(0,LV.sky[0]);
  sky.addColorStop(1,LV.sky[1]);
  ctx.fillStyle=sky;ctx.fillRect(0,0,cv.width,cv.height);

  // parallax: sun, clouds, hills
  ctx.save();
  const ox=(cam.x*s), oy=(cam.y*s), shx=SX.x*s, shy=SX.y*s;
  // sun
  const sunX=(CW*.78 - ox*0.05)+shx, sunY=(CH*.18 - oy*0.05)+shy;
  const glow=ctx.createRadialGradient(sunX,sunY,10,CW*.78+shx,sunY,CH*.55);
  glow.addColorStop(0,'rgba(255,228,92,.55)');
  glow.addColorStop(1,'rgba(255,228,92,0)');
  ctx.fillStyle=glow;ctx.fillRect(0,0,cv.width,cv.height*.7);
  ctx.fillStyle=LV.sun;ctx.beginPath();ctx.arc(sunX,sunY,CH*.09,0,TAU);ctx.fill();

  // far clouds
  drawClouds(cam.x*0.15,CV=CH*.12,CV2=CH*.08,0.55);
  // mid clouds
  drawClouds(cam.x*0.3,CH*.26,CH*.11,0.75);

  // hills (two parallax layers)
  drawHills(cam.x*0.35,s*s,LV.hills[0],CH*.62,CH*.18,1400);
  drawHills(cam.x*0.5,s*s,LV.hills[1],CH*.72,CH*.14,1000);
  ctx.restore();

  // world transform (with shake)
  ctx.setTransform(s,0,0,s,-cam.x*s+SX.x*s,-cam.y*s+SX.y*s);

  // bushes behind
  drawBushes();

  // ground
  for(const [x,y,w,h] of LV.ground){
    // dirt
    const dirtGrad=ctx.createLinearGradient(0,y,0,y+h);
    dirtGrad.addColorStop(0,'#6a4020');
    dirtGrad.addColorStop(1,'#3a2010');
    ctx.fillStyle=dirtGrad;ctx.fillRect(x,y,w,h);
    // grass top
    ctx.fillStyle='#4a7a2a';ctx.fillRect(x,y,w,14);
    ctx.fillStyle='#5a9a34';ctx.fillRect(x,y,w,6);
    // grass blades
    ctx.fillStyle='#6ab040';
    for(let gx=x;gx<x+w;gx+=12){
      const sway=Math.sin(G.time*2+gx*.05)*2;
      ctx.fillRect(gx+sway,y-4,2,6);
    }
  }

  // platforms
  for(const [x,y,w,h] of (LV.plats||[])){
    ctx.fillStyle='#5a3518';ctx.fillRect(x,y+4,w,h);
    ctx.fillStyle='#8a6a30';ctx.fillRect(x,y,w,h);
    ctx.fillStyle='#a07840';ctx.fillRect(x,y,w,4);
    ctx.fillStyle='#7fd13b';ctx.fillRect(x,y,w,2);
  }

  drawHaz();drawExit();drawCoins();
  drawEnemies();
  drawPlayer();

  // particles in world space
  drawParticles();
  drawFloaters(s);
  drawAmbient(dt);

  // foreground grass (over everything)
  drawForeground();

  // HUD (screen space)
  drawHUD(s);

  // banner
  if(G.levelBanner>0){
    const a=Math.min(1,G.levelBanner/1.5);
    ctx.setTransform(1,0,0,1,0,0);
    ctx.globalAlpha=a;
    ctx.fillStyle='rgba(0,0,0,.5)';
    ctx.fillRect(CW*.25,CH*.4,CW*.5,CH*.15);
    ctx.fillStyle='#ffe45c';
    ctx.font='bold '+(CH*.09)+'px sans-serif';
    ctx.textAlign='center';
    ctx.fillText(L(LV.name),CW/2,CH*.51);
    ctx.globalAlpha=1;
  }

  // vignette
  ctx.setTransform(1,0,0,1,0,0);
  const vg=ctx.createRadialGradient(CW/2,CH/2,CH*.4,CW/2,CH/2,CH*.85);
  vg.addColorStop(0,'rgba(0,0,0,0)');
  vg.addColorStop(1,'rgba(0,0,0,.35)');
  ctx.fillStyle=vg;ctx.fillRect(0,0,cv.width,cv.height);

  // hurt flash
  if(P.inv>0&&P.inv>.9){
    ctx.fillStyle='rgba(255,60,60,'+((P.inv-.9)*2.5)+')';
    ctx.fillRect(0,0,cv.width,cv.height);
  }
}

let CV=0,CV2=0;
function drawClouds(offset,y,r,alpha){
  ctx.globalAlpha=alpha;
  ctx.fillStyle='#fff';
  for(let i=0;i<6;i++){
    const bx=(i*380 - offset)%(CW+500)-250;
    const by=y+Math.sin(i*2.1)*30;
    const rr=r*(0.8+i*.08);
    ctx.beginPath();
    ctx.arc(bx,by,rr,0,TAU);
    ctx.arc(bx+rr,by+rr*.2,rr*.7,0,TAU);
    ctx.arc(bx-rr,by+rr*.2,rr*.65,0,TAU);
    ctx.arc(bx+rr*.4,by-rr*.4,rr*.6,0,TAU);
    ctx.fill();
  }
  ctx.globalAlpha=1;
}
function drawHills(offset,s,color,baseY,height,wavelength){
  ctx.fillStyle=color;
  ctx.beginPath();
  ctx.moveTo(-100,CH);
  for(let x=-100;x<=CW+100;x+=8){
    const wx=(x+offset);
    const y=baseY - Math.abs(Math.sin(wx/wavelength*Math.PI))*height;
    ctx.lineTo(x,y);
  }
  ctx.lineTo(CW+100,CH);
  ctx.closePath();ctx.fill();
}
function drawBushes(){
  const startX=Math.max(0,cam.x-100), endX=Math.min(LV.width,cam.x+W+100);
  for(let x=Math.floor(startX/80)*80;x<endX;x+=80){
    const bx=x, by=418;
    const sway=Math.sin(G.time*1.5+x*.03)*3;
    ctx.fillStyle='#3a6a24';
    ctx.beginPath();ctx.ellipse(bx+sway,by,42,26,0,0,TAU);ctx.fill();
    ctx.fillStyle='#4a8a2c';
    ctx.beginPath();ctx.ellipse(bx+sway,by-4,32,18,0,0,TAU);ctx.fill();
    ctx.fillStyle='#6ab040';
    ctx.beginPath();ctx.ellipse(bx+sway-8,by-8,12,8,0,0,TAU);ctx.fill();
  }
}
function drawForeground(){
  const startX=Math.max(0,cam.x-50), endX=Math.min(LV.width,cam.x+W+50);
  ctx.fillStyle='#2a4a14';
  for(let x=Math.floor(startX/30)*30;x<endX;x+=30){
    const gy=470;
    const sway=Math.sin(G.time*2.5+x*.04)*4;
    ctx.beginPath();
    ctx.moveTo(x,gy+40);
    ctx.quadraticCurveTo(x+sway,gy-10,x+sway*1.5,gy-40);
    ctx.quadraticCurveTo(x+4+sway,gy-10,x+4,gy+40);
    ctx.fill();
  }
}

/* ========== PLAYER DRAW ========== */
function drawPlayer(){
  if(!P||!P.alive)return;
  const {x,y,w,h}=P;
  // shadow
  ctx.save();
  ctx.fillStyle='rgba(0,0,0,.28)';
  ctx.beginPath();ctx.ellipse(x,y+h/2+2,18,4,0,0,TAU);ctx.fill();
  ctx.restore();

  // flash if invuln
  const flash=P.inv>0&&Math.floor(P.inv*20)%2;
  ctx.save();
  ctx.translate(x,y+P.bob);
  ctx.scale(P.sx*P.face,P.sy);

  const walk=Math.abs(P.vx)>30?Math.sin(G.time*14):0;
  const airSway=!P.onG?Math.sin(G.time*6)*.3:0;

  // leaf arms (behind)
  ctx.strokeStyle='#4a9a26';ctx.lineWidth=4;ctx.lineCap='round';
  // back arm
  ctx.beginPath();
  ctx.moveTo(-4,-4);
  const backArmX=-14-walk*3, backArmY=4+walk*2;
  ctx.quadraticCurveTo(-12,0,backArmX,backArmY);
  ctx.stroke();
  // back leaf
  ctx.fillStyle='#5aaa2c';
  ctx.beginPath();ctx.ellipse(backArmX,backArmY,6,3,.4,0,TAU);ctx.fill();

  // legs/boots
  ctx.fillStyle='#3a2010';
  const stepL=walk*4,stepR=-walk*4;
  ctx.fillRect(-8,h*.4-14+stepL,6,14);
  ctx.fillRect(2,h*.4-14+stepR,6,14);
  ctx.fillStyle='#5a3010';
  ctx.fillRect(-9,h*.4+stepL,8,4);
  ctx.fillRect(1,h*.4+stepR,8,4);

  // body (stem)
  const bodyGrad=ctx.createLinearGradient(0,-h*.3,0,h*.4);
  bodyGrad.addColorStop(0,'#7fd13b');
  bodyGrad.addColorStop(1,'#3a8a2a');
  ctx.fillStyle=flash?'#fff':bodyGrad;
  ctx.beginPath();
  ctx.ellipse(0,4,w*.42,h*.34,0,0,TAU);
  ctx.fill();
  // highlight
  ctx.fillStyle='rgba(255,255,255,.25)';
  ctx.beginPath();ctx.ellipse(-4,-4,w*.16,h*.18,0,0,TAU);ctx.fill();

  // head
  ctx.fillStyle=flash?'#fff':'#8ade4c';
  ctx.beginPath();ctx.ellipse(0,-h*.28,w*.48,h*.3,0,0,TAU);ctx.fill();

  // hat
  ctx.fillStyle='#c89850';
  ctx.beginPath();ctx.ellipse(0,-h*.52,w*.62,6,0,0,TAU);ctx.fill();
  ctx.fillStyle='#a87840';
  ctx.beginPath();
  ctx.moveTo(-w*.34,-h*.53);
  ctx.quadraticCurveTo(-w*.2,-h*.72,0,-h*.74);
  ctx.quadraticCurveTo(w*.2,-h*.72,w*.34,-h*.53);
  ctx.closePath();ctx.fill();
  // hat band
  ctx.fillStyle='#7a4a1a';
  ctx.fillRect(-w*.32,-h*.58,w*.64,3);

  // eyes
  const blink=P.blink<.12;
  if(!blink){
    ctx.fillStyle='#1a1a1a';
    ctx.beginPath();ctx.arc(-6,-h*.26,3.2,0,TAU);ctx.arc(6,-h*.26,3.2,0,TAU);ctx.fill();
    // eye shine
    ctx.fillStyle='#fff';
    ctx.beginPath();ctx.arc(-7,-h*.27,1.2,0,TAU);ctx.arc(5,-h*.27,1.2,0,TAU);ctx.fill();
  }else{
    ctx.strokeStyle='#1a1a1a';ctx.lineWidth=2;
    ctx.beginPath();ctx.moveTo(-9,-h*.26);ctx.lineTo(-3,-h*.26);
    ctx.moveTo(3,-h*.26);ctx.lineTo(9,-h*.26);ctx.stroke();
  }
  // mouth (smile)
  ctx.strokeStyle='#1a1a1a';ctx.lineWidth=1.8;
  ctx.beginPath();ctx.arc(0,-h*.20,4,.2*Math.PI,.8*Math.PI);ctx.stroke();

  // front arm (over body)
  ctx.strokeStyle='#5aab2e';ctx.lineWidth=4;ctx.lineCap='round';
  ctx.beginPath();
  const attackArc=P.attackT>0?(1-P.attackT/.22):0;
  const swing=P.attackT>0?Math.sin(attackArc*Math.PI)*1.5:0;
  const frontArmX=14+walk*3+swing*8;
  const frontArmY=4-walk*2-swing*10;
  ctx.moveTo(4,-4);
  ctx.quadraticCurveTo(12,0,frontArmX,frontArmY);
  ctx.stroke();
  // front leaf
  ctx.fillStyle='#7fd13b';
  ctx.beginPath();ctx.ellipse(frontArmX,frontArmY,7,3.5,.4-swing*.3,0,TAU);ctx.fill();

  // attack swing arc
  if(P.attackT>0){
    ctx.strokeStyle='rgba(255,228,92,'+(P.attackT/.22*.9)+')';
    ctx.lineWidth=6;ctx.lineCap='round';
    ctx.beginPath();
    const arc=Math.PI*.7;
    const a0=-arc/2+ (1-P.attackT/.22)*arc*.5;
    ctx.arc(6,-4,26,a0,a0+arc*.7);
    ctx.stroke();
    ctx.strokeStyle='rgba(255,255,255,'+(P.attackT/.22*.6)+')';
    ctx.lineWidth=2;
    ctx.beginPath();ctx.arc(6,-4,26,a0,a0+arc*.7);ctx.stroke();
  }

  ctx.restore();
}

/* ========== ENEMIES ========== */
function drawEnemies(){
  for(const e of enemies){
    if(e.dead&&e.dieT>.6)continue;
    ctx.save();
    ctx.translate(e.x,e.y);
    const dieScale=e.dead?Math.max(0,1-e.dieT*2):1;
    ctx.scale(dieScale,dieScale);
    ctx.globalAlpha=dieScale;

    // shadow
    ctx.fillStyle='rgba(0,0,0,.25)';
    ctx.beginPath();ctx.ellipse(0,e.h/2+2,e.w*.5,4,0,0,TAU);ctx.fill();

    if(e.type==='fly'){
      drawFly(e);
    }else{
      drawBeetle(e);
    }
    ctx.restore();
  }
}
function drawBeetle(e){
  const walk=Math.sin(e.anim*10);
  // legs (3 pairs)
  ctx.strokeStyle='#2a1810';ctx.lineWidth=2;ctx.lineCap='round';
  for(let s=-1;s<=1;s+=2){
    for(let i=0;i<3;i++){
      const lx=s*(6+i*3);
      const swing=Math.sin(e.anim*10+i*1.4)*3;
      ctx.beginPath();
      ctx.moveTo(lx,6);
      ctx.lineTo(lx+s*4,12+swing);
      ctx.stroke();
    }
  }
  // body shell
  const bodyGrad=ctx.createRadialGradient(-4,-6,2,0,0,18);
  bodyGrad.addColorStop(0,'#6a3a1a');
  bodyGrad.addColorStop(1,'#2a1408');
  ctx.fillStyle=bodyGrad;
  ctx.beginPath();ctx.ellipse(0,0,18,12,0,0,TAU);ctx.fill();
  // segment lines
  ctx.strokeStyle='#1a0a04';ctx.lineWidth=1.5;
  ctx.beginPath();ctx.moveTo(-6,-11);ctx.quadraticCurveTo(-8,0,-6,11);ctx.stroke();
  ctx.beginPath();ctx.moveTo(4,-11);ctx.quadraticCurveTo(2,0,4,11);ctx.stroke();
  // sheen
  ctx.fillStyle='rgba(255,220,160,.35)';
  ctx.beginPath();ctx.ellipse(-4,-6,7,3,-.4,0,TAU);ctx.fill();
  // head
  ctx.fillStyle='#1a0a04';
  ctx.beginPath();ctx.ellipse(e.vx>0?12:-12,-2,7,6,0,0,TAU);ctx.fill();
  // antennae
  const ax=e.vx>0?1:-1;
  ctx.strokeStyle='#1a0a04';ctx.lineWidth=1.5;
  ctx.beginPath();ctx.moveTo(e.vx>0?14:-14,-4);ctx.lineTo(e.vx>0?20:-20,-14+walk*1.5);ctx.stroke();
  ctx.beginPath();ctx.moveTo(e.vx>0?14:-14,-6);ctx.lineTo(e.vx>0?22:-22,-4+walk*1.5);ctx.stroke();
  // eyes
  ctx.fillStyle='#fff';
  ctx.beginPath();ctx.arc(e.vx>0?14:-14,-4,2,0,TAU);ctx.fill();
  ctx.fillStyle='#c00';
  ctx.beginPath();ctx.arc(e.vx>0?14:-14,-4,1.2,0,TAU);ctx.fill();
}
function drawFly(e){
  const buzz=Math.sin(e.anim*40);
  // legs
  ctx.strokeStyle='#111';ctx.lineWidth=1.2;
  for(let s=-1;s<=1;s+=2){
    ctx.beginPath();ctx.moveTo(s*4,8);ctx.lineTo(s*6,14);ctx.stroke();
  }
  // wings (back)
  ctx.fillStyle='rgba(220,230,255,.55)';
  ctx.beginPath();ctx.ellipse(-8,-4,10,5,buzz*.3,0,TAU);ctx.fill();
  ctx.beginPath();ctx.ellipse(8,-4,10,5,-buzz*.3,0,TAU);ctx.fill();
  // body
  const g=ctx.createRadialGradient(-2,-3,1,0,0,12);
  g.addColorStop(0,'#4a4a4a');g.addColorStop(1,'#111');
  ctx.fillStyle=g;
  ctx.beginPath();ctx.ellipse(0,2,10,11,0,0,TAU);ctx.fill();
  // head
  ctx.fillStyle='#1a1a1a';
  ctx.beginPath();ctx.arc(0,-8,7,0,TAU);ctx.fill();
  // compound eyes
  ctx.fillStyle='#e03030';
  ctx.beginPath();ctx.arc(-4,-9,3.5,0,TAU);ctx.arc(4,-9,3.5,0,TAU);ctx.fill();
  ctx.fillStyle='#fff';
  ctx.beginPath();ctx.arc(-5,-10,1,0,TAU);ctx.arc(3,-10,1,0,TAU);ctx.fill();
}

/* ========== COINS / HAZ / EXIT ========== */
function drawCoins(){
  for(const c of AC){
    if(c.got)continue;
    const bob=Math.sin(c.t)*3;
    const scX=Math.cos(c.spin); // 3D spin illusion
    ctx.save();
    ctx.translate(c.x,c.y+bob);
    // glow
    ctx.globalAlpha=.35;
    const glow=ctx.createRadialGradient(0,0,2,0,0,20);
    glow.addColorStop(0,'#ffe45c');glow.addColorStop(1,'rgba(255,228,92,0)');
    ctx.fillStyle=glow;ctx.beginPath();ctx.arc(0,0,20,0,TAU);ctx.fill();
    ctx.globalAlpha=1;
    ctx.scale(Math.max(.15,Math.abs(scX)),1);
    ctx.fillStyle='#ffb400';ctx.beginPath();ctx.arc(0,0,c.r,0,TAU);ctx.fill();
    ctx.fillStyle='#ffe45c';ctx.beginPath();ctx.arc(0,0,c.r*.85,0,TAU);ctx.fill();
    ctx.fillStyle='#7fd13b';ctx.beginPath();ctx.ellipse(0,-1,4,6,0,0,TAU);ctx.fill();
    ctx.fillStyle='#4a8a2c';ctx.fillRect(-1,-2,2,3);
    ctx.restore();
  }
}
function drawHaz(){
  for(const h of haz){
    // base
    ctx.fillStyle='#3a2010';ctx.fillRect(h.x,h.y,h.w,h.h);
    // spikes
    ctx.fillStyle='#8a4a1a';
    for(let x=h.x;x<h.x+h.w-6;x+=10){
      ctx.beginPath();
      ctx.moveTo(x,h.y);
      ctx.lineTo(x+5,h.y-14);
      ctx.lineTo(x+10,h.y);
      ctx.closePath();ctx.fill();
    }
    // tips
    ctx.fillStyle='#c07030';
    for(let x=h.x;x<h.x+h.w-6;x+=10){
      ctx.beginPath();
      ctx.moveTo(x+3,h.y-4);
      ctx.lineTo(x+5,h.y-14);
      ctx.lineTo(x+7,h.y-4);
      ctx.fill();
    }
  }
}
function drawExit(){
  if(!LV.exit)return;
  const [x,y,w,h]=LV.exit;
  const pulse=Math.sin(G.time*3)*.15+.85;
  // glow
  ctx.globalAlpha=.4*pulse;
  const g=ctx.createRadialGradient(x+w/2,y+h/2,4,x+w/2,y+h/2,w);
  g.addColorStop(0,'#7fd13b');g.addColorStop(1,'rgba(127,209,59,0)');
  ctx.fillStyle=g;ctx.beginPath();ctx.arc(x+w/2,y+h/2,w,0,TAU);ctx.fill();
  ctx.globalAlpha=1;
  // door
  ctx.fillStyle='#8a6a30';ctx.fillRect(x,y,w,h);
  ctx.fillStyle='#5a3518';ctx.fillRect(x+4,y+4,w-8,h-8);
  // portal
  ctx.fillStyle='#7fd13b';ctx.beginPath();ctx.arc(x+w/2,y+h/2,w*.35,0,TAU);ctx.fill();
  ctx.fillStyle='#a8e858';ctx.beginPath();ctx.arc(x+w/2,y+h/2,w*.22,0,TAU);ctx.fill();
  ctx.fillStyle='#fff';ctx.font='bold 16px sans-serif';ctx.textAlign='center';
  ctx.fillText('→',x+w/2,y+h/2+6);
}

/* ========== HUD ========== */
function drawHUD(s){
  // hearts
  for(let i=0;i<3;i++){
    const hx=28*s+i*30*s, hy=28*s;
    const filled=i<P.hp;
    drawHeart(hx,hy,10*s,filled?'#e94b4b':'#4a2020',filled?'#ff8080':'#6a3030');
  }
  // coins with icon
  const cx=cv.width-90*s, cy=28*s;
  ctx.save();
  ctx.translate(cx,cy);
  ctx.scale(Math.max(.15,Math.abs(Math.cos(G.time*2))),1);
  ctx.fillStyle='#ffb400';ctx.beginPath();ctx.arc(0,0,10*s,0,TAU);ctx.fill();
  ctx.fillStyle='#ffe45c';ctx.beginPath();ctx.arc(0,0,7*s,0,TAU);ctx.fill();
  ctx.restore();
  ctx.fillStyle='#fff';ctx.font='bold '+(20*s)+'px sans-serif';ctx.textAlign='left';
  ctx.textBaseline='middle';
  ctx.fillText(G.coins,cx+16*s,cy);

  ctx.textBaseline='alphabetic';
}
function drawHeart(x,y,r,fill,stroke){
  ctx.save();
  ctx.translate(x,y);
  ctx.beginPath();
  ctx.moveTo(0,r*.3);
  ctx.bezierCurveTo(-r,-r*.6,-r*.6,-r*1.2,0,-r*.4);
  ctx.bezierCurveTo(r*.6,-r*1.2,r,-r*.6,0,r*.3);
  ctx.closePath();
  ctx.fillStyle=fill;ctx.fill();
  ctx.strokeStyle='rgba(0,0,0,.4)';ctx.lineWidth=1.5;ctx.stroke();
  // highlight
  ctx.fillStyle='rgba(255,255,255,.3)';
  ctx.beginPath();ctx.ellipse(-r*.35,-r*.3,r*.2,r*.15,-.5,0,TAU);ctx.fill();
  ctx.restore();
}

/* ========== LOOP ========== */
let last=0,fpsS=60,ftA=0,ftN=0,warm=0,autoTier='high';
function loop(ts){
  requestAnimationFrame(loop);
  if(!last)last=ts;
  const d=Math.min((ts-last)/1000,.1);
  last=ts;
  if(d<=0)return;
  fpsS+=(1/d-fpsS)*.05;
  RDT=Math.min(d,.05);
  if(mode==='menu'||!LV)return;

  if(mode==='play'){
    if(isTouch&&innerHeight>innerWidth){pauseGame()}
    else if(CFG.quality==='auto'&&autoTier!=='low'&&(warm+=d)>3){
      ftA+=d;
      if(++ftN>=90){
        const avg=ftA/ftN;ftA=ftN=0;
        if(avg>.03){
          autoTier=autoTier==='high'?'med':'low';
          applyQuality();
          toast(L('graphics'));
        }
      }
    }
    if(mode==='play'){
      let dt=d;
      if(G.hitstop>0){G.hitstop-=d;dt=d*.04}
      else if(G.slow>0){G.slow-=d;dt=d*.4}
      const n=dt>1/45?2:1;
      for(let i=0;i<n;i++){update(dt/n);inp.jumpPressed=false}
    }
  }else if(mode==='over'){
    G.overT+=d;G.time+=d;
    updateParticles(d);
    if(G.overT>1.1&&$('panel').style.display!=='flex')showOver();
  }
  render(d);
}
let RDT=0;

/* ========== MENU ========== */
function buildMenu(){
  const m=$('menu');
  const maxW=Math.min(innerWidth,760);
  const maxH=innerHeight*.9;
  let w=maxW,h=w*.75;
  if(h>maxH){h=maxH;w=h/0.75}
  m.style.width=w+'px';m.style.height=h+'px';
  m.style.backgroundImage='url('+SRC.menu+')';
  m.innerHTML=
    '<div style="position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:flex-start;padding-top:6%;pointer-events:none">'+
      '<div style="font-size:clamp(28px,6vh,52px);font-weight:900;color:#ffe45c;text-shadow:0 4px 0 #3a2110,0 0 20px #000;letter-spacing:.05em">SPROUT</div>'+
      '<div style="font-size:clamp(12px,2vh,16px);color:#fbeec1;opacity:.85;margin-top:4px">'+(CFG.lang==='ru'?"Путь садовника":"A Gardener's Journey")+'</div>'+
    '</div>';
  const spec=[
    [7.2,42.6,24.6,10.3,levelSelect,'play'],
    [6.95,54.1,26,9.8,()=>settingsPanel(),'settings'],
    [7.5,65.6,27.5,9.8,()=>collectionPanel(),'collection'],
    [7.5,76.9,29.7,9.8,exitPanel,'more']
  ];
  spec.forEach(([l,t,w,h,fn,key])=>{
    const b=document.createElement('button');
    b.className='hot';
    b.style.cssText='left:'+l+'%;top:'+t+'%;width:'+w+'%;height:'+h+'%';
    const sp=document.createElement('span');
    sp.textContent=L(key);
    b.appendChild(sp);
    b.onclick=()=>{initAudio();sfx('click');fn()};
    b.onmouseenter=()=>sfx('swap');
    m.appendChild(b);
  });
  $('langBtn').onclick=()=>{
    CFG.lang=CFG.lang==='ru'?'en':'ru';
    saveCfg();initAudio();sfx('click');
    buildMenu();
  };
  applyLang();
}
function applyLang(){
  $('langBtn').textContent=CFG.lang==='ru'?'RU · EN':'EN · RU';
  $('rot').textContent=L('rotate');
}

/* ========== PANELS ========== */
function hidePanel(){$('panel').style.display='none'}
function levelSelect(){
  const p=$('panel'),box=$('pbox');
  p.style.display='flex';box.className='box';
  box.innerHTML='<h2>'+L('levels')+'</h2><div class="row" data-row></div><button class="btn" data-back>'+L('back')+'</button>';
  const row=box.querySelector('[data-row]');
  LEVELS.forEach((lv,i)=>{
    const unlocked=i<=PROG.levels;
    const b=document.createElement('button');
    b.className='btn green';
    b.disabled=!unlocked;
    b.textContent=(i+1)+'. '+L(lv.name)+(unlocked?'':' 🔒');
    if(unlocked)b.onclick=()=>{initAudio();sfx('click');hidePanel();go(i)};
    row.appendChild(b);
  });
  box.querySelector('[data-back]').onclick=hidePanel;
}
function settingsPanel(){
  const p=$('panel'),box=$('pbox');
  p.style.display='flex';box.className='box';
  const q=CFG.quality;
  box.innerHTML=
    '<h2>'+L('settings')+'</h2>'+
    '<div class="stat"><span>'+L('music')+'</span><input type="range" min="0" max="1" step="0.05" value="'+CFG.audio.music+'" data-music></div>'+
    '<div class="stat"><span>'+L('sfx')+'</span><input type="range" min="0" max="1" step="0.05" value="'+CFG.audio.sfx+'" data-sfx></div>'+
    '<div class="stat"><span>'+L('quality')+'</span><div class="seg">'+
      ['auto','high','med','low'].map(v=>'<button class="sw '+(q===v?'on':'')+'" data-q="'+v+'">'+L(v)+'</button>').join('')+
    '</div></div>'+
    '<div class="stat"><span>'+L('lefty')+'</span><button class="sw '+(CFG.lefty?'on':'')+'" data-lefty>'+(CFG.lefty?'ON':'OFF')+'</button></div>'+
    '<div class="stat"><span>'+L('hint')+'</span></div>'+
    '<button class="btn" data-back>'+L('back')+'</button>';
  box.querySelector('[data-music]').oninput=e=>{CFG.audio.music=+e.target.value;saveCfg()};
  box.querySelector('[data-sfx]').oninput=e=>{CFG.audio.sfx=+e.target.value;saveCfg()};
  box.querySelectorAll('[data-q]').forEach(b=>b.onclick=()=>{
    CFG.quality=b.dataset.q;saveCfg();applyQuality();settingsPanel();
  });
  box.querySelector('[data-lefty]').onclick=()=>{
    CFG.lefty=!CFG.lefty;saveCfg();applyTouch();settingsPanel();
  };
  box.querySelector('[data-back]').onclick=hidePanel;
}
function collectionPanel(){
  const p=$('panel'),box=$('pbox');
  p.style.display='flex';box.className='box bookbox';
  box.innerHTML=
    '<h2>'+L('collection')+'</h2>'+
    '<div class="book">'+
      '<div class="bpage"><h3>'+L('info')+'</h3>'+
        '<div class="bgrid">'+
          '<div class="bcard"><img src="'+SRC.hatlas+'"><b>'+L('sprout')+'</b><small>'+L('sprout_d')+'</small></div>'+
          '<div class="bcard"><img src="'+SRC.beetle+'"><b>'+L('beetle')+'</b><small>'+L('beetle_d')+'</small></div>'+
          '<div class="bcard"><img src="'+SRC.fly+'"><b>'+L('fly')+'</b><small>'+L('fly_d')+'</small></div>'+
        '</div>'+
      '</div>'+
      '<div class="bspine"></div>'+
      '<div class="bpage"><h3>'+L('stats')+'</h3>'+
        '<div class="stat"><span>'+L('levels')+'</span><b>'+PROG.levels+'/'+LEVELS.length+'</b></div>'+
        '<div class="stat"><span>'+L('coins')+'</span><b>'+PROG.coins+'</b></div>'+
        '<div class="stat"><span>'+L('ability')+'</span><b>'+(PROG.ability?L('unlocked'):L('locked'))+'</b></div>'+
      '</div>'+
    '</div>'+
    '<button class="btn" data-back>'+L('back')+'</button>';
  box.querySelector('[data-back]').onclick=hidePanel;
}
function exitPanel(){
  const p=$('panel'),box=$('pbox');
  p.style.display='flex';box.className='box';
  box.innerHTML=
    '<h2>'+L('exit')+'</h2>'+
    '<button class="btn green" data-fs>'+L('fullscreen')+'</button>'+
    '<button class="btn" data-back>'+L('back')+'</button>';
  box.querySelector('[data-fs]').onclick=()=>{
    if(!document.fullscreenElement)document.documentElement.requestFullscreen&&document.documentElement.requestFullscreen();
    else document.exitFullscreen&&document.exitFullscreen();
  };
  box.querySelector('[data-back]').onclick=hidePanel;
}
function pauseGame(){
  if(mode!=='play')return;
  mode='pause';
  const p=$('panel'),box=$('pbox');
  p.style.display='flex';box.className='box';
  box.innerHTML=
    '<h2>'+L('paused')+'</h2>'+
    '<button class="btn green" data-r>'+L('resume')+'</button>'+
    '<button class="btn" data-s>'+L('restart')+'</button>'+
    '<button class="btn" data-m>'+L('toMenu')+'</button>';
  box.querySelector('[data-r]').onclick=()=>{mode='play';hidePanel()};
  box.querySelector('[data-s]').onclick=()=>startLevel(LV.index);
  box.querySelector('[data-m]').onclick=toMenu;
}
function showOver(){
  const p=$('panel'),box=$('pbox');
  p.style.display='flex';box.className='box';
  box.innerHTML=
    '<h2>'+(G.won?L('youWin'):L('gameOver'))+'</h2>'+
    '<p>'+L('coins')+': <b>'+G.coins+'</b></p>'+
    '<button class="btn green" data-r>'+L('restart')+'</button>'+
    '<button class="btn" data-m>'+L('toMenu')+'</button>';
  box.querySelector('[data-r]').onclick=()=>startLevel(LV.index);
  box.querySelector('[data-m]').onclick=toMenu;
}
$('pauseBtn').onclick=()=>{if(mode==='play')pauseGame();else if(mode==='pause'){mode='play';hidePanel()}};

/* ========== BOOT ========== */
function initGfx(){layout()}
const loadAll=()=>Promise.all(Object.keys(SRC).map(k=>new Promise(res=>{
  const im=new Image();
  im.onload=()=>{IMG[k]=im;res()};
  im.onerror=res;
  im.src=SRC[k];
})));

[['blur',audioSuspend],['focus',audioResume],['pagehide',audioSuspend],
 ['pageshow',audioResume],['freeze',audioSuspend],['resume',audioResume]]
  .forEach(([e,f])=>addEventListener(e,f));
document.addEventListener('visibilitychange',()=>document.hidden?audioSuspend():audioResume());

loadCfg();loadProg();
applyLang();
loadAll().then(()=>{
  initGfx();
  buildMenu();
  applyQuality();
  applyTouch();
  requestAnimationFrame(loop);
});

window.__sprout={
  get cam(){return cam},get AC(){return AC},get P(){return P},
  get enemies(){return enemies},get LV(){return LV},
  get mode(){return mode},get Qe(){return Qe},
  startLevel,go,render,applyQuality,G,CFG,keys
};
})();
</script>
</body>
</html>
