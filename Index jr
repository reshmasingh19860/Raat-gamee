चार दोस्तों का इम्पोस्टर गेम
यह गेम एचटीएमएल और जावास्क्रिप्ट में है। इसे कोडपेन डॉट आईओ में एक ही फ़ाइल की तरह पेस्ट करके चला सकते हैं।
गेम के नियम
चार खिलाड़ी, हर एक का अपना घर। एक छिपा हुआ इम्पोस्टर है। दिन तीन मिनट का और रात एक मिनट की। रात में इम्पोस्टर किसी को खत्म करे तो ज़ोर की आवाज़ आती है, पाँच सेकंड बाद सुबह होती है, और इम्पोस्टर के पास अपने घर लौटने के पंद्रह सेकंड होते हैं। सुबह सब वोट करते हैं। हर रात के बाद हर खिलाड़ी को एक गैजेट मिलता है: टॉर्च, अलार्म, कैमरा, रडार या ताला। इम्पोस्टर को जैमर, नकली आवाज़, तेज़ दौड़ या सेंध में से एक छिपी ताकत मिलती है। दिन में मिशन पूरे करने होते हैं, और बीच में एक मुर्गा है जो दिन-रात बदलने पर बोलता है।
पहला हिस्सा: पेज और मैप
अभी इस दस्तावेज़ में पहला हिस्सा बन रहा है, यानी पेज, आसमान, सूरज, चाँद और चार घरों का मैप। बाकी हिस्से अगले चरण में जुड़ेंगे।
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Imposter Mohalla</title>
<style>
body{margin:0;background:#111;color:#fff;font-family:sans-serif;text-align:center}
canvas{background:#222;max-width:100%;touch-action:none}
#hud{padding:6px;font-size:16px}
</style>
</head>
<body>
<div id="hud">Day 1 - 3:00</div>
<canvas id="game" width="800" height="500"></canvas>
<script>
const c=document.getElementById('game');
const g=c.getContext('2d');
const W=800,H=500;
let isDay=true, timeLeft=180, dayNo=1;

// four houses, one per player
const houses=[
 {x:40,y:60,w:150,h:120,color:'#e74c3c',name:'P1'},
 {x:610,y:60,w:150,h:120,color:'#3498db',name:'P2'},
 {x:40,y:320,w:150,h:120,color:'#2ecc71',name:'P3'},
 {x:610,y:320,w:150,h:120,color:'#f1c40f',name:'P4'}
];

function drawSky(){
 g.fillStyle=isDay?'#87ceeb':'#0b1030';
 g.fillRect(0,0,W,H);
 if(isDay){
  g.fillStyle='#ffd700';
  g.beginPath();g.arc(400,40,25,0,7);g.fill();
 }else{
  g.fillStyle='#eee';
  g.beginPath();g.arc(400,40,20,0,7);g.fill();
 }
}

function drawHouses(){
 for(const h of houses){
  g.fillStyle=h.color;
  g.fillRect(h.x,h.y,h.w,h.h);
  g.fillStyle='#000';
  g.fillRect(h.x+h.w/2-12,h.y+h.h-35,24,35);
  g.fillStyle='#fff';
  g.fillText(h.name,h.x+5,h.y+15);
 }
}

function draw(){
 drawSky();
 drawHouses();
}
draw();
</script>
</body>
</html>
अगले हिस्सों में घरों के अंदर का सामान, किरदारों की चाल, दिन-रात का टाइमर, इम्पोस्टर की ताकतें, गैजेट, मिशन, मुर्गा और वोटिंग जुड़ेगी।
🌙 रात का मोहल्ला: पूरा गेम
गेम का नाम है रात का मोहल्ला। ऊपर वाला पहला कोड सिर्फ़ टेस्ट था, उसे छोड़ दें। असली गेम तीन फ़ाइलों का है और चारों फ़ोन पर ऑनलाइन चलता है।
फ़ोन पर चलाने का तरीका:
1.  replit.com पर Node.js का नया प्रोजेक्ट बनाएँ।
2.  नीचे की तीनों फ़ाइलें पेस्ट करें। index.js और package.json मौजूद फ़ाइलों में बदलें, और public नाम का फ़ोल्डर बनाकर उसमें index.html रखें।
3.  Run दबाएँ और जो लिंक मिले, वह चारों दोस्तों को भेजें।
4.  सब एक ही कमरे का कोड डालें, पहला खिलाड़ी गेम शुरू करे। फ़ोन आड़ा (लैंडस्केप) रखें।
गेम में क्या है: हर खिलाड़ी का अपना घर (सोफ़ा, टीवी, रसोई), दिन 3 मिनट और रात 1 मिनट, सूरज-चाँद-तारे, मुर्गा, ताले, 5 गैजेट क्रू के लिए और 4 इम्पोस्टर के लिए (किसी को दूसरे का गैजेट नहीं दिखता), टाइमर वाले मिशन, सीसीटीवी सुराग, वार के बाद 5 सेकंड में सुबह, 15 सेकंड में घर लौटना और फिर वोटिंग।
1. package.json
{"name":"raat-ka-mohalla","version":"1.0.0","main":"index.js","scripts":{"start":"node index.js"},"dependencies":{"express":"4.19.2","socket.io":"4.7.5"}}
2. index.js (सर्वर)
const express = require('express');
const http = require('http');
const { Server } = require('socket.io');
const app = express();
const srv = http.createServer(app);
const io = new Server(srv);
app.use(express.static(__dirname + '/public'));

const HS = [[30,80,170,130,1],[600,80,170,130,1],[30,400,170,130,0],[600,400,170,130,0]].map(a => ({ x: a[0], y: a[1], w: a[2], h: a[3], top: !!a[4] }));
const DAY = 180, NIGHT = 60, DAWN = 5, RUN = 15, VOTE = 30;
const CREW_G = ['torch','alarm','camera','radar','lock'];
const IMP_G = ['jammer','fake','sprint','window'];
const GN = { torch:'टॉर्च', alarm:'अलार्म', camera:'कैमरा', radar:'रडार', lock:'ताला', jammer:'जैमर', fake:'नकली आवाज़', sprint:'तेज़ दौड़', window:'सेंध' };
const MIS = [
  { name: 'टीवी चालू करो', t: 'tv' },
  { name: 'खाना बनाओ', t: 'kitchen' },
  { name: 'फ्यूज़ ठीक करो', t: 'pt', x: 400, y: 400 },
  { name: 'खोई चाबी ढूँढो', t: 'pt', x: 400, y: 220 }
];
const rooms = {};
const pick = a => a[Math.floor(Math.random() * a.length)];
const aliveOf = r => r.players.filter(p => p.alive);
const toastAll = (r, t) => io.to(r.code).emit('toast', t);
const toastTo = (p, t) => io.to(p.id).emit('toast', t);
function front(i) { const h = HS[i]; return { x: h.x + h.w / 2, y: h.top ? h.y + h.h + 25 : h.y - 25 }; }
function inHouse(p, i) { const h = HS[i]; return p.x > h.x && p.x < h.x + h.w && p.y > h.y && p.y < h.y + h.h; }

function giveMission(r, p) {
  if (!p.alive) return;
  const m = pick(MIS), h = HS[p.i];
  let x = m.x, y = m.y;
  if (m.t === 'tv') { x = h.x + 30; y = h.y + h.h / 2; }
  if (m.t === 'kitchen') { x = h.x + h.w - 30; y = h.y + h.h / 2; }
  p.mission = { name: m.name, x, y, until: Date.now() + (r.phase === 'night' ? 30000 : 90000) };
}

function startDay(r) {
  r.day++; r.phase = 'day'; r.tEnd = Date.now() + DAY * 1000;
  r.locked = {}; r.jam = false; r.entered = {};
  for (const p of aliveOf(r)) {
    p.gadget = pick(p.imp ? IMP_G : CREW_G); p.gUsed = false;
    p.radarLeft = p.gadget === 'radar' ? 2 : 0; p.radarUntil = 0;
    p.torch = p.alarm = p.camera = p.window = p.alarmRang = false; p.sprintUntil = 0;
    giveMission(r, p);
    toastTo(p, '🎁 नया गैजेट मिला: ' + GN[p.gadget]);
  }
  toastAll(r, '🐓 कुकड़ू-कूँ! सुबह हो गई, दिन ' + r.day);
}

function startNight(r) {
  r.phase = 'night'; r.tEnd = Date.now() + NIGHT * 1000;
  for (const p of aliveOf(r)) giveMission(r, p);
  toastAll(r, '🌙 रात हो गई! अँधेरे में सावधान रहो');
}

function checkWin(r) {
  const imp = r.players.find(p => p.imp);
  const crew = r.players.filter(p => !p.imp && p.alive).length;
  let w = null;
  if (!imp.alive) w = 'crew'; else if (crew <= 1) w = 'imp'; else if (r.score >= r.target) w = 'crew';
  if (w) { r.phase = 'over'; r.winner = w; return true; }
  return false;
}

function nextPhase(r) {
  if (r.phase === 'day') return startNight(r);
  if (r.phase === 'night') { toastAll(r, '😴 रात बिना किसी हत्या के बीती'); return startDay(r); }
  if (r.phase === 'dawn') { r.phase = 'run'; r.tEnd = Date.now() + RUN * 1000; toastAll(r, '🏃 इम्पोस्टर के पास 15 सेकंड हैं घर लौटने के'); return; }
  if (r.phase === 'run') {
    const imp = r.players.find(p => p.imp);
    if (imp.alive && !inHouse(imp, imp.i)) {
      let b = 0, bd = 1e9;
      for (let j = 0; j < r.players.length; j++) { const h = HS[j], d = Math.hypot(imp.x - (h.x + h.w / 2), imp.y - (h.y + h.h / 2)); if (d < bd) { bd = d; b = j; } }
      toastAll(r, '👀 ' + r.players[b].name + ' के घर के पास किसी की परछाईं दिखी!');
    } else toastAll(r, '🤷 कोई परछाईं नहीं दिखी');
    r.phase = 'vote'; r.votes = {}; r.tEnd = Date.now() + VOTE * 1000; return;
  }
  if (r.phase === 'vote') {
    const c = {};
    for (const k in r.votes) { const t = r.votes[k]; if (t >= 0) c[t] = (c[t] || 0) + 1; }
    let best = -1, bc = 0;
    for (const t in c) if (c[t] > bc) { bc = c[t]; best = +t; }
    const need = Math.floor(aliveOf(r).length / 2) + 1;
    if (best >= 0 && bc >= need) {
      const v = r.players[best]; v.alive = false;
      toastAll(r, '🗳️ ' + v.name + ' को निकाल दिया गया: ' + (v.imp ? 'वही इम्पोस्टर था!' : 'वह इम्पोस्टर नहीं था'));
    } else toastAll(r, '🗳️ किसी को नहीं निकाला गया');
    if (!checkWin(r)) startDay(r);
  }
}

function nightWatch(r) {
  for (const p of aliveOf(r)) for (let j = 0; j < r.players.length; j++) {
    if (j === p.i || !inHouse(p, j)) continue;
    if (p.imp) r.entered[j] = true;
    const o = r.players[j];
    if (o.alive && o.alarm && !r.jam && !o.alarmRang) { o.alarmRang = true; toastTo(o, '🚨 अलार्म बज रहा है! तुम्हारे घर में कोई घुसा!'); }
  }
}

function broadcast(r) {
  const sh = {
    phase: r.phase, tEnd: r.tEnd, day: r.day, score: r.score, target: r.target, n: r.players.length,
    locked: r.locked || {}, host: r.host, winner: r.winner || null,
    votes: Object.keys(r.votes || {}).length,
    impIdx: r.phase === 'over' ? r.players.findIndex(p => p.imp) : -1,
    players: r.players.map(p => ({ i: p.i, name: p.name, x: p.x, y: p.y, alive: p.alive }))
  };
  for (const p of r.players) {
    io.to(p.id).emit('state', Object.assign({}, sh, { me: {
      i: p.i, imp: !!p.imp, alive: p.alive, gadget: p.gadget, gUsed: p.gUsed, radarLeft: p.radarLeft || 0,
      radarUntil: p.radarUntil || 0, torch: !!p.torch, sprintUntil: p.sprintUntil || 0, window: !!p.window, mission: p.mission
    } }));
  }
}

function tick(r) {
  if (r.phase === 'lobby' || r.phase === 'over') return broadcast(r);
  const t = Date.now();
  if (r.phase === 'day' || r.phase === 'night' || r.phase === 'run') {
    for (const p of r.players) if (p.alive && p.mission && t > p.mission.until) {
      if (!p.imp) r.score = Math.max(0, r.score - 1);
      toastTo(p, '⏰ मिशन छूट गया!'); giveMission(r, p);
    }
  }
  if (r.phase === 'night') nightWatch(r);
  if (t >= r.tEnd) nextPhase(r);
  broadcast(r);
}
setInterval(() => { for (const r of Object.values(rooms)) tick(r); }, 100);

io.on('connection', socket => {
  let r = null, me = null;

  socket.on('join', d => {
    const code = String((d && d.room) || 'ROOM1').toUpperCase().slice(0, 8);
    const room = rooms[code] || (rooms[code] = { code, players: [], phase: 'lobby', tEnd: 0, day: 0, score: 0, target: 0, locked: {}, votes: {}, entered: {}, host: null });
    if (room.phase !== 'lobby' || room.players.length >= 4) return socket.emit('toast', 'कमरा भरा है या गेम शुरू हो चुका है');
    r = room;
    const i = r.players.length;
    me = { id: socket.id, name: String((d && d.name) || 'P' + (i + 1)).slice(0, 10), i, alive: true, x: 0, y: 0 };
    r.players.push(me); socket.join(code); r.host = r.players[0].id;
  });

  socket.on('start', () => {
    if (!r || !me || r.phase !== 'lobby' || r.host !== me.id || r.players.length < 2) return;
    pick(r.players).imp = true;
    r.players.forEach(p => { const f = front(p.i); p.x = f.x; p.y = f.y; p.alive = true; });
    r.target = (r.players.length - 1) * 3; r.score = 0; r.day = 0;
    startDay(r);
    r.players.forEach(p => toastTo(p, p.imp ? '😈 तुम इम्पोस्टर हो!' : '🙂 तुम क्रू हो, मिशन करो और इम्पोस्टर को पकड़ो'));
  });

  socket.on('pos', d => {
    if (!r || !me || !me.alive || !['day','night','run','dawn'].includes(r.phase) || !d) return;
    if (typeof d.x === 'number' && typeof d.y === 'number') { me.x = Math.max(10, Math.min(790, d.x)); me.y = Math.max(70, Math.min(550, d.y)); }
  });

  socket.on('act', () => {
    if (!r || !me || !me.alive || !me.mission || !['day','night','run'].includes(r.phase)) return;
    const m = me.mission;
    if (Math.hypot(me.x - m.x, me.y - m.y) > 40) return toastTo(me, 'मिशन की जगह के पास जाओ');
    if (!me.imp) { r.score++; toastTo(me, '✅ मिशन पूरा! टीम स्कोर +1'); } else toastTo(me, '✅ (नकली मिशन पूरा)');
    giveMission(r, me);
    checkWin(r);
  });

  socket.on('gadget', () => {
    if (!r || !me || !me.alive || !me.gadget || ['lobby','over','vote'].includes(r.phase)) return;
    if (me.gadget !== 'radar' && me.gUsed) return;
    const g = me.gadget;
    if (g === 'torch') me.torch = true;
    if (g === 'alarm') me.alarm = true;
    if (g === 'camera') me.camera = true;
    if (g === 'lock') { r.locked[me.i] = true; }
    if (g === 'jammer') r.jam = true;
    if (g === 'sprint') me.sprintUntil = Date.now() + 20000;
    if (g === 'window') me.window = true;
    if (g === 'radar') { if (me.radarLeft <= 0) return; me.radarLeft--; me.radarUntil = Date.now() + 3000; }
    if (g === 'fake') {
      const o = r.players.filter(p => p.i !== me.i);
      toastAll(r, '👣 ' + pick(o).name + ' के घर की तरफ़ से आवाज़ आई!');
    }
    me.gUsed = true;
    toastTo(me, '✔ ' + GN[g] + ' चालू');
  });

  socket.on('kill', () => {
    if (!r || !me || !me.imp || !me.alive || r.phase !== 'night') return;
    let t = null, d = 45;
    for (const q of r.players) if (q.alive && !q.imp) { const e = Math.hypot(q.x - me.x, q.y - me.y); if (e < d) { d = e; t = q; } }
    if (!t) return toastTo(me, 'कोई पास में नहीं है');
    t.alive = false;
    io.to(r.code).emit('boom');
    toastAll(r, '💀 किसी की चीख़ सुनाई दी!');
    for (const c of r.players) if (c.alive && c.camera && !r.jam && r.entered[c.i]) toastTo(c, '📷 कैमरे में तुम्हारे घर में किसी की परछाईं दिखी!');
    r.phase = 'dawn'; r.tEnd = Date.now() + DAWN * 1000;
    checkWin(r);
  });

  socket.on('vote', t => {
    if (!r || !me || !me.alive || r.phase !== 'vote') return;
    t = +t;
    if (!(t === -1 || (r.players[t] && r.players[t].alive && t !== me.i))) return;
    r.votes[me.i] = t;
    if (Object.keys(r.votes).length >= aliveOf(r).length) r.tEnd = Date.now();
  });

  socket.on('rooster', () => {
    if (!r || !me || !me.imp || r.phase !== 'night' || Date.now() < (r.roosterAt || 0)) return;
    r.roosterAt = Date.now() + 8000;
    toastAll(r, '🐓 मुर्गा अचानक चिल्लाया!');
  });

  socket.on('disconnect', () => {
    if (!r || !me) return;
    if (r.phase === 'lobby') {
      r.players = r.players.filter(p => p !== me);
      r.players.forEach((p, k) => { p.i = k; });
      if (r.players[0]) r.host = r.players[0].id; else delete rooms[r.code];
    } else { me.alive = false; if (r.phase !== 'over') checkWin(r); }
  });
});

srv.listen(process.env.PORT || 3000, () => console.log('रात का मोहल्ला चालू'));
3. public/index.html (गेम की स्क्रीन)
<!DOCTYPE html>
<html lang='hi'><head><meta charset='UTF-8'>
<meta name='viewport' content='width=device-width,initial-scale=1,user-scalable=no'>
<title>रात का मोहल्ला</title>
<style>
*{box-sizing:border-box;user-select:none;-webkit-tap-highlight-color:transparent}
body{margin:0;background:#0d0d14;color:#fff;font-family:sans-serif;overflow:hidden;touch-action:none}
#hud{position:fixed;top:0;left:0;right:0;padding:5px 8px;font-size:13px;background:rgba(0,0,0,.65);z-index:5;line-height:1.4}
#c{width:100%;display:block;margin-top:46px}
#toasts{position:fixed;top:52px;left:0;right:0;z-index:6;text-align:center;pointer-events:none}
#toasts div{display:inline-block;margin:2px;padding:6px 12px;background:rgba(0,0,0,.8);border-radius:14px;font-size:14px}
.ov{position:fixed;top:0;left:0;right:0;bottom:0;background:rgba(5,5,15,.93);z-index:9;display:none;flex-direction:column;align-items:center;justify-content:center;gap:10px;padding:20px;text-align:center}
.ov.on{display:flex}
input,button{font-size:16px;padding:10px 16px;border-radius:10px;border:0}
input{width:230px}
button{background:#f5a623;color:#111;font-weight:bold}
#pad{position:fixed;left:16px;bottom:16px;width:120px;height:120px;border-radius:50%;background:rgba(255,255,255,.12);z-index:4}
#knob{position:absolute;left:40px;top:40px;width:40px;height:40px;border-radius:50%;background:rgba(255,255,255,.5)}
#btns{position:fixed;right:12px;bottom:16px;display:flex;flex-direction:column;gap:8px;z-index:4}
#btns button{min-width:130px;opacity:.92}
#bk{background:#d33;color:#fff;display:none}
</style></head><body>
<div id='hud'></div><div id='toasts'></div>
<canvas id='c'></canvas>
<div id='pad'><div id='knob'></div></div>
<div id='btns'><button id='ba'>✋ काम</button><button id='bg'>🎁 गैजेट</button><button id='bk'>🔪 वार</button></div>
<div id='jn' class='ov on'><h2>🌙 रात का मोहल्ला</h2><input id='nm' placeholder='अपना नाम'><input id='rm' placeholder='कमरे का कोड (जैसे ABC)'><button id='bj'>शामिल हो जाओ</button></div>
<div id='lb' class='ov'><h2 id='lt'></h2><div id='ll'></div><button id='bs'>गेम शुरू करो</button><div id='lw'>पहले खिलाड़ी (होस्ट) के शुरू करने का इंतज़ार... कम से कम 2 खिलाड़ी चाहिए</div></div>
<div id='vt' class='ov'></div>
<div id='ed' class='ov'></div>
<script src='/socket.io/socket.io.js'></script>
<script>
const socket = io(), W = 800, H = 560, T = 6, GAP = 40, R = 9;
const HS = [[30,80,170,130,1],[600,80,170,130,1],[30,400,170,130,0],[600,400,170,130,0]].map(a => ({ x: a[0], y: a[1], w: a[2], h: a[3], top: !!a[4] }));
const COL = ['#e74c3c','#3498db','#2ecc71','#f1c40f'];
const GN = { torch:'टॉर्च', alarm:'अलार्म', camera:'कैमरा', radar:'रडार', lock:'ताला', jammer:'जैमर', fake:'नकली आवाज़', sprint:'तेज़ दौड़', window:'सेंध' };
const PN = { day:'दिन ☀️', night:'रात 🌙', dawn:'सुबह 🌅', run:'दिन ☀️ भागो!', vote:'🗳️ वोटिंग', lobby:'लॉबी', over:'खत्म' };
const $ = id => document.getElementById(id);
const esc = s => String(s).replace(/[&<>]/g, c => ({ '&':'&amp;', '<':'&lt;', '>':'&gt;' }[c]));
const cv = $('c'), g = cv.getContext('2d'); cv.width = W; cv.height = H;
const fog = document.createElement('canvas'); fog.width = W; fog.height = H; const fg = fog.getContext('2d');
const stars = Array.from({ length: 30 }, () => [Math.random() * W, Math.random() * 55]);
let S = null, me = null, pos = { x: 400, y: 300 }, started = false, vec = { x: 0, y: 0 }, keys = {}, disp = {}, roosterCool = 0, myRoom = '';

let ac;
function beep(f, d, t, v) { try { ac = ac || new (window.AudioContext || window.webkitAudioContext)(); const o = ac.createOscillator(), gn = ac.createGain(); o.type = t || 'sine'; o.frequency.value = f; gn.gain.value = v || 0.15; o.connect(gn); gn.connect(ac.destination); o.start(); o.stop(ac.currentTime + d); } catch (e) {} }
function say(t, p) { try { const u = new SpeechSynthesisUtterance(t); u.lang = 'hi-IN'; u.pitch = p || 1; u.rate = 1.1; speechSynthesis.cancel(); speechSynthesis.speak(u); } catch (e) {} }
function toast(t) { const d = document.createElement('div'); d.textContent = t; $('toasts').appendChild(d); setTimeout(() => d.remove(), 4500); }

function walls(i) {
  const h = HS[i], a = (h.w - GAP) / 2, w = [[h.x, h.y, T, h.h], [h.x + h.w - T, h.y, T, h.h]];
  if (h.top) w.push([h.x, h.y, h.w, T], [h.x, h.y + h.h - T, a, T], [h.x + a + GAP, h.y + h.h - T, a, T]);
  else w.push([h.x, h.y + h.h - T, h.w, T], [h.x, h.y, a, T], [h.x + a + GAP, h.y, a, T]);
  return w;
}
function doorRect(i) { const h = HS[i], a = (h.w - GAP) / 2; return h.top ? [h.x + a, h.y + h.h - T, GAP, T] : [h.x + a, h.y, GAP, T]; }
function doorBlocked(i) {
  if (!S || S.phase !== 'night' || me.i === i) return false;
  if (me.imp && (!S.locked[i] || me.window)) return false;
  return true;
}
function hitR(x, y, r, w) { const cx = Math.max(w[0], Math.min(x, w[0] + w[2])), cy = Math.max(w[1], Math.min(y, w[1] + w[3])); return (x - cx) * (x - cx) + (y - cy) * (y - cy) < r * r; }
function hit(x, y) {
  for (let i = 0; i < S.n; i++) {
    for (const w of walls(i)) if (hitR(x, y, R, w)) return true;
    if (doorBlocked(i) && hitR(x, y, R, doorRect(i))) return true;
  }
  return false;
}

function step() {
  if (!me.alive || !['day','night','run','dawn'].includes(S.phase)) return;
  let dx = vec.x + ((keys.arrowright || keys.d) ? 1 : 0) - ((keys.arrowleft || keys.a) ? 1 : 0);
  let dy = vec.y + ((keys.arrowdown || keys.s) ? 1 : 0) - ((keys.arrowup || keys.w) ? 1 : 0);
  const m = Math.hypot(dx, dy); if (m > 1) { dx /= m; dy /= m; }
  let sp = 2.3; if (me.imp) sp *= 1.1; if (me.sprintUntil > Date.now()) sp *= 1.8;
  const nx = pos.x + dx * sp, ny = pos.y + dy * sp;
  if (!hit(nx, pos.y)) pos.x = Math.max(10, Math.min(790, nx));
  if (!hit(pos.x, ny)) pos.y = Math.max(70, Math.min(550, ny));
  if (me.imp && S.phase === 'night' && Math.hypot(pos.x - 400, pos.y - 125) < 45 && Date.now() > roosterCool) { roosterCool = Date.now() + 8000; socket.emit('rooster'); }
}
setInterval(() => { if (S && me && me.alive) socket.emit('pos', pos); }, 50);

function draw() {
  const night = S.phase === 'night', ph = S.phase;
  g.fillStyle = night ? '#070b1f' : '#7ec8ee'; g.fillRect(0, 0, W, 60);
  const total = night ? 60000 : 180000, left = Math.max(0, S.tEnd - Date.now());
  const f = (ph === 'day' || ph === 'night') ? 1 - left / total : 0.04;
  const sx = 40 + f * 720, sy = 48 - Math.sin(f * Math.PI) * 30;
  if (night) {
    g.fillStyle = '#fff'; for (const s of stars) g.fillRect(s[0], s[1], 2, 2);
    g.fillStyle = '#eee'; g.beginPath(); g.arc(sx, sy, 13, 0, 7); g.fill();
    g.fillStyle = '#070b1f'; g.beginPath(); g.arc(sx + 6, sy - 3, 11, 0, 7); g.fill();
  } else {
    g.fillStyle = 'rgba(255,210,63,.35)'; g.beginPath(); g.arc(sx, sy, 24, 0, 7); g.fill();
    g.fillStyle = '#ffd23f'; g.beginPath(); g.arc(sx, sy, 16, 0, 7); g.fill();
  }
  g.fillStyle = night ? '#16261a' : '#5a9e45'; g.fillRect(0, 60, W, H - 60);
  g.fillStyle = night ? '#2a2a22' : '#c9b27c'; g.fillRect(0, 290, W, 40); g.fillRect(380, 60, 40, H - 60);
  g.font = '24px serif'; g.textAlign = 'center';
  g.fillText('🐓', 400, 135); g.fillText('🔌', 400, 410); g.fillText('🔑', 400, 230);
  for (let i = 0; i < S.n; i++) {
    const h = HS[i], col = COL[i];
    g.fillStyle = night ? '#2b2b33' : '#f2e6d0'; g.fillRect(h.x, h.y, h.w, h.h);
    g.fillStyle = col + '44'; g.fillRect(h.x + T, h.y + T, h.w - 2 * T, h.h - 2 * T);
    g.fillStyle = '#7a4b8a'; g.fillRect(h.x + h.w / 2 - 30, h.top ? h.y + T + 4 : h.y + h.h - T - 22, 60, 18);
    g.fillStyle = '#111'; g.fillRect(h.x + T + 2, h.y + h.h / 2 - 16, 10, 32);
    g.fillStyle = night ? '#335' : '#5cf'; g.fillRect(h.x + T + 4, h.y + h.h / 2 - 13, 6, 26);
    g.fillStyle = '#aaa'; g.fillRect(h.x + h.w - T - 14, h.y + h.h / 2 - 18, 12, 36);
    g.fillStyle = col; for (const w of walls(i)) g.fillRect(w[0], w[1], w[2], w[3]);
    const d = doorRect(i); g.fillStyle = doorBlocked(i) ? '#c0392b' : '#8b5a2b'; g.fillRect(d[0], d[1], d[2], d[3]);
    g.fillStyle = '#fff'; g.font = '12px sans-serif';
    g.fillText(S.players[i] ? S.players[i].name : 'P' + (i + 1), h.x + h.w / 2, h.top ? h.y - 6 : h.y + h.h + 14);
  }
  if (me.alive && me.mission) { const m = me.mission, p = 3 * Math.sin(Date.now() / 200); g.strokeStyle = '#ffe14d'; g.lineWidth = 3; g.beginPath(); g.arc(m.x, m.y, 14 + p, 0, 7); g.stroke(); }
  for (const p of S.players) {
    const d = disp[p.i] || (disp[p.i] = { x: p.x, y: p.y });
    if (p.i === me.i) { d.x = pos.x; d.y = pos.y; } else { d.x += (p.x - d.x) * 0.25; d.y += (p.y - d.y) * 0.25; }
    if (!p.alive) { g.fillStyle = '#999'; g.font = 'bold 18px sans-serif'; g.fillText('✕', d.x, d.y + 6); continue; }
    g.fillStyle = COL[p.i]; g.beginPath(); g.arc(d.x, d.y, R, 0, 7); g.fill();
    g.strokeStyle = (S.impIdx === p.i || (p.i === me.i && me.imp)) ? '#f00' : '#fff'; g.lineWidth = 2; g.stroke();
    g.fillStyle = '#fff'; g.font = '11px sans-serif'; g.fillText(p.name, d.x, d.y - 14);
  }
  if (night && me.alive) {
    fg.globalCompositeOperation = 'source-over'; fg.clearRect(0, 0, W, H);
    fg.fillStyle = 'rgba(2,4,14,.97)'; fg.fillRect(0, 0, W, H);
    const rad = me.torch ? 150 : 75;
    const gr = fg.createRadialGradient(pos.x, pos.y, rad * 0.3, pos.x, pos.y, rad);
    gr.addColorStop(0, 'rgba(0,0,0,1)'); gr.addColorStop(1, 'rgba(0,0,0,0)');
    fg.globalCompositeOperation = 'destination-out'; fg.fillStyle = gr; fg.beginPath(); fg.arc(pos.x, pos.y, rad, 0, 7); fg.fill();
    g.drawImage(fog, 0, 0);
    if (me.radarUntil > Date.now()) {
      for (const p of S.players) if (p.alive && p.i !== me.i && Math.hypot(p.x - pos.x, p.y - pos.y) < 170) { g.fillStyle = '#ff3b3b'; g.beginPath(); g.arc(p.x, p.y, 6, 0, 7); g.fill(); }
      g.strokeStyle = '#3f3'; g.lineWidth = 1; g.beginPath(); g.arc(pos.x, pos.y, 170, 0, 7); g.stroke();
    }
  }
  const sec = Math.max(0, Math.ceil((S.tEnd - Date.now()) / 1000));
  let l2 = '💀 तुम खत्म हो, देखते रहो';
  if (me.alive) l2 = (me.imp ? '😈 तुम इम्पोस्टर हो | ' : '🙂 क्रू | ') + (me.mission ? '📋 ' + me.mission.name + ' (' + Math.max(0, Math.ceil((me.mission.until - Date.now()) / 1000)) + 's)' : '');
  $('hud').innerHTML = PN[ph] + ' • दिन ' + S.day + ' • ⏱ ' + sec + 's • टीम स्कोर ' + S.score + '/' + S.target + '<br>' + l2;
}

function ui() {
  $('jn').classList.remove('on');
  const lobby = S.phase === 'lobby';
  $('lb').classList.toggle('on', lobby);
  if (lobby) {
    $('lt').textContent = 'कमरा: ' + myRoom;
    $('ll').innerHTML = S.players.map(p => '<div>' + (p.i + 1) + '. ' + esc(p.name) + '</div>').join('');
    const host = S.host === socket.id;
    $('bs').style.display = host && S.players.length >= 2 ? 'block' : 'none';
    $('lw').style.display = host && S.players.length >= 2 ? 'none' : 'block';
  }
  const vote = S.phase === 'vote' && me.alive;
  if (vote && !$('vt').classList.contains('on')) {
    $('vt').innerHTML = '<h2>🗳️ इम्पोस्टर कौन है?</h2>' + S.players.filter(p => p.alive && p.i !== me.i).map(p => '<button data-i=' + p.i + '>' + esc(p.name) + '</button>').join('') + '<button data-i=-1 style=background:#888>⏭ स्किप</button><div id=vm></div><div id=vc></div>';
  }
  $('vt').classList.toggle('on', vote);
  if (vote && $('vc')) $('vc').textContent = S.votes + ' ने वोट दिया';
  const over = S.phase === 'over';
  $('ed').classList.toggle('on', over);
  if (over) $('ed').innerHTML = '<h1>' + (S.winner === 'crew' ? '🎉 क्रू जीत गया!' : '😈 इम्पोस्टर जीत गया!') + '</h1><div>इम्पोस्टर था: ' + esc(S.players[S.impIdx] ? S.players[S.impIdx].name : '') + '</div><button onclick=location.reload()>फिर से खेलो</button>';
  if (me.gadget) { let gl = '🎁 ' + GN[me.gadget]; if (me.gadget === 'radar') gl += ' x' + me.radarLeft; else if (me.gUsed) gl += ' ✔'; $('bg').textContent = gl; }
  $('bk').style.display = me.imp && me.alive && S.phase === 'night' ? 'block' : 'none';
}

function onPhase(p) {
  if (p === 'night') { beep(180, 0.6, 'sawtooth', 0.2); say('रात हो गई', 0.5); }
  else if (p === 'day') { beep(900, 0.15); say('कुकड़ू कूँ', 1.4); }
  else if (p === 'vote') beep(500, 0.3, 'square');
}

socket.on('state', s => {
  const old = S && S.phase; S = s; me = s.me;
  if (s.phase !== 'lobby' && !started) { started = true; const mp = s.players[me.i]; pos = { x: mp.x, y: mp.y }; }
  if (s.phase !== old) onPhase(s.phase);
  ui();
});
socket.on('toast', toast);
socket.on('boom', () => beep(70, 0.7, 'sawtooth', 0.4));

$('bj').onclick = () => { myRoom = ($('rm').value || 'ROOM1').toUpperCase(); beep(1, 0.01); socket.emit('join', { room: myRoom, name: $('nm').value }); };
$('bs').onclick = () => socket.emit('start');
$('ba').onclick = () => socket.emit('act');
$('bg').onclick = () => socket.emit('gadget');
$('bk').onclick = () => socket.emit('kill');
$('vt').onclick = e => { const b = e.target.closest('button'); if (b) { socket.emit('vote', +b.dataset.i); $('vm').textContent = '✔ तुमने वोट दे दिया'; } };

const pad = $('pad'), kn = $('knob'); let down = false;
function pm(e) { const r = pad.getBoundingClientRect(); let dx = e.clientX - (r.left + 60), dy = e.clientY - (r.top + 60); const m = Math.hypot(dx, dy) || 1, k = Math.min(m, 50) / m; dx *= k; dy *= k; vec = { x: dx / 50, y: dy / 50 }; kn.style.transform = 'translate(' + dx + 'px,' + dy + 'px)'; }
pad.addEventListener('pointerdown', e => { down = true; pad.setPointerCapture(e.pointerId); pm(e); });
pad.addEventListener('pointermove', e => { if (down) pm(e); });
const rel = () => { down = false; vec = { x: 0, y: 0 }; kn.style.transform = ''; };
pad.addEventListener('pointerup', rel); pad.addEventListener('pointercancel', rel);
window.addEventListener('keydown', e => { const k = e.key.toLowerCase(); keys[k] = true; if (k === ' ') socket.emit('act'); if (k === 'e') socket.emit('gadget'); if (k === 'k') socket.emit('kill'); });
window.addEventListener('keyup', e => { keys[e.key.toLowerCase()] = false; });

function loop() { if (S && me && S.phase !== 'lobby') { step(); draw(); } requestAnimationFrame(loop); }
loop();
</script></body></html>
खेलने के नियम: चलने के लिए बाईं तरफ़ जॉयस्टिक, मिशन की जगह (पीला घेरा) पर जाकर ✋ दबाएँ। 🎁 से गैजेट चालू होता है, रडार के दो उपयोग होते हैं। इम्पोस्टर रात में किसी के पास जाकर 🔪 दबाता है। वार के बाद 5 सेकंड में सुबह, 15 सेकंड में इम्पोस्टर को घर लौटना है, फिर 30 सेकंड की वोटिंग। क्रू तब जीतता है जब टीम स्कोर लक्ष्य तक पहुँचे या इम्पोस्टर निकाल दिया जाए। इम्पोस्टर तब जीतता है जब क्रू में सिर्फ़ एक बचे।
⚡ एक ही फ़ाइल वाला वर्ज़न (यही इस्तेमाल करें)
ऊपर की तीनों फ़ाइलें छोड़ दें। यह एक ही फ़ाइल में पूरा गेम है, सर्वर भी और स्क्रीन भी।
1.  replit.com पर Node.js का नया प्रोजेक्ट बनाएँ।
2.  index.js खोलकर उसका सारा लिखा मिटाएँ और नीचे का पूरा कोड पेस्ट करें। package.json और बाकी फ़ाइलों को हाथ न लगाएँ।
3.  Run दबाएँ। Replit खुद express और socket.io इंस्टॉल कर लेता है। अगर न करे, तो Shell में लिखें: npm install express socket.io
4.  जो लिंक मिले, वह चारों दोस्तों को भेजें। सब एक ही कमरे का कोड डालें।
const express = require('express');
const http = require('http');
const { Server } = require('socket.io');
const app = express();
const srv = http.createServer(app);
const io = new Server(srv);
app.get('/', (q, s) => s.send(PAGE));

const HS = [[30,80,170,130,1],[600,80,170,130,1],[30,400,170,130,0],[600,400,170,130,0]].map(a => ({ x: a[0], y: a[1], w: a[2], h: a[3], top: !!a[4] }));
const DAY = 180, NIGHT = 60, DAWN = 5, RUN = 15, VOTE = 30;
const CREW_G = ['torch','alarm','camera','radar','lock'];
const IMP_G = ['jammer','fake','sprint','window'];
const GN = { torch:'टॉर्च', alarm:'अलार्म', camera:'कैमरा', radar:'रडार', lock:'ताला', jammer:'जैमर', fake:'नकली आवाज़', sprint:'तेज़ दौड़', window:'सेंध' };
const MIS = [
  { name: 'टीवी चालू करो', t: 'tv' },
  { name: 'खाना बनाओ', t: 'kitchen' },
  { name: 'फ्यूज़ ठीक करो', t: 'pt', x: 400, y: 400 },
  { name: 'खोई चाबी ढूँढो', t: 'pt', x: 400, y: 220 }
];
const rooms = {};
const pick = a => a[Math.floor(Math.random() * a.length)];
const aliveOf = r => r.players.filter(p => p.alive);
const toastAll = (r, t) => io.to(r.code).emit('toast', t);
const toastTo = (p, t) => io.to(p.id).emit('toast', t);
function front(i) { const h = HS[i]; return { x: h.x + h.w / 2, y: h.top ? h.y + h.h + 25 : h.y - 25 }; }
function inHouse(p, i) { const h = HS[i]; return p.x > h.x && p.x < h.x + h.w && p.y > h.y && p.y < h.y + h.h; }

function giveMission(r, p) {
  if (!p.alive) return;
  const m = pick(MIS), h = HS[p.i];
  let x = m.x, y = m.y;
  if (m.t === 'tv') { x = h.x + 30; y = h.y + h.h / 2; }
  if (m.t === 'kitchen') { x = h.x + h.w - 30; y = h.y + h.h / 2; }
  p.mission = { name: m.name, x, y, until: Date.now() + (r.phase === 'night' ? 30000 : 90000) };
}

function startDay(r) {
  r.day++; r.phase = 'day'; r.tEnd = Date.now() + DAY * 1000;
  r.locked = {}; r.jam = false; r.entered = {};
  for (const p of aliveOf(r)) {
    p.gadget = pick(p.imp ? IMP_G : CREW_G); p.gUsed = false;
    p.radarLeft = p.gadget === 'radar' ? 2 : 0; p.radarUntil = 0;
    p.torch = p.alarm = p.camera = p.window = p.alarmRang = false; p.sprintUntil = 0;
    giveMission(r, p);
    toastTo(p, '🎁 नया गैजेट मिला: ' + GN[p.gadget]);
  }
  toastAll(r, '🐓 कुकड़ू-कूँ! सुबह हो गई, दिन ' + r.day);
}

function startNight(r) {
  r.phase = 'night'; r.tEnd = Date.now() + NIGHT * 1000;
  for (const p of aliveOf(r)) giveMission(r, p);
  toastAll(r, '🌙 रात हो गई! अँधेरे में सावधान रहो');
}

function checkWin(r) {
  const imp = r.players.find(p => p.imp);
  const crew = r.players.filter(p => !p.imp && p.alive).length;
  let w = null;
  if (!imp.alive) w = 'crew'; else if (crew <= 1) w = 'imp'; else if (r.score >= r.target) w = 'crew';
  if (w) { r.phase = 'over'; r.winner = w; return true; }
  return false;
}

function nextPhase(r) {
  if (r.phase === 'day') return startNight(r);
  if (r.phase === 'night') { toastAll(r, '😴 रात बिना किसी हत्या के बीती'); return startDay(r); }
  if (r.phase === 'dawn') { r.phase = 'run'; r.tEnd = Date.now() + RUN * 1000; toastAll(r, '🏃 इम्पोस्टर के पास 15 सेकंड हैं घर लौटने के'); return; }
  if (r.phase === 'run') {
    const imp = r.players.find(p => p.imp);
    if (imp.alive && !inHouse(imp, imp.i)) {
      let b = 0, bd = 1e9;
      for (let j = 0; j < r.players.length; j++) { const h = HS[j], d = Math.hypot(imp.x - (h.x + h.w / 2), imp.y - (h.y + h.h / 2)); if (d < bd) { bd = d; b = j; } }
      toastAll(r, '👀 ' + r.players[b].name + ' के घर के पास किसी की परछाईं दिखी!');
    } else toastAll(r, '🤷 कोई परछाईं नहीं दिखी');
    r.phase = 'vote'; r.votes = {}; r.tEnd = Date.now() + VOTE * 1000; return;
  }
  if (r.phase === 'vote') {
    const c = {};
    for (const k in r.votes) { const t = r.votes[k]; if (t >= 0) c[t] = (c[t] || 0) + 1; }
    let best = -1, bc = 0;
    for (const t in c) if (c[t] > bc) { bc = c[t]; best = +t; }
    const need = Math.floor(aliveOf(r).length / 2) + 1;
    if (best >= 0 && bc >= need) {
      const v = r.players[best]; v.alive = false;
      toastAll(r, '🗳️ ' + v.name + ' को निकाल दिया गया: ' + (v.imp ? 'वही इम्पोस्टर था!' : 'वह इम्पोस्टर नहीं था'));
    } else toastAll(r, '🗳️ किसी को नहीं निकाला गया');
    if (!checkWin(r)) startDay(r);
  }
}

function nightWatch(r) {
  for (const p of aliveOf(r)) for (let j = 0; j < r.players.length; j++) {
    if (j === p.i || !inHouse(p, j)) continue;
    if (p.imp) r.entered[j] = true;
    const o = r.players[j];
    if (o.alive && o.alarm && !r.jam && !o.alarmRang) { o.alarmRang = true; toastTo(o, '🚨 अलार्म बज रहा है! तुम्हारे घर में कोई घुसा!'); }
  }
}

function broadcast(r) {
  const sh = {
    phase: r.phase, tEnd: r.tEnd, day: r.day, score: r.score, target: r.target, n: r.players.length,
    locked: r.locked || {}, host: r.host, winner: r.winner || null,
    votes: Object.keys(r.votes || {}).length,
    impIdx: r.phase === 'over' ? r.players.findIndex(p => p.imp) : -1,
    players: r.players.map(p => ({ i: p.i, name: p.name, x: p.x, y: p.y, alive: p.alive }))
  };
  for (const p of r.players) {
    io.to(p.id).emit('state', Object.assign({}, sh, { me: {
      i: p.i, imp: !!p.imp, alive: p.alive, gadget: p.gadget, gUsed: p.gUsed, radarLeft: p.radarLeft || 0,
      radarUntil: p.radarUntil || 0, torch: !!p.torch, sprintUntil: p.sprintUntil || 0, window: !!p.window, mission: p.mission
    } }));
  }
}

function tick(r) {
  if (r.phase === 'lobby' || r.phase === 'over') return broadcast(r);
  const t = Date.now();
  if (r.phase === 'day' || r.phase === 'night' || r.phase === 'run') {
    for (const p of r.players) if (p.alive && p.mission && t > p.mission.until) {
      if (!p.imp) r.score = Math.max(0, r.score - 1);
      toastTo(p, '⏰ मिशन छूट गया!'); giveMission(r, p);
    }
  }
  if (r.phase === 'night') nightWatch(r);
  if (t >= r.tEnd) nextPhase(r);
  broadcast(r);
}
setInterval(() => { for (const r of Object.values(rooms)) tick(r); }, 100);

io.on('connection', socket => {
  let r = null, me = null;

  socket.on('join', d => {
    const code = String((d && d.room) || 'ROOM1').toUpperCase().slice(0, 8);
    const room = rooms[code] || (rooms[code] = { code, players: [], phase: 'lobby', tEnd: 0, day: 0, score: 0, target: 0, locked: {}, votes: {}, entered: {}, host: null });
    if (room.phase !== 'lobby' || room.players.length >= 4) return socket.emit('toast', 'कमरा भरा है या गेम शुरू हो चुका है');
    r = room;
    const i = r.players.length;
    me = { id: socket.id, name: String((d && d.name) || 'P' + (i + 1)).slice(0, 10), i, alive: true, x: 0, y: 0 };
    r.players.push(me); socket.join(code); r.host = r.players[0].id;
  });

  socket.on('start', () => {
    if (!r || !me || r.phase !== 'lobby' || r.host !== me.id || r.players.length < 2) return;
    pick(r.players).imp = true;
    r.players.forEach(p => { const f = front(p.i); p.x = f.x; p.y = f.y; p.alive = true; });
    r.target = (r.players.length - 1) * 3; r.score = 0; r.day = 0;
    startDay(r);
    r.players.forEach(p => toastTo(p, p.imp ? '😈 तुम इम्पोस्टर हो!' : '🙂 तुम क्रू हो, मिशन करो और इम्पोस्टर को पकड़ो'));
  });

  socket.on('pos', d => {
    if (!r || !me || !me.alive || !['day','night','run','dawn'].includes(r.phase) || !d) return;
    if (typeof d.x === 'number' && typeof d.y === 'number') { me.x = Math.max(10, Math.min(790, d.x)); me.y = Math.max(70, Math.min(550, d.y)); }
  });

  socket.on('act', () => {
    if (!r || !me || !me.alive || !me.mission || !['day','night','run'].includes(r.phase)) return;
    const m = me.mission;
    if (Math.hypot(me.x - m.x, me.y - m.y) > 40) return toastTo(me, 'मिशन की जगह के पास जाओ');
    if (!me.imp) { r.score++; toastTo(me, '✅ मिशन पूरा! टीम स्कोर +1'); } else toastTo(me, '✅ (नकली मिशन पूरा)');
    giveMission(r, me);
    checkWin(r);
  });

  socket.on('gadget', () => {
    if (!r || !me || !me.alive || !me.gadget || ['lobby','over','vote'].includes(r.phase)) return;
    if (me.gadget !== 'radar' && me.gUsed) return;
    const g = me.gadget;
    if (g === 'torch') me.torch = true;
    if (g === 'alarm') me.alarm = true;
    if (g === 'camera') me.camera = true;
    if (g === 'lock') { r.locked[me.i] = true; }
    if (g === 'jammer') r.jam = true;
    if (g === 'sprint') me.sprintUntil = Date.now() + 20000;
    if (g === 'window') me.window = true;
    if (g === 'radar') { if (me.radarLeft <= 0) return; me.radarLeft--; me.radarUntil = Date.now() + 3000; }
    if (g === 'fake') {
      const o = r.players.filter(p => p.i !== me.i);
      toastAll(r, '👣 ' + pick(o).name + ' के घर की तरफ़ से आवाज़ आई!');
    }
    me.gUsed = true;
    toastTo(me, '✔ ' + GN[g] + ' चालू');
  });

  socket.on('kill', () => {
    if (!r || !me || !me.imp || !me.alive || r.phase !== 'night') return;
    let t = null, d = 45;
    for (const q of r.players) if (q.alive && !q.imp) { const e = Math.hypot(q.x - me.x, q.y - me.y); if (e < d) { d = e; t = q; } }
    if (!t) return toastTo(me, 'कोई पास में नहीं है');
    t.alive = false;
    io.to(r.code).emit('boom');
    toastAll(r, '💀 किसी की चीख़ सुनाई दी!');
    for (const c of r.players) if (c.alive && c.camera && !r.jam && r.entered[c.i]) toastTo(c, '📷 कैमरे में तुम्हारे घर में किसी की परछाईं दिखी!');
    r.phase = 'dawn'; r.tEnd = Date.now() + DAWN * 1000;
    checkWin(r);
  });

  socket.on('vote', t => {
    if (!r || !me || !me.alive || r.phase !== 'vote') return;
    t = +t;
    if (!(t === -1 || (r.players[t] && r.players[t].alive && t !== me.i))) return;
    r.votes[me.i] = t;
    if (Object.keys(r.votes).length >= aliveOf(r).length) r.tEnd = Date.now();
  });

  socket.on('rooster', () => {
    if (!r || !me || !me.imp || r.phase !== 'night' || Date.now() < (r.roosterAt || 0)) return;
    r.roosterAt = Date.now() + 8000;
    toastAll(r, '🐓 मुर्गा अचानक चिल्लाया!');
  });

  socket.on('disconnect', () => {
    if (!r || !me) return;
    if (r.phase === 'lobby') {
      r.players = r.players.filter(p => p !== me);
      r.players.forEach((p, k) => { p.i = k; });
      if (r.players[0]) r.host = r.players[0].id; else delete rooms[r.code];
    } else { me.alive = false; if (r.phase !== 'over') checkWin(r); }
  });
});

const PAGE = `<!DOCTYPE html>
<html lang='hi'><head><meta charset='UTF-8'>
<meta name='viewport' content='width=device-width,initial-scale=1,user-scalable=no'>
<title>रात का मोहल्ला</title>
<style>
*{box-sizing:border-box;user-select:none;-webkit-tap-highlight-color:transparent}
body{margin:0;background:#0d0d14;color:#fff;font-family:sans-serif;overflow:hidden;touch-action:none}
#hud{position:fixed;top:0;left:0;right:0;padding:5px 8px;font-size:13px;background:rgba(0,0,0,.65);z-index:5;line-height:1.4}
#c{width:100%;display:block;margin-top:46px}
#toasts{position:fixed;top:52px;left:0;right:0;z-index:6;text-align:center;pointer-events:none}
#toasts div{display:inline-block;margin:2px;padding:6px 12px;background:rgba(0,0,0,.8);border-radius:14px;font-size:14px}
.ov{position:fixed;top:0;left:0;right:0;bottom:0;background:rgba(5,5,15,.93);z-index:9;display:none;flex-direction:column;align-items:center;justify-content:center;gap:10px;padding:20px;text-align:center}
.ov.on{display:flex}
input,button{font-size:16px;padding:10px 16px;border-radius:10px;border:0}
input{width:230px}
button{background:#f5a623;color:#111;font-weight:bold}
#pad{position:fixed;left:16px;bottom:16px;width:120px;height:120px;border-radius:50%;background:rgba(255,255,255,.12);z-index:4}
#knob{position:absolute;left:40px;top:40px;width:40px;height:40px;border-radius:50%;background:rgba(255,255,255,.5)}
#btns{position:fixed;right:12px;bottom:16px;display:flex;flex-direction:column;gap:8px;z-index:4}
#btns button{min-width:130px;opacity:.92}
#bk{background:#d33;color:#fff;display:none}
</style></head><body>
<div id='hud'></div><div id='toasts'></div>
<canvas id='c'></canvas>
<div id='pad'><div id='knob'></div></div>
<div id='btns'><button id='ba'>✋ काम</button><button id='bg'>🎁 गैजेट</button><button id='bk'>🔪 वार</button><button id='bq' style=background:#555;color:#fff>❓ मदद</button></div>
<div id='jn' class='ov on'><h2>🌙 रात का मोहल्ला</h2><input id='nm' placeholder='अपना नाम'><input id='rm' placeholder='कमरे का कोड (जैसे ABC)'><button id='bj'>शामिल हो जाओ</button><button id='bh' style=background:#444;color:#fff>📖 कैसे खेलें</button></div>
<div id='lb' class='ov'><h2 id='lt'></h2><div id='ll'></div><button id='bs'>गेम शुरू करो</button><div id='lw'>पहले खिलाड़ी (होस्ट) के शुरू करने का इंतज़ार... कम से कम 2 खिलाड़ी चाहिए</div></div>
<div id='vt' class='ov'></div>
<div id='ed' class='ov'></div><div id='tt' class='ov'></div>
<script src='/socket.io/socket.io.js'></script>
<script>
const socket = io(), W = 800, H = 560, T = 6, GAP = 40, R = 9;
const HS = [[30,80,170,130,1],[600,80,170,130,1],[30,400,170,130,0],[600,400,170,130,0]].map(a => ({ x: a[0], y: a[1], w: a[2], h: a[3], top: !!a[4] }));
const COL = ['#e74c3c','#3498db','#2ecc71','#f1c40f'];
const GN = { torch:'टॉर्च', alarm:'अलार्म', camera:'कैमरा', radar:'रडार', lock:'ताला', jammer:'जैमर', fake:'नकली आवाज़', sprint:'तेज़ दौड़', window:'सेंध' };
const PN = { day:'दिन ☀️', night:'रात 🌙', dawn:'सुबह 🌅', run:'दिन ☀️ भागो!', vote:'🗳️ वोटिंग', lobby:'लॉबी', over:'खत्म' };
const $ = id => document.getElementById(id);
const esc = s => String(s).replace(/[&<>]/g, c => ({ '&':'&amp;', '<':'&lt;', '>':'&gt;' }[c]));
const cv = $('c'), g = cv.getContext('2d'); cv.width = W; cv.height = H;
const fog = document.createElement('canvas'); fog.width = W; fog.height = H; const fg = fog.getContext('2d');
const stars = Array.from({ length: 30 }, () => [Math.random() * W, Math.random() * 55]);
let S = null, me = null, pos = { x: 400, y: 300 }, started = false, vec = { x: 0, y: 0 }, keys = {}, disp = {}, roosterCool = 0, myRoom = '';

let ac;
function beep(f, d, t, v) { try { ac = ac || new (window.AudioContext || window.webkitAudioContext)(); const o = ac.createOscillator(), gn = ac.createGain(); o.type = t || 'sine'; o.frequency.value = f; gn.gain.value = v || 0.15; o.connect(gn); gn.connect(ac.destination); o.start(); o.stop(ac.currentTime + d); } catch (e) {} }
function say(t, p) { try { const u = new SpeechSynthesisUtterance(t); u.lang = 'hi-IN'; u.pitch = p || 1; u.rate = 1.1; speechSynthesis.cancel(); speechSynthesis.speak(u); } catch (e) {} }
function toast(t) { const d = document.createElement('div'); d.textContent = t; $('toasts').appendChild(d); setTimeout(() => d.remove(), 4500); }

function walls(i) {
  const h = HS[i], a = (h.w - GAP) / 2, w = [[h.x, h.y, T, h.h], [h.x + h.w - T, h.y, T, h.h]];
  if (h.top) w.push([h.x, h.y, h.w, T], [h.x, h.y + h.h - T, a, T], [h.x + a + GAP, h.y + h.h - T, a, T]);
  else w.push([h.x, h.y + h.h - T, h.w, T], [h.x, h.y, a, T], [h.x + a + GAP, h.y, a, T]);
  return w;
}
function doorRect(i) { const h = HS[i], a = (h.w - GAP) / 2; return h.top ? [h.x + a, h.y + h.h - T, GAP, T] : [h.x + a, h.y, GAP, T]; }
function doorBlocked(i) {
  if (!S || S.phase !== 'night' || me.i === i) return false;
  if (me.imp && (!S.locked[i] || me.window)) return false;
  return true;
}
function hitR(x, y, r, w) { const cx = Math.max(w[0], Math.min(x, w[0] + w[2])), cy = Math.max(w[1], Math.min(y, w[1] + w[3])); return (x - cx) * (x - cx) + (y - cy) * (y - cy) < r * r; }
function hit(x, y) {
  for (let i = 0; i < S.n; i++) {
    for (const w of walls(i)) if (hitR(x, y, R, w)) return true;
    if (doorBlocked(i) && hitR(x, y, R, doorRect(i))) return true;
  }
  return false;
}

function step() {
  if (!me.alive || !['day','night','run','dawn'].includes(S.phase)) return;
  let dx = vec.x + ((keys.arrowright || keys.d) ? 1 : 0) - ((keys.arrowleft || keys.a) ? 1 : 0);
  let dy = vec.y + ((keys.arrowdown || keys.s) ? 1 : 0) - ((keys.arrowup || keys.w) ? 1 : 0);
  const m = Math.hypot(dx, dy); if (m > 1) { dx /= m; dy /= m; }
  let sp = 2.3; if (me.imp) sp *= 1.1; if (me.sprintUntil > Date.now()) sp *= 1.8;
  const nx = pos.x + dx * sp, ny = pos.y + dy * sp;
  if (!hit(nx, pos.y)) pos.x = Math.max(10, Math.min(790, nx));
  if (!hit(pos.x, ny)) pos.y = Math.max(70, Math.min(550, ny));
  if (me.imp && S.phase === 'night' && Math.hypot(pos.x - 400, pos.y - 125) < 45 && Date.now() > roosterCool) { roosterCool = Date.now() + 8000; socket.emit('rooster'); }
}
setInterval(() => { if (S && me && me.alive) socket.emit('pos', pos); }, 50);

function draw() {
  const night = S.phase === 'night', ph = S.phase;
  g.fillStyle = night ? '#070b1f' : '#7ec8ee'; g.fillRect(0, 0, W, 60);
  const total = night ? 60000 : 180000, left = Math.max(0, S.tEnd - Date.now());
  const f = (ph === 'day' || ph === 'night') ? 1 - left / total : 0.04;
  const sx = 40 + f * 720, sy = 48 - Math.sin(f * Math.PI) * 30;
  if (night) {
    g.fillStyle = '#fff'; for (const s of stars) g.fillRect(s[0], s[1], 2, 2);
    g.fillStyle = '#eee'; g.beginPath(); g.arc(sx, sy, 13, 0, 7); g.fill();
    g.fillStyle = '#070b1f'; g.beginPath(); g.arc(sx + 6, sy - 3, 11, 0, 7); g.fill();
  } else {
    g.fillStyle = 'rgba(255,210,63,.35)'; g.beginPath(); g.arc(sx, sy, 24, 0, 7); g.fill();
    g.fillStyle = '#ffd23f'; g.beginPath(); g.arc(sx, sy, 16, 0, 7); g.fill();
  }
  g.fillStyle = night ? '#16261a' : '#5a9e45'; g.fillRect(0, 60, W, H - 60);
  g.fillStyle = night ? '#2a2a22' : '#c9b27c'; g.fillRect(0, 290, W, 40); g.fillRect(380, 60, 40, H - 60);
  g.font = '24px serif'; g.textAlign = 'center';
  g.fillText('🐓', 400, 135); g.fillText('🔌', 400, 410); g.fillText('🔑', 400, 230);
  for (let i = 0; i < S.n; i++) {
    const h = HS[i], col = COL[i];
    g.fillStyle = night ? '#2b2b33' : '#f2e6d0'; g.fillRect(h.x, h.y, h.w, h.h);
    g.fillStyle = col + '44'; g.fillRect(h.x + T, h.y + T, h.w - 2 * T, h.h - 2 * T);
    g.fillStyle = '#7a4b8a'; g.fillRect(h.x + h.w / 2 - 30, h.top ? h.y + T + 4 : h.y + h.h - T - 22, 60, 18);
    g.fillStyle = '#111'; g.fillRect(h.x + T + 2, h.y + h.h / 2 - 16, 10, 32);
    g.fillStyle = night ? '#335' : '#5cf'; g.fillRect(h.x + T + 4, h.y + h.h / 2 - 13, 6, 26);
    g.fillStyle = '#aaa'; g.fillRect(h.x + h.w - T - 14, h.y + h.h / 2 - 18, 12, 36);
    g.fillStyle = col; for (const w of walls(i)) g.fillRect(w[0], w[1], w[2], w[3]);
    const d = doorRect(i); g.fillStyle = doorBlocked(i) ? '#c0392b' : '#8b5a2b'; g.fillRect(d[0], d[1], d[2], d[3]);
    g.fillStyle = '#fff'; g.font = '12px sans-serif';
    g.fillText(S.players[i] ? S.players[i].name : 'P' + (i + 1), h.x + h.w / 2, h.top ? h.y - 6 : h.y + h.h + 14);
  }
  if (me.alive && me.mission) { const m = me.mission, p = 3 * Math.sin(Date.now() / 200); g.strokeStyle = '#ffe14d'; g.lineWidth = 3; g.beginPath(); g.arc(m.x, m.y, 14 + p, 0, 7); g.stroke(); }
  for (const p of S.players) {
    const d = disp[p.i] || (disp[p.i] = { x: p.x, y: p.y });
    if (p.i === me.i) { d.x = pos.x; d.y = pos.y; } else { d.x += (p.x - d.x) * 0.25; d.y += (p.y - d.y) * 0.25; }
    if (!p.alive) { g.fillStyle = '#999'; g.font = 'bold 18px sans-serif'; g.fillText('✕', d.x, d.y + 6); continue; }
    g.fillStyle = COL[p.i]; g.beginPath(); g.arc(d.x, d.y, R, 0, 7); g.fill();
    g.strokeStyle = (S.impIdx === p.i || (p.i === me.i && me.imp)) ? '#f00' : '#fff'; g.lineWidth = 2; g.stroke();
    g.fillStyle = '#fff'; g.font = '11px sans-serif'; g.fillText(p.name, d.x, d.y - 14);
  }
  if (night && me.alive) {
    fg.globalCompositeOperation = 'source-over'; fg.clearRect(0, 0, W, H);
    fg.fillStyle = 'rgba(2,4,14,.97)'; fg.fillRect(0, 0, W, H);
    const rad = me.torch ? 150 : 75;
    const gr = fg.createRadialGradient(pos.x, pos.y, rad * 0.3, pos.x, pos.y, rad);
    gr.addColorStop(0, 'rgba(0,0,0,1)'); gr.addColorStop(1, 'rgba(0,0,0,0)');
    fg.globalCompositeOperation = 'destination-out'; fg.fillStyle = gr; fg.beginPath(); fg.arc(pos.x, pos.y, rad, 0, 7); fg.fill();
    g.drawImage(fog, 0, 0);
    if (me.radarUntil > Date.now()) {
      for (const p of S.players) if (p.alive && p.i !== me.i && Math.hypot(p.x - pos.x, p.y - pos.y) < 170) { g.fillStyle = '#ff3b3b'; g.beginPath(); g.arc(p.x, p.y, 6, 0, 7); g.fill(); }
      g.strokeStyle = '#3f3'; g.lineWidth = 1; g.beginPath(); g.arc(pos.x, pos.y, 170, 0, 7); g.stroke();
    }
  }
  const sec = Math.max(0, Math.ceil((S.tEnd - Date.now()) / 1000));
  let l2 = '💀 तुम खत्म हो, देखते रहो';
  if (me.alive) l2 = (me.imp ? '😈 तुम इम्पोस्टर हो | ' : '🙂 क्रू | ') + (me.mission ? '📋 ' + me.mission.name + ' (' + Math.max(0, Math.ceil((me.mission.until - Date.now()) / 1000)) + 's)' : '');
  $('hud').innerHTML = PN[ph] + ' • दिन ' + S.day + ' • ⏱ ' + sec + 's • टीम स्कोर ' + S.score + '/' + S.target + '<br>' + l2;
}

function ui() {
  $('jn').classList.remove('on');
  const lobby = S.phase === 'lobby';
  $('lb').classList.toggle('on', lobby);
  if (lobby) {
    $('lt').textContent = 'कमरा: ' + myRoom;
    $('ll').innerHTML = S.players.map(p => '<div>' + (p.i + 1) + '. ' + esc(p.name) + '</div>').join('');
    const host = S.host === socket.id;
    $('bs').style.display = host && S.players.length >= 2 ? 'block' : 'none';
    $('lw').style.display = host && S.players.length >= 2 ? 'none' : 'block';
  }
  const vote = S.phase === 'vote' && me.alive;
  if (vote && !$('vt').classList.contains('on')) {
    $('vt').innerHTML = '<h2>🗳️ इम्पोस्टर कौन है?</h2>' + S.players.filter(p => p.alive && p.i !== me.i).map(p => '<button data-i=' + p.i + '>' + esc(p.name) + '</button>').join('') + '<button data-i=-1 style=background:#888>⏭ स्किप</button><div id=vm></div><div id=vc></div>';
  }
  $('vt').classList.toggle('on', vote);
  if (vote && $('vc')) $('vc').textContent = S.votes + ' ने वोट दिया';
  const over = S.phase === 'over';
  $('ed').classList.toggle('on', over);
  if (over) $('ed').innerHTML = '<h1>' + (S.winner === 'crew' ? '🎉 क्रू जीत गया!' : '😈 इम्पोस्टर जीत गया!') + '</h1><div>इम्पोस्टर था: ' + esc(S.players[S.impIdx] ? S.players[S.impIdx].name : '') + '</div><button onclick=location.reload()>फिर से खेलो</button>';
  if (me.gadget) { let gl = '🎁 ' + GN[me.gadget]; if (me.gadget === 'radar') gl += ' x' + me.radarLeft; else if (me.gUsed) gl += ' ✔'; $('bg').textContent = gl; }
  $('bk').style.display = me.imp && me.alive && S.phase === 'night' ? 'block' : 'none';
}

function onPhase(p) {
  if (p === 'night') { beep(180, 0.6, 'sawtooth', 0.2); say('रात हो गई', 0.5); }
  else if (p === 'day') { beep(900, 0.15); say('कुकड़ू कूँ', 1.4); }
  else if (p === 'vote') beep(500, 0.3, 'square');
}

socket.on('state', s => {
  const old = S && S.phase; S = s; me = s.me;
  if (s.phase !== 'lobby' && !started) { started = true; const mp = s.players[me.i]; pos = { x: mp.x, y: mp.y }; help(); }
  if (s.phase !== old) onPhase(s.phase);
  ui();
});
socket.on('toast', toast);
socket.on('boom', () => beep(70, 0.7, 'sawtooth', 0.4)); function help() { const imp = me && me.imp; $('tt').innerHTML = '<h2>📖 कैसे खेलें</h2><div style=text-align:left;max-width:340px;font-size:15px;line-height:1.6>🕹️ <b>चलना:</b> बाईं तरफ़ जॉयस्टिक<br>✋ <b>काम:</b> पीले घेरे पर जाकर दबाओ, समय खत्म होने से पहले<br>🎁 <b>गैजेट:</b> हर सुबह एक नया मिलता है, दबाकर चालू करो<br>🌙 <b>रात:</b> अँधेरा रहता है, सिर्फ़ टॉर्च के घेरे में दिखता है, और दूसरों के घर बंद रहते हैं<br>🗳️ <b>वोटिंग:</b> कोई मरे तो सुबह वोट करके इम्पोस्टर को निकालो<br><br>' + (me ? (imp ? '😈 <b>तुम इम्पोस्टर हो:</b> रात में किसी के पास जाकर 🔪 दबाओ, फिर 15 सेकंड में अपने घर लौटो। तुम किसी का भी दरवाज़ा खोल सकते हो।' : '🙂 <b>तुम क्रू हो:</b> मिशन पूरे करो और वोटिंग में इम्पोस्टर को पहचानो।') : '') + '</div><button id=tc>समझ गया</button>'; $('tt').classList.add('on'); $('tc').onclick = () => $('tt').classList.remove('on'); } $('bq').onclick = help; $('bh').onclick = help;

$('bj').onclick = () => { myRoom = ($('rm').value || 'ROOM1').toUpperCase(); beep(1, 0.01); socket.emit('join', { room: myRoom, name: $('nm').value }); };
$('bs').onclick = () => socket.emit('start');
$('ba').onclick = () => socket.emit('act');
$('bg').onclick = () => socket.emit('gadget');
$('bk').onclick = () => socket.emit('kill');
$('vt').onclick = e => { const b = e.target.closest('button'); if (b) { socket.emit('vote', +b.dataset.i); $('vm').textContent = '✔ तुमने वोट दे दिया'; } };

const pad = $('pad'), kn = $('knob'); let down = false;
function pm(e) { const r = pad.getBoundingClientRect(); let dx = e.clientX - (r.left + 60), dy = e.clientY - (r.top + 60); const m = Math.hypot(dx, dy) || 1, k = Math.min(m, 50) / m; dx *= k; dy *= k; vec = { x: dx / 50, y: dy / 50 }; kn.style.transform = 'translate(' + dx + 'px,' + dy + 'px)'; }
pad.addEventListener('pointerdown', e => { down = true; pad.setPointerCapture(e.pointerId); pm(e); });
pad.addEventListener('pointermove', e => { if (down) pm(e); });
const rel = () => { down = false; vec = { x: 0, y: 0 }; kn.style.transform = ''; };
pad.addEventListener('pointerup', rel); pad.addEventListener('pointercancel', rel);
window.addEventListener('keydown', e => { const k = e.key.toLowerCase(); keys[k] = true; if (k === ' ') socket.emit('act'); if (k === 'e') socket.emit('gadget'); if (k === 'k') socket.emit('kill'); });
window.addEventListener('keyup', e => { keys[e.key.toLowerCase()] = false; });

function loop() { if (S && me && S.phase !== 'lobby') { step(); draw(); } requestAnimationFrame(loop); }
loop();
</script></body></html>`;

srv.listen(process.env.PORT || 3000, () => console.log('रात का मोहल्ला चालू'));
खेलने के नियम ऊपर वाले हिस्से में लिखे हैं, गेम वही है।
