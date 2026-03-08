<!DOCTYPE html>
<html lang="te">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover"/>
<title>వాక్యధార – బైబిల్ పఠన పురోగతి</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Telugu:wght@300;400;500;600;700&display=swap" rel="stylesheet"/>
<style>
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
body{background:#f0f4f8;color:#1a2332;font-family:'Noto Sans Telugu','Segoe UI',sans-serif;min-height:100vh;max-width:480px;margin:0 auto}
input,button{font-family:'Noto Sans Telugu','Segoe UI',sans-serif}

@keyframes fall{0%{transform:translateY(-10px) rotate(0deg);opacity:1}100%{transform:translateY(110vh) rotate(720deg);opacity:0}}
@keyframes slideDown{from{transform:translateY(-16px);opacity:0}to{transform:translateY(0);opacity:1}}
@keyframes popIn{0%{transform:scale(.75);opacity:0}70%{transform:scale(1.04)}100%{transform:scale(1);opacity:1}}
@keyframes shimmer{0%{background-position:200% 0}100%{background-position:-200% 0}}

.confetti-p{position:fixed;top:0;pointer-events:none;z-index:9999;border-radius:2px;animation:fall 2.4s ease-in forwards}

.toast{position:fixed;top:20px;left:50%;transform:translateX(-50%);background:#1a2332;border-radius:14px;padding:12px 22px;font-size:14px;color:#fff;z-index:1000;display:flex;align-items:center;gap:10px;font-weight:600;white-space:nowrap;animation:slideDown .2s ease;box-shadow:0 8px 32px rgba(0,0,0,.2)}

.cel-overlay{position:fixed;inset:0;background:rgba(15,20,30,.85);display:flex;align-items:center;justify-content:center;z-index:1001;padding:0 24px;backdrop-filter:blur(6px)}
.cel-card{background:#fff;border-radius:28px;padding:36px 32px;text-align:center;width:100%;max-width:320px;animation:popIn .35s ease;box-shadow:0 24px 80px rgba(0,0,0,.18)}

.badge-overlay{position:fixed;inset:0;background:rgba(15,20,30,.7);z-index:1001;display:flex;flex-direction:column;justify-content:flex-end;backdrop-filter:blur(4px)}
.badge-sheet{background:#fff;border-radius:24px 24px 0 0;padding:24px 20px 48px;max-height:78vh;overflow-y:auto;box-shadow:0 -8px 40px rgba(0,0,0,.12)}

.hero{background:linear-gradient(145deg,#1e3a5f,#2d5a8e);border-radius:0 0 32px 32px;padding:28px 20px 24px;position:relative;overflow:hidden}
.hero::before{content:'';position:absolute;top:-60px;right:-60px;width:200px;height:200px;background:rgba(255,255,255,.05);border-radius:50%}
.hero::after{content:'';position:absolute;bottom:-40px;left:-40px;width:160px;height:160px;background:rgba(255,255,255,.04);border-radius:50%}

.stat-pill{background:rgba(255,255,255,.12);border-radius:14px;padding:12px 10px;text-align:center;backdrop-filter:blur(10px)}

.book-card{background:#fff;border-radius:18px;margin-bottom:8px;overflow:hidden;box-shadow:0 2px 12px rgba(0,0,0,.06);transition:box-shadow .2s}
.book-card:active{box-shadow:0 1px 6px rgba(0,0,0,.08)}
.book-row{display:flex;align-items:center;gap:12px;padding:14px 16px;cursor:pointer;user-select:none}
.book-icon{width:44px;height:44px;border-radius:13px;display:flex;align-items:center;justify-content:center;font-size:20px;flex-shrink:0}

.chap-panel{background:#f8fafc;border-top:1px solid #eef2f7;padding:16px 14px 18px}
.chap-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(42px,1fr));gap:7px}
.chbtn{height:42px;border-radius:11px;font-size:13px;font-weight:600;cursor:pointer;transition:all .15s;border:2px solid #e2e8f0;background:#fff;color:#94a3b8}
.chbtn.done{background:linear-gradient(135deg,#2d5a8e,#4a90d9);border-color:transparent;color:#fff;box-shadow:0 3px 10px rgba(45,90,142,.3)}
.chbtn:active{transform:scale(.87)}

.fbtn{padding:8px 16px;border-radius:20px;font-size:13px;cursor:pointer;white-space:nowrap;flex-shrink:0;transition:all .2s;border:2px solid #e2e8f0;background:#fff;color:#64748b;font-weight:500}
.fbtn.on{background:#1e3a5f;border-color:#1e3a5f;color:#fff;font-weight:600}

.share-btn{display:flex;align-items:center;justify-content:center;gap:10px;width:100%;padding:15px;border-radius:16px;border:none;background:linear-gradient(135deg,#25D366,#1aad52);color:#fff;font-size:15px;font-weight:700;cursor:pointer;margin-top:16px;letter-spacing:.3px;box-shadow:0 4px 20px rgba(37,211,102,.35)}
.share-btn:active{opacity:.88;transform:scale(.98)}

#share-card{position:fixed;left:-9999px;top:0;width:400px}
</style>
</head>
<body>

<div id="conf-box"></div>
<div id="toast-el" class="toast" style="display:none"><span id="t-icon" style="font-size:18px"></span><span id="t-msg"></span></div>

<!-- Celebrate modal -->
<div id="cel-overlay" class="cel-overlay" style="display:none" onclick="hideCel()">
  <div class="cel-card" onclick="event.stopPropagation()">
    <div id="cel-icon" style="font-size:64px;margin-bottom:14px;line-height:1"></div>
    <div style="font-size:11px;letter-spacing:3px;color:#64748b;text-transform:uppercase;margin-bottom:8px">సాధన సిద్ధించింది!</div>
    <div id="cel-label" style="font-size:22px;color:#1e3a5f;font-weight:700;margin-bottom:10px"></div>
    <div id="cel-msg" style="font-size:15px;color:#64748b;line-height:1.8;margin-bottom:24px"></div>
    <button onclick="hideCel()" style="background:#1e3a5f;color:#fff;border:none;border-radius:14px;padding:12px 28px;font-size:14px;font-weight:600;cursor:pointer;font-family:inherit">కొనసాగించు</button>
  </div>
</div>

<!-- Badges sheet -->
<div id="badge-overlay" class="badge-overlay" style="display:none" onclick="hideBadges()">
  <div class="badge-sheet" onclick="event.stopPropagation()">
    <div style="width:40px;height:4px;background:#e2e8f0;border-radius:2px;margin:0 auto 20px"></div>
    <div style="font-size:11px;letter-spacing:3px;color:#94a3b8;text-transform:uppercase;margin-bottom:16px">మీ బ్యాడ్జీలు · <span id="bdg-count">0</span>/10</div>
    <div id="bdg-list"></div>
  </div>
</div>

<div id="share-card"></div>

<!-- Hero -->
<div class="hero">
  <div style="position:relative;z-index:1">
    <div style="text-align:center;margin-bottom:22px">
      <div style="font-size:10px;letter-spacing:5px;color:rgba(255,255,255,.5);margin-bottom:6px;text-transform:uppercase">Vaakyadhaara</div>
      <div style="font-size:28px;font-weight:700;color:#fff;line-height:1.2;margin-bottom:4px">వాక్యధార</div>
      <div style="font-size:12px;color:rgba(255,255,255,.55);font-style:italic">"నీ వాక్యము నా పాదములకు దీపమును" — కీర్తనలు ౧౧౯:౧౦౫</div>
    </div>

    <!-- Big % -->
    <div style="text-align:center;margin-bottom:18px">
      <div style="font-size:52px;font-weight:800;color:#fff;line-height:1"><span id="h-pct">0</span><span style="font-size:26px;color:rgba(255,255,255,.5);font-weight:400">%</span></div>
      <div style="font-size:13px;color:rgba(255,255,255,.6);margin-top:2px"><span id="h-done">0</span> / 1189 అధ్యాయాలు పూర్తయ్యాయి</div>
    </div>

    <!-- Progress bar -->
    <div style="background:rgba(255,255,255,.15);border-radius:20px;height:10px;overflow:hidden;margin-bottom:6px">
      <div id="h-bar" style="background:linear-gradient(90deg,#74c0fc,#a5f3fc);height:100%;width:0%;border-radius:20px;transition:width .6s ease"></div>
    </div>
    <div style="display:flex;justify-content:space-between;font-size:10px;color:rgba(255,255,255,.4);margin-bottom:20px">
      <span id="h-pl">0 అధ్యాయాలు</span><span id="h-pr"></span>
    </div>

    <!-- Stats row -->
    <div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;margin-bottom:4px">
      <div class="stat-pill">
        <div style="font-size:18px;font-weight:700;color:#fff"><span id="h-ot">0</span><span style="font-size:11px;color:rgba(255,255,255,.45);font-weight:400">/929</span></div>
        <div style="font-size:9px;color:rgba(255,255,255,.5);letter-spacing:.5px;margin-top:3px;line-height:1.4">పాత నిబంధన</div>
      </div>
      <div class="stat-pill">
        <div style="font-size:18px;font-weight:700;color:#fff"><span id="h-nt">0</span><span style="font-size:11px;color:rgba(255,255,255,.45);font-weight:400">/260</span></div>
        <div style="font-size:9px;color:rgba(255,255,255,.5);letter-spacing:.5px;margin-top:3px;line-height:1.4">కొత్త నిబంధన</div>
      </div>
      <div class="stat-pill" onclick="showBadges()" style="cursor:pointer">
        <div style="font-size:18px;font-weight:700;color:#ffd700"><span id="h-bdg">0</span><span style="font-size:11px;color:rgba(255,255,255,.45);font-weight:400">/10</span></div>
        <div style="font-size:9px;color:rgba(255,255,255,.5);letter-spacing:.5px;margin-top:3px;line-height:1.4">బ్యాడ్జీలు 🏅</div>
      </div>
    </div>

    <!-- Next milestone -->
    <div id="h-next-wrap" style="margin-top:14px;background:rgba(255,255,255,.1);border-radius:14px;padding:12px 16px;display:flex;align-items:center;gap:12px"></div>

    <!-- WhatsApp share -->
    <button class="share-btn" onclick="shareProgress()">
      <svg width="20" height="20" viewBox="0 0 24 24" fill="white"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
      WhatsApp లో షేర్ చేయండి
    </button>
  </div>
</div>

<!-- Search + filters -->
<div style="padding:16px 16px 10px">
  <div style="position:relative;margin-bottom:10px">
    <span style="position:absolute;left:14px;top:50%;transform:translateY(-50%);font-size:15px;color:#94a3b8">🔍</span>
    <input id="srch" oninput="render()" placeholder="పుస్తకం వెతకండి..."
      style="width:100%;padding:13px 14px 13px 42px;border-radius:14px;border:2px solid #e2e8f0;background:#fff;color:#1a2332;font-size:15px;outline:none;-webkit-appearance:none;box-shadow:0 2px 8px rgba(0,0,0,.05)"/>
  </div>
  <div style="display:flex;gap:8px;overflow-x:auto;padding-bottom:4px">
    <button class="fbtn on" id="fALL" onclick="setFilter('ALL')">అన్నీ</button>
    <button class="fbtn" id="fOT" onclick="setFilter('OT')">పాత నిబంధన</button>
    <button class="fbtn" id="fNT" onclick="setFilter('NT')">కొత్త నిబంధన</button>
    <span id="sav-lbl" style="font-size:11px;color:#94a3b8;align-self:center;flex-shrink:0;display:none">సేవ్ అవుతోంది...</span>
  </div>
</div>

<div id="book-list" style="padding:0 16px 32px"></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script>
var BOOKS = [
  {b:"ఆదికాండము",en:"Genesis",ch:50,t:"OT"},{b:"నిర్గమకాండము",en:"Exodus",ch:40,t:"OT"},{b:"లేవీయకాండము",en:"Leviticus",ch:27,t:"OT"},{b:"సంఖ్యాకాండము",en:"Numbers",ch:36,t:"OT"},{b:"ద్వితీయోపదేశకాండము",en:"Deuteronomy",ch:34,t:"OT"},{b:"యెహోషువ",en:"Joshua",ch:24,t:"OT"},{b:"న్యాయాధిపతులు",en:"Judges",ch:21,t:"OT"},{b:"రూతు",en:"Ruth",ch:4,t:"OT"},{b:"1 సమూయేలు",en:"1 Samuel",ch:31,t:"OT"},{b:"2 సమూయేలు",en:"2 Samuel",ch:24,t:"OT"},{b:"1 రాజులు",en:"1 Kings",ch:22,t:"OT"},{b:"2 రాజులు",en:"2 Kings",ch:25,t:"OT"},{b:"1 దినవృత్తాంతములు",en:"1 Chronicles",ch:29,t:"OT"},{b:"2 దినవృత్తాంతములు",en:"2 Chronicles",ch:36,t:"OT"},{b:"ఎజ్రా",en:"Ezra",ch:10,t:"OT"},{b:"నెహెమ్యా",en:"Nehemiah",ch:13,t:"OT"},{b:"ఎస్తేరు",en:"Esther",ch:10,t:"OT"},{b:"యోబు",en:"Job",ch:42,t:"OT"},{b:"కీర్తనలు",en:"Psalms",ch:150,t:"OT",now:true},{b:"సామెతలు",en:"Proverbs",ch:31,t:"OT"},{b:"ప్రసంగి",en:"Ecclesiastes",ch:12,t:"OT"},{b:"పరమగీతము",en:"Song of Solomon",ch:8,t:"OT"},{b:"యెషయా",en:"Isaiah",ch:66,t:"OT"},{b:"యిర్మీయా",en:"Jeremiah",ch:52,t:"OT"},{b:"విలాపవాక్యములు",en:"Lamentations",ch:5,t:"OT"},{b:"యెహెఙ్కేలు",en:"Ezekiel",ch:48,t:"OT"},{b:"దానియేలు",en:"Daniel",ch:12,t:"OT"},{b:"హోషేయ",en:"Hosea",ch:14,t:"OT"},{b:"యోవేలు",en:"Joel",ch:3,t:"OT"},{b:"ఆమోసు",en:"Amos",ch:9,t:"OT"},{b:"ఓబద్యా",en:"Obadiah",ch:1,t:"OT"},{b:"యోనా",en:"Jonah",ch:4,t:"OT"},{b:"మీకా",en:"Micah",ch:7,t:"OT"},{b:"నాహూము",en:"Nahum",ch:3,t:"OT"},{b:"హబక్కూకు",en:"Habakkuk",ch:3,t:"OT"},{b:"జెఫన్యా",en:"Zephaniah",ch:3,t:"OT"},{b:"హగ్గయి",en:"Haggai",ch:2,t:"OT"},{b:"జెకర్యా",en:"Zechariah",ch:14,t:"OT"},{b:"మలాకీ",en:"Malachi",ch:4,t:"OT"},
  {b:"మత్తయి",en:"Matthew",ch:28,t:"NT"},{b:"మార్కు",en:"Mark",ch:16,t:"NT"},{b:"లూకా",en:"Luke",ch:24,t:"NT"},{b:"యోహాను",en:"John",ch:21,t:"NT"},{b:"అపొస్తలుల కార్యములు",en:"Acts",ch:28,t:"NT"},{b:"రోమీయులకు",en:"Romans",ch:16,t:"NT"},{b:"1 కొరింథీయులకు",en:"1 Corinthians",ch:16,t:"NT"},{b:"2 కొరింథీయులకు",en:"2 Corinthians",ch:13,t:"NT"},{b:"గలతీయులకు",en:"Galatians",ch:6,t:"NT"},{b:"ఎఫెసీయులకు",en:"Ephesians",ch:6,t:"NT"},{b:"ఫిలిప్పీయులకు",en:"Philippians",ch:4,t:"NT"},{b:"కొలొస్సయులకు",en:"Colossians",ch:4,t:"NT"},{b:"1 థెస్సలొనీకయులకు",en:"1 Thessalonians",ch:5,t:"NT"},{b:"2 థెస్సలొనీకయులకు",en:"2 Thessalonians",ch:3,t:"NT"},{b:"1 తిమోతికి",en:"1 Timothy",ch:6,t:"NT"},{b:"2 తిమోతికి",en:"2 Timothy",ch:4,t:"NT"},{b:"తీతుకు",en:"Titus",ch:3,t:"NT"},{b:"ఫిలేమోనుకు",en:"Philemon",ch:1,t:"NT"},{b:"హెబ్రీయులకు",en:"Hebrews",ch:13,t:"NT"},{b:"యాకోబు",en:"James",ch:5,t:"NT"},{b:"1 పేతురు",en:"1 Peter",ch:5,t:"NT"},{b:"2 పేతురు",en:"2 Peter",ch:3,t:"NT"},{b:"1 యోహాను",en:"1 John",ch:5,t:"NT"},{b:"2 యోహాను",en:"2 John",ch:1,t:"NT"},{b:"3 యోహాను",en:"3 John",ch:1,t:"NT"},{b:"యూదా",en:"Jude",ch:1,t:"NT"},{b:"ప్రకటన గ్రంథము",en:"Revelation",ch:22,t:"NT"}
];

var REWARDS = [
  {at:1,icon:"🌱",label:"మొదటి అడుగు",msg:"గొప్ప యాత్ర మొదలైంది!"},
  {at:10,icon:"🔥",label:"జ్వలిస్తున్నారు!",msg:"10 అధ్యాయాలు! వాక్యం మీలో జీవిస్తోంది."},
  {at:25,icon:"⭐",label:"అన్వేషకుడు",msg:"25 అధ్యాయాలు! అన్వేషణ కొనసాగించండి."},
  {at:50,icon:"📖",label:"భక్తి పాఠకుడు",msg:"50 అధ్యాయాలు! విశ్వాసం పెరుగుతోంది."},
  {at:100,icon:"🏅",label:"శతకం",msg:"100 అధ్యాయాలు! నిజంగా అంకితభావం."},
  {at:150,icon:"💎",label:"కీర్తనలు పూర్తి!",msg:"150 కీర్తనలు! దేవుని హృదయపు పాటలు."},
  {at:250,icon:"🌟",label:"వాక్య యాత్రికుడు",msg:"250 అధ్యాయాలు! వాక్యంలో నడుస్తున్నారు."},
  {at:500,icon:"🏆",label:"సగం పూర్తి!",msg:"500 అధ్యాయాలు! బైబిల్ సగం చదివారు!"},
  {at:929,icon:"👑",label:"పాత నిబంధన పూర్తి",msg:"సంపూర్ణ పాత నిబంధన! అద్భుతం!"},
  {at:1189,icon:"✝️",label:"బైబిల్ పూర్తి!",msg:"మొత్తం పవిత్ర బైబిల్ చదివారు! దేవుడు మీకు మహిమ ఇచ్చుగాక!"}
];

var done = {}, openBook = "కీర్తనలు", curFilter = "ALL", prevTotal = 0, toastTimer = null;

function load() {
  try { var s = localStorage.getItem("vd_te"); if (s) done = JSON.parse(s); } catch(e) {}
  for (var i = 0; i < BOOKS.length; i++) { if (!done[BOOKS[i].b]) done[BOOKS[i].b] = {}; }
  prevTotal = totalDone();
}

function saveDone() {
  try { localStorage.setItem("vd_te", JSON.stringify(done)); } catch(e) {}
  var l = document.getElementById("sav-lbl");
  l.style.display = "inline";
  setTimeout(function() { l.style.display = "none"; }, 900);
}

function rec(book) {
  var b = done[book]; if (!b) return 0;
  var v = Object.values(b), c = 0;
  for (var i = 0; i < v.length; i++) { if (v[i]) c++; }
  return c;
}

function totalDone() {
  var t = 0;
  for (var i = 0; i < BOOKS.length; i++) t += rec(BOOKS[i].b);
  return t;
}

function updateHero() {
  var td = totalDone(), pct = Math.round(td / 1189 * 100);
  var otD = 0, ntD = 0, earned = 0;
  for (var i = 0; i < BOOKS.length; i++) {
    if (BOOKS[i].t === "OT") otD += rec(BOOKS[i].b); else ntD += rec(BOOKS[i].b);
  }
  for (var j = 0; j < REWARDS.length; j++) { if (REWARDS[j].at <= td) earned++; }
  var next = null;
  for (var k = 0; k < REWARDS.length; k++) { if (REWARDS[k].at > td) { next = REWARDS[k]; break; } }

  document.getElementById("h-pct").textContent = pct;
  document.getElementById("h-done").textContent = td;
  document.getElementById("h-bar").style.width = pct + "%";
  document.getElementById("h-pl").textContent = td + " అధ్యాయాలు";
  document.getElementById("h-ot").textContent = otD;
  document.getElementById("h-nt").textContent = ntD;
  document.getElementById("h-bdg").textContent = earned;
  document.getElementById("bdg-count").textContent = earned;

  var nw = document.getElementById("h-next-wrap");
  if (next) {
    document.getElementById("h-pr").textContent = next.at + " అధ్యాయాలు";
    nw.style.display = "flex";
    nw.innerHTML = '<div style="font-size:28px">' + next.icon + '</div>'
      + '<div><div style="font-size:10px;color:rgba(255,255,255,.5);letter-spacing:2px;text-transform:uppercase;margin-bottom:2px">తదుపరి సాధన</div>'
      + '<div style="font-size:14px;color:#fff;font-weight:600">' + next.label + '</div>'
      + '<div style="font-size:11px;color:rgba(255,255,255,.5);margin-top:1px">' + (next.at - td) + ' అధ్యాయాలు మిగిలాయి</div></div>';
  } else { nw.style.display = "none"; }
}

function render() {
  var q = document.getElementById("srch").value;
  var list = document.getElementById("book-list");
  list.innerHTML = "";

  for (var i = 0; i < BOOKS.length; i++) {
    var bk = BOOKS[i];
    if (curFilter !== "ALL" && bk.t !== curFilter) continue;
    if (q && bk.b.indexOf(q) === -1 && bk.en.toLowerCase().indexOf(q.toLowerCase()) === -1) continue;

    var r = rec(bk.b), p = Math.round(r / bk.ch * 100), isDone = r === bk.ch, isOpen = openBook === bk.b;
    var icon = isDone ? "✅" : bk.now ? "📖" : bk.t === "NT" ? "✝️" : "📜";
    var iconBg = isDone ? "#dcfce7" : bk.now ? "#dbeafe" : bk.t === "NT" ? "#fef3c7" : "#f1f5f9";
    var nameColor = isDone ? "#16a34a" : bk.now ? "#1e40af" : "#1a2332";
    var barColor = isDone ? "linear-gradient(90deg,#16a34a,#4ade80)" : bk.now ? "linear-gradient(90deg,#2d5a8e,#4a90d9)" : "linear-gradient(90deg,#94a3b8,#cbd5e1)";
    var statColor = isDone ? "#16a34a" : "#1e3a5f";

    var nowBadge = bk.now ? '<span style="font-size:10px;background:#dbeafe;color:#1e40af;padding:3px 9px;border-radius:20px;font-weight:600;flex-shrink:0">ఇప్పుడు</span>' : "";
    var doneBadge = isDone ? '<span style="font-size:10px;background:#dcfce7;color:#16a34a;padding:3px 9px;border-radius:20px;font-weight:600;flex-shrink:0">పూర్తి ✓</span>' : "";

    var wrap = document.createElement("div");
    wrap.className = "book-card";

    wrap.innerHTML = '<div class="book-row" data-book="' + bk.b + '">'
      + '<div class="book-icon" style="background:' + iconBg + '">' + icon + '</div>'
      + '<div style="flex:1;min-width:0">'
      + '<div style="display:flex;align-items:center;gap:7px;margin-bottom:6px;flex-wrap:wrap">'
      + '<span style="font-size:15px;font-weight:600;color:' + nameColor + ';line-height:1.4">' + bk.b + '</span>'
      + nowBadge + doneBadge + '</div>'
      + '<div style="background:#f1f5f9;border-radius:6px;height:5px;overflow:hidden">'
      + '<div style="background:' + barColor + ';height:100%;width:' + p + '%;border-radius:6px;transition:width .4s"></div></div></div>'
      + '<div style="text-align:right;flex-shrink:0;margin-left:8px">'
      + '<div style="font-size:15px;font-weight:700;color:' + statColor + ';line-height:1">' + r
      + '<span style="font-size:10px;color:#94a3b8;font-weight:400">/' + bk.ch + '</span></div>'
      + '<div style="font-size:10px;color:#94a3b8;margin-top:3px">' + p + '%</div></div>'
      + '<div style="color:#cbd5e1;font-size:12px;flex-shrink:0;margin-left:6px">' + (isOpen ? "▲" : "▼") + '</div>'
      + '</div>';

    if (isOpen) {
      var panel = document.createElement("div");
      panel.className = "chap-panel";
      var gh = '<div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px">'
        + '<div style="font-size:12px;color:#64748b;font-weight:500">' + bk.b + ' · అధ్యాయాలు</div>'
        + '<div style="font-size:12px;color:#2d5a8e;font-weight:600;background:#dbeafe;padding:3px 10px;border-radius:20px">' + r + '/' + bk.ch + '</div></div>'
        + '<div class="chap-grid">';
      for (var c = 1; c <= bk.ch; c++) {
        var cd = done[bk.b] && done[bk.b][c] ? true : false;
        gh += '<button class="chbtn' + (cd ? " done" : "") + '" data-book="' + bk.b + '" data-ch="' + c + '">' + c + '</button>';
      }
      gh += '</div><div style="font-size:11px;color:#94a3b8;margin-top:12px;text-align:center">అధ్యాయం తాకి గుర్తించండి ✓</div>';
      panel.innerHTML = gh;
      wrap.appendChild(panel);
    }
    list.appendChild(wrap);
  }

  var rows = list.querySelectorAll(".book-row");
  for (var ri = 0; ri < rows.length; ri++) rows[ri].addEventListener("click", onBookClick);
  var cbtns = list.querySelectorAll(".chbtn");
  for (var ci = 0; ci < cbtns.length; ci++) cbtns[ci].addEventListener("click", onChapClick);
}

function onBookClick(e) {
  var name = e.currentTarget.getAttribute("data-book");
  openBook = openBook === name ? null : name;
  render();
}

function onChapClick(e) {
  e.stopPropagation();
  var book = e.currentTarget.getAttribute("data-book");
  var ch = parseInt(e.currentTarget.getAttribute("data-ch"), 10);
  if (!done[book]) done[book] = {};
  done[book][ch] = !done[book][ch];
  var newTotal = totalDone();
  var bk = null;
  for (var i = 0; i < BOOKS.length; i++) { if (BOOKS[i].b === book) { bk = BOOKS[i]; break; } }
  var isBookDone = bk && rec(book) === bk.ch;
  var reward = null;
  if (newTotal > prevTotal) {
    for (var j = 0; j < REWARDS.length; j++) { if (REWARDS[j].at === newTotal) { reward = REWARDS[j]; break; } }
  }
  if (reward) { fireConfetti(); showCel(reward); }
  else if (isBookDone && done[book][ch]) { fireConfetti(); showToast(book + " పూర్తయింది! 🎉", "🎊", 3000); }
  else if (done[book][ch]) { showToast("అధ్యాయం గుర్తించబడింది!", "✓", 2000); }
  prevTotal = newTotal;
  saveDone(); updateHero(); render();
}

function fireConfetti() {
  var box = document.getElementById("conf-box");
  box.innerHTML = "";
  var colors = ["#2d5a8e","#4a90d9","#ffd700","#ff6b6b","#4ade80","#fff"];
  for (var i = 0; i < 32; i++) {
    var el = document.createElement("div");
    var sz = 5 + Math.random() * 8;
    el.className = "confetti-p";
    el.style.left = (15 + Math.random() * 70) + "%";
    el.style.width = sz + "px"; el.style.height = sz + "px";
    el.style.background = colors[i % 6];
    el.style.animationDelay = (Math.random() * 0.5) + "s";
    box.appendChild(el);
  }
  setTimeout(function() { box.innerHTML = ""; }, 2800);
}

function showToast(msg, icon, dur) {
  if (toastTimer) clearTimeout(toastTimer);
  document.getElementById("t-icon").textContent = icon;
  document.getElementById("t-msg").textContent = msg;
  var t = document.getElementById("toast-el");
  t.style.display = "flex";
  toastTimer = setTimeout(function() { t.style.display = "none"; }, dur);
}

function showCel(r) {
  document.getElementById("cel-icon").textContent = r.icon;
  document.getElementById("cel-label").textContent = r.label;
  document.getElementById("cel-msg").textContent = r.msg;
  document.getElementById("cel-overlay").style.display = "flex";
}
function hideCel() { document.getElementById("cel-overlay").style.display = "none"; }

function showBadges() {
  var td = totalDone(), html = "";
  for (var i = 0; i < REWARDS.length; i++) {
    var r = REWARDS[i], earned = r.at <= td;
    html += '<div style="display:flex;align-items:center;gap:14px;padding:13px 0;border-bottom:1px solid #f1f5f9;opacity:' + (earned ? 1 : 0.4) + '">'
      + '<div style="width:46px;height:46px;border-radius:13px;background:' + (earned ? "#dbeafe" : "#f1f5f9") + ';display:flex;align-items:center;justify-content:center;font-size:22px;flex-shrink:0">' + r.icon + '</div>'
      + '<div style="flex:1"><div style="font-size:14px;font-weight:600;color:' + (earned ? "#1e3a5f" : "#94a3b8") + '">' + r.label + '</div>'
      + '<div style="font-size:12px;color:#94a3b8;margin-top:2px;line-height:1.5">' + (earned ? "సాధించారు! " + r.msg : r.at + " అధ్యాయాలలో అన్‌లాక్") + '</div></div>'
      + (earned ? '<div style="font-size:18px">✅</div>' : "") + '</div>';
  }
  document.getElementById("bdg-list").innerHTML = html;
  document.getElementById("badge-overlay").style.display = "flex";
}
function hideBadges() { document.getElementById("badge-overlay").style.display = "none"; }

function setFilter(f) {
  curFilter = f;
  var ids = ["ALL","OT","NT"];
  for (var i = 0; i < ids.length; i++) {
    document.getElementById("f" + ids[i]).className = "fbtn" + (ids[i] === f ? " on" : "");
  }
  render();
}

function shareProgress() {
  var td = totalDone(), pct = Math.round(td / 1189 * 100);
  var otD = 0, ntD = 0, earned = 0;
  for (var i = 0; i < BOOKS.length; i++) {
    if (BOOKS[i].t === "OT") otD += rec(BOOKS[i].b); else ntD += rec(BOOKS[i].b);
  }
  for (var j = 0; j < REWARDS.length; j++) { if (REWARDS[j].at <= td) earned++; }
  var recent = [];
  for (var k = BOOKS.length - 1; k >= 0 && recent.length < 4; k--) {
    if (rec(BOOKS[k].b) > 0) recent.unshift(BOOKS[k]);
  }
  var barsHTML = "";
  for (var b = 0; b < recent.length; b++) {
    var bk = recent[b], r = rec(bk.b), bp = Math.round(r / bk.ch * 100);
    barsHTML += '<div style="margin-bottom:10px">'
      + '<div style="display:flex;justify-content:space-between;font-size:12px;color:#475569;margin-bottom:4px;font-family:sans-serif"><span>' + bk.b + '</span><span>' + r + '/' + bk.ch + '</span></div>'
      + '<div style="background:#e2e8f0;border-radius:4px;height:7px;overflow:hidden"><div style="background:linear-gradient(90deg,#2d5a8e,#4a90d9);height:100%;width:' + bp + '%;border-radius:4px"></div></div></div>';
  }

  var card = document.getElementById("share-card");
  card.style.cssText = "position:fixed;left:-9999px;top:0;width:420px;background:#f0f4f8";
  card.innerHTML = '<div style="background:#fff;padding:0;border-radius:0;font-family:sans-serif;overflow:hidden">'
    + '<div style="background:linear-gradient(145deg,#1e3a5f,#2d5a8e);padding:28px 24px 24px;text-align:center">'
    + '<div style="font-size:10px;letter-spacing:4px;color:rgba(255,255,255,.5);margin-bottom:6px">VAAKYADHAARA</div>'
    + '<div style="font-size:22px;font-weight:800;color:#fff;margin-bottom:4px">వాక్యధార</div>'
    + '<div style="font-size:11px;color:rgba(255,255,255,.55);font-style:italic">నీ వాక్యము నా పాదములకు దీపమును</div>'
    + '<div style="font-size:52px;font-weight:900;color:#fff;line-height:1;margin:16px 0 4px">' + pct + '<span style="font-size:26px;color:rgba(255,255,255,.5);font-weight:400">%</span></div>'
    + '<div style="font-size:13px;color:rgba(255,255,255,.6)">' + td + ' / 1189 అధ్యాయాలు</div>'
    + '<div style="background:rgba(255,255,255,.15);border-radius:20px;height:8px;overflow:hidden;margin:14px 0 6px">'
    + '<div style="background:linear-gradient(90deg,#74c0fc,#a5f3fc);height:100%;width:' + pct + '%;border-radius:20px"></div></div>'
    + '<div style="display:flex;justify-content:center;gap:24px;font-size:11px;color:rgba(255,255,255,.5)">'
    + '<span>పాత నిబంధన: ' + otD + '/929</span><span>కొత్త నిబంధన: ' + ntD + '/260</span></div></div>'
    + (recent.length ? '<div style="padding:20px 24px 8px"><div style="font-size:10px;letter-spacing:2px;color:#94a3b8;margin-bottom:12px;font-family:sans-serif">ఇటీవల చదివిన పుస్తకాలు</div>' + barsHTML + '</div>' : '')
    + '<div style="padding:12px 24px 20px;display:flex;justify-content:space-between;align-items:center;border-top:1px solid #f1f5f9">'
    + '<span style="font-size:12px;color:#94a3b8;font-family:sans-serif">🏅 ' + earned + '/10 బ్యాడ్జీలు</span>'
    + '<span style="font-size:12px;color:#2d5a8e;font-weight:600;font-family:sans-serif">వాక్యధారతో చదవండి</span></div></div>';

  if (typeof html2canvas !== "undefined") {
    showToast("చిత్రం తయారవుతోంది...", "📸", 3000);
    html2canvas(card, {backgroundColor:"#ffffff", scale:2, useCORS:true, logging:false}).then(function(canvas) {
      card.innerHTML = "";
      canvas.toBlob(function(blob) {
        var txt = "వాక్యధారతో నా బైబిల్ పఠన పురోగతి:\n\n📖 " + td + "/1189 అధ్యాయాలు (" + pct + "%) పూర్తయింది!\n🏅 " + earned + "/10 బ్యాడ్జీలు\n\nమీరు కూడా చదవండి! 🙏\n#వాక్యధార #బైబిల్ #తెలుగు";
        if (navigator.share && blob) {
          var file = new File([blob], "vaakyadhaara_progress.png", {type:"image/png"});
          navigator.share({title:"వాక్యధార – నా బైబిల్ పురోగతి", text:txt, files:[file]})
            .catch(function() { fallbackShare(canvas, txt); });
        } else { fallbackShare(canvas, txt); }
      }, "image/png");
    }).catch(function() { textShare(); });
  } else { textShare(); }
}

function fallbackShare(canvas, txt) {
  var a = document.createElement("a");
  a.download = "vaakyadhaara_progress.png";
  a.href = canvas.toDataURL("image/png");
  a.click();
  setTimeout(function() {
    window.open("https://wa.me/?text=" + encodeURIComponent(txt), "_blank");
    showToast("చిత్రం డౌన్‌లోడ్ అయింది! WhatsApp లో జోడించండి", "📲", 4000);
  }, 800);
}

function textShare() {
  var td = totalDone(), pct = Math.round(td / 1189 * 100);
  window.open("https://wa.me/?text=" + encodeURIComponent("వాక్యధారతో నా బైబిల్ పఠన పురోగతి:\n\n📖 " + td + "/1189 అధ్యాయాలు (" + pct + "%) పూర్తయింది!\n\n#వాక్యధార #బైబిల్ #తెలుగు"), "_blank");
}

load(); updateHero(); render();
</script>
</body>
</html>
