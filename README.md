<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1.0"/>
<title>Kindness Tree Tracker</title>
<link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800;900&family=Lora:wght@400;600&display=swap" rel="stylesheet"/>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --gd:#2d6a3f;--gm:#4a9b61;--gl:#d4edda;--gp:#f0faf3;
  --amber:#e07b2a;--al:#fff3e0;
  --pink:#c0395a;--pl:#fdeef2;
  --blue:#2563a8;--bl:#e8f1fb;
  --tx:#1e1e1e;--txm:#6b7280;--txl:#9ca3af;
  --bg:#f4f7f2;--surf:#fff;--bdr:#e2e8e0;
  --r:13px;--rs:8px;
  --sh:0 2px 12px rgba(45,106,63,.09);
}
body{font-family:'Nunito',sans-serif;background:var(--bg);color:var(--tx);min-height:100vh}
/* HEADER */
header{background:var(--gd);padding:1rem 1.5rem;display:flex;align-items:center;gap:12px;box-shadow:0 3px 16px rgba(45,106,63,.3);flex-wrap:wrap}
.htxt h1{font-family:'Lora',serif;font-size:19px;font-weight:600;color:#fff}
.htxt p{font-size:12px;color:rgba(255,255,255,.7);margin-top:1px}
.hright{margin-left:auto;display:flex;align-items:center;gap:7px;flex-wrap:wrap}
.hsel{font-family:'Nunito',sans-serif;font-size:13px;font-weight:700;background:rgba(255,255,255,.15);color:#fff;border:1px solid rgba(255,255,255,.3);border-radius:20px;padding:5px 13px;cursor:pointer;outline:none}
.hsel option{color:#1e1e1e;background:#fff}
.hbtn{font-family:'Nunito',sans-serif;font-size:12px;font-weight:700;background:rgba(255,255,255,.15);color:#fff;border:1px solid rgba(255,255,255,.3);border-radius:20px;padding:5px 13px;cursor:pointer;white-space:nowrap}
.hbtn:hover{background:rgba(255,255,255,.25)}
.hbadge{background:rgba(255,255,255,.15);border:1px solid rgba(255,255,255,.25);border-radius:20px;padding:5px 13px;font-size:11px;color:rgba(255,255,255,.9);font-weight:700;letter-spacing:.06em;text-transform:uppercase}
/* LAYOUT */
.wrap{max-width:1040px;margin:0 auto;padding:1.4rem}
/* TABS */
.tabs{display:flex;gap:4px;margin-bottom:1.4rem;background:var(--surf);padding:5px;border-radius:13px;box-shadow:var(--sh);border:1px solid var(--bdr);flex-wrap:wrap}
.tab{flex:1;min-width:80px;padding:8px 8px;border-radius:8px;border:none;background:transparent;font-family:'Nunito',sans-serif;font-size:12px;font-weight:700;color:var(--txm);cursor:pointer;transition:.14s;display:flex;align-items:center;justify-content:center;gap:4px}
.tab:hover{background:var(--gp);color:var(--gd)}
.tab.active{background:var(--gd);color:#fff;box-shadow:0 2px 8px rgba(45,106,63,.3)}
.tab.report-tab{background:linear-gradient(135deg,#c0395a,#e07b2a);color:#fff}
.tab.report-tab:hover{opacity:.9}
.tab.report-tab.active{background:linear-gradient(135deg,#a02f4a,#c06820)}
/* SECTIONS */
.sec{display:none}
.sec.on{display:block;animation:fi .18s ease}
@keyframes fi{from{opacity:0;transform:translateY(4px)}to{opacity:1;transform:translateY(0)}}
/* CARDS */
.card{background:var(--surf);border-radius:var(--r);border:1px solid var(--bdr);padding:1.2rem 1.4rem;margin-bottom:1.2rem;box-shadow:var(--sh)}
.ctitle{font-size:11px;font-weight:800;color:var(--txm);text-transform:uppercase;letter-spacing:.08em;margin-bottom:.9rem}
/* METRICS */
.mgrid{display:grid;grid-template-columns:repeat(auto-fit,minmax(125px,1fr));gap:10px;margin-bottom:1.2rem}
.met{background:var(--surf);border-radius:var(--r);border:1px solid var(--bdr);padding:.85rem 1rem;box-shadow:var(--sh);position:relative;overflow:hidden}
.met::before{content:'';position:absolute;top:0;left:0;right:0;height:3px;background:var(--gm);border-radius:var(--r) var(--r) 0 0}
.met.pink::before{background:var(--pink)}
.met.amber::before{background:var(--amber)}
.met.blue::before{background:var(--blue)}
.mlbl{font-size:11px;font-weight:700;color:var(--txm);text-transform:uppercase;letter-spacing:.05em;margin-bottom:4px}
.mval{font-size:26px;font-weight:900;color:var(--tx);line-height:1}
.msub{font-size:11px;color:var(--txl);margin-top:2px}
/* FORMS */
.fg2{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:10px}
.fg3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;margin-bottom:10px}
.fg{display:flex;flex-direction:column;gap:4px}
label{font-size:11px;font-weight:800;color:var(--txm);text-transform:uppercase;letter-spacing:.05em}
input[type=text],input[type=date],select,textarea{font-family:'Nunito',sans-serif;font-size:14px;padding:8px 10px;border:1.5px solid var(--bdr);border-radius:var(--rs);background:var(--bg);color:var(--tx);outline:none;transition:border-color .14s;width:100%}
input:focus,select:focus,textarea:focus{border-color:var(--gm);background:#fff}
textarea{resize:vertical;min-height:60px}
/* BUTTONS */
.btn{font-family:'Nunito',sans-serif;font-weight:700;font-size:13px;padding:8px 18px;border-radius:var(--rs);border:none;cursor:pointer;transition:all .14s;display:inline-flex;align-items:center;gap:6px}
.bp{background:var(--gd);color:#fff}
.bp:hover{background:var(--gm);transform:translateY(-1px)}
.bs{background:transparent;border:1.5px solid var(--bdr);color:var(--txm)}
.bs:hover{border-color:var(--gm);color:var(--gd)}
.bd{background:transparent;border:1.5px solid #fca5a5;color:#dc2626;font-size:11px;padding:3px 8px;border-radius:6px;font-family:'Nunito',sans-serif;font-weight:700;cursor:pointer}
.bd:hover{background:#fef2f2}
/* STUDENT GRID */
.sgrid{display:grid;grid-template-columns:repeat(auto-fill,minmax(160px,1fr));gap:10px;margin-bottom:1rem}
.scard{background:var(--surf);border:2px solid var(--bdr);border-radius:var(--r);padding:.9rem;text-align:center;cursor:pointer;transition:all .16s;position:relative}
.scard:hover{border-color:var(--gm);background:var(--gp);transform:translateY(-2px)}
.scard.sel{border-color:var(--gd);background:var(--gp)}
.sini{width:48px;height:48px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:15px;font-weight:900;margin:0 auto 7px}
.sname{font-weight:800;font-size:13px;margin-bottom:2px}
.smeta{font-size:11px;color:var(--txm)}
.stoks{display:flex;justify-content:center;gap:7px;margin-top:5px;font-size:12px;font-weight:700}
.sdel{position:absolute;top:5px;right:7px;background:none;border:none;color:var(--txl);cursor:pointer;font-size:13px;font-weight:900;line-height:1;padding:2px 4px;border-radius:4px}
.sdel:hover{color:#dc2626;background:#fef2f2}
/* TOKEN PICKER */
.tpick{display:flex;gap:10px;margin-bottom:13px}
.tpk{flex:1;padding:11px;border-radius:var(--r);border:2.5px solid var(--bdr);background:var(--surf);cursor:pointer;text-align:center;transition:all .14s;font-size:13px;font-weight:700;color:var(--txm);user-select:none}
.tpk .ti{font-size:28px;display:block;margin-bottom:4px}
.tpk:hover{border-color:var(--gm);background:var(--gp)}
.tpk.selh{border-color:var(--pink);background:var(--pl);color:var(--pink)}
.tpk.sela{border-color:var(--amber);background:var(--al);color:var(--amber)}
/* BANNER */
.sbanner{background:linear-gradient(135deg,var(--gd),var(--gm));border-radius:var(--r);padding:.85rem 1.2rem;display:flex;align-items:center;gap:11px;margin-bottom:1.2rem;color:#fff}
.bini{width:40px;height:40px;border-radius:50%;background:rgba(255,255,255,.22);display:flex;align-items:center;justify-content:center;font-size:14px;font-weight:900;flex-shrink:0}
.bname{font-size:15px;font-weight:800}
.bmeta{font-size:12px;opacity:.8}
/* LOG LIST */
.li{display:flex;align-items:flex-start;gap:10px;padding:10px 0;border-bottom:1px solid var(--bdr)}
.li:last-child{border-bottom:none}
.lav{width:32px;height:32px;border-radius:50%;background:var(--gl);display:flex;align-items:center;justify-content:center;font-size:16px;flex-shrink:0}
.ln{font-weight:700;font-size:13px}
.lt{font-size:12px;color:var(--txm);margin-top:1px}
.ld{font-size:11px;color:var(--txl);margin-top:1px;font-style:italic}
.ldate{font-size:11px;color:var(--txl);white-space:nowrap}
/* BARS */
.bw{margin-bottom:8px}
.bh{display:flex;justify-content:space-between;font-size:12px;margin-bottom:3px;font-weight:600}
.bt{background:var(--gp);border-radius:4px;height:8px}
.bf{height:8px;border-radius:4px;transition:width .35s ease}
/* STUDENT TABLE */
.stbl{width:100%;border-collapse:collapse;font-size:13px}
.stbl th{text-align:left;font-size:10px;font-weight:800;color:var(--txm);text-transform:uppercase;letter-spacing:.07em;padding:5px 7px;border-bottom:2px solid var(--bdr)}
.stbl td{padding:8px 7px;border-bottom:1px solid var(--bdr);vertical-align:middle}
.stbl tr:last-child td{border-bottom:none}
.stbl tr:hover td{background:var(--gp)}
.ini{width:28px;height:28px;border-radius:50%;display:inline-flex;align-items:center;justify-content:center;font-size:10px;font-weight:800}
/* HIGHLIGHT CARDS */
.hcards{display:grid;grid-template-columns:repeat(auto-fit,minmax(185px,1fr));gap:10px;margin-bottom:1.2rem}
.hcard{border-radius:var(--r);padding:.9rem 1.1rem;border:1px solid}
.hcard.gold{background:#fffbeb;border-color:#fde68a}
.hcard.green{background:var(--gp);border-color:var(--gl)}
.hcard.red{background:#fff5f5;border-color:#fecaca}
.hcard.blue{background:var(--bl);border-color:#bfdbfe}
.hclbl{font-size:10px;font-weight:800;text-transform:uppercase;letter-spacing:.07em;margin-bottom:5px}
.hcard.gold .hclbl{color:#92400e}
.hcard.green .hclbl{color:var(--gd)}
.hcard.red .hclbl{color:#991b1b}
.hcard.blue .hclbl{color:var(--blue)}
.hcval{font-size:15px;font-weight:800}
.hcsub{font-size:11px;color:var(--txm);margin-top:2px}
/* YEAR COMPARE */
.yrcards{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:10px;margin-bottom:1.2rem}
.yrcard{background:var(--surf);border:1px solid var(--bdr);border-radius:var(--r);padding:.9rem 1.1rem;box-shadow:var(--sh)}
.yrcard.cur{border-color:var(--gm);border-width:2px}
/* TREE GRID */
.tgrid{display:grid;grid-template-columns:repeat(auto-fill,minmax(230px,1fr));gap:1rem;margin-bottom:1rem}
.tcard{background:var(--surf);border-radius:var(--r);border:1px solid var(--bdr);overflow:hidden;box-shadow:var(--sh);cursor:pointer;transition:all .16s}
.tcard:hover{transform:translateY(-3px);box-shadow:0 6px 20px rgba(45,106,63,.15);border-color:var(--gm)}
.tch{padding:.65rem .9rem;display:flex;align-items:center;gap:9px}
.tch-ini{width:32px;height:32px;border-radius:50%;background:rgba(255,255,255,.25);color:#fff;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:900;flex-shrink:0}
.tch-name{color:#fff;font-weight:800;font-size:13px}
.tch-sub{color:rgba(255,255,255,.8);font-size:11px}
.tcstage{background:linear-gradient(180deg,#dceefb 0%,#c5e8c8 60%,#a5d6a7 100%);min-height:155px;display:flex;align-items:center;justify-content:center;padding:.4rem}
.tcstage svg{width:100%;height:155px}
.tcfoot{padding:.55rem .9rem;display:flex;justify-content:space-between;font-size:12px;font-weight:700;color:var(--txm);border-top:1px solid var(--bdr)}
/* MODAL */
.mbg{display:none;position:fixed;inset:0;background:rgba(0,0,0,.48);z-index:800;align-items:center;justify-content:center;padding:1rem}
.mbg.open{display:flex}
.modal{background:var(--surf);border-radius:var(--r);padding:1.4rem;width:100%;max-width:450px;box-shadow:0 8px 40px rgba(0,0,0,.22);max-height:90vh;overflow-y:auto}
.modal h2{font-family:'Lora',serif;font-size:17px;font-weight:600;margin-bottom:.9rem;color:var(--gd)}
/* STUDENT DETAIL MODAL */
.smmodal{max-width:530px}
.bigtree{background:linear-gradient(180deg,#c8e6f7 0%,#dceefb 35%,#c5e8c8 65%,#a5d6a7 100%);border-radius:var(--r);margin-bottom:1rem;display:flex;justify-content:center;min-height:280px;border:1px solid var(--gl)}
.bigtree svg{max-width:100%;height:270px}
/* REFLECTION */
.imp{display:flex;gap:8px;padding:7px 0;border-bottom:1px solid var(--bdr);font-size:13px}
.imp:last-child{border-bottom:none}
.impn{font-weight:800;color:var(--gm);min-width:20px}
/* EMPTY */
.empty{text-align:center;padding:1.4rem;color:var(--txm);font-size:13px}
.eico{font-size:26px;display:block;margin-bottom:5px}
/* TOAST */
#toast{position:fixed;bottom:20px;left:50%;transform:translateX(-50%) translateY(80px);background:var(--gd);color:#fff;padding:8px 20px;border-radius:28px;font-size:13px;font-weight:700;box-shadow:0 4px 18px rgba(0,0,0,.2);transition:transform .28s ease;z-index:9999;pointer-events:none;white-space:nowrap}
#toast.show{transform:translateX(-50%) translateY(0)}
@media(max-width:580px){.fg3{grid-template-columns:1fr 1fr}.sgrid{grid-template-columns:repeat(auto-fill,minmax(130px,1fr))}.tgrid{grid-template-columns:1fr 1fr}}
@media print{header,#toast,.tabs,.btn,.hbtn,.sdel{display:none!important}.sec{display:block!important;margin-bottom:2rem}}
</style>
</head>
<body>

<header>
  <div style="font-size:30px">🌳</div>
  <div class="htxt">
    <h1>Kindness Tree Tracker</h1>
    <p>SEE Learning · Preschool · <span id="yr-lbl"></span></p>
  </div>
  <div class="hright">
    <select id="yr-sel" class="hsel"></select>
    <button class="hbtn" onclick="openNewYear()">+ New year</button>
    <button class="hbtn" onclick="doExportCSV()">⬇ Export</button>
    <button class="hbtn" onclick="window.print()">🖨 Print</button>
    <button class="hbtn" onclick="resetData()" style="background:rgba(255,80,80,.2);border-color:rgba(255,120,120,.4)">↺ Reload data</button><div class="hbadge">PD Evidence</div>
  </div>
</header>

<div class="wrap">
  <div class="tabs">
    <button class="tab active" id="tab-btn-roster" onclick="goTab('roster',this)">👦 Students</button>
    <button class="tab" id="tab-btn-log" onclick="goTab('log',this)">❤️ Log act</button>
    <button class="tab" id="tab-btn-trees" onclick="goTab('trees',this)">🌳 All trees</button>
    <button class="tab" id="tab-btn-stats" onclick="goTab('stats',this)">📊 Class stats</button>
    <button class="tab" id="tab-btn-compare" onclick="goTab('compare',this)">📅 Year compare</button>
    <button class="tab" id="tab-btn-reflect" onclick="goTab('reflect',this)">💡 Reflection</button>
    <button class="tab report-tab" id="tab-btn-report" onclick="goTab('report',this)">📄 Report</button>
  </div>

  <!-- STUDENTS TAB -->
  <div class="sec on" id="tab-roster">
    <div class="card">
      <div class="ctitle">Add students to your class</div>
      <div style="display:flex;gap:8px;margin-bottom:9px;flex-wrap:wrap">
        <input type="text" id="rs-input" placeholder="Type a student name…" style="flex:1;min-width:150px" onkeydown="if(event.key==='Enter')addStudent()"/>
        <button class="btn bp" onclick="addStudent()">+ Add student</button>
        <button class="btn bs" onclick="openBulkModal()">📋 Paste full list</button>
      </div>
      <p style="font-size:12px;color:var(--txm)">Tip: use "Paste full list" to add all names at once — one name per line.</p>
    </div>
    <div class="card">
      <div class="ctitle">Class roster — <span id="roster-count">0</span> students</div>
      <div id="student-grid" class="sgrid">
        <div class="empty"><span class="eico">👦</span>No students yet — add names above</div>
      </div>
    </div>
  </div>

  <!-- LOG TAB -->
  <div class="sec" id="tab-log">
    <div class="card">
      <div class="ctitle">Step 1 — Select a student</div>
      <div id="log-chips" style="display:flex;flex-wrap:wrap;gap:7px;margin-bottom:5px">
        <div class="empty" style="padding:.4rem"><span class="eico">👦</span>Add students in the Students tab first</div>
      </div>
    </div>
    <div id="log-form" style="display:none">
      <div class="sbanner">
        <div class="bini" id="b-ini"></div>
        <div style="flex:1"><div class="bname" id="b-name"></div><div class="bmeta" id="b-meta"></div></div>
        <div style="font-size:18px" id="b-toks"></div>
      </div>
      <div class="card">
        <div class="ctitle">Step 2 — Choose a token</div>
        <div class="tpick">
          <div class="tpk" id="tpk-h" onclick="pickToken('h')"><span class="ti">❤️</span>Heart</div>
          <div class="tpk" id="tpk-a" onclick="pickToken('a')"><span class="ti">🍎</span>Apple</div>
        </div>
        <div class="ctitle">Step 3 — Details</div>
        <div class="fg3">
          <div class="fg"><label>Date</label><input type="date" id="f-date"/></div>
          <div class="fg">
            <label>Type of kindness</label>
            <select id="f-type">
              <option value="">Select…</option>
              <option>Sharing</option>
              <option>Comforting a friend</option>
              <option>Including someone left out</option>
              <option>Saying kind words</option>
              <option>Cleaning up for others</option>

            </select>
          </div>
          <div class="fg">
            <label>Where did it happen?</label>
            <select id="f-ctx">
              <option value="">— optional —</option>
              <option>Learning Center</option>
              <option>Outside Play</option>
              <option>Choice Time</option>
              <option>Specials</option>
            </select>
          </div>
        </div>
        <div class="fg" style="margin-bottom:13px">
          <label>What happened? (optional)</label>
          <textarea id="f-desc" placeholder="Describe the act in a few words…"></textarea>
        </div>
        <div style="display:flex;gap:9px;flex-wrap:wrap;align-items:center">
          <button class="btn bp" onclick="addEntry()">+ Add to tree</button>
          <span id="log-fb" style="font-size:13px;color:var(--gd);font-weight:700"></span>
        </div>
      </div>
      <div class="card">
        <div class="ctitle">Recent acts — <span id="log-sname"></span> <span id="log-cnt" style="font-weight:400;color:var(--txl)"></span></div>
        <div id="log-list"><div class="empty"><span class="eico">🌱</span>No acts logged yet for this student</div></div>
      </div>
    </div>
  </div>

  <!-- ALL TREES TAB -->
  <div class="sec" id="tab-trees">
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:1rem;flex-wrap:wrap;gap:7px">
      <div style="font-family:'Lora',serif;font-size:17px;font-weight:600;color:var(--gd)">Every student's kindness tree</div>
      <span style="font-size:13px;color:var(--txm)">Click a tree to see full details</span>
    </div>
    <div id="all-trees" class="tgrid"></div>
  </div>

  <!-- STATS TAB -->
  <div class="sec" id="tab-stats">
    <div class="mgrid">
      <div class="met"><div class="mlbl">Total acts</div><div class="mval" id="s-tot">0</div><div class="msub">this year</div></div>
      <div class="met blue"><div class="mlbl">Students</div><div class="mval" id="s-stu">0</div><div class="msub">in class</div></div>
      <div class="met pink"><div class="mlbl">Hearts ❤️</div><div class="mval" id="s-h">0</div><div class="msub">given</div></div>
      <div class="met amber"><div class="mlbl">Apples 🍎</div><div class="mval" id="s-a">0</div><div class="msub">given</div></div>
    </div>
    <div class="hcards">
      <div class="hcard gold"><div class="hclbl">🏆 Kindest student</div><div class="hcval" id="hs-k">—</div><div class="hcsub" id="hs-ks"></div></div>
      <div class="hcard green"><div class="hclbl">⭐ Most seen act</div><div class="hcval" id="hs-top">—</div><div class="hcsub" id="hs-tops"></div></div>
      <div class="hcard red"><div class="hclbl">💬 Least seen act</div><div class="hcval" id="hs-low">—</div><div class="hcsub" id="hs-lows"></div></div>
      <div class="hcard blue"><div class="hclbl">📍 Top context</div><div class="hcval" id="hs-ctx">—</div><div class="hcsub" id="hs-ctxs"></div></div>
    </div>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:1.2rem;margin-bottom:1.2rem">
      <div class="card" style="margin:0"><div class="ctitle">Kindness types — most to least</div><div id="type-bars"></div></div>
      <div class="card" style="margin:0"><div class="ctitle">By location</div><div id="ctx-bars"></div></div>
    </div>
    <div class="card"><div class="ctitle">Student summary</div><div id="stbl-wrap"></div></div>
    <div class="card"><div class="ctitle">Acts needing more encouragement</div><div id="low-acts"></div></div>
  </div>

  <!-- COMPARE TAB -->
  <div class="sec" id="tab-compare">
    <div style="font-family:'Lora',serif;font-size:17px;font-weight:600;color:var(--gd);margin-bottom:1rem">Year-on-year comparison</div>
    <div id="yr-cards" class="yrcards"></div>
    <div class="card"><div class="ctitle">Total acts per year</div><div id="cmp-bars"></div></div>
    <div class="card"><div class="ctitle">Kindness type breakdown across years</div><div id="cmp-types"></div></div>
  </div>

  <!-- REFLECTION TAB -->
  <div class="sec" id="tab-reflect">
    <div class="card"><div class="ctitle">What is working well</div><div id="wins"></div></div>
    <div class="card">
      <div class="ctitle">What we could do better</div>
      <div class="imp"><span class="impn">1.</span><span>Introduce a "kindness of the week" story to model specific behaviours</span></div>
      <div class="imp"><span class="impn">2.</span><span>Create a buddy system to help quieter students practise inclusion</span></div>
      <div class="imp"><span class="impn">3.</span><span>Add a group celebration when the tree is fully covered in tokens</span></div>
      <div class="imp"><span class="impn">4.</span><span>Send a note home when a student earns 5+ tokens so families celebrate too</span></div>
      <div class="imp"><span class="impn">5.</span><span>Track which context produces most kindness to design richer activities</span></div>
      <div class="imp"><span class="impn">6.</span><span>Complete the SEE Learning PD modules in the next cycle</span></div>
    </div>
    <div class="card">
      <div class="ctitle">SEE Learning connection</div>
      <p style="font-size:13px;color:var(--txm);margin-bottom:11px">The Kindness Tree supports SEE Learning's three core domains:</p>
      <div style="display:flex;gap:7px;align-items:center;padding:5px 0;font-size:13px"><span style="background:var(--bl);color:var(--blue);font-size:11px;font-weight:800;padding:3px 9px;border-radius:9px;flex-shrink:0">Personal</span> Students recognise their own capacity to act with care</div>
      <div style="display:flex;gap:7px;align-items:center;padding:5px 0;font-size:13px"><span style="background:var(--gl);color:var(--gd);font-size:11px;font-weight:800;padding:3px 9px;border-radius:9px;flex-shrink:0">Social</span> Sharing, comforting, and including build relational skills</div>
      <div style="display:flex;gap:7px;align-items:center;padding:5px 0;font-size:13px"><span style="background:var(--al);color:var(--amber);font-size:11px;font-weight:800;padding:3px 9px;border-radius:9px;flex-shrink:0">Systems</span> The visible tree shows students that kindness has collective impact</div>
    </div>
    <div class="card">
      <div class="ctitle">Personal notes &amp; reflections</div>
      <textarea id="notes-area" style="width:100%;min-height:100px" placeholder="Write personal reflections, observations, ideas…"></textarea>
    </div>
  </div>

  <!-- REPORT TAB -->
  <div class="sec" id="tab-report">
    <div style="background:linear-gradient(135deg,#1e3a2f,#2d6a3f);border-radius:var(--r);padding:1.8rem;margin-bottom:1.2rem;color:#fff;text-align:center">
      <div style="font-size:38px;margin-bottom:.7rem">📄</div>
      <h2 style="font-family:'Lora',serif;font-size:21px;font-weight:600;margin-bottom:.4rem">Generate your evaluation report</h2>
      <p style="font-size:13px;opacity:.8;max-width:460px;margin:0 auto 1.3rem">Creates a complete, professional PDF-ready report to email to your principal — no login or account needed.</p>
      <div style="display:flex;gap:9px;justify-content:center;flex-wrap:wrap;margin-bottom:1.3rem">
        <div style="background:rgba(255,255,255,.12);border-radius:9px;padding:.65rem 1rem;font-size:12px">🌳 Cover + class summary</div>
        <div style="background:rgba(255,255,255,.12);border-radius:9px;padding:.65rem 1rem;font-size:12px">📊 Stats &amp; highlights</div>
        <div style="background:rgba(255,255,255,.12);border-radius:9px;padding:.65rem 1rem;font-size:12px">👦 Every student's tree</div>
        <div style="background:rgba(255,255,255,.12);border-radius:9px;padding:.65rem 1rem;font-size:12px">💡 SEE Learning reflection</div>
      </div>
      <button onclick="generateReport()" style="font-family:'Nunito',sans-serif;font-weight:800;font-size:14px;padding:11px 28px;border-radius:28px;border:none;background:#fff;color:#2d6a3f;cursor:pointer;box-shadow:0 4px 14px rgba(0,0,0,.2)">📄 Open Report in New Tab</button>
    </div>
    <div class="card">
      <div class="ctitle">Personal message for your principal (optional)</div>
      <textarea id="report-msg" style="width:100%;min-height:95px" placeholder="e.g. Dear [Principal name], please find below my end-of-year evidence for my SEE Learning professional development goal…"></textarea>
      <p style="font-size:12px;color:var(--txm);margin-top:7px">This message will appear at the top of the report.</p>
    </div>
    <div class="card">
      <div class="ctitle">How to save as PDF &amp; share</div>
      <div style="display:flex;flex-direction:column;gap:9px">
        <div style="display:flex;gap:9px;align-items:flex-start;font-size:13px"><span style="background:var(--gd);color:#fff;border-radius:50%;width:21px;height:21px;display:flex;align-items:center;justify-content:center;font-weight:800;font-size:11px;flex-shrink:0">1</span><span>Click <strong>Open Report in New Tab</strong></span></div>
        <div style="display:flex;gap:9px;align-items:flex-start;font-size:13px"><span style="background:var(--gd);color:#fff;border-radius:50%;width:21px;height:21px;display:flex;align-items:center;justify-content:center;font-weight:800;font-size:11px;flex-shrink:0">2</span><span>Press <strong>Ctrl+P</strong> (Windows) or <strong>Cmd+P</strong> (Mac)</span></div>
        <div style="display:flex;gap:9px;align-items:flex-start;font-size:13px"><span style="background:var(--gd);color:#fff;border-radius:50%;width:21px;height:21px;display:flex;align-items:center;justify-content:center;font-weight:800;font-size:11px;flex-shrink:0">3</span><span>Set destination to <strong>"Save as PDF"</strong></span></div>
        <div style="display:flex;gap:9px;align-items:flex-start;font-size:13px"><span style="background:var(--gd);color:#fff;border-radius:50%;width:21px;height:21px;display:flex;align-items:center;justify-content:center;font-weight:800;font-size:11px;flex-shrink:0">4</span><span>Email the PDF to your principal</span></div>
      </div>
    </div>
  </div>
</div>

<!-- NEW YEAR MODAL -->
<div class="mbg" id="ny-modal">
  <div class="modal">
    <h2>Start a new school year</h2>
    <div class="fg" style="margin-bottom:11px"><label>School year</label><input type="text" id="ny-input" placeholder="e.g. 2025-2026"/></div>
    <p style="font-size:13px;color:var(--txm);margin-bottom:13px">Your current year data stays saved. Switch anytime from the dropdown.</p>
    <div style="display:flex;gap:7px">
      <button class="btn bp" onclick="createNewYear()">Create year</button>
      <button class="btn bs" onclick="closeModal('ny-modal')">Cancel</button>
    </div>
  </div>
</div>

<!-- BULK MODAL -->
<div class="mbg" id="bulk-modal">
  <div class="modal">
    <h2>Paste your class list</h2>
    <p style="font-size:13px;color:var(--txm);margin-bottom:9px">One student name per line. Duplicates are ignored.</p>
    <textarea id="bulk-input" style="width:100%;min-height:150px;margin-bottom:11px" placeholder="Amina&#10;Bilal&#10;Sofia&#10;Lucas&#10;…"></textarea>
    <div style="display:flex;gap:7px">
      <button class="btn bp" onclick="confirmBulk()">Add all students</button>
      <button class="btn bs" onclick="closeModal('bulk-modal')">Cancel</button>
    </div>
  </div>
</div>

<!-- STUDENT DETAIL MODAL -->
<div class="mbg" id="stu-modal">
  <div class="modal smmodal">
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:.9rem">
      <h2 id="sm-name" style="margin:0"></h2>
      <button class="btn bs" style="padding:4px 11px;font-size:12px" onclick="closeModal('stu-modal')">✕ Close</button>
    </div>
    <div class="bigtree"><svg id="sm-tree" viewBox="0 0 420 270" xmlns="http://www.w3.org/2000/svg"></svg></div>
    <div style="display:flex;justify-content:center;gap:18px;font-size:13px;font-weight:700;color:var(--txm);margin-bottom:.9rem">
      <span>❤️ <strong id="sm-h">0</strong></span>
      <span>🍎 <strong id="sm-a">0</strong></span>
      <span>Total: <strong id="sm-tot">0</strong></span>
    </div>
    <div class="ctitle">All acts</div>
    <div id="sm-log" style="max-height:210px;overflow-y:auto"></div>
  </div>
</div>

<div id="toast"></div>

<script>
var KT_STUDENTS = ["Lilly", "Zahed", "Ghali", "Indigo", "Ozzie", "Oscar", "Sophia", "Mehdi", "Dario", "Teny", "Maya", "Anais", "Juna", "Dylan", "Amir"];
var KT_ENTRIES = [{"id":1650000198026,"name":"Lilly","date":"2025-05-16","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1650000198046,"name":"Zahed","date":"2025-05-16","type":"Sharing","token":"a","ctx":"Outside Play","desc":"Let a friend join their card game during Choice Time"},{"id":1650000198082,"name":"Teny","date":"2025-05-16","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Told a friend their work was really good"},{"id":1650000198133,"name":"Dylan","date":"2025-05-16","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Put away puzzle pieces a friend had left behind"},{"id":1750000000027,"name":"Maya","date":"2025-05-16","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Said kind and encouraging words to a friend who was trying hard"},{"id":1750000000055,"name":"Juna","date":"2025-05-16","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Gave a hug to a friend who was feeling down"},{"id":1750000000083,"name":"Anais","date":"2025-05-16","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Gave a warm greeting to a friend arriving at school"},{"id":1750000000139,"name":"Ozzie","date":"2025-05-16","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Made sure every friend had a spot in the circle"},{"id":1750000000195,"name":"Indigo","date":"2025-05-16","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Asked a friend with no partner to be their partner"},{"id":1750000000251,"name":"Sophia","date":"2025-05-16","type":"Including someone left out","token":"h","ctx":"Specials","desc":"Made room in the group for a friend who was standing on the side"},{"id":1750000000279,"name":"Ghali","date":"2025-05-16","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Sat next to a friend who was upset and offered kind words"},{"id":1750000000307,"name":"Amir","date":"2025-05-16","type":"Sharing","token":"h","ctx":"Outside Play","desc":"Gave a friend some of their materials to finish their project"},{"id":1750000000335,"name":"Dario","date":"2025-05-16","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Gave a hug to a friend who was feeling down"},{"id":1750000000363,"name":"Oscar","date":"2025-05-16","type":"Cleaning up for others","token":"a","ctx":"Outside Play","desc":"Tidied the art materials after Learning Center"},{"id":1650000114000,"name":"Amir","date":"2025-05-15","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Put away the blocks after Outside Play even though they were not all theirs"},{"id":1650000198038,"name":"Ozzie","date":"2025-05-15","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Complimented a friend on their new shoes"},{"id":1650000198068,"name":"Indigo","date":"2025-05-15","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Told a friend it was going to be okay when they were worried"},{"id":1750000000054,"name":"Juna","date":"2025-05-15","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Picked up toys left on the floor during clean-up"},{"id":1750000000167,"name":"Zahed","date":"2025-05-15","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Put away the blocks after Outside Play even though they were not all theirs"},{"id":1750000000223,"name":"Teny","date":"2025-05-15","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Made room in the group for a friend who was standing on the side"},{"id":1750000000250,"name":"Sophia","date":"2025-05-15","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Brought a tissue to a friend who was upset"},{"id":1750000000391,"name":"Dylan","date":"2025-05-15","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Gave a hug to a friend who was feeling down"},{"id":1750000000419,"name":"Mehdi","date":"2025-05-15","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Picked up items from the floor without being asked"},{"id":1650000038000,"name":"Juna","date":"2025-05-14","type":"Sharing","token":"h","ctx":"Choice Time","desc":"Gave a friend some of their blocks to finish their tower"},{"id":1650000072000,"name":"Lilly","date":"2025-05-14","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Told a friend their outfit was so cool"},{"id":1650000127000,"name":"Zahed","date":"2025-05-14","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Cleaned up the board game after everyone had left the table"},{"id":1650000198069,"name":"Indigo","date":"2025-05-14","type":"Cleaning up for others","token":"a","ctx":"Outside Play","desc":"Helped put away materials left on the table after the activity"},{"id":1650000198086,"name":"Sophia","date":"2025-05-14","type":"Sharing","token":"h","ctx":"Outside Play","desc":"Let a friend join their card game during Choice Time"},{"id":1750000000026,"name":"Maya","date":"2025-05-14","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Complimented a friend on their drawing"},{"id":1750000000138,"name":"Ozzie","date":"2025-05-14","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Noticed a friend sitting alone and invited them to join"},{"id":1750000000306,"name":"Amir","date":"2025-05-14","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Told a friend their outfit looked wonderful"},{"id":1750000000362,"name":"Oscar","date":"2025-05-14","type":"Sharing","token":"a","ctx":"Outside Play","desc":"Offered their snack to a friend who had forgotten theirs"},{"id":1650000021000,"name":"Maya","date":"2025-05-13","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Made room in the group for a friend who was standing on the side"},{"id":1650000071000,"name":"Lilly","date":"2025-05-13","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Noticed a friend sitting by themselves and invited them to join the game"},{"id":1650000126000,"name":"Zahed","date":"2025-05-13","type":"Sharing","token":"a","ctx":"Choice Time","desc":"Shared the board game pieces so everyone could play during Choice Time"},{"id":1650000142000,"name":"Ghali","date":"2025-05-13","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Made sure a friend who was left out had a spot in the circle"},{"id":1650000198164,"name":"Mehdi","date":"2025-05-13","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Helped put away materials left on the table after the activity"},{"id":1750000000305,"name":"Amir","date":"2025-05-13","type":"Sharing","token":"a","ctx":"Specials","desc":"Shared the Lego blocks with a friend who needed more pieces"},{"id":1750000000334,"name":"Dario","date":"2025-05-13","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Told a friend their feelings were valid and stayed close"},{"id":1750000000390,"name":"Dylan","date":"2025-05-13","type":"Including someone left out","token":"a","ctx":"Specials","desc":"Invited a new friend to sit with them at the table"},{"id":1650000070000,"name":"Lilly","date":"2025-05-12","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Put their arm around a friend who was feeling sad"},{"id":1650000125000,"name":"Zahed","date":"2025-05-12","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Asked a friend who had no partner to be their partner"},{"id":1650000141000,"name":"Ghali","date":"2025-05-12","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Tidied the art materials after Learning Center activity"},{"id":1650000184000,"name":"Indigo","date":"2025-05-12","type":"Cleaning up for others","token":"a","ctx":"Outside Play","desc":"Helped tidy up the area after the activity without being asked"},{"id":1650000191000,"name":"Oscar","date":"2025-05-12","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Noticed a friend sitting by themselves and invited them to join the game"},{"id":1650000198163,"name":"Dario","date":"2025-05-12","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Said we missed you when a friend returned after being away"},{"id":1650000198170,"name":"Mehdi","date":"2025-05-12","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Gave a compliment about a friend's drawing"},{"id":1750000000025,"name":"Maya","date":"2025-05-12","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1750000000053,"name":"Juna","date":"2025-05-12","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Said kind and encouraging words to a friend who was trying hard"},{"id":1750000000082,"name":"Anais","date":"2025-05-12","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Went up to a friend playing alone and said come play with us"},{"id":1750000000137,"name":"Ozzie","date":"2025-05-12","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Told a friend they did a great job during the activity"},{"id":1750000000249,"name":"Sophia","date":"2025-05-12","type":"Cleaning up for others","token":"h","ctx":"Outside Play","desc":"Picked up items from the floor without being asked"},{"id":1750000000304,"name":"Amir","date":"2025-05-12","type":"Sharing","token":"h","ctx":"Specials","desc":"Gave a friend some of their blocks to finish their tower"},{"id":1750000000389,"name":"Dylan","date":"2025-05-12","type":"Cleaning up for others","token":"a","ctx":"Outside Play","desc":"Helped stack chairs after an activity without being told"},{"id":1650000020000,"name":"Maya","date":"2025-05-09","type":"Comforting a friend","token":"h","ctx":"Choice Time","desc":"Brought a tissue to a friend who was upset outside"},{"id":1650000124000,"name":"Zahed","date":"2025-05-09","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Sat next to a friend who was crying outside and stayed with them"},{"id":1650000198117,"name":"Oscar","date":"2025-05-09","type":"Sharing","token":"a","ctx":"Learning Center","desc":"Offered their snack to a friend who had forgotten theirs"},{"id":1750000000052,"name":"Juna","date":"2025-05-09","type":"Including someone left out","token":"h","ctx":"Learning Center","desc":"Invited a new friend to sit with them at the table"},{"id":1750000000081,"name":"Anais","date":"2025-05-09","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Comforted a friend after they fell and was crying"},{"id":1750000000111,"name":"Lilly","date":"2025-05-09","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Said something kind to a friend who looked nervous"},{"id":1750000000136,"name":"Ozzie","date":"2025-05-09","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Put away the blocks after Outside Play even though they were not all theirs"},{"id":1750000000194,"name":"Indigo","date":"2025-05-09","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Picked up items from the floor without being asked"},{"id":1750000000222,"name":"Teny","date":"2025-05-09","type":"Sharing","token":"h","ctx":"Learning Center","desc":"Shared building blocks equally so all friends had some"},{"id":1750000000303,"name":"Amir","date":"2025-05-09","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Said thank you to the teacher for helping them"},{"id":1750000000388,"name":"Dylan","date":"2025-05-09","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Gave a warm greeting to a friend arriving at school"},{"id":1750000000418,"name":"Mehdi","date":"2025-05-09","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Stayed beside a friend who missed their parent at drop-off"},{"id":1650000086000,"name":"Anais","date":"2025-05-08","type":"Sharing","token":"h","ctx":"Choice Time","desc":"Gave a friend some of their blocks to finish their tower"},{"id":1650000097000,"name":"Teny","date":"2025-05-08","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Brought a tissue to a friend who was upset outside"},{"id":1650000175000,"name":"Dario","date":"2025-05-08","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Made sure a friend who was left out had a spot in the circle"},{"id":1650000198067,"name":"Indigo","date":"2025-05-08","type":"Sharing","token":"h","ctx":"Choice Time","desc":"Shared Lego blocks with a friend who needed more pieces"},{"id":1650000198089,"name":"Sophia","date":"2025-05-08","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Asked a friend with no partner to be their partner"},{"id":1650000198114,"name":"Oscar","date":"2025-05-08","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Complimented a friend on their new shoes"},{"id":1750000000024,"name":"Maya","date":"2025-05-08","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Made room in the group for a friend who was standing on the side"},{"id":1750000000051,"name":"Juna","date":"2025-05-08","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Complimented a friend on their drawing"},{"id":1750000000110,"name":"Lilly","date":"2025-05-08","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Noticed a friend was sad and asked if they were alright"},{"id":1750000000166,"name":"Zahed","date":"2025-05-08","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Said we missed you when a friend returned after being away"},{"id":1750000000302,"name":"Amir","date":"2025-05-08","type":"Sharing","token":"a","ctx":"Choice Time","desc":"Gave a friend some of their materials to finish their project"},{"id":1750000000387,"name":"Dylan","date":"2025-05-08","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Made sure no one was left out during the game"},{"id":1750000000417,"name":"Mehdi","date":"2025-05-08","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Helped put away materials left on the table after the activity"},{"id":1650000019000,"name":"Maya","date":"2025-05-07","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Said your hair looks so nice today to a friend"},{"id":1650000037000,"name":"Juna","date":"2025-05-07","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Made room in the group for a friend who was standing on the side"},{"id":1650000056000,"name":"Sophia","date":"2025-05-07","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Said to the teacher you look so beautiful today"},{"id":1650000140000,"name":"Ghali","date":"2025-05-07","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Asked a friend who had no partner to be their partner"},{"id":1650000183000,"name":"Indigo","date":"2025-05-07","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Said to the teacher you look so beautiful today"},{"id":1650000198136,"name":"Dylan","date":"2025-05-07","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Said thank you to the teacher for helping them"},{"id":1650000198145,"name":"Amir","date":"2025-05-07","type":"Sharing","token":"a","ctx":"Learning Center","desc":"Gave a friend some of their materials to finish their project"},{"id":1650000198169,"name":"Mehdi","date":"2025-05-07","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Invited a friend who was sitting alone to join the game"},{"id":1750000000080,"name":"Anais","date":"2025-05-07","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Told a friend their outfit looked wonderful"},{"id":1750000000109,"name":"Lilly","date":"2025-05-07","type":"Including someone left out","token":"h","ctx":"Choice Time","desc":"Made room in the group for a friend who was standing on the side"},{"id":1750000000165,"name":"Zahed","date":"2025-05-07","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Helped tidy up the area after the activity without being asked"},{"id":1750000000221,"name":"Teny","date":"2025-05-07","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Said thank you to the teacher for helping them"},{"id":1750000000333,"name":"Dario","date":"2025-05-07","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Sat quietly beside a friend who was having a hard morning"},{"id":1650000055000,"name":"Sophia","date":"2025-05-06","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Tidied the art materials after Learning Center activity"},{"id":1650000096000,"name":"Teny","date":"2025-05-06","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Told a friend their outfit was so cool"},{"id":1650000123000,"name":"Zahed","date":"2025-05-06","type":"Sharing","token":"a","ctx":"Outside Play","desc":"Let two friends join their card game during Choice Time"},{"id":1650000198021,"name":"Anais","date":"2025-05-06","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1650000198065,"name":"Indigo","date":"2025-05-06","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Invited a friend who was sitting alone to join the game"},{"id":1750000000023,"name":"Maya","date":"2025-05-06","type":"Comforting a friend","token":"h","ctx":"Choice Time","desc":"Sat next to a friend who was upset and offered kind words"},{"id":1750000000108,"name":"Lilly","date":"2025-05-06","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Gave a warm greeting to a friend arriving at school"},{"id":1750000000135,"name":"Ozzie","date":"2025-05-06","type":"Sharing","token":"a","ctx":"Outside Play","desc":"Let a friend join their card game during Choice Time"},{"id":1750000000301,"name":"Amir","date":"2025-05-06","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Tidied up blocks that were left on the floor during clean-up"},{"id":1750000000361,"name":"Oscar","date":"2025-05-06","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Stacked books back on the shelf after Learning Center"},{"id":1750000000386,"name":"Dylan","date":"2025-05-06","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Told a friend their work was really good"},{"id":1750000000416,"name":"Mehdi","date":"2025-05-06","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Waved a friend over to join the group outside"},{"id":1650000113000,"name":"Amir","date":"2025-05-05","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Said kind and encouraging words to a friend"},{"id":1650000155000,"name":"Ozzie","date":"2025-05-05","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Sat next to a friend who was crying outside and stayed with them"},{"id":1650000198099,"name":"Ghali","date":"2025-05-05","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Said we missed you when a friend returned after being away"},{"id":1750000000022,"name":"Maya","date":"2025-05-05","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Made room in the group for a friend who was standing on the side"},{"id":1750000000107,"name":"Lilly","date":"2025-05-05","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Sat quietly beside a friend who was having a hard morning"},{"id":1750000000164,"name":"Zahed","date":"2025-05-05","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Told a friend their work was really good"},{"id":1750000000193,"name":"Indigo","date":"2025-05-05","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Noticed a friend sitting alone and invited them to join"},{"id":1750000000332,"name":"Dario","date":"2025-05-05","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Helped tidy up the area after the activity without being asked"},{"id":1750000000360,"name":"Oscar","date":"2025-05-05","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Stacked books back on the shelf after Learning Center"},{"id":1750000000385,"name":"Dylan","date":"2025-05-05","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Said something kind to a friend who looked nervous"},{"id":1650000112000,"name":"Amir","date":"2025-05-02","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Put their arm around a friend who was feeling sad"},{"id":1650000154000,"name":"Ozzie","date":"2025-05-02","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Put away the blocks after Outside Play even though they were not all theirs"},{"id":1650000198112,"name":"Oscar","date":"2025-05-02","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Noticed a friend was sad and asked if they were alright"},{"id":1650000198159,"name":"Dario","date":"2025-05-02","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Told a friend their outfit looked wonderful"},{"id":1750000000050,"name":"Juna","date":"2025-05-02","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Sat next to a friend who was upset and offered kind words"},{"id":1750000000079,"name":"Anais","date":"2025-05-02","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Said your hair looks so nice today to a friend"},{"id":1750000000106,"name":"Lilly","date":"2025-05-02","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Noticed a friend was sad and asked if they were alright"},{"id":1750000000163,"name":"Zahed","date":"2025-05-02","type":"Sharing","token":"a","ctx":"Specials","desc":"Offered their snack to a friend who had forgotten theirs"},{"id":1750000000192,"name":"Indigo","date":"2025-05-02","type":"Sharing","token":"a","ctx":"Learning Center","desc":"Let a friend use their art supplies when they ran out"},{"id":1750000000384,"name":"Dylan","date":"2025-05-02","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Told a friend they did a great job during the activity"},{"id":1650000018000,"name":"Maya","date":"2025-05-01","type":"Sharing","token":"h","ctx":"Choice Time","desc":"Shared the Lego blocks with a friend during Outside Play"},{"id":1650000069000,"name":"Lilly","date":"2025-05-01","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Said to the teacher you look so beautiful today"},{"id":1650000111000,"name":"Amir","date":"2025-05-01","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Said kind and encouraging words to a friend"},{"id":1650000153000,"name":"Ozzie","date":"2025-05-01","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Told a friend who was back after being sick we are so happy you are here"},{"id":1650000174000,"name":"Dario","date":"2025-05-01","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Gave a warm compliment to a friend"},{"id":1650000198061,"name":"Indigo","date":"2025-05-01","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Gave a compliment about a friend's drawing"},{"id":1650000198131,"name":"Dylan","date":"2025-05-01","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Helped put away materials left on the table after the activity"},{"id":1750000000220,"name":"Teny","date":"2025-05-01","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Actively encouraged a friend to join the group activity"},{"id":1750000000359,"name":"Oscar","date":"2025-05-01","type":"Sharing","token":"h","ctx":"Choice Time","desc":"Let a friend use their art supplies when they ran out"},{"id":1750000000415,"name":"Mehdi","date":"2025-05-01","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Noticed a friend was sad and asked if they were alright"},{"id":1650000054000,"name":"Sophia","date":"2025-04-30","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Helped clean up after the group activity"},{"id":1650000068000,"name":"Lilly","date":"2025-04-30","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Picked up toys left on the floor during Choice Time clean-up"},{"id":1650000085000,"name":"Anais","date":"2025-04-30","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Stacked the books back on the shelf after Learning Center"},{"id":1650000095000,"name":"Teny","date":"2025-04-30","type":"Including someone left out","token":"h","ctx":"Learning Center","desc":"Made sure a friend who was left out had a spot in the circle"},{"id":1650000198012,"name":"Juna","date":"2025-04-30","type":"Including someone left out","token":"h","ctx":"Choice Time","desc":"Made room in the group for a friend standing on the side"},{"id":1650000198044,"name":"Zahed","date":"2025-04-30","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Brought a tissue to a friend who was crying"},{"id":1650000198103,"name":"Oscar","date":"2025-04-30","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Put away puzzle pieces a friend had left behind"},{"id":1650000198175,"name":"Mehdi","date":"2025-04-30","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Said kind words to a friend who looked nervous"},{"id":1750000000021,"name":"Maya","date":"2025-04-30","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Told a friend their feelings were valid and stayed close"},{"id":1750000000134,"name":"Ozzie","date":"2025-04-30","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Comforted a friend after they fell and was crying"},{"id":1750000000191,"name":"Indigo","date":"2025-04-30","type":"Sharing","token":"h","ctx":"Specials","desc":"Gave a friend some of their materials to finish their project"},{"id":1750000000300,"name":"Amir","date":"2025-04-30","type":"Sharing","token":"a","ctx":"Choice Time","desc":"Shared building blocks equally so all friends had some"},{"id":1750000000331,"name":"Dario","date":"2025-04-30","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Put away the blocks after Outside Play even though they were not all theirs"},{"id":1750000000383,"name":"Dylan","date":"2025-04-30","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Tidied the art materials after Learning Center"},{"id":1650000067000,"name":"Lilly","date":"2025-04-29","type":"Comforting a friend","token":"h","ctx":"Choice Time","desc":"Stayed beside a friend who missed their parent at drop-off"},{"id":1650000139000,"name":"Ghali","date":"2025-04-29","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Tidied the art materials after Learning Center activity"},{"id":1650000198079,"name":"Teny","date":"2025-04-29","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Made room in the group for a friend standing on the side"},{"id":1650000198176,"name":"Mehdi","date":"2025-04-29","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Told a friend their work was really good"},{"id":1750000000020,"name":"Maya","date":"2025-04-29","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Checked on a friend who looked unhappy and stayed with them"},{"id":1750000000049,"name":"Juna","date":"2025-04-29","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Told a friend their feelings were valid and stayed close"},{"id":1750000000078,"name":"Anais","date":"2025-04-29","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Said we missed you when a friend returned after being away"},{"id":1750000000133,"name":"Ozzie","date":"2025-04-29","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Sat quietly beside a friend who was having a hard morning"},{"id":1750000000162,"name":"Zahed","date":"2025-04-29","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Put away the blocks after Outside Play even though they were not all theirs"},{"id":1750000000190,"name":"Indigo","date":"2025-04-29","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Said thank you to the teacher for helping them"},{"id":1750000000248,"name":"Sophia","date":"2025-04-29","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Went up to a friend playing alone and said come play with us"},{"id":1750000000299,"name":"Amir","date":"2025-04-29","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Checked on a friend who looked unhappy and stayed with them"},{"id":1750000000330,"name":"Dario","date":"2025-04-29","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Invited a new friend to sit with them at the table"},{"id":1750000000358,"name":"Oscar","date":"2025-04-29","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Invited a new friend to sit with them at the table"},{"id":1650000017000,"name":"Maya","date":"2025-04-28","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Welcomed a friend back warmly after they had been absent"},{"id":1650000138000,"name":"Ghali","date":"2025-04-28","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Stayed with a friend who needed support and comfort"},{"id":1650000166000,"name":"Mehdi","date":"2025-04-28","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Complimented a friend on their new shoes"},{"id":1650000198060,"name":"Indigo","date":"2025-04-28","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Gave a compliment about a friend's drawing"},{"id":1650000198074,"name":"Teny","date":"2025-04-28","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Helped stack chairs after an activity without being told"},{"id":1650000198105,"name":"Oscar","date":"2025-04-28","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Brought a tissue to a friend who was crying"},{"id":1650000198126,"name":"Dylan","date":"2025-04-28","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Went up to a friend who looked left out and included them"},{"id":1750000000048,"name":"Juna","date":"2025-04-28","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Actively encouraged a friend to join the group activity"},{"id":1750000000077,"name":"Anais","date":"2025-04-28","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Said thank you to the teacher for helping them"},{"id":1750000000105,"name":"Lilly","date":"2025-04-28","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Noticed a friend sitting alone and invited them to join"},{"id":1750000000132,"name":"Ozzie","date":"2025-04-28","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Stayed beside a friend who missed their parent at drop-off"},{"id":1750000000161,"name":"Zahed","date":"2025-04-28","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Cleaned up the game pieces after Choice Time without being asked"},{"id":1750000000247,"name":"Sophia","date":"2025-04-28","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Said your hair looks so nice today to a friend"},{"id":1750000000298,"name":"Amir","date":"2025-04-28","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Said thank you to the teacher for helping them"},{"id":1750000000329,"name":"Dario","date":"2025-04-28","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Put away puzzle pieces a friend had left behind"},{"id":1650000016000,"name":"Maya","date":"2025-04-25","type":"Including someone left out","token":"h","ctx":"Specials","desc":"Actively encouraged a friend to join the group activity"},{"id":1650000094000,"name":"Teny","date":"2025-04-25","type":"Comforting a friend","token":"h","ctx":"Choice Time","desc":"Checked on a friend who was sitting alone and looked unhappy"},{"id":1650000173000,"name":"Dario","date":"2025-04-25","type":"Including someone left out","token":"h","ctx":"Learning Center","desc":"Asked a friend who had no partner to be their partner"},{"id":1650000198022,"name":"Anais","date":"2025-04-25","type":"Including someone left out","token":"h","ctx":"Choice Time","desc":"Asked a friend with no partner to be their partner"},{"id":1650000198043,"name":"Ozzie","date":"2025-04-25","type":"Comforting a friend","token":"h","ctx":"Choice Time","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1650000198059,"name":"Indigo","date":"2025-04-25","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Told a friend their work was really good"},{"id":1650000198102,"name":"Ghali","date":"2025-04-25","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Stacked books back on the shelf after Learning Center"},{"id":1650000198142,"name":"Amir","date":"2025-04-25","type":"Comforting a friend","token":"h","ctx":"Choice Time","desc":"Checked on a friend who looked unhappy and stayed with them"},{"id":1750000000104,"name":"Lilly","date":"2025-04-25","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Noticed a friend sitting alone and invited them to join"},{"id":1750000000160,"name":"Zahed","date":"2025-04-25","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Said we missed you when a friend returned after being away"},{"id":1750000000246,"name":"Sophia","date":"2025-04-25","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Actively encouraged a friend to join the group activity"},{"id":1750000000357,"name":"Oscar","date":"2025-04-25","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Told a friend their feelings were valid and stayed close"},{"id":1750000000414,"name":"Mehdi","date":"2025-04-25","type":"Cleaning up for others","token":"a","ctx":"Outside Play","desc":"Cleaned up the board game after everyone had left the table"},{"id":1650000036000,"name":"Juna","date":"2025-04-24","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Brought a tissue to a friend who was upset outside"},{"id":1650000093000,"name":"Teny","date":"2025-04-24","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Complimented a friend on their new shoes"},{"id":1650000152000,"name":"Ozzie","date":"2025-04-24","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Stayed beside a friend who missed their parent at drop-off"},{"id":1650000198111,"name":"Oscar","date":"2025-04-24","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Gave a warm greeting to a friend arriving at school"},{"id":1650000198141,"name":"Amir","date":"2025-04-24","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Picked up items from the floor without being asked"},{"id":1650000198171,"name":"Mehdi","date":"2025-04-24","type":"Cleaning up for others","token":"a","ctx":"Outside Play","desc":"Stacked books back on the shelf after Learning Center"},{"id":1750000000076,"name":"Anais","date":"2025-04-24","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Complimented a friend on their drawing"},{"id":1750000000103,"name":"Lilly","date":"2025-04-24","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Stayed beside a friend who missed their parent at drop-off"},{"id":1750000000159,"name":"Zahed","date":"2025-04-24","type":"Including someone left out","token":"a","ctx":"Specials","desc":"Made sure every friend had a spot in the circle"},{"id":1750000000189,"name":"Indigo","date":"2025-04-24","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Made sure every friend had a spot in the circle"},{"id":1750000000245,"name":"Sophia","date":"2025-04-24","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Cleaned up the board game after everyone had left the table"},{"id":1750000000278,"name":"Ghali","date":"2025-04-24","type":"Sharing","token":"h","ctx":"Choice Time","desc":"Let a friend use their art supplies when they ran out"},{"id":1750000000328,"name":"Dario","date":"2025-04-24","type":"Sharing","token":"a","ctx":"Learning Center","desc":"Divided up the game pieces fairly so everyone could join"},{"id":1750000000382,"name":"Dylan","date":"2025-04-24","type":"Sharing","token":"a","ctx":"Specials","desc":"Shared the Lego blocks with a friend who needed more pieces"},{"id":1650000198017,"name":"Anais","date":"2025-04-23","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Sat beside a friend who was upset and offered kind words"},{"id":1650000198031,"name":"Lilly","date":"2025-04-23","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Said kind words to a friend who looked nervous"},{"id":1650000198034,"name":"Ozzie","date":"2025-04-23","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Helped put away materials left on the table after the activity"},{"id":1650000198161,"name":"Dario","date":"2025-04-23","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Sat beside a friend who was upset and offered kind words"},{"id":1650000198177,"name":"Mehdi","date":"2025-04-23","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Told a friend it was going to be okay when they were worried"},{"id":1750000000019,"name":"Maya","date":"2025-04-23","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Complimented a friend on their drawing"},{"id":1750000000188,"name":"Indigo","date":"2025-04-23","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Sat next to a friend who was upset and offered kind words"},{"id":1750000000219,"name":"Teny","date":"2025-04-23","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Said we missed you when a friend returned after being away"},{"id":1750000000244,"name":"Sophia","date":"2025-04-23","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Helped put away materials left on the table after the activity"},{"id":1750000000277,"name":"Ghali","date":"2025-04-23","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Gave a hug to a friend who was feeling down"},{"id":1650000035000,"name":"Juna","date":"2025-04-22","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Tidied the art materials after Learning Center activity"},{"id":1650000198058,"name":"Indigo","date":"2025-04-22","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Put away puzzle pieces a friend had left behind"},{"id":1750000000018,"name":"Maya","date":"2025-04-22","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Walked over to a friend sitting alone and started a conversation"},{"id":1750000000102,"name":"Lilly","date":"2025-04-22","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Welcomed a friend back warmly after they had been absent"},{"id":1750000000131,"name":"Ozzie","date":"2025-04-22","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Told a friend their outfit looked wonderful"},{"id":1750000000158,"name":"Zahed","date":"2025-04-22","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Waved a friend over to join the group outside"},{"id":1750000000218,"name":"Teny","date":"2025-04-22","type":"Including someone left out","token":"h","ctx":"Specials","desc":"Made sure no one was left out during the game"},{"id":1750000000243,"name":"Sophia","date":"2025-04-22","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Said thank you to the teacher for helping them"},{"id":1750000000276,"name":"Ghali","date":"2025-04-22","type":"Sharing","token":"h","ctx":"Choice Time","desc":"Divided up the game pieces fairly so everyone could join"},{"id":1750000000297,"name":"Amir","date":"2025-04-22","type":"Sharing","token":"a","ctx":"Choice Time","desc":"Shared the Lego blocks with a friend who needed more pieces"},{"id":1750000000356,"name":"Oscar","date":"2025-04-22","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Gave a hug to a friend who was feeling down"},{"id":1750000000381,"name":"Dylan","date":"2025-04-22","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Helped stack chairs after an activity without being told"},{"id":1750000000413,"name":"Mehdi","date":"2025-04-22","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Put away the blocks after Outside Play even though they were not all theirs"},{"id":1650000084000,"name":"Anais","date":"2025-04-21","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Checked on a friend who was sitting alone and looked unhappy"},{"id":1650000198023,"name":"Lilly","date":"2025-04-21","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Gave a hug to a friend who was feeling down"},{"id":1650000198064,"name":"Indigo","date":"2025-04-21","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Made room in the group for a friend standing on the side"},{"id":1750000000017,"name":"Maya","date":"2025-04-21","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Welcomed a friend back warmly after they had been absent"},{"id":1750000000047,"name":"Juna","date":"2025-04-21","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Cleaned up the game pieces after Choice Time without being asked"},{"id":1750000000130,"name":"Ozzie","date":"2025-04-21","type":"Including someone left out","token":"a","ctx":"Specials","desc":"Walked over to a friend sitting alone and started a conversation"},{"id":1750000000296,"name":"Amir","date":"2025-04-21","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Gave a compliment about a friend's new shoes"},{"id":1750000000355,"name":"Oscar","date":"2025-04-21","type":"Sharing","token":"h","ctx":"Learning Center","desc":"Shared the board game pieces so everyone could play"},{"id":1750000000412,"name":"Mehdi","date":"2025-04-21","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Told a friend it was going to be okay when they were worried"},{"id":1650000083000,"name":"Anais","date":"2025-04-18","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Welcomed the teacher back after they were absent saying we missed you"},{"id":1650000197000,"name":"Dylan","date":"2025-04-18","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Put away the blocks after Outside Play even though they were not all theirs"},{"id":1650000053000,"name":"Sophia","date":"2025-04-17","type":"Sharing","token":"h","ctx":"Choice Time","desc":"Let two friends join their card game during Choice Time"},{"id":1650000066000,"name":"Lilly","date":"2025-04-17","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Said your hair looks so nice today to a friend"},{"id":1650000110000,"name":"Amir","date":"2025-04-17","type":"Comforting a friend","token":"h","ctx":"Choice Time","desc":"Told a friend it was okay when they made a mistake"},{"id":1650000172000,"name":"Dario","date":"2025-04-17","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Sat next to a friend who was crying outside and stayed with them"},{"id":1650000151000,"name":"Ozzie","date":"2025-04-16","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Said to the teacher you look so beautiful today"},{"id":1650000137000,"name":"Ghali","date":"2025-04-15","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Picked up toys left on the floor during Choice Time clean-up"},{"id":1650000015000,"name":"Maya","date":"2025-04-14","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Went up to a friend playing alone outside and said come play with us"},{"id":1650000052000,"name":"Sophia","date":"2025-04-14","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Said I love your earrings to a friend"},{"id":1650000150000,"name":"Ozzie","date":"2025-04-14","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Brought a tissue to a friend who was upset outside"},{"id":1650000034000,"name":"Juna","date":"2025-04-11","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Waved a friend over to join the group outside"},{"id":1650000136000,"name":"Ghali","date":"2025-04-11","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Put their arm around a friend who was feeling sad"},{"id":1650000196000,"name":"Dylan","date":"2025-04-11","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Told a friend it was okay when they made a mistake"},{"id":1650000198051,"name":"Zahed","date":"2025-04-11","type":"Sharing","token":"h","ctx":"Learning Center","desc":"Shared the board game pieces so everyone could play"},{"id":1650000198107,"name":"Oscar","date":"2025-04-11","type":"Including someone left out","token":"h","ctx":"Specials","desc":"Made room in the group for a friend standing on the side"},{"id":1750000000075,"name":"Anais","date":"2025-04-11","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Made room in the group for a friend who was standing on the side"},{"id":1750000000101,"name":"Lilly","date":"2025-04-11","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Told a friend it was going to be okay when they were worried"},{"id":1750000000129,"name":"Ozzie","date":"2025-04-11","type":"Including someone left out","token":"h","ctx":"Learning Center","desc":"Walked over to a friend sitting alone and started a conversation"},{"id":1750000000295,"name":"Amir","date":"2025-04-11","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Made sure no one was left out during the game"},{"id":1650000033000,"name":"Juna","date":"2025-04-10","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Tidied the art materials after Learning Center activity"},{"id":1650000135000,"name":"Ghali","date":"2025-04-10","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Picked up toys left on the floor during Choice Time clean-up"},{"id":1650000149000,"name":"Ozzie","date":"2025-04-10","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Checked on a friend and offered kind words of support"},{"id":1650000198083,"name":"Teny","date":"2025-04-10","type":"Including someone left out","token":"h","ctx":"Choice Time","desc":"Invited a friend who was sitting alone to join the game"},{"id":1650000198144,"name":"Amir","date":"2025-04-10","type":"Sharing","token":"a","ctx":"Choice Time","desc":"Let a friend join their card game during Choice Time"},{"id":1650000198149,"name":"Dario","date":"2025-04-10","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Cleaned up the board game after everyone had left the table"},{"id":1650000198167,"name":"Mehdi","date":"2025-04-10","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Told a friend their work was really good"},{"id":1750000000016,"name":"Maya","date":"2025-04-10","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Complimented a friend on their drawing"},{"id":1750000000074,"name":"Anais","date":"2025-04-10","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Checked on a friend who looked unhappy and stayed with them"},{"id":1750000000157,"name":"Zahed","date":"2025-04-10","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Picked up toys left on the floor during clean-up"},{"id":1750000000242,"name":"Sophia","date":"2025-04-10","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Actively encouraged a friend to join the group activity"},{"id":1750000000354,"name":"Oscar","date":"2025-04-10","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Waved a friend over to join the group outside"},{"id":1750000000380,"name":"Dylan","date":"2025-04-10","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Complimented a friend on their drawing"},{"id":1650000198096,"name":"Ghali","date":"2025-04-09","type":"Sharing","token":"a","ctx":"Outside Play","desc":"Offered their snack to a friend who had forgotten theirs"},{"id":1650000198109,"name":"Oscar","date":"2025-04-09","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Went up to a friend who looked left out and included them"},{"id":1650000198127,"name":"Dylan","date":"2025-04-09","type":"Including someone left out","token":"h","ctx":"Choice Time","desc":"Went up to a friend who looked left out and included them"},{"id":1750000000015,"name":"Maya","date":"2025-04-09","type":"Sharing","token":"a","ctx":"Learning Center","desc":"Gave a friend some of their materials to finish their project"},{"id":1750000000073,"name":"Anais","date":"2025-04-09","type":"Including someone left out","token":"h","ctx":"Choice Time","desc":"Invited a new friend to sit with them at the table"},{"id":1750000000128,"name":"Ozzie","date":"2025-04-09","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Noticed a friend was sad and asked if they were alright"},{"id":1750000000217,"name":"Teny","date":"2025-04-09","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Welcomed a friend back warmly after they had been absent"},{"id":1750000000327,"name":"Dario","date":"2025-04-09","type":"Sharing","token":"h","ctx":"Outside Play","desc":"Divided up the game pieces fairly so everyone could join"},{"id":1750000000411,"name":"Mehdi","date":"2025-04-09","type":"Including someone left out","token":"a","ctx":"Specials","desc":"Noticed a friend sitting alone and invited them to join"},{"id":1650000109000,"name":"Amir","date":"2025-04-08","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Put away the puzzle pieces a friend had left on the table"},{"id":1650000122000,"name":"Zahed","date":"2025-04-08","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Put away the blocks after Outside Play even though they were not all theirs"},{"id":1650000198000,"name":"Maya","date":"2025-04-08","type":"Comforting a friend","token":"h","ctx":"Choice Time","desc":"Noticed a friend was sad and asked if they were alright"},{"id":1650000198081,"name":"Teny","date":"2025-04-08","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Gave a warm greeting to a friend arriving at school"},{"id":1650000198134,"name":"Dylan","date":"2025-04-08","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Said thank you to the teacher for helping them"},{"id":1750000000046,"name":"Juna","date":"2025-04-08","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Went up to a friend playing alone and said come play with us"},{"id":1750000000072,"name":"Anais","date":"2025-04-08","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Said thank you to the teacher for helping them"},{"id":1750000000187,"name":"Indigo","date":"2025-04-08","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Brought a tissue to a friend who was upset"},{"id":1750000000326,"name":"Dario","date":"2025-04-08","type":"Sharing","token":"h","ctx":"Outside Play","desc":"Divided up the game pieces fairly so everyone could join"},{"id":1750000000353,"name":"Oscar","date":"2025-04-08","type":"Including someone left out","token":"h","ctx":"Learning Center","desc":"Made sure every friend had a spot in the circle"},{"id":1750000000410,"name":"Mehdi","date":"2025-04-08","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Told a friend their outfit looked wonderful"},{"id":1650000198042,"name":"Ozzie","date":"2025-04-07","type":"Sharing","token":"a","ctx":"Outside Play","desc":"Offered their snack to a friend who had forgotten theirs"},{"id":1650000198045,"name":"Zahed","date":"2025-04-07","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Picked up items from the floor without being asked"},{"id":1650000198125,"name":"Dylan","date":"2025-04-07","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Brought a tissue to a friend who was crying"},{"id":1750000000014,"name":"Maya","date":"2025-04-07","type":"Cleaning up for others","token":"a","ctx":"Outside Play","desc":"Put away the blocks after Outside Play even though they were not all theirs"},{"id":1750000000071,"name":"Anais","date":"2025-04-07","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Comforted a friend after they fell and was crying"},{"id":1750000000100,"name":"Lilly","date":"2025-04-07","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Gave a hug to a friend who was feeling down"},{"id":1750000000216,"name":"Teny","date":"2025-04-07","type":"Sharing","token":"a","ctx":"Specials","desc":"Let a friend use their art supplies when they ran out"},{"id":1750000000325,"name":"Dario","date":"2025-04-07","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Gave a compliment about a friend's new shoes"},{"id":1750000000352,"name":"Oscar","date":"2025-04-07","type":"Sharing","token":"a","ctx":"Learning Center","desc":"Gave a friend some of their blocks to finish their tower"},{"id":1750000000409,"name":"Mehdi","date":"2025-04-07","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Sat quietly beside a friend who was having a hard morning"},{"id":1650000014000,"name":"Maya","date":"2025-04-04","type":"Including someone left out","token":"h","ctx":"Specials","desc":"Actively encouraged a friend to join the group activity"},{"id":1650000082000,"name":"Anais","date":"2025-04-04","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Helped stack all the chairs after an activity without being told"},{"id":1650000121000,"name":"Zahed","date":"2025-04-04","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Made room in the group for a friend who was standing on the side"},{"id":1650000134000,"name":"Ghali","date":"2025-04-04","type":"Sharing","token":"h","ctx":"Outside Play","desc":"Shared the building blocks equally so all friends had some"},{"id":1650000013000,"name":"Maya","date":"2025-04-03","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Stayed beside a friend who missed their parent at drop-off"},{"id":1650000133000,"name":"Ghali","date":"2025-04-03","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Stacked the books back on the shelf after Learning Center"},{"id":1650000148000,"name":"Ozzie","date":"2025-04-03","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Told a friend their outfit was so cool"},{"id":1650000190000,"name":"Oscar","date":"2025-04-03","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Helped clean up during the group activity"},{"id":1650000012000,"name":"Maya","date":"2025-04-02","type":"Including someone left out","token":"h","ctx":"Specials","desc":"Actively encouraged a friend to join the group activity"},{"id":1650000171000,"name":"Dario","date":"2025-04-02","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Gave a warm compliment to a friend"},{"id":1650000032000,"name":"Juna","date":"2025-04-01","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Gave a hug to a friend who fell in the playground"},{"id":1650000065000,"name":"Lilly","date":"2025-04-01","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Cheered on and stayed close to a friend who was feeling upset"},{"id":1650000081000,"name":"Anais","date":"2025-04-01","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Said to the teacher you look so beautiful today"},{"id":1650000108000,"name":"Amir","date":"2025-04-01","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Noticed a friend sitting by themselves and invited them to join the game"},{"id":1650000182000,"name":"Indigo","date":"2025-04-01","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Helped tidy up the area after the activity without being asked"},{"id":1650000189000,"name":"Oscar","date":"2025-04-01","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Cleaned up the board game after everyone had left the table"},{"id":1650000198078,"name":"Teny","date":"2025-04-01","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Put away puzzle pieces a friend had left behind"},{"id":1650000198128,"name":"Dylan","date":"2025-04-01","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Cleaned up the board game after everyone had left the table"},{"id":1650000107000,"name":"Amir","date":"2025-03-31","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Said kind and encouraging words to a friend"},{"id":1650000165000,"name":"Mehdi","date":"2025-03-31","type":"Cleaning up for others","token":"h","ctx":"Outside Play","desc":"Tidied up the space after the session without being asked"},{"id":1650000181000,"name":"Indigo","date":"2025-03-31","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Sat next to a friend who was crying outside and stayed with them"},{"id":1650000198013,"name":"Anais","date":"2025-03-31","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Helped stack chairs after an activity without being told"},{"id":1650000198027,"name":"Lilly","date":"2025-03-31","type":"Cleaning up for others","token":"a","ctx":"Outside Play","desc":"Tidied up blocks that were left on the floor during clean-up"},{"id":1650000198076,"name":"Teny","date":"2025-03-31","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Said we missed you when a friend returned after being away"},{"id":1650000198116,"name":"Oscar","date":"2025-03-31","type":"Sharing","token":"a","ctx":"Choice Time","desc":"Shared the board game pieces so everyone could play"},{"id":1650000198152,"name":"Dario","date":"2025-03-31","type":"Sharing","token":"a","ctx":"Specials","desc":"Let two friends join their activity during Choice Time"},{"id":1650000051000,"name":"Sophia","date":"2025-03-28","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Helped clean up after the group activity"},{"id":1650000080000,"name":"Anais","date":"2025-03-28","type":"Sharing","token":"h","ctx":"Outside Play","desc":"Let a friend join their game of catch during Outside Play"},{"id":1650000198049,"name":"Zahed","date":"2025-03-28","type":"Including someone left out","token":"a","ctx":"Specials","desc":"Asked a friend with no partner to be their partner"},{"id":1650000198080,"name":"Teny","date":"2025-03-28","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Helped put away materials left on the table after the activity"},{"id":1650000198115,"name":"Oscar","date":"2025-03-28","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Cleaned up the board game after everyone had left the table"},{"id":1750000000013,"name":"Maya","date":"2025-03-28","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1750000000045,"name":"Juna","date":"2025-03-28","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Picked up toys left on the floor during clean-up"},{"id":1750000000127,"name":"Ozzie","date":"2025-03-28","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Gave a warm greeting to a friend arriving at school"},{"id":1750000000186,"name":"Indigo","date":"2025-03-28","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Noticed a friend sitting alone and invited them to join"},{"id":1750000000275,"name":"Ghali","date":"2025-03-28","type":"Sharing","token":"a","ctx":"Outside Play","desc":"Gave a friend some of their blocks to finish their tower"},{"id":1750000000408,"name":"Mehdi","date":"2025-03-28","type":"Including someone left out","token":"h","ctx":"Choice Time","desc":"Asked a friend with no partner to be their partner"},{"id":1650000011000,"name":"Maya","date":"2025-03-27","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Went to a friend who was alone and started playing with them"},{"id":1650000031000,"name":"Juna","date":"2025-03-27","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Encouraged and comforted a friend who needed support"},{"id":1650000120000,"name":"Zahed","date":"2025-03-27","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Said to the teacher you look so beautiful today"},{"id":1650000132000,"name":"Ghali","date":"2025-03-27","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Stayed with a friend who needed support and comfort"},{"id":1650000147000,"name":"Ozzie","date":"2025-03-27","type":"Sharing","token":"h","ctx":"Outside Play","desc":"Shared the board game pieces so everyone could play during Choice Time"},{"id":1650000180000,"name":"Indigo","date":"2025-03-27","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Put away the puzzle pieces a friend had left on the table"},{"id":1650000198020,"name":"Anais","date":"2025-03-27","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Gave a warm greeting to a friend arriving at school"},{"id":1650000198153,"name":"Dario","date":"2025-03-27","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Helped clean up the art area after the group activity"},{"id":1750000000099,"name":"Lilly","date":"2025-03-27","type":"Including someone left out","token":"h","ctx":"Specials","desc":"Noticed a friend sitting alone and invited them to join"},{"id":1750000000351,"name":"Oscar","date":"2025-03-27","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Noticed a friend sitting alone and invited them to join"},{"id":1750000000379,"name":"Dylan","date":"2025-03-27","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Gave a compliment about a friend's new shoes"},{"id":1650000106000,"name":"Amir","date":"2025-03-26","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Went to a friend who was alone and started playing with them"},{"id":1650000146000,"name":"Ozzie","date":"2025-03-26","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Told a friend it was okay when they made a mistake"},{"id":1650000198002,"name":"Maya","date":"2025-03-26","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Picked up items from the floor without being asked"},{"id":1650000198016,"name":"Anais","date":"2025-03-26","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1650000198088,"name":"Sophia","date":"2025-03-26","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Sat beside a friend who was upset and offered kind words"},{"id":1650000198165,"name":"Mehdi","date":"2025-03-26","type":"Sharing","token":"a","ctx":"Choice Time","desc":"Offered their snack to a friend who had forgotten theirs"},{"id":1750000000044,"name":"Juna","date":"2025-03-26","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Said kind and encouraging words to a friend who was trying hard"},{"id":1750000000098,"name":"Lilly","date":"2025-03-26","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Helped stack chairs after an activity without being told"},{"id":1750000000156,"name":"Zahed","date":"2025-03-26","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Put away puzzle pieces a friend had left behind"},{"id":1750000000185,"name":"Indigo","date":"2025-03-26","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Gave a compliment about a friend's new shoes"},{"id":1750000000215,"name":"Teny","date":"2025-03-26","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Gave a compliment about a friend's new shoes"},{"id":1750000000274,"name":"Ghali","date":"2025-03-26","type":"Including someone left out","token":"a","ctx":"Specials","desc":"Invited a new friend to sit with them at the table"},{"id":1650000198001,"name":"Maya","date":"2025-03-25","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Invited a friend who was sitting alone to join the game"},{"id":1650000198015,"name":"Anais","date":"2025-03-25","type":"Sharing","token":"h","ctx":"Outside Play","desc":"Let two friends join their activity during Choice Time"},{"id":1650000198039,"name":"Ozzie","date":"2025-03-25","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Cleaned up the board game after everyone had left the table"},{"id":1650000198072,"name":"Teny","date":"2025-03-25","type":"Cleaning up for others","token":"h","ctx":"Outside Play","desc":"Cleaned up the board game after everyone had left the table"},{"id":1650000198098,"name":"Ghali","date":"2025-03-25","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Gave a compliment about a friend's drawing"},{"id":1650000198140,"name":"Amir","date":"2025-03-25","type":"Sharing","token":"a","ctx":"Learning Center","desc":"Let two friends join their activity during Choice Time"},{"id":1650000198154,"name":"Dario","date":"2025-03-25","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Told a friend their outfit looked wonderful"},{"id":1650000198173,"name":"Mehdi","date":"2025-03-25","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Checked on a friend who looked unhappy and stayed with them"},{"id":1750000000043,"name":"Juna","date":"2025-03-25","type":"Including someone left out","token":"h","ctx":"Specials","desc":"Noticed a friend sitting alone and invited them to join"},{"id":1750000000097,"name":"Lilly","date":"2025-03-25","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Gave a compliment about a friend's new shoes"},{"id":1750000000155,"name":"Zahed","date":"2025-03-25","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Sat quietly beside a friend who was having a hard morning"},{"id":1750000000184,"name":"Indigo","date":"2025-03-25","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1750000000241,"name":"Sophia","date":"2025-03-25","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Stayed beside a friend who missed their parent at drop-off"},{"id":1750000000350,"name":"Oscar","date":"2025-03-25","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Made sure no one was left out during the game"},{"id":1750000000378,"name":"Dylan","date":"2025-03-25","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Brought a tissue to a friend who was upset"},{"id":1650000198011,"name":"Juna","date":"2025-03-24","type":"Sharing","token":"a","ctx":"Learning Center","desc":"Gave a friend some of their materials to finish their project"},{"id":1650000198093,"name":"Ghali","date":"2025-03-24","type":"Sharing","token":"a","ctx":"Learning Center","desc":"Let a friend join their card game during Choice Time"},{"id":1650000198122,"name":"Dylan","date":"2025-03-24","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Made sure every friend had a spot in the circle"},{"id":1650000198146,"name":"Amir","date":"2025-03-24","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Stayed with a friend who was missing their parent at drop-off"},{"id":1650000198157,"name":"Dario","date":"2025-03-24","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Told a friend their work was really good"},{"id":1750000000012,"name":"Maya","date":"2025-03-24","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Welcomed a friend back warmly after they had been absent"},{"id":1750000000070,"name":"Anais","date":"2025-03-24","type":"Comforting a friend","token":"h","ctx":"Choice Time","desc":"Brought a tissue to a friend who was upset"},{"id":1750000000096,"name":"Lilly","date":"2025-03-24","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Checked on a friend who looked unhappy and stayed with them"},{"id":1750000000126,"name":"Ozzie","date":"2025-03-24","type":"Sharing","token":"a","ctx":"Outside Play","desc":"Shared the board game pieces so everyone could play"},{"id":1750000000154,"name":"Zahed","date":"2025-03-24","type":"Including someone left out","token":"a","ctx":"Specials","desc":"Made sure every friend had a spot in the circle"},{"id":1750000000214,"name":"Teny","date":"2025-03-24","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Said your hair looks so nice today to a friend"},{"id":1750000000240,"name":"Sophia","date":"2025-03-24","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Said something kind to a friend who looked nervous"},{"id":1750000000407,"name":"Mehdi","date":"2025-03-24","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Tidied the art materials after Learning Center"},{"id":1650000030000,"name":"Juna","date":"2025-03-21","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Complimented a friend on their new shoes"},{"id":1650000079000,"name":"Anais","date":"2025-03-21","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Said your hair looks so nice today to a friend"},{"id":1650000092000,"name":"Teny","date":"2025-03-21","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Checked on a friend who was sitting alone and looked unhappy"},{"id":1650000198004,"name":"Maya","date":"2025-03-21","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Told a friend their outfit looked wonderful"},{"id":1650000198047,"name":"Zahed","date":"2025-03-21","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Stacked books back on the shelf after Learning Center"},{"id":1650000198066,"name":"Indigo","date":"2025-03-21","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Said thank you to the teacher for helping them"},{"id":1650000198104,"name":"Oscar","date":"2025-03-21","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Stacked books back on the shelf after Learning Center"},{"id":1650000198139,"name":"Dylan","date":"2025-03-21","type":"Sharing","token":"a","ctx":"Outside Play","desc":"Let a friend join their card game during Choice Time"},{"id":1750000000095,"name":"Lilly","date":"2025-03-21","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Put away the blocks after Outside Play even though they were not all theirs"},{"id":1750000000125,"name":"Ozzie","date":"2025-03-21","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Gave a hug to a friend who was feeling down"},{"id":1750000000239,"name":"Sophia","date":"2025-03-21","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Went up to a friend playing alone and said come play with us"},{"id":1750000000294,"name":"Amir","date":"2025-03-21","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Helped put away materials left on the table after the activity"},{"id":1750000000324,"name":"Dario","date":"2025-03-21","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Made sure no one was left out during the game"},{"id":1750000000406,"name":"Mehdi","date":"2025-03-21","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Said we missed you when a friend returned after being away"},{"id":1650000029000,"name":"Juna","date":"2025-03-20","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Made sure a friend who was left out had a spot in the circle"},{"id":1650000198024,"name":"Lilly","date":"2025-03-20","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Sat beside a friend who was upset and offered kind words"},{"id":1650000198053,"name":"Zahed","date":"2025-03-20","type":"Cleaning up for others","token":"h","ctx":"Outside Play","desc":"Put away puzzle pieces a friend had left behind"},{"id":1650000198085,"name":"Teny","date":"2025-03-20","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Went up to a friend who looked left out and included them"},{"id":1750000000011,"name":"Maya","date":"2025-03-20","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Comforted a friend after they fell and was crying"},{"id":1750000000069,"name":"Anais","date":"2025-03-20","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Said kind and encouraging words to a friend who was trying hard"},{"id":1750000000183,"name":"Indigo","date":"2025-03-20","type":"Including someone left out","token":"h","ctx":"Choice Time","desc":"Made sure every friend had a spot in the circle"},{"id":1750000000238,"name":"Sophia","date":"2025-03-20","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Helped stack chairs after an activity without being told"},{"id":1750000000273,"name":"Ghali","date":"2025-03-20","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Stacked books back on the shelf after Learning Center"},{"id":1750000000323,"name":"Dario","date":"2025-03-20","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Said thank you to the teacher for helping them"},{"id":1750000000405,"name":"Mehdi","date":"2025-03-20","type":"Including someone left out","token":"h","ctx":"Learning Center","desc":"Noticed a friend sitting alone and invited them to join"},{"id":1650000050000,"name":"Sophia","date":"2025-03-19","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Stayed beside a friend who missed their parent at drop-off"},{"id":1650000064000,"name":"Lilly","date":"2025-03-19","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Checked on a friend who was sitting alone and looked unhappy"},{"id":1650000078000,"name":"Anais","date":"2025-03-19","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Asked a friend who had no partner to be their partner"},{"id":1650000091000,"name":"Teny","date":"2025-03-19","type":"Sharing","token":"h","ctx":"Outside Play","desc":"Gave a friend some of their blocks to finish their tower"},{"id":1650000198172,"name":"Mehdi","date":"2025-03-19","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Invited a friend who was sitting alone to join the game"},{"id":1750000000010,"name":"Maya","date":"2025-03-19","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Welcomed a friend back warmly after they had been absent"},{"id":1750000000153,"name":"Zahed","date":"2025-03-19","type":"Including someone left out","token":"h","ctx":"Choice Time","desc":"Noticed a friend sitting alone and invited them to join"},{"id":1750000000182,"name":"Indigo","date":"2025-03-19","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Sat quietly beside a friend who was having a hard morning"},{"id":1750000000272,"name":"Ghali","date":"2025-03-19","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Walked over to a friend sitting alone and started a conversation"},{"id":1750000000322,"name":"Dario","date":"2025-03-19","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Helped tidy up the area after the activity without being asked"},{"id":1650000049000,"name":"Sophia","date":"2025-03-18","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Helped clean up after the group activity"},{"id":1650000164000,"name":"Mehdi","date":"2025-03-18","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Cleaned up the game pieces after Choice Time without being asked"},{"id":1650000170000,"name":"Dario","date":"2025-03-18","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Picked up toys left on the floor during Choice Time clean-up"},{"id":1650000198143,"name":"Amir","date":"2025-03-18","type":"Cleaning up for others","token":"h","ctx":"Outside Play","desc":"Cleaned up the board game after everyone had left the table"},{"id":1750000000009,"name":"Maya","date":"2025-03-18","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Told a friend their outfit looked wonderful"},{"id":1750000000042,"name":"Juna","date":"2025-03-18","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1750000000068,"name":"Anais","date":"2025-03-18","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Tidied the art materials after Learning Center"},{"id":1750000000124,"name":"Ozzie","date":"2025-03-18","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Stayed with a friend who needed comfort and support"},{"id":1750000000152,"name":"Zahed","date":"2025-03-18","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Cleaned up the board game after everyone had left the table"},{"id":1750000000213,"name":"Teny","date":"2025-03-18","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Stacked books back on the shelf after Learning Center"},{"id":1750000000271,"name":"Ghali","date":"2025-03-18","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Told a friend it was going to be okay when they were worried"},{"id":1650000028000,"name":"Juna","date":"2025-03-17","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Checked on a friend who was sitting alone and looked unhappy"},{"id":1650000169000,"name":"Dario","date":"2025-03-17","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Told a friend it was okay when they made a mistake"},{"id":1650000188000,"name":"Oscar","date":"2025-03-17","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Stayed beside a friend who missed their parent at drop-off"},{"id":1650000198054,"name":"Zahed","date":"2025-03-17","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Sat beside a friend who was upset and offered kind words"},{"id":1650000198168,"name":"Mehdi","date":"2025-03-17","type":"Including someone left out","token":"a","ctx":"Specials","desc":"Made sure every friend had a spot in the circle"},{"id":1750000000008,"name":"Maya","date":"2025-03-17","type":"Including someone left out","token":"h","ctx":"Choice Time","desc":"Made sure every friend had a spot in the circle"},{"id":1750000000067,"name":"Anais","date":"2025-03-17","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Welcomed a friend back warmly after they had been absent"},{"id":1750000000181,"name":"Indigo","date":"2025-03-17","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Sat quietly beside a friend who was having a hard morning"},{"id":1750000000212,"name":"Teny","date":"2025-03-17","type":"Including someone left out","token":"h","ctx":"Specials","desc":"Actively encouraged a friend to join the group activity"},{"id":1750000000237,"name":"Sophia","date":"2025-03-17","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Complimented a friend on their drawing"},{"id":1750000000270,"name":"Ghali","date":"2025-03-17","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Sat next to a friend who was upset and offered kind words"},{"id":1750000000293,"name":"Amir","date":"2025-03-17","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Said we missed you when a friend returned after being away"},{"id":1650000063000,"name":"Lilly","date":"2025-03-14","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Noticed a friend sitting by themselves and invited them to join the game"},{"id":1650000119000,"name":"Zahed","date":"2025-03-14","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Made room in the group for a friend who was standing on the side"},{"id":1650000195000,"name":"Dylan","date":"2025-03-14","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Made room in the group for a friend who was standing on the side"},{"id":1650000198120,"name":"Oscar","date":"2025-03-14","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Noticed a friend was sad and asked if they were alright"},{"id":1750000000041,"name":"Juna","date":"2025-03-14","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Made sure no one was left out during the game"},{"id":1750000000180,"name":"Indigo","date":"2025-03-14","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Helped put away materials left on the table after the activity"},{"id":1750000000211,"name":"Teny","date":"2025-03-14","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Told a friend their outfit looked wonderful"},{"id":1750000000236,"name":"Sophia","date":"2025-03-14","type":"Comforting a friend","token":"h","ctx":"Choice Time","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1750000000292,"name":"Amir","date":"2025-03-14","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Sat next to a friend who was upset and offered kind words"},{"id":1750000000321,"name":"Dario","date":"2025-03-14","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Helped stack chairs after an activity without being told"},{"id":1750000000404,"name":"Mehdi","date":"2025-03-14","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Picked up toys left on the floor during clean-up"},{"id":1650000010000,"name":"Maya","date":"2025-03-13","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Helped stack all the chairs after an activity without being told"},{"id":1650000062000,"name":"Lilly","date":"2025-03-13","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Complimented a friend on their new shoes"},{"id":1650000077000,"name":"Anais","date":"2025-03-13","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Told a friend it was okay when they made a mistake"},{"id":1650000163000,"name":"Mehdi","date":"2025-03-13","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Tidied up the space after the session without being asked"},{"id":1650000198056,"name":"Indigo","date":"2025-03-13","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Told a friend their work was really good"},{"id":1650000198094,"name":"Ghali","date":"2025-03-13","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Tidied up blocks that were left on the floor during clean-up"},{"id":1650000198106,"name":"Oscar","date":"2025-03-13","type":"Including someone left out","token":"h","ctx":"Choice Time","desc":"Made room in the group for a friend standing on the side"},{"id":1650000198138,"name":"Dylan","date":"2025-03-13","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Picked up items from the floor without being asked"},{"id":1650000198160,"name":"Dario","date":"2025-03-13","type":"Cleaning up for others","token":"h","ctx":"Outside Play","desc":"Tidied up blocks that were left on the floor during clean-up"},{"id":1750000000123,"name":"Ozzie","date":"2025-03-13","type":"Comforting a friend","token":"h","ctx":"Choice Time","desc":"Stayed beside a friend who missed their parent at drop-off"},{"id":1750000000151,"name":"Zahed","date":"2025-03-13","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Welcomed a friend back warmly after they had been absent"},{"id":1750000000235,"name":"Sophia","date":"2025-03-13","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Checked on a friend who looked unhappy and stayed with them"},{"id":1750000000291,"name":"Amir","date":"2025-03-13","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Picked up items from the floor without being asked"},{"id":1650000009000,"name":"Maya","date":"2025-03-12","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Waved a friend over to join the group outside"},{"id":1650000076000,"name":"Anais","date":"2025-03-12","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Welcomed the teacher back after they were absent saying we missed you"},{"id":1650000105000,"name":"Amir","date":"2025-03-12","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Said kind and encouraging words to a friend"},{"id":1650000145000,"name":"Ozzie","date":"2025-03-12","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Waved a friend over to join the group outside"},{"id":1650000179000,"name":"Indigo","date":"2025-03-12","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Helped tidy up the area after the activity without being asked"},{"id":1650000198090,"name":"Sophia","date":"2025-03-12","type":"Cleaning up for others","token":"a","ctx":"Outside Play","desc":"Helped put away materials left on the table after the activity"},{"id":1650000198158,"name":"Dario","date":"2025-03-12","type":"Sharing","token":"a","ctx":"Learning Center","desc":"Gave a friend some of their materials to finish their project"},{"id":1750000000040,"name":"Juna","date":"2025-03-12","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Stacked books back on the shelf after Learning Center"},{"id":1750000000150,"name":"Zahed","date":"2025-03-12","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Brought a tissue to a friend who was upset"},{"id":1750000000269,"name":"Ghali","date":"2025-03-12","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Told a friend they did a great job during the activity"},{"id":1750000000349,"name":"Oscar","date":"2025-03-12","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Tidied up blocks that were left on the floor during clean-up"},{"id":1750000000377,"name":"Dylan","date":"2025-03-12","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Said something kind to a friend who looked nervous"},{"id":1650000008000,"name":"Maya","date":"2025-03-11","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Stayed beside a friend who missed their parent at drop-off"},{"id":1650000048000,"name":"Sophia","date":"2025-03-11","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Went up to a friend playing alone outside and said come play with us"},{"id":1650000198048,"name":"Zahed","date":"2025-03-11","type":"Cleaning up for others","token":"a","ctx":"Outside Play","desc":"Helped put away materials left on the table after the activity"},{"id":1650000198077,"name":"Teny","date":"2025-03-11","type":"Including someone left out","token":"a","ctx":"Specials","desc":"Asked a friend with no partner to be their partner"},{"id":1650000198162,"name":"Dario","date":"2025-03-11","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Said kind words to a friend who looked nervous"},{"id":1750000000094,"name":"Lilly","date":"2025-03-11","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Said thank you to the teacher for helping them"},{"id":1750000000122,"name":"Ozzie","date":"2025-03-11","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Told a friend their work was really good"},{"id":1750000000179,"name":"Indigo","date":"2025-03-11","type":"Sharing","token":"h","ctx":"Outside Play","desc":"Shared building blocks equally so all friends had some"},{"id":1750000000268,"name":"Ghali","date":"2025-03-11","type":"Sharing","token":"h","ctx":"Choice Time","desc":"Let a friend join their card game during Choice Time"},{"id":1750000000290,"name":"Amir","date":"2025-03-11","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Said kind and encouraging words to a friend who was trying hard"},{"id":1750000000348,"name":"Oscar","date":"2025-03-11","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Helped put away materials left on the table after the activity"},{"id":1750000000376,"name":"Dylan","date":"2025-03-11","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Told a friend it was going to be okay when they were worried"},{"id":1650000027000,"name":"Juna","date":"2025-03-10","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Cleaned up the board game after everyone had left the table"},{"id":1650000118000,"name":"Zahed","date":"2025-03-10","type":"Sharing","token":"a","ctx":"Choice Time","desc":"Shared the Lego blocks with a friend during Outside Play"},{"id":1650000194000,"name":"Dylan","date":"2025-03-10","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Helped put things away after the activity"},{"id":1650000198063,"name":"Indigo","date":"2025-03-10","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Said kind words to a friend who looked nervous"},{"id":1650000198174,"name":"Mehdi","date":"2025-03-10","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Picked up items from the floor without being asked"},{"id":1750000000007,"name":"Maya","date":"2025-03-10","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Said your hair looks so nice today to a friend"},{"id":1750000000093,"name":"Lilly","date":"2025-03-10","type":"Sharing","token":"h","ctx":"Specials","desc":"Divided up the game pieces fairly so everyone could join"},{"id":1750000000210,"name":"Teny","date":"2025-03-10","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Told a friend they did a great job during the activity"},{"id":1750000000234,"name":"Sophia","date":"2025-03-10","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Sat quietly beside a friend who was having a hard morning"},{"id":1750000000267,"name":"Ghali","date":"2025-03-10","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Said your hair looks so nice today to a friend"},{"id":1750000000289,"name":"Amir","date":"2025-03-10","type":"Sharing","token":"a","ctx":"Outside Play","desc":"Let a friend join their card game during Choice Time"},{"id":1750000000320,"name":"Dario","date":"2025-03-10","type":"Sharing","token":"h","ctx":"Outside Play","desc":"Let two friends join their activity during Choice Time"},{"id":1750000000347,"name":"Oscar","date":"2025-03-10","type":"Including someone left out","token":"h","ctx":"Choice Time","desc":"Waved a friend over to join the group outside"},{"id":1650000007000,"name":"Maya","date":"2025-03-07","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Put away the blocks after Outside Play even though they were not all theirs"},{"id":1650000026000,"name":"Juna","date":"2025-03-07","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Gave a hug to a friend who fell in the playground"},{"id":1650000131000,"name":"Ghali","date":"2025-03-07","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Said your hair looks so nice today to a friend"},{"id":1650000198084,"name":"Teny","date":"2025-03-07","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Gave a hug to a friend who was feeling down"},{"id":1650000198151,"name":"Dario","date":"2025-03-07","type":"Including someone left out","token":"h","ctx":"Learning Center","desc":"Made room in the group for a friend standing on the side"},{"id":1750000000178,"name":"Indigo","date":"2025-03-07","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Told a friend their work was really good"},{"id":1750000000233,"name":"Sophia","date":"2025-03-07","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Picked up toys left on the floor during clean-up"},{"id":1750000000288,"name":"Amir","date":"2025-03-07","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Told a friend their outfit looked wonderful"},{"id":1750000000346,"name":"Oscar","date":"2025-03-07","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Sat next to a friend who was upset and offered kind words"},{"id":1750000000375,"name":"Dylan","date":"2025-03-07","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Gave a hug to a friend who was feeling down"},{"id":1750000000403,"name":"Mehdi","date":"2025-03-07","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Checked on a friend who looked unhappy and stayed with them"},{"id":1650000006000,"name":"Maya","date":"2025-03-06","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Waved a friend over to join the group outside"},{"id":1650000162000,"name":"Mehdi","date":"2025-03-06","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Helped stack all the chairs after an activity without being told"},{"id":1650000198008,"name":"Juna","date":"2025-03-06","type":"Sharing","token":"a","ctx":"Choice Time","desc":"Shared Lego blocks with a friend who needed more pieces"},{"id":1650000198028,"name":"Lilly","date":"2025-03-06","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Gave a hug to a friend who was feeling down"},{"id":1650000198071,"name":"Indigo","date":"2025-03-06","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Said kind words to a friend who looked nervous"},{"id":1650000198075,"name":"Teny","date":"2025-03-06","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Helped stack chairs after an activity without being told"},{"id":1650000198091,"name":"Sophia","date":"2025-03-06","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1650000198100,"name":"Ghali","date":"2025-03-06","type":"Cleaning up for others","token":"h","ctx":"Outside Play","desc":"Helped put away materials left on the table after the activity"},{"id":1650000198121,"name":"Dylan","date":"2025-03-06","type":"Including someone left out","token":"h","ctx":"Learning Center","desc":"Noticed a friend was alone outside and went to play with them"},{"id":1650000198156,"name":"Dario","date":"2025-03-06","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Helped stack chairs after an activity without being told"},{"id":1750000000121,"name":"Ozzie","date":"2025-03-06","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Said thank you to the teacher for helping them"},{"id":1750000000149,"name":"Zahed","date":"2025-03-06","type":"Sharing","token":"h","ctx":"Specials","desc":"Gave a friend some of their blocks to finish their tower"},{"id":1750000000287,"name":"Amir","date":"2025-03-06","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Put away puzzle pieces a friend had left behind"},{"id":1750000000345,"name":"Oscar","date":"2025-03-06","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Stayed with a friend who needed comfort and support"},{"id":1650000061000,"name":"Lilly","date":"2025-03-05","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Cheered on and stayed close to a friend who was feeling upset"},{"id":1650000168000,"name":"Dario","date":"2025-03-05","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Complimented a friend on their new shoes"},{"id":1650000178000,"name":"Indigo","date":"2025-03-05","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Cleaned up the game pieces after Choice Time without being asked"},{"id":1750000000120,"name":"Ozzie","date":"2025-03-05","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Told a friend they did a great job during the activity"},{"id":1750000000148,"name":"Zahed","date":"2025-03-05","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Tidied up blocks that were left on the floor during clean-up"},{"id":1750000000209,"name":"Teny","date":"2025-03-05","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Said thank you to the teacher for helping them"},{"id":1750000000232,"name":"Sophia","date":"2025-03-05","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Actively encouraged a friend to join the group activity"},{"id":1750000000266,"name":"Ghali","date":"2025-03-05","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Told a friend their work was really good"},{"id":1750000000402,"name":"Mehdi","date":"2025-03-05","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Cleaned up the board game after everyone had left the table"},{"id":1650000025000,"name":"Juna","date":"2025-03-04","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Said I love your earrings to a friend"},{"id":1650000060000,"name":"Lilly","date":"2025-03-04","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Welcomed the teacher back after they were absent saying we missed you"},{"id":1650000090000,"name":"Teny","date":"2025-03-04","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Went up to a friend playing alone outside and said come play with us"},{"id":1650000198095,"name":"Ghali","date":"2025-03-04","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Helped clean up the art area after the group activity"},{"id":1650000198130,"name":"Dylan","date":"2025-03-04","type":"Sharing","token":"a","ctx":"Choice Time","desc":"Offered their snack to a friend who had forgotten theirs"},{"id":1750000000066,"name":"Anais","date":"2025-03-04","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Cleaned up the board game after everyone had left the table"},{"id":1750000000119,"name":"Ozzie","date":"2025-03-04","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1750000000231,"name":"Sophia","date":"2025-03-04","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Gave a compliment about a friend's new shoes"},{"id":1750000000286,"name":"Amir","date":"2025-03-04","type":"Including someone left out","token":"h","ctx":"Specials","desc":"Made sure no one was left out during the game"},{"id":1750000000319,"name":"Dario","date":"2025-03-04","type":"Including someone left out","token":"a","ctx":"Specials","desc":"Made room in the group for a friend who was standing on the side"},{"id":1750000000344,"name":"Oscar","date":"2025-03-04","type":"Sharing","token":"a","ctx":"Outside Play","desc":"Let two friends join their activity during Choice Time"},{"id":1750000000401,"name":"Mehdi","date":"2025-03-04","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1650000005000,"name":"Maya","date":"2025-03-03","type":"Comforting a friend","token":"h","ctx":"Choice Time","desc":"Gave a hug to a friend who fell in the playground"},{"id":1650000047000,"name":"Sophia","date":"2025-03-03","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Told a friend who was back after being sick we are so happy you are here"},{"id":1650000075000,"name":"Anais","date":"2025-03-03","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Comforted a friend who was feeling down during the activity"},{"id":1650000198055,"name":"Zahed","date":"2025-03-03","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Told a friend their outfit looked wonderful"},{"id":1750000000118,"name":"Ozzie","date":"2025-03-03","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Walked over to a friend sitting alone and started a conversation"},{"id":1750000000177,"name":"Indigo","date":"2025-03-03","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Told a friend it was going to be okay when they were worried"},{"id":1750000000208,"name":"Teny","date":"2025-03-03","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Tidied up blocks that were left on the floor during clean-up"},{"id":1750000000265,"name":"Ghali","date":"2025-03-03","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Helped stack chairs after an activity without being told"},{"id":1750000000318,"name":"Dario","date":"2025-03-03","type":"Cleaning up for others","token":"h","ctx":"Outside Play","desc":"Cleaned up the game pieces after Choice Time without being asked"},{"id":1750000000343,"name":"Oscar","date":"2025-03-03","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Stayed beside a friend who missed their parent at drop-off"},{"id":1750000000400,"name":"Mehdi","date":"2025-03-03","type":"Sharing","token":"a","ctx":"Specials","desc":"Shared building blocks equally so all friends had some"},{"id":1650000104000,"name":"Amir","date":"2025-02-28","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Stayed beside a friend who missed their parent at drop-off"},{"id":1650000117000,"name":"Zahed","date":"2025-02-28","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Stayed beside a friend who needed encouragement"},{"id":1750000000006,"name":"Maya","date":"2025-02-28","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Went up to a friend playing alone and said come play with us"},{"id":1750000000039,"name":"Juna","date":"2025-02-28","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Noticed a friend was sad and asked if they were alright"},{"id":1750000000065,"name":"Anais","date":"2025-02-28","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Stacked books back on the shelf after Learning Center"},{"id":1750000000092,"name":"Lilly","date":"2025-02-28","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Said we missed you when a friend returned after being away"},{"id":1750000000207,"name":"Teny","date":"2025-02-28","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Noticed a friend was sad and asked if they were alright"},{"id":1750000000230,"name":"Sophia","date":"2025-02-28","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Comforted a friend after they fell and was crying"},{"id":1750000000264,"name":"Ghali","date":"2025-02-28","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Actively encouraged a friend to join the group activity"},{"id":1750000000342,"name":"Oscar","date":"2025-02-28","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Made sure no one was left out during the game"},{"id":1750000000374,"name":"Dylan","date":"2025-02-28","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Made sure no one was left out during the game"},{"id":1650000046000,"name":"Sophia","date":"2025-02-27","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Helped clean up after the group activity"},{"id":1650000187000,"name":"Oscar","date":"2025-02-27","type":"Cleaning up for others","token":"a","ctx":"Outside Play","desc":"Helped clean up during the group activity"},{"id":1650000198007,"name":"Juna","date":"2025-02-27","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Checked on a friend who looked unhappy and stayed with them"},{"id":1650000198019,"name":"Anais","date":"2025-02-27","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Said thank you to the teacher for helping them"},{"id":1650000198036,"name":"Ozzie","date":"2025-02-27","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Made room in the group for a friend standing on the side"},{"id":1750000000005,"name":"Maya","date":"2025-02-27","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Sat quietly beside a friend who was having a hard morning"},{"id":1750000000147,"name":"Zahed","date":"2025-02-27","type":"Cleaning up for others","token":"h","ctx":"Outside Play","desc":"Picked up items from the floor without being asked"},{"id":1750000000176,"name":"Indigo","date":"2025-02-27","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Walked over to a friend sitting alone and started a conversation"},{"id":1750000000263,"name":"Ghali","date":"2025-02-27","type":"Including someone left out","token":"h","ctx":"Learning Center","desc":"Asked a friend with no partner to be their partner"},{"id":1750000000285,"name":"Amir","date":"2025-02-27","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Stayed beside a friend who missed their parent at drop-off"},{"id":1750000000317,"name":"Dario","date":"2025-02-27","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Told a friend their feelings were valid and stayed close"},{"id":1750000000373,"name":"Dylan","date":"2025-02-27","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Cleaned up the game pieces after Choice Time without being asked"},{"id":1750000000399,"name":"Mehdi","date":"2025-02-27","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1650000004000,"name":"Maya","date":"2025-02-26","type":"Including someone left out","token":"h","ctx":"Choice Time","desc":"Went up to a friend playing alone outside and said come play with us"},{"id":1650000045000,"name":"Sophia","date":"2025-02-26","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Sat next to a friend who was crying outside and stayed with them"},{"id":1650000198014,"name":"Anais","date":"2025-02-26","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Told a friend their outfit looked wonderful"},{"id":1650000198129,"name":"Dylan","date":"2025-02-26","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Waved a friend over to join their activity"},{"id":1750000000038,"name":"Juna","date":"2025-02-26","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Said we missed you when a friend returned after being away"},{"id":1750000000091,"name":"Lilly","date":"2025-02-26","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Checked on a friend who looked unhappy and stayed with them"},{"id":1750000000117,"name":"Ozzie","date":"2025-02-26","type":"Including someone left out","token":"h","ctx":"Specials","desc":"Walked over to a friend sitting alone and started a conversation"},{"id":1750000000146,"name":"Zahed","date":"2025-02-26","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Told a friend their work was really good"},{"id":1750000000175,"name":"Indigo","date":"2025-02-26","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Told a friend their work was really good"},{"id":1750000000206,"name":"Teny","date":"2025-02-26","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1750000000262,"name":"Ghali","date":"2025-02-26","type":"Including someone left out","token":"a","ctx":"Specials","desc":"Made room in the group for a friend who was standing on the side"},{"id":1750000000284,"name":"Amir","date":"2025-02-26","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1750000000316,"name":"Dario","date":"2025-02-26","type":"Sharing","token":"h","ctx":"Choice Time","desc":"Let a friend join their card game during Choice Time"},{"id":1750000000341,"name":"Oscar","date":"2025-02-26","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Gave a warm greeting to a friend arriving at school"},{"id":1750000000398,"name":"Mehdi","date":"2025-02-26","type":"Cleaning up for others","token":"a","ctx":"Outside Play","desc":"Helped tidy up the area after the activity without being asked"},{"id":1650000059000,"name":"Lilly","date":"2025-02-25","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Cheered on and stayed close to a friend who was feeling upset"},{"id":1650000074000,"name":"Anais","date":"2025-02-25","type":"Sharing","token":"h","ctx":"Choice Time","desc":"Shared the Lego blocks with a friend during Outside Play"},{"id":1650000103000,"name":"Amir","date":"2025-02-25","type":"Sharing","token":"a","ctx":"Choice Time","desc":"Shared the Lego blocks with a friend during Outside Play"},{"id":1650000198003,"name":"Maya","date":"2025-02-25","type":"Sharing","token":"h","ctx":"Learning Center","desc":"Shared Lego blocks with a friend who needed more pieces"},{"id":1650000198033,"name":"Ozzie","date":"2025-02-25","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Noticed a friend was sad and asked if they were alright"},{"id":1650000198113,"name":"Oscar","date":"2025-02-25","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Told a friend it was going to be okay when they were worried"},{"id":1650000198124,"name":"Dylan","date":"2025-02-25","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Said thank you to the teacher for helping them"},{"id":1750000000037,"name":"Juna","date":"2025-02-25","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Cleaned up the board game after everyone had left the table"},{"id":1750000000145,"name":"Zahed","date":"2025-02-25","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Said your hair looks so nice today to a friend"},{"id":1750000000174,"name":"Indigo","date":"2025-02-25","type":"Sharing","token":"h","ctx":"Specials","desc":"Gave a friend some of their materials to finish their project"},{"id":1750000000205,"name":"Teny","date":"2025-02-25","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Made room in the group for a friend who was standing on the side"},{"id":1750000000261,"name":"Ghali","date":"2025-02-25","type":"Cleaning up for others","token":"a","ctx":"Outside Play","desc":"Picked up items from the floor without being asked"},{"id":1750000000315,"name":"Dario","date":"2025-02-25","type":"Sharing","token":"a","ctx":"Outside Play","desc":"Let two friends join their activity during Choice Time"},{"id":1750000000397,"name":"Mehdi","date":"2025-02-25","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Gave a compliment about a friend's new shoes"},{"id":1750000000004,"name":"Maya","date":"2025-02-24","type":"Sharing","token":"h","ctx":"Specials","desc":"Shared the board game pieces so everyone could play"},{"id":1750000000036,"name":"Juna","date":"2025-02-24","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Stayed with a friend who needed comfort and support"},{"id":1750000000090,"name":"Lilly","date":"2025-02-24","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Checked on a friend who looked unhappy and stayed with them"},{"id":1750000000116,"name":"Ozzie","date":"2025-02-24","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Said we missed you when a friend returned after being away"},{"id":1750000000173,"name":"Indigo","date":"2025-02-24","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Checked on a friend who looked unhappy and stayed with them"},{"id":1750000000204,"name":"Teny","date":"2025-02-24","type":"Including someone left out","token":"h","ctx":"Choice Time","desc":"Waved a friend over to join the group outside"},{"id":1750000000260,"name":"Ghali","date":"2025-02-24","type":"Comforting a friend","token":"h","ctx":"Choice Time","desc":"Sat quietly beside a friend who was having a hard morning"},{"id":1750000000372,"name":"Dylan","date":"2025-02-24","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Tidied up blocks that were left on the floor during clean-up"},{"id":1750000000396,"name":"Mehdi","date":"2025-02-24","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Welcomed a friend back warmly after they had been absent"},{"id":1650000102000,"name":"Amir","date":"2025-02-21","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Said kind and encouraging words to a friend"},{"id":1650000116000,"name":"Zahed","date":"2025-02-21","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Sat next to a friend who was crying outside and stayed with them"},{"id":1650000161000,"name":"Mehdi","date":"2025-02-21","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Went to a friend who was alone and started playing with them"},{"id":1650000198010,"name":"Juna","date":"2025-02-21","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Helped put away materials left on the table after the activity"},{"id":1650000198040,"name":"Ozzie","date":"2025-02-21","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Said thank you to the teacher for helping them"},{"id":1650000198073,"name":"Teny","date":"2025-02-21","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Made sure every friend had a spot in the circle"},{"id":1650000198097,"name":"Ghali","date":"2025-02-21","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Helped stack chairs after an activity without being told"},{"id":1650000198137,"name":"Dylan","date":"2025-02-21","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Told a friend it was going to be okay when they were worried"},{"id":1650000198155,"name":"Dario","date":"2025-02-21","type":"Cleaning up for others","token":"a","ctx":"Outside Play","desc":"Helped stack chairs after an activity without being told"},{"id":1750000000003,"name":"Maya","date":"2025-02-21","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Told a friend their outfit looked wonderful"},{"id":1750000000064,"name":"Anais","date":"2025-02-21","type":"Cleaning up for others","token":"h","ctx":"Outside Play","desc":"Stacked books back on the shelf after Learning Center"},{"id":1750000000229,"name":"Sophia","date":"2025-02-21","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Cleaned up the game pieces after Choice Time without being asked"},{"id":1650000044000,"name":"Sophia","date":"2025-02-20","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Picked up toys left on the floor during Choice Time clean-up"},{"id":1650000198029,"name":"Lilly","date":"2025-02-20","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Tidied up blocks that were left on the floor during clean-up"},{"id":1750000000002,"name":"Maya","date":"2025-02-20","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Brought a tissue to a friend who was upset"},{"id":1750000000035,"name":"Juna","date":"2025-02-20","type":"Sharing","token":"a","ctx":"Learning Center","desc":"Let a friend join their card game during Choice Time"},{"id":1750000000063,"name":"Anais","date":"2025-02-20","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Told a friend their feelings were valid and stayed close"},{"id":1750000000203,"name":"Teny","date":"2025-02-20","type":"Including someone left out","token":"h","ctx":"Choice Time","desc":"Invited a new friend to sit with them at the table"},{"id":1750000000283,"name":"Amir","date":"2025-02-20","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Brought a tissue to a friend who was upset"},{"id":1750000000314,"name":"Dario","date":"2025-02-20","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Told a friend their work was really good"},{"id":1750000000371,"name":"Dylan","date":"2025-02-20","type":"Sharing","token":"a","ctx":"Specials","desc":"Shared the Lego blocks with a friend who needed more pieces"},{"id":1650000101000,"name":"Amir","date":"2025-02-19","type":"Including someone left out","token":"h","ctx":"Learning Center","desc":"Made room in the group for a friend who was standing on the side"},{"id":1650000160000,"name":"Mehdi","date":"2025-02-19","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Complimented a friend on their new shoes"},{"id":1650000186000,"name":"Oscar","date":"2025-02-19","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Told a friend it was okay when they made a mistake"},{"id":1650000198009,"name":"Juna","date":"2025-02-19","type":"Sharing","token":"a","ctx":"Choice Time","desc":"Shared the board game pieces so everyone could play"},{"id":1650000198030,"name":"Lilly","date":"2025-02-19","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Complimented a friend on their new shoes"},{"id":1750000000062,"name":"Anais","date":"2025-02-19","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Put away the blocks after Outside Play even though they were not all theirs"},{"id":1750000000172,"name":"Indigo","date":"2025-02-19","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Said your hair looks so nice today to a friend"},{"id":1750000000202,"name":"Teny","date":"2025-02-19","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Went up to a friend playing alone and said come play with us"},{"id":1750000000228,"name":"Sophia","date":"2025-02-19","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Waved a friend over to join the group outside"},{"id":1750000000259,"name":"Ghali","date":"2025-02-19","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Picked up items from the floor without being asked"},{"id":1650000003000,"name":"Maya","date":"2025-02-18","type":"Including someone left out","token":"a","ctx":"Specials","desc":"Actively encouraged a friend to join the group activity"},{"id":1650000024000,"name":"Juna","date":"2025-02-18","type":"Sharing","token":"a","ctx":"Outside Play","desc":"Gave a friend some of their blocks to finish their tower"},{"id":1650000185000,"name":"Oscar","date":"2025-02-18","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Waved a friend over to join the group outside"},{"id":1650000198052,"name":"Zahed","date":"2025-02-18","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Picked up items from the floor without being asked"},{"id":1650000198132,"name":"Dylan","date":"2025-02-18","type":"Sharing","token":"a","ctx":"Outside Play","desc":"Gave a friend some of their materials to finish their project"},{"id":1750000000089,"name":"Lilly","date":"2025-02-18","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Said kind and encouraging words to a friend who was trying hard"},{"id":1750000000115,"name":"Ozzie","date":"2025-02-18","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Tidied up blocks that were left on the floor during clean-up"},{"id":1750000000201,"name":"Teny","date":"2025-02-18","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Stayed with a friend who needed comfort and support"},{"id":1750000000227,"name":"Sophia","date":"2025-02-18","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Cleaned up the board game after everyone had left the table"},{"id":1750000000258,"name":"Ghali","date":"2025-02-18","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Stayed beside a friend who missed their parent at drop-off"},{"id":1750000000395,"name":"Mehdi","date":"2025-02-18","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Said your hair looks so nice today to a friend"},{"id":1650000089000,"name":"Teny","date":"2025-02-17","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Brought a tissue to a friend who was upset outside"},{"id":1650000100000,"name":"Amir","date":"2025-02-17","type":"Sharing","token":"a","ctx":"Outside Play","desc":"Shared the board game pieces so everyone could play during Choice Time"},{"id":1650000198041,"name":"Ozzie","date":"2025-02-17","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Checked on a friend who looked unhappy and stayed with them"},{"id":1650000198108,"name":"Oscar","date":"2025-02-17","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Told a friend their outfit looked wonderful"},{"id":1650000198123,"name":"Dylan","date":"2025-02-17","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Sat beside a friend who was upset and offered kind words"},{"id":1750000000034,"name":"Juna","date":"2025-02-17","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Gave a warm greeting to a friend arriving at school"},{"id":1750000000088,"name":"Lilly","date":"2025-02-17","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Went up to a friend playing alone and said come play with us"},{"id":1750000000144,"name":"Zahed","date":"2025-02-17","type":"Including someone left out","token":"a","ctx":"Specials","desc":"Waved a friend over to join the group outside"},{"id":1750000000171,"name":"Indigo","date":"2025-02-17","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Helped stack chairs after an activity without being told"},{"id":1750000000257,"name":"Ghali","date":"2025-02-17","type":"Sharing","token":"h","ctx":"Choice Time","desc":"Divided up the game pieces fairly so everyone could join"},{"id":1750000000313,"name":"Dario","date":"2025-02-17","type":"Sharing","token":"h","ctx":"Outside Play","desc":"Let a friend join their card game during Choice Time"},{"id":1650000043000,"name":"Sophia","date":"2025-02-14","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Gave a hug to a friend who fell in the playground"},{"id":1650000193000,"name":"Dylan","date":"2025-02-14","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Told a friend their outfit was so cool"},{"id":1650000198119,"name":"Oscar","date":"2025-02-14","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Told a friend their outfit looked wonderful"},{"id":1750000000033,"name":"Juna","date":"2025-02-14","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1750000000087,"name":"Lilly","date":"2025-02-14","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Made sure every friend had a spot in the circle"},{"id":1750000000170,"name":"Indigo","date":"2025-02-14","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Put away puzzle pieces a friend had left behind"},{"id":1750000000256,"name":"Ghali","date":"2025-02-14","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Tidied the art materials after Learning Center"},{"id":1750000000282,"name":"Amir","date":"2025-02-14","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Told a friend their work was really good"},{"id":1750000000312,"name":"Dario","date":"2025-02-14","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Tidied up blocks that were left on the floor during clean-up"},{"id":1650000002000,"name":"Maya","date":"2025-02-13","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Cleaned up the board game after everyone had left the table"},{"id":1650000042000,"name":"Sophia","date":"2025-02-13","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Complimented a friend on their new shoes"},{"id":1650000159000,"name":"Mehdi","date":"2025-02-13","type":"Comforting a friend","token":"a","ctx":"Outside Play","desc":"Gave a hug to a friend who fell in the playground"},{"id":1650000177000,"name":"Indigo","date":"2025-02-13","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Asked a friend who had no partner to be their partner"},{"id":1650000198037,"name":"Ozzie","date":"2025-02-13","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Went up to a friend who looked left out and included them"},{"id":1650000198135,"name":"Dylan","date":"2025-02-13","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Noticed a friend was sad and asked if they were alright"},{"id":1650000198148,"name":"Dario","date":"2025-02-13","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Sat beside a friend who was upset and offered kind words"},{"id":1750000000032,"name":"Juna","date":"2025-02-13","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Told a friend their feelings were valid and stayed close"},{"id":1750000000086,"name":"Lilly","date":"2025-02-13","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Picked up items from the floor without being asked"},{"id":1750000000143,"name":"Zahed","date":"2025-02-13","type":"Comforting a friend","token":"h","ctx":"Choice Time","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1750000000200,"name":"Teny","date":"2025-02-13","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Went up to a friend playing alone and said come play with us"},{"id":1650000001000,"name":"Maya","date":"2025-02-12","type":"Including someone left out","token":"h","ctx":"Outside Play","desc":"Noticed a friend sitting by themselves and invited them to join the game"},{"id":1650000130000,"name":"Ghali","date":"2025-02-12","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Waved a friend over to join the group outside"},{"id":1650000158000,"name":"Mehdi","date":"2025-02-12","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Complimented a friend on their new shoes"},{"id":1650000198006,"name":"Juna","date":"2025-02-12","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Noticed a friend was sad and asked if they were alright"},{"id":1650000198018,"name":"Anais","date":"2025-02-12","type":"Cleaning up for others","token":"a","ctx":"Outside Play","desc":"Put away puzzle pieces a friend had left behind"},{"id":1650000198025,"name":"Lilly","date":"2025-02-12","type":"Comforting a friend","token":"h","ctx":"Choice Time","desc":"Noticed a friend was sad and asked if they were alright"},{"id":1750000000114,"name":"Ozzie","date":"2025-02-12","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Brought a tissue to a friend who was upset"},{"id":1750000000142,"name":"Zahed","date":"2025-02-12","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Actively encouraged a friend to join the group activity"},{"id":1750000000199,"name":"Teny","date":"2025-02-12","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1750000000226,"name":"Sophia","date":"2025-02-12","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Told a friend their feelings were valid and stayed close"},{"id":1750000000281,"name":"Amir","date":"2025-02-12","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Said we missed you when a friend returned after being away"},{"id":1750000000311,"name":"Dario","date":"2025-02-12","type":"Sharing","token":"a","ctx":"Choice Time","desc":"Let a friend join their card game during Choice Time"},{"id":1750000000340,"name":"Oscar","date":"2025-02-12","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Welcomed a friend back warmly after they had been absent"},{"id":1750000000370,"name":"Dylan","date":"2025-02-12","type":"Sharing","token":"a","ctx":"Outside Play","desc":"Gave a friend some of their materials to finish their project"},{"id":1650000041000,"name":"Sophia","date":"2025-02-11","type":"Sharing","token":"a","ctx":"Outside Play","desc":"Shared the board game pieces so everyone could play during Choice Time"},{"id":1650000115000,"name":"Zahed","date":"2025-02-11","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Stayed beside a friend who needed encouragement"},{"id":1650000167000,"name":"Dario","date":"2025-02-11","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Put away the blocks after Outside Play even though they were not all theirs"},{"id":1650000176000,"name":"Indigo","date":"2025-02-11","type":"Comforting a friend","token":"h","ctx":"Choice Time","desc":"Told a friend it was okay when they made a mistake"},{"id":1650000198166,"name":"Mehdi","date":"2025-02-11","type":"Sharing","token":"h","ctx":"Outside Play","desc":"Shared the board game pieces so everyone could play"},{"id":1750000000031,"name":"Juna","date":"2025-02-11","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Said something kind to a friend who looked nervous"},{"id":1750000000061,"name":"Anais","date":"2025-02-11","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Put away puzzle pieces a friend had left behind"},{"id":1750000000255,"name":"Ghali","date":"2025-02-11","type":"Including someone left out","token":"h","ctx":"Choice Time","desc":"Invited a new friend to sit with them at the table"},{"id":1750000000339,"name":"Oscar","date":"2025-02-11","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Brought a tissue to a friend who was upset"},{"id":1750000000369,"name":"Dylan","date":"2025-02-11","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Complimented a friend on their drawing"},{"id":1650000023000,"name":"Juna","date":"2025-02-10","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Said to the teacher you look so beautiful today"},{"id":1650000073000,"name":"Anais","date":"2025-02-10","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Tidied the art materials after Learning Center activity"},{"id":1650000198035,"name":"Ozzie","date":"2025-02-10","type":"Comforting a friend","token":"h","ctx":"Outside Play","desc":"Sat beside a friend who was upset and offered kind words"},{"id":1650000198070,"name":"Indigo","date":"2025-02-10","type":"Saying kind words","token":"a","ctx":"Choice Time","desc":"Complimented a friend on their new shoes"},{"id":1650000198118,"name":"Oscar","date":"2025-02-10","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Stacked books back on the shelf after Learning Center"},{"id":1750000000001,"name":"Maya","date":"2025-02-10","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Said kind and encouraging words to a friend who was trying hard"},{"id":1750000000085,"name":"Lilly","date":"2025-02-10","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Walked over to a friend sitting alone and started a conversation"},{"id":1750000000198,"name":"Teny","date":"2025-02-10","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Said we missed you when a friend returned after being away"},{"id":1750000000225,"name":"Sophia","date":"2025-02-10","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Said your hair looks so nice today to a friend"},{"id":1750000000254,"name":"Ghali","date":"2025-02-10","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Told a friend their feelings were valid and stayed close"},{"id":1750000000368,"name":"Dylan","date":"2025-02-10","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Brought a tissue to a friend who was upset"},{"id":1650000058000,"name":"Lilly","date":"2025-02-07","type":"Saying kind words","token":"a","ctx":"Specials","desc":"Said to the teacher you look so beautiful today"},{"id":1650000144000,"name":"Ozzie","date":"2025-02-07","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Cleaned up the board game after everyone had left the table"},{"id":1650000157000,"name":"Mehdi","date":"2025-02-07","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Made sure a friend who was left out had a spot in the circle"},{"id":1650000198092,"name":"Sophia","date":"2025-02-07","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Sat beside a friend who was upset and offered kind words"},{"id":1650000198101,"name":"Ghali","date":"2025-02-07","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Helped stack chairs after an activity without being told"},{"id":1650000198110,"name":"Oscar","date":"2025-02-07","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Gave a compliment about a friend's drawing"},{"id":1650000198147,"name":"Amir","date":"2025-02-07","type":"Sharing","token":"a","ctx":"Learning Center","desc":"Let a friend join their card game during Choice Time"},{"id":1750000000000,"name":"Maya","date":"2025-02-07","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Asked a friend with no partner to be their partner"},{"id":1750000000030,"name":"Juna","date":"2025-02-07","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Checked on a friend who looked unhappy and stayed with them"},{"id":1750000000060,"name":"Anais","date":"2025-02-07","type":"Sharing","token":"h","ctx":"Outside Play","desc":"Shared the board game pieces so everyone could play"},{"id":1750000000141,"name":"Zahed","date":"2025-02-07","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Walked over to a friend sitting alone and started a conversation"},{"id":1750000000197,"name":"Teny","date":"2025-02-07","type":"Cleaning up for others","token":"a","ctx":"Learning Center","desc":"Picked up items from the floor without being asked"},{"id":1750000000310,"name":"Dario","date":"2025-02-07","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Stacked books back on the shelf after Learning Center"},{"id":1750000000367,"name":"Dylan","date":"2025-02-07","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Walked over to a friend sitting alone and started a conversation"},{"id":1650000040000,"name":"Sophia","date":"2025-02-06","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Welcomed the teacher back after they were absent saying we missed you"},{"id":1650000057000,"name":"Lilly","date":"2025-02-06","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Cheered on and stayed close to a friend who was feeling upset"},{"id":1650000088000,"name":"Teny","date":"2025-02-06","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Said encouraging and kind words to a friend who was trying hard"},{"id":1650000129000,"name":"Ghali","date":"2025-02-06","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Put away the puzzle pieces a friend had left on the table"},{"id":1650000156000,"name":"Mehdi","date":"2025-02-06","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Welcomed a friend back warmly after they had been absent"},{"id":1650000198032,"name":"Ozzie","date":"2025-02-06","type":"Including someone left out","token":"a","ctx":"Learning Center","desc":"Went up to a friend who looked left out and included them"},{"id":1650000198050,"name":"Zahed","date":"2025-02-06","type":"Sharing","token":"h","ctx":"Choice Time","desc":"Shared the board game pieces so everyone could play"},{"id":1650000198062,"name":"Indigo","date":"2025-02-06","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Invited a friend who was sitting alone to join the game"},{"id":1650000198150,"name":"Dario","date":"2025-02-06","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Put a gentle hand on a friend's shoulder when they were sad"},{"id":1750000000029,"name":"Juna","date":"2025-02-06","type":"Sharing","token":"h","ctx":"Learning Center","desc":"Gave a friend some of their blocks to finish their tower"},{"id":1750000000059,"name":"Anais","date":"2025-02-06","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Made sure no one was left out during the game"},{"id":1750000000366,"name":"Dylan","date":"2025-02-06","type":"Cleaning up for others","token":"h","ctx":"Outside Play","desc":"Helped stack chairs after an activity without being told"},{"id":1650000143000,"name":"Ozzie","date":"2025-02-05","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Checked on a friend and offered kind words of support"},{"id":1650000192000,"name":"Dylan","date":"2025-02-05","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Stacked the books back on the shelf after Learning Center"},{"id":1650000198057,"name":"Indigo","date":"2025-02-05","type":"Cleaning up for others","token":"a","ctx":"Outside Play","desc":"Stacked books back on the shelf after Learning Center"},{"id":1750000000028,"name":"Juna","date":"2025-02-05","type":"Including someone left out","token":"a","ctx":"Outside Play","desc":"Invited a new friend to sit with them at the table"},{"id":1750000000058,"name":"Anais","date":"2025-02-05","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Cleaned up the board game after everyone had left the table"},{"id":1750000000140,"name":"Zahed","date":"2025-02-05","type":"Cleaning up for others","token":"a","ctx":"Choice Time","desc":"Tidied the art materials after Learning Center"},{"id":1750000000224,"name":"Sophia","date":"2025-02-05","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Brought a tissue to a friend who was upset"},{"id":1750000000253,"name":"Ghali","date":"2025-02-05","type":"Cleaning up for others","token":"h","ctx":"Outside Play","desc":"Helped put away materials left on the table after the activity"},{"id":1750000000280,"name":"Amir","date":"2025-02-05","type":"Saying kind words","token":"h","ctx":"Choice Time","desc":"Gave a warm greeting to a friend arriving at school"},{"id":1750000000338,"name":"Oscar","date":"2025-02-05","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Told a friend their outfit looked wonderful"},{"id":1750000000394,"name":"Mehdi","date":"2025-02-05","type":"Sharing","token":"a","ctx":"Learning Center","desc":"Let a friend join their card game during Choice Time"},{"id":1650000000000,"name":"Maya","date":"2025-02-04","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Put away the puzzle pieces a friend had left on the table"},{"id":1650000087000,"name":"Teny","date":"2025-02-04","type":"Saying kind words","token":"a","ctx":"Learning Center","desc":"Complimented a friend on their new shoes"},{"id":1650000099000,"name":"Amir","date":"2025-02-04","type":"Cleaning up for others","token":"h","ctx":"Choice Time","desc":"Cleaned up the board game after everyone had left the table"},{"id":1650000128000,"name":"Ghali","date":"2025-02-04","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Gave a hug to a friend who fell in the playground"},{"id":1650000198005,"name":"Juna","date":"2025-02-04","type":"Sharing","token":"h","ctx":"Outside Play","desc":"Shared the board game pieces so everyone could play"},{"id":1650000198087,"name":"Sophia","date":"2025-02-04","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Brought a tissue to a friend who was crying"},{"id":1750000000057,"name":"Anais","date":"2025-02-04","type":"Comforting a friend","token":"a","ctx":"Learning Center","desc":"Brought a tissue to a friend who was upset"},{"id":1750000000113,"name":"Ozzie","date":"2025-02-04","type":"Comforting a friend","token":"h","ctx":"Specials","desc":"Told a friend it was going to be okay when they were worried"},{"id":1750000000169,"name":"Indigo","date":"2025-02-04","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Brought a tissue to a friend who was upset"},{"id":1750000000309,"name":"Dario","date":"2025-02-04","type":"Saying kind words","token":"a","ctx":"Outside Play","desc":"Complimented a friend on their drawing"},{"id":1750000000337,"name":"Oscar","date":"2025-02-04","type":"Comforting a friend","token":"a","ctx":"Specials","desc":"Brought a tissue to a friend who was upset"},{"id":1750000000365,"name":"Dylan","date":"2025-02-04","type":"Cleaning up for others","token":"a","ctx":"Specials","desc":"Put away the blocks after Outside Play even though they were not all theirs"},{"id":1750000000393,"name":"Mehdi","date":"2025-02-04","type":"Saying kind words","token":"h","ctx":"Learning Center","desc":"Said something kind to a friend who looked nervous"},{"id":1650000022000,"name":"Juna","date":"2025-02-03","type":"Including someone left out","token":"h","ctx":"Learning Center","desc":"Waved a friend over to join the group outside"},{"id":1650000039000,"name":"Sophia","date":"2025-02-03","type":"Comforting a friend","token":"a","ctx":"Choice Time","desc":"Sat next to a friend who was crying outside and stayed with them"},{"id":1650000098000,"name":"Amir","date":"2025-02-03","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Said kind and encouraging words to a friend"},{"id":1750000000056,"name":"Anais","date":"2025-02-03","type":"Saying kind words","token":"h","ctx":"Specials","desc":"Said thank you to the teacher for helping them"},{"id":1750000000084,"name":"Lilly","date":"2025-02-03","type":"Cleaning up for others","token":"a","ctx":"Outside Play","desc":"Helped tidy up the area after the activity without being asked"},{"id":1750000000112,"name":"Ozzie","date":"2025-02-03","type":"Including someone left out","token":"a","ctx":"Choice Time","desc":"Invited a new friend to sit with them at the table"},{"id":1750000000168,"name":"Indigo","date":"2025-02-03","type":"Cleaning up for others","token":"h","ctx":"Specials","desc":"Picked up toys left on the floor during clean-up"},{"id":1750000000196,"name":"Teny","date":"2025-02-03","type":"Sharing","token":"h","ctx":"Choice Time","desc":"Let two friends join their activity during Choice Time"},{"id":1750000000252,"name":"Ghali","date":"2025-02-03","type":"Cleaning up for others","token":"h","ctx":"Learning Center","desc":"Stacked books back on the shelf after Learning Center"},{"id":1750000000308,"name":"Dario","date":"2025-02-03","type":"Sharing","token":"h","ctx":"Learning Center","desc":"Shared building blocks equally so all friends had some"},{"id":1750000000336,"name":"Oscar","date":"2025-02-03","type":"Including someone left out","token":"h","ctx":"Choice Time","desc":"Went up to a friend playing alone and said come play with us"},{"id":1750000000364,"name":"Dylan","date":"2025-02-03","type":"Saying kind words","token":"h","ctx":"Outside Play","desc":"Said kind and encouraging words to a friend who was trying hard"},{"id":1750000000392,"name":"Mehdi","date":"2025-02-03","type":"Comforting a friend","token":"h","ctx":"Learning Center","desc":"Comforted a friend after they fell and was crying"}];

// ── STORAGE ──────────────────────────────────────────────────
function lsGet(k, def) {
  try { var v = localStorage.getItem(k); return v !== null ? JSON.parse(v) : def; } catch(e) { return def; }
}
function lsSet(k, v) {
  try { localStorage.setItem(k, JSON.stringify(v)); } catch(e) {}
}

// ── YEAR MANAGEMENT ──────────────────────────────────────────
function guessYear() {
  var n = new Date(), y = n.getFullYear(), m = n.getMonth();
  return m >= 8 ? (y + '-' + (y+1)) : ((y-1) + '-' + y);
}
function getAllYears() { return lsGet('kt_years', []); }
function ensureYear(yr) {
  var a = getAllYears();
  if (a.indexOf(yr) === -1) { a.unshift(yr); lsSet('kt_years', a); }
}

var activeYear = "2024-2025";
ensureYear(activeYear);

function buildYearSelect() {
  var sel = document.getElementById('yr-sel');
  var years = getAllYears();
  var html = '';
  for (var i = 0; i < years.length; i++) {
    html += '<option value="' + years[i] + '"' + (years[i] === activeYear ? ' selected' : '') + '>' + years[i] + '</option>';
  }
  sel.innerHTML = html;
  document.getElementById('yr-lbl').textContent = activeYear;
}

document.getElementById('yr-sel').addEventListener('change', function() {
  activeYear = this.value;
  lsSet('kt_active_year', activeYear);
  loadYear();
  buildYearSelect();
  renderRoster();
  renderLogChips();
  showToast('Switched to ' + activeYear);
});

function openNewYear() {
  var n = new Date(), y = n.getFullYear();
  document.getElementById('ny-input').value = y + '-' + (y+1);
  document.getElementById('ny-modal').classList.add('open');
}
function createNewYear() {
  var yr = document.getElementById('ny-input').value.trim();
  if (!yr) return;
  if (getAllYears().indexOf(yr) !== -1) { alert('That year already exists — select it from the dropdown.'); return; }
  if (entries.length && confirm('Export current year (' + activeYear + ') data as CSV first?')) doExportCSV();
  ensureYear(yr);
  activeYear = yr;
  lsSet('kt_active_year', yr);
  entries = []; students = []; notes = '';
  saveAll();
  buildYearSelect();
  renderRoster();
  renderLogChips();
  closeModal('ny-modal');
  showToast('New year ' + yr + ' started!');
}
function closeModal(id) { document.getElementById(id).classList.remove('open'); }

// ── DATA ─────────────────────────────────────────────────────
var entries = [], students = [], notes = '';

function loadYear() {
  var yr = activeYear;
  if (yr === "2024-2025") {
    // Always seed from built-in data — ensures latest entries are always loaded
    try {
      var existing = lsGet("kt_entries_" + yr, []);
      if (existing.length < KT_ENTRIES.length) {
        lsSet("kt_students_" + yr, KT_STUDENTS);
        lsSet("kt_entries_"  + yr, KT_ENTRIES);
        lsSet("kt_notes_"    + yr, "Kindness Tree data covers February through May 2025.");
        lsSet("kt_years",        [yr]);
        lsSet("kt_active_year",   yr);
      }
    } catch(e) {
      lsSet("kt_students_" + yr, KT_STUDENTS);
      lsSet("kt_entries_"  + yr, KT_ENTRIES);
    }
  }
  entries  = lsGet("kt_entries_"  + yr, []);
  students = lsGet("kt_students_" + yr, []);
  notes    = lsGet("kt_notes_"    + yr, "");
}
function saveAll() {
  lsSet('kt_entries_' + activeYear, entries);
  lsSet('kt_students_' + activeYear, students);
  lsSet('kt_notes_' + activeYear, notes);
}
loadYear();
buildYearSelect();

document.getElementById('notes-area').addEventListener('input', function() {
  notes = this.value;
  lsSet('kt_notes_' + activeYear, notes);
});

// ── TOAST ────────────────────────────────────────────────────
var toastTimer;
function showToast(msg) {
  var t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  clearTimeout(toastTimer);
  toastTimer = setTimeout(function() { t.classList.remove('show'); }, 2400);
}

// ── TABS ─────────────────────────────────────────────────────
function goTab(name, btn) {
  var secs = document.querySelectorAll('.sec');
  for (var i = 0; i < secs.length; i++) secs[i].classList.remove('on');
  var tabs = document.querySelectorAll('.tab');
  for (var i = 0; i < tabs.length; i++) tabs[i].classList.remove('active');
  document.getElementById('tab-' + name).classList.add('on');
  btn.classList.add('active');
  if (name === 'trees') renderAllTrees();
  if (name === 'stats') renderStats();
  if (name === 'compare') renderCompare();
  if (name === 'reflect') { renderReflect(); document.getElementById('notes-area').value = notes; }
}

// ── HELPERS ──────────────────────────────────────────────────
function esc(s) {
  return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');
}
function fmtDate(d) {
  if (!d) return '';
  var p = d.split('-');
  return p[2] + '/' + p[1] + '/' + p[0];
}
function initials(n) {
  return n.trim().split(' ').map(function(w){return w[0]||'';}).join('').slice(0,2).toUpperCase();
}
function nameColor(n) {
  var cols = ['#2563a8','#c0395a','#e07b2a','#2d6a3f','#7c3aed','#0891b2','#be185d','#b45309'];
  var h = 0;
  for (var i = 0; i < n.length; i++) h = (h * 31 + n.charCodeAt(i)) % cols.length;
  return cols[h];
}
function countBy(arr, field, skipEmpty) {
  var c = {};
  for (var i = 0; i < arr.length; i++) {
    var k = arr[i][field];
    if (skipEmpty && !k) continue;
    c[k] = (c[k] || 0) + 1;
  }
  var out = [];
  for (var k in c) out.push([k, c[k]]);
  out.sort(function(a,b){return b[1]-a[1];});
  return out;
}
function entriesFor(name) {
  return entries.filter(function(e){return e.name === name;});
}

// ── STUDENT MANAGEMENT ───────────────────────────────────────
function addStudent() {
  var val = document.getElementById('rs-input').value.trim();
  if (!val) return;
  var names = val.split(',');
  for (var i = 0; i < names.length; i++) {
    var n = names[i].trim();
    if (n && students.indexOf(n) === -1) students.push(n);
  }
  students.sort(function(a,b){return a.localeCompare(b);});
  document.getElementById('rs-input').value = '';
  saveAll();
  renderRoster();
  renderLogChips();
  showToast('Student added!');
}

function openBulkModal() {
  document.getElementById('bulk-modal').classList.add('open');
}

function confirmBulk() {
  var lines = document.getElementById('bulk-input').value.split('\n');
  var added = 0;
  for (var i = 0; i < lines.length; i++) {
    var n = lines[i].trim();
    if (n && students.indexOf(n) === -1) { students.push(n); added++; }
  }
  students.sort(function(a,b){return a.localeCompare(b);});
  document.getElementById('bulk-input').value = '';
  saveAll();
  renderRoster();
  renderLogChips();
  closeModal('bulk-modal');
  showToast(added + ' students added!');
}

function removeStudent(name) {
  if (!confirm('Remove ' + name + ' from roster? Their logged acts will remain.')) return;
  students = students.filter(function(s){return s !== name;});
  if (selStudent === name) {
    selStudent = null;
    document.getElementById('log-form').style.display = 'none';
  }
  saveAll();
  renderRoster();
  renderLogChips();
  showToast(name + ' removed from roster');
}

function renderRoster() {
  var el = document.getElementById('student-grid');
  document.getElementById('roster-count').textContent = students.length;
  if (!students.length) {
    el.innerHTML = '<div class="empty"><span class="eico">👦</span>No students yet — add names above</div>';
    return;
  }
  var html = '';
  for (var i = 0; i < students.length; i++) {
    var n = students[i];
    var ents = entriesFor(n);
    var h = 0, a = 0;
    for (var j = 0; j < ents.length; j++) { if (ents[j].token === 'h') h++; else a++; }
    var col = nameColor(n);
    var bg = selStudent === n ? '#2d6a3f' : col + '22';
    var fg = selStudent === n ? '#fff' : col;
    var sel = selStudent === n ? ' sel' : '';
    html += '<div class="scard' + sel + '" onclick="selectStudent(\'' + esc(n) + '\')">'
          + '<button class="sdel" onclick="event.stopPropagation();removeStudent(\'' + esc(n) + '\')">✕</button>'
          + '<div class="sini" style="background:' + bg + ';color:' + fg + '">' + initials(n) + '</div>'
          + '<div class="sname">' + esc(n) + '</div>'
          + '<div class="smeta">' + ents.length + ' act' + (ents.length !== 1 ? 's' : '') + '</div>'
          + '<div class="stoks"><span>❤️ ' + h + '</span><span>🍎 ' + a + '</span></div>'
          + '</div>';
  }
  el.innerHTML = html;
}

// ── LOG TAB ──────────────────────────────────────────────────
var selStudent = null;
var selToken = null;

function renderLogChips() {
  var el = document.getElementById('log-chips');
  if (!students.length) {
    el.innerHTML = '<div class="empty" style="padding:.4rem"><span class="eico">👦</span>Add students in the Students tab first</div>';
    return;
  }
  var html = '';
  for (var i = 0; i < students.length; i++) {
    var n = students[i];
    var ents = entriesFor(n);
    var col = nameColor(n);
    var isSel = selStudent === n;
    var bdr = isSel ? '#2d6a3f' : '#e2e8e0';
    var bg = isSel ? '#2d6a3f' : '#fff';
    var fg = isSel ? '#fff' : '#6b7280';
    html += '<div onclick="selectStudent(\'' + esc(n) + '\')" style="padding:7px 14px;border-radius:20px;cursor:pointer;border:2px solid ' + bdr + ';background:' + bg + ';color:' + fg + ';font-weight:700;font-size:13px;display:inline-flex;align-items:center;gap:6px;transition:all .14s">'
          + '<span style="width:20px;height:20px;border-radius:50%;background:' + (isSel ? 'rgba(255,255,255,.25)' : col+'22') + ';color:' + (isSel ? '#fff' : col) + ';display:inline-flex;align-items:center;justify-content:center;font-size:9px;font-weight:900">' + initials(n) + '</span>'
          + esc(n)
          + '<span style="opacity:.6;font-size:11px">' + ents.length + '✓</span>'
          + '</div>';
  }
  el.innerHTML = html;
}

function selectStudent(name) {
  selStudent = name;
  selToken = null;
  document.getElementById('tpk-h').className = 'tpk';
  document.getElementById('tpk-a').className = 'tpk';
  document.getElementById('log-form').style.display = 'block';
  updateBanner();
  renderLogList();
  renderRoster();
  renderLogChips();
}

function updateBanner() {
  if (!selStudent) return;
  var ents = entriesFor(selStudent);
  var h = 0, a = 0;
  for (var i = 0; i < ents.length; i++) { if (ents[i].token === 'h') h++; else a++; }
  document.getElementById('b-ini').textContent = initials(selStudent);
  document.getElementById('b-ini').style.background = nameColor(selStudent) + '55';
  document.getElementById('b-name').textContent = selStudent;
  document.getElementById('b-meta').textContent = ents.length + ' act' + (ents.length !== 1 ? 's' : '') + ' logged';
  document.getElementById('b-toks').textContent = '❤️ ' + h + '  🍎 ' + a;
  document.getElementById('log-sname').textContent = selStudent;
}

function pickToken(t) {
  selToken = t;
  document.getElementById('tpk-h').className = 'tpk' + (t === 'h' ? ' selh' : '');
  document.getElementById('tpk-a').className = 'tpk' + (t === 'a' ? ' sela' : '');
}

function addEntry() {
  if (!selStudent) { alert('Please select a student first.'); return; }
  if (!selToken) { alert('Please choose a token — Heart or Apple.'); return; }
  var type = document.getElementById('f-type').value;
  if (!type) { alert('Please select a type of kindness.'); return; }
  var entry = {
    id: Date.now(),
    name: selStudent,
    date: document.getElementById('f-date').value,
    type: type,
    token: selToken,
    ctx: document.getElementById('f-ctx').value,
    desc: document.getElementById('f-desc').value.trim()
  };
  entries.unshift(entry);
  saveAll();
  document.getElementById('f-type').value = '';
  document.getElementById('f-ctx').value = '';
  document.getElementById('f-desc').value = '';
  updateBanner();
  renderLogList();
  renderRoster();
  renderLogChips();
  var fb = document.getElementById('log-fb');
  fb.textContent = (selToken === 'h' ? '❤️' : '🍎') + ' Added!';
  setTimeout(function(){fb.textContent='';}, 2200);
  showToast((selToken === 'h' ? '❤️' : '🍎') + ' Act logged for ' + selStudent + '!');
}

function deleteEntry(id) {
  if (!confirm('Remove this entry?')) return;
  entries = entries.filter(function(e){return e.id !== id;});
  saveAll();
  renderLogList();
  renderRoster();
  showToast('Entry removed');
}

function renderLogList() {
  var el = document.getElementById('log-list');
  var ents = entriesFor(selStudent);
  document.getElementById('log-cnt').textContent = ents.length ? '(' + ents.length + ' total)' : '';
  if (!ents.length) { el.innerHTML = '<div class="empty"><span class="eico">🌱</span>No acts logged yet</div>'; return; }
  var html = '';
  for (var i = 0; i < ents.length; i++) {
    var e = ents[i];
    var tok = e.token === 'h' ? '❤️' : '🍎';
    html += '<div class="li">'
          + '<div class="lav">' + tok + '</div>'
          + '<div style="flex:1;min-width:0"><div class="ln">' + esc(e.type) + '</div>'
          + '<div class="lt">' + (e.ctx ? esc(e.ctx) : '') + '</div>'
          + (e.desc ? '<div class="ld">' + esc(e.desc.slice(0,80)) + (e.desc.length>80?'…':'') + '</div>' : '')
          + '</div>'
          + '<div style="display:flex;flex-direction:column;align-items:flex-end;gap:4px;margin-left:auto">'
          + '<div class="ldate">' + fmtDate(e.date) + '</div>'
          + '<button class="bd" onclick="deleteEntry(' + e.id + ')">✕</button>'
          + '</div></div>';
  }
  el.innerHTML = html;
}

// ── SVG TREE BUILDER ─────────────────────────────────────────
var SPOTS_BIG = [
  [140,100],[195,82],[168,68],[112,122],[228,72],[158,52],[183,102],
  [252,88],[208,118],[122,88],[238,52],[143,72],[172,122],[102,102],
  [212,62],[188,82],[132,132],[248,108],[162,98],[198,42],[218,98],
  [108,138],[242,128],[152,112],[172,48],[228,132],[138,52],[198,128],
  [118,112],[208,82],[162,132],[238,78],[172,88],[122,68],[252,68]
];
var SPOTS_SM = [
  [100,82],[132,66],[118,54],[82,98],[150,72],[128,50],[142,88],
  [72,82],[110,96],[92,66],[152,56],[106,78],[132,98],[70,98],
  [142,46],[118,82],[80,108],[148,92],[92,54],[132,72],[82,70]
];

function buildTree(ents, spots, w, h) {
  var cx = w / 2, base = h - 15;
  var th = h * 0.52, tw = w * 0.055;
  var svg = '';
  // ground
  svg += '<ellipse cx="' + cx + '" cy="' + base + '" rx="' + (w*0.44) + '" ry="11" fill="#81c784" opacity=".32"/>';
  // trunk
  svg += '<rect x="' + (cx-tw) + '" y="' + (base-th) + '" width="' + (tw*2) + '" height="' + th + '" rx="' + tw + '" fill="#6d4c41"/>';
  // roots
  svg += '<path d="M' + (cx-tw) + ' ' + base + ' Q' + (cx-tw*4) + ' ' + (base+4) + ' ' + (cx-tw*6) + ' ' + base + '" stroke="#5d4037" stroke-width="3" fill="none" stroke-linecap="round"/>';
  svg += '<path d="M' + (cx+tw) + ' ' + base + ' Q' + (cx+tw*4) + ' ' + (base+4) + ' ' + (cx+tw*6) + ' ' + base + '" stroke="#5d4037" stroke-width="3" fill="none" stroke-linecap="round"/>';
  // branches
  var by = base - th;
  var brs = [
    [cx,by,cx-w*.28,by-h*.22,w*.022],
    [cx,by,cx-w*.18,by-h*.3,w*.018],
    [cx,by,cx,by-h*.35,w*.018],
    [cx,by,cx+w*.18,by-h*.3,w*.018],
    [cx,by,cx+w*.28,by-h*.22,w*.022],
    [cx-w*.28,by-h*.22,cx-w*.38,by-h*.33,w*.012],
    [cx+w*.28,by-h*.22,cx+w*.38,by-h*.33,w*.012],
    [cx-w*.18,by-h*.3,cx-w*.24,by-h*.4,w*.010],
    [cx+w*.18,by-h*.3,cx+w*.24,by-h*.4,w*.010],
    [cx,by-h*.35,cx-w*.07,by-h*.45,w*.009],
    [cx,by-h*.35,cx+w*.07,by-h*.45,w*.009]
  ];
  for (var i = 0; i < brs.length; i++) {
    var b = brs[i];
    svg += '<line x1="' + b[0] + '" y1="' + b[1] + '" x2="' + b[2] + '" y2="' + b[3] + '" stroke="#795548" stroke-width="' + b[4] + '" stroke-linecap="round"/>';
  }
  // foliage
  var fr = w * 0.28, fcy = by - fr * 0.52;
  svg += '<ellipse cx="' + cx + '" cy="' + fcy + '" rx="' + (fr*1.3) + '" ry="' + fr + '" fill="#43a85a" opacity=".28"/>';
  svg += '<ellipse cx="' + (cx-fr*.42) + '" cy="' + (fcy+fr*.18) + '" rx="' + (fr*.78) + '" ry="' + (fr*.62) + '" fill="#388e3c" opacity=".38"/>';
  svg += '<ellipse cx="' + (cx+fr*.42) + '" cy="' + (fcy+fr*.18) + '" rx="' + (fr*.78) + '" ry="' + (fr*.62) + '" fill="#388e3c" opacity=".38"/>';
  svg += '<ellipse cx="' + cx + '" cy="' + (fcy-fr*.12) + '" rx="' + (fr*.82) + '" ry="' + (fr*.68) + '" fill="#2e7d32" opacity=".42"/>';
  svg += '<ellipse cx="' + cx + '" cy="' + fcy + '" rx="' + (fr*1.22) + '" ry="' + (fr*.88) + '" fill="#4caf50" opacity=".16"/>';
  // tokens
  var shown = ents.slice(0, spots.length);
  var r = w < 250 ? 8 : 11;
  var fs = w < 250 ? 12 : 16;
  if (!shown.length) {
    svg += '<text x="' + cx + '" y="' + (fcy+6) + '" text-anchor="middle" fill="#2e7d32" font-size="' + (w<250?9:12) + '" font-family="Nunito,sans-serif" font-weight="700" opacity=".8">No acts yet</text>';
  } else {
    for (var i = 0; i < shown.length; i++) {
      var sp = spots[i] || [cx, fcy];
      var tok = shown[i].token === 'h' ? '❤️' : '🍎';
      svg += '<g transform="translate(' + sp[0] + ',' + sp[1] + ')">'
           + '<circle r="' + r + '" fill="rgba(255,255,255,.78)"/>'
           + '<text x="0" y="' + Math.round(r*0.38) + '" text-anchor="middle" font-size="' + fs + '">' + tok + '</text>'
           + '</g>';
    }
    if (ents.length > spots.length) {
      svg += '<text x="' + cx + '" y="' + (base-6) + '" text-anchor="middle" fill="#2d6a3f" font-size="10" font-family="Nunito,sans-serif" font-weight="800">+' + (ents.length-spots.length) + ' more!</text>';
    }
  }
  return svg;
}

// ── ALL TREES TAB ────────────────────────────────────────────
function renderAllTrees() {
  var el = document.getElementById('all-trees');
  if (!students.length) { el.innerHTML = '<div class="empty"><span class="eico">🌳</span>Add students to see their trees</div>'; return; }
  var html = '';
  for (var i = 0; i < students.length; i++) {
    var n = students[i];
    var ents = entriesFor(n);
    var h = 0, a = 0;
    for (var j = 0; j < ents.length; j++) { if (ents[j].token === 'h') h++; else a++; }
    var col = nameColor(n);
    var treeSVG = buildTree(ents, SPOTS_SM, 200, 155);
    html += '<div class="tcard" onclick="openStudentModal(\'' + esc(n) + '\')">'
          + '<div class="tch" style="background:linear-gradient(135deg,' + col + ',' + col + 'bb)">'
          + '<div class="tch-ini">' + initials(n) + '</div>'
          + '<div><div class="tch-name">' + esc(n) + '</div><div class="tch-sub">' + ents.length + ' act' + (ents.length!==1?'s':'') + '</div></div>'
          + '</div>'
          + '<div class="tcstage"><svg viewBox="0 0 200 155" xmlns="http://www.w3.org/2000/svg" style="width:100%;height:155px">' + treeSVG + '</svg></div>'
          + '<div class="tcfoot"><span>❤️ ' + h + '</span><span>🍎 ' + a + '</span><span style="color:var(--gd)">View →</span></div>'
          + '</div>';
  }
  el.innerHTML = html;
}

function openStudentModal(name) {
  var ents = entriesFor(name);
  var h = 0, a = 0;
  for (var i = 0; i < ents.length; i++) { if (ents[i].token === 'h') h++; else a++; }
  document.getElementById('sm-name').textContent = '🌳 ' + name;
  document.getElementById('sm-h').textContent = h;
  document.getElementById('sm-a').textContent = a;
  document.getElementById('sm-tot').textContent = ents.length;
  var svg = document.getElementById('sm-tree');
  svg.innerHTML = buildTree(ents, SPOTS_BIG, 420, 270);
  var logEl = document.getElementById('sm-log');
  if (!ents.length) { logEl.innerHTML = '<div class="empty">No acts yet — log one from the Log act tab!</div>'; }
  else {
    var html = '';
    for (var i = 0; i < ents.length; i++) {
      var e = ents[i];
      var tok = e.token === 'h' ? '❤️' : '🍎';
      html += '<div class="li">'
            + '<div class="lav" style="width:28px;height:28px;font-size:14px">' + tok + '</div>'
            + '<div style="flex:1"><div class="ln">' + esc(e.type) + '</div>'
            + '<div class="lt">' + (e.ctx?esc(e.ctx):'') + (e.desc?' · '+esc(e.desc.slice(0,50)):'') + '</div></div>'
            + '<div class="ldate">' + fmtDate(e.date) + '</div>'
            + '</div>';
    }
    logEl.innerHTML = html;
  }
  document.getElementById('stu-modal').classList.add('open');
}

// ── STATS TAB ────────────────────────────────────────────────
function renderBars(elId, data, color) {
  var el = document.getElementById(elId);
  if (!data.length) { el.innerHTML = '<div class="empty" style="padding:.5rem">No data yet</div>'; return; }
  var max = data[0][1];
  var html = '';
  for (var i = 0; i < data.length; i++) {
    var pct = Math.round(data[i][1] / max * 100);
    html += '<div class="bw">'
          + '<div class="bh"><span>' + esc(data[i][0]) + '</span><span>' + data[i][1] + '</span></div>'
          + '<div class="bt"><div class="bf" style="width:' + pct + '%;background:' + color + '"></div></div>'
          + '</div>';
  }
  el.innerHTML = html;
}

function renderStats() {
  var total = entries.length;
  var hearts = 0, apples = 0;
  for (var i = 0; i < entries.length; i++) { if (entries[i].token === 'h') hearts++; else apples++; }
  document.getElementById('s-tot').textContent = total;
  document.getElementById('s-stu').textContent = students.length;
  document.getElementById('s-h').textContent = hearts;
  document.getElementById('s-a').textContent = apples;

  var byName = {};
  for (var i = 0; i < entries.length; i++) byName[entries[i].name] = (byName[entries[i].name]||0)+1;
  var topStuArr = [];
  for (var k in byName) topStuArr.push([k, byName[k]]);
  topStuArr.sort(function(a,b){return b[1]-a[1];});
  var topStu = topStuArr[0];
  document.getElementById('hs-k').textContent = topStu ? topStu[0] : '—';
  document.getElementById('hs-ks').textContent = topStu ? topStu[1] + ' acts' : 'No data';

  var types = countBy(entries, 'type');
  var topT = types[0], lowT = types.length > 1 ? types[types.length-1] : null;
  document.getElementById('hs-top').textContent = topT ? topT[0] : '—';
  document.getElementById('hs-tops').textContent = topT ? topT[1] + ' times' : '';
  document.getElementById('hs-low').textContent = lowT ? lowT[0] : '—';
  document.getElementById('hs-lows').textContent = lowT ? lowT[1] + ' times — encourage more!' : '';

  var ctxs = countBy(entries, 'ctx', true);
  var topC = ctxs[0];
  document.getElementById('hs-ctx').textContent = topC ? topC[0] : '—';
  document.getElementById('hs-ctxs').textContent = topC ? topC[1] + ' acts here' : 'No context logged';

  renderBars('type-bars', types, '#4a9b61');
  renderBars('ctx-bars', ctxs, '#2563a8');

  // student table
  var rows = [];
  for (var i = 0; i < students.length; i++) {
    var n = students[i];
    var ents = entriesFor(n);
    var h = 0, a = 0, st = {};
    for (var j = 0; j < ents.length; j++) {
      if (ents[j].token === 'h') h++; else a++;
      st[ents[j].type] = (st[ents[j].type]||0)+1;
    }
    var topArr = [];
    for (var k in st) topArr.push([k,st[k]]);
    topArr.sort(function(a,b){return b[1]-a[1];});
    rows.push({n:n,total:ents.length,h:h,a:a,top:topArr[0]?topArr[0][0]:'—'});
  }
  rows.sort(function(a,b){return b.total-a.total;});

  var stblEl = document.getElementById('stbl-wrap');
  if (!rows.length) { stblEl.innerHTML = '<div class="empty">No students yet</div>'; }
  else {
    var th = '<thead><tr><th></th><th>Name</th><th>Acts</th><th>❤️</th><th>🍎</th><th>Most common</th></tr></thead><tbody>';
    var tbody = '';
    for (var i = 0; i < rows.length; i++) {
      var r = rows[i];
      var col = nameColor(r.n);
      tbody += '<tr>'
             + '<td>' + (i===0&&r.total>0?'👑':'') + '<div class="ini" style="background:' + col + '22;color:' + col + '">' + initials(r.n) + '</div></td>'
             + '<td style="font-weight:700">' + esc(r.n) + '</td>'
             + '<td style="font-weight:800;color:var(--gd)">' + r.total + '</td>'
             + '<td>' + r.h + '</td><td>' + r.a + '</td>'
             + '<td style="font-size:12px;color:var(--txm)">' + esc(r.top) + '</td>'
             + '</tr>';
    }
    stblEl.innerHTML = '<div style="overflow-x:auto"><table class="stbl">' + th + tbody + '</tbody></table></div>';
  }

  // least practised
  var allTypes = ['Sharing','Comforting a friend','Including someone left out','Saying kind words','Cleaning up for others'];
  var typeMap = {};
  for (var i = 0; i < types.length; i++) typeMap[types[i][0]] = types[i][1];
  var missing = [], rare = [];
  for (var i = 0; i < allTypes.length; i++) { if (!typeMap[allTypes[i]]) missing.push(allTypes[i]); }
  for (var i = 0; i < types.length; i++) { if (types[i][1] === 1) rare.push(types[i][0]); }
  var lowEl = document.getElementById('low-acts');
  if (!total) { lowEl.innerHTML = '<div class="empty">No data yet</div>'; }
  else {
    var html = '';
    if (missing.length) {
      html += '<p style="font-size:13px;color:var(--txm);margin-bottom:7px"><strong>Never seen:</strong><br>';
      for (var i = 0; i < missing.length; i++) html += '<span style="background:var(--pl);color:var(--pink);border-radius:9px;padding:2px 8px;font-size:12px;font-weight:700;margin:2px 2px 2px 0;display:inline-block">' + missing[i] + '</span>';
      html += '</p>';
    }
    if (rare.length) {
      html += '<p style="font-size:13px;color:var(--txm)"><strong>Seen only once:</strong><br>';
      for (var i = 0; i < rare.length; i++) html += '<span style="background:var(--al);color:var(--amber);border-radius:9px;padding:2px 8px;font-size:12px;font-weight:700;margin:2px 2px 2px 0;display:inline-block">' + rare[i] + '</span>';
      html += '</p>';
    }
    if (!missing.length && !rare.length) html = '<div style="font-size:13px;color:var(--gd);font-weight:700;padding:7px 0">All kindness types practised multiple times — great variety!</div>';
    lowEl.innerHTML = html;
  }
}

// ── COMPARE TAB ──────────────────────────────────────────────
function renderCompare() {
  var years = getAllYears();
  var data = [];
  for (var i = 0; i < years.length; i++) {
    var yr = years[i];
    var ents = lsGet('kt_entries_' + yr, []);
    var stus = lsGet('kt_students_' + yr, []);
    var h = 0, a = 0, types = {};
    for (var j = 0; j < ents.length; j++) {
      if (ents[j].token === 'h') h++; else a++;
      types[ents[j].type] = (types[ents[j].type]||0)+1;
    }
    var topArr = [];
    for (var k in types) topArr.push([k,types[k]]);
    topArr.sort(function(x,y){return y[1]-x[1];});
    data.push({yr:yr,total:ents.length,studs:stus.length,h:h,a:a,top:topArr[0],types:types});
  }

  var yc = document.getElementById('yr-cards');
  if (!data.length) { yc.innerHTML = '<div class="empty">No years yet</div>'; return; }
  var html = '';
  for (var i = 0; i < data.length; i++) {
    var d = data[i];
    var cur = d.yr === activeYear;
    html += '<div class="yrcard' + (cur?' cur':'') + '">'
          + '<div style="font-size:11px;font-weight:800;text-transform:uppercase;letter-spacing:.07em;color:var(--txm);margin-bottom:7px;display:flex;align-items:center;gap:5px">'
          + '<span style="width:7px;height:7px;border-radius:50%;background:var(--gm);display:inline-block"></span>'
          + d.yr + (cur?' <span style="font-size:10px;background:var(--gl);color:var(--gd);padding:1px 7px;border-radius:7px">current</span>':'')
          + '</div>'
          + '<div style="font-size:27px;font-weight:900;color:var(--gd);line-height:1">' + d.total + '</div>'
          + '<div style="font-size:11px;color:var(--txm);margin-bottom:5px">acts recorded</div>'
          + '<div style="display:flex;justify-content:space-between;font-size:12px;color:var(--txm);margin-top:3px"><span>❤️ ' + d.h + '</span><span>🍎 ' + d.a + '</span><span>👦 ' + d.studs + '</span></div>'
          + (d.top ? '<div style="font-size:11px;color:var(--txm);margin-top:5px">Top: <strong>' + esc(d.top[0]) + '</strong> (' + d.top[1] + '×)</div>' : '')
          + '</div>';
  }
  yc.innerHTML = html;

  var cb = document.getElementById('cmp-bars');
  if (data.length < 2) { cb.innerHTML = '<div class="empty">Add at least 2 years to compare</div>'; }
  else {
    var max = 0;
    for (var i = 0; i < data.length; i++) if (data[i].total > max) max = data[i].total;
    var html2 = '';
    for (var i = 0; i < data.length; i++) {
      var pct = max ? Math.round(data[i].total/max*100) : 0;
      html2 += '<div class="bw"><div class="bh"><span>' + data[i].yr + '</span><span>' + data[i].total + ' acts</span></div>'
             + '<div class="bt"><div class="bf" style="width:' + pct + '%;background:var(--gm)"></div></div></div>';
    }
    cb.innerHTML = html2;
  }

  var ct = document.getElementById('cmp-types');
  if (data.length < 2) { ct.innerHTML = '<div class="empty">Log data across multiple years to see this</div>'; }
  else {
    var allT = {};
    for (var i = 0; i < data.length; i++) for (var k in data[i].types) allT[k] = true;
    var keys = Object.keys(allT);
    var th2 = '<thead><tr><th>Kindness type</th>';
    for (var i = 0; i < data.length; i++) th2 += '<th>' + data[i].yr + '</th>';
    th2 += '</tr></thead><tbody>';
    var tbody2 = '';
    for (var ki = 0; ki < keys.length; ki++) {
      tbody2 += '<tr><td style="font-size:12px">' + esc(keys[ki]) + '</td>';
      for (var i = 0; i < data.length; i++) tbody2 += '<td style="font-weight:700;color:var(--gd)">' + (data[i].types[keys[ki]]||0) + '</td>';
      tbody2 += '</tr>';
    }
    ct.innerHTML = '<div style="overflow-x:auto"><table class="stbl">' + th2 + tbody2 + '</tbody></table></div>';
  }
}

// ── REFLECTION TAB ───────────────────────────────────────────
function renderReflect() {
  var total = entries.length;
  var names = {};
  var types = countBy(entries, 'type');
  for (var i = 0; i < entries.length; i++) names[entries[i].name.toLowerCase()] = true;
  var stuCount = Object.keys(names).length;
  var wins = [];
  if (total > 0) wins.push(total + ' kindness acts recorded — strong engagement with the Kindness Tree activity');
  if (stuCount > 0) wins.push(stuCount + ' student' + (stuCount>1?'s':'') + ' participated — broad reach across the classroom');
  if (types[0]) wins.push('"' + types[0][0] + '" was the most practised behaviour (' + types[0][1] + ' times) — students are naturally building this skill');
  if (total >= 5) wins.push('Each student has their own personal tree — making individual progress visible and motivating');
  if (total >= 10) wins.push('10+ acts logged — enough to demonstrate a sustained culture of kindness over time');
  var el = document.getElementById('wins');
  if (!wins.length) { el.innerHTML = '<div class="empty"><span class="eico">✅</span>Log acts to generate your wins summary</div>'; }
  else {
    var html = '';
    for (var i = 0; i < wins.length; i++) html += '<div class="imp"><span class="impn">' + (i+1) + '.</span><span>' + wins[i] + '</span></div>';
    el.innerHTML = html;
  }
}

// ── EXPORT CSV ───────────────────────────────────────────────
function doExportCSV() {
  if (!entries.length) { alert('No entries to export yet!'); return; }
  var hdr = ['Date','Student','Type','Token','Location','Description'];
  var rows = [hdr.join(',')];
  for (var i = 0; i < entries.length; i++) {
    var e = entries[i];
    var tok = e.token === 'h' ? 'Heart' : 'Apple';
    var row = [e.date,e.name,e.type,tok,e.ctx||'',e.desc||''].map(function(v){return '"'+String(v).replace(/"/g,'""')+'"';});
    rows.push(row.join(','));
  }
  var a = document.createElement('a');
  a.href = URL.createObjectURL(new Blob([rows.join('\n')], {type:'text/csv'}));
  a.download = 'kindness_tree_' + activeYear + '.csv';
  a.click();
}

// ── GENERATE REPORT ──────────────────────────────────────────
function generateReport() {
  var msg = document.getElementById('report-msg').value.trim();
  var total = entries.length;
  var hearts = 0, apples = 0;
  for (var i = 0; i < entries.length; i++) { if (entries[i].token === 'h') hearts++; else apples++; }
  var types = countBy(entries, 'type');
  var ctxs = countBy(entries, 'ctx', true);
  var byName = {};
  for (var i = 0; i < entries.length; i++) byName[entries[i].name] = (byName[entries[i].name]||0)+1;
  var topStuArr = [];
  for (var k in byName) topStuArr.push([k,byName[k]]);
  topStuArr.sort(function(a,b){return b[1]-a[1];});
  var topStu = topStuArr[0];
  var topT = types[0];
  var lowT = types.length > 1 ? types[types.length-1] : null;
  var topC = ctxs[0];
  var today = new Date().toLocaleDateString('en-GB',{day:'numeric',month:'long',year:'numeric'});

  function barHTML(data, color) {
    if (!data.length) return '<p style="color:#9ca3af;font-size:13px">No data recorded</p>';
    var max = data[0][1], out = '';
    for (var i = 0; i < data.length; i++) {
      var pct = Math.round(data[i][1]/max*100);
      out += '<div style="margin-bottom:7px">'
           + '<div style="display:flex;justify-content:space-between;font-size:12px;font-weight:700;margin-bottom:2px"><span>' + esc(data[i][0]) + '</span><span>' + data[i][1] + '</span></div>'
           + '<div style="background:#f0faf3;border-radius:3px;height:7px"><div style="width:' + pct + '%;height:7px;border-radius:3px;background:' + color + '"></div></div>'
           + '</div>';
    }
    return out;
  }

  function miniTreeHTML(ents) {
    var spots = [[55,52],[80,40],[65,30],[40,60],[95,46],[72,23],[88,60],[45,43],[100,58],[60,46],[85,33],[50,36],[78,66],[35,53],[92,36]];
    var svgContent = buildTree(ents, spots, 130, 115);
    return '<svg viewBox="0 0 130 115" xmlns="http://www.w3.org/2000/svg" style="width:130px;height:115px">' + svgContent + '</svg>';
  }

  var allTypes = ['Sharing','Comforting a friend','Including someone left out','Saying kind words','Cleaning up for others'];
  var typeMap = {};
  for (var i = 0; i < types.length; i++) typeMap[types[i][0]] = types[i][1];
  var missing = [], rare = [];
  for (var i = 0; i < allTypes.length; i++) { if (!typeMap[allTypes[i]]) missing.push(allTypes[i]); }
  for (var i = 0; i < types.length; i++) { if (types[i][1] === 1) rare.push(types[i][0]); }

  var stuSections = '';
  for (var si = 0; si < students.length; si++) {
    var n = students[si];
    var ents = entriesFor(n);
    var sh = 0, sa = 0, st = {};
    for (var j = 0; j < ents.length; j++) {
      if (ents[j].token === 'h') sh++; else sa++;
      st[ents[j].type] = (st[ents[j].type]||0)+1;
    }
    var stArr = [];
    for (var k in st) stArr.push([k,st[k]]);
    stArr.sort(function(a,b){return b[1]-a[1];});
    var stop = stArr[0];
    var col = nameColor(n);
    var isTop = topStu && topStu[0] === n && topStu[1] > 0;
    var recentRows = '';
    var shown = ents.slice(0,5);
    for (var j = 0; j < shown.length; j++) {
      var e = shown[j];
      var tok = e.token === 'h' ? '❤️' : '🍎';
      recentRows += '<div style="font-size:12px;padding:3px 0;border-bottom:1px solid #f0f0f0;display:flex;gap:7px">'
                  + '<span>' + tok + '</span><span style="flex:1">' + esc(e.type) + (e.ctx?' · '+esc(e.ctx):'') + '</span>'
                  + '<span style="color:#9ca3af;white-space:nowrap">' + fmtDate(e.date) + '</span></div>';
    }
    if (!shown.length) recentRows = '<div style="font-size:12px;color:#9ca3af;font-style:italic">No acts logged yet</div>';
    if (ents.length > 5) recentRows += '<div style="font-size:11px;color:#9ca3af;margin-top:3px">+ ' + (ents.length-5) + ' more acts</div>';

    stuSections += '<div style="break-inside:avoid;background:#fff;border:1px solid #e2e8e0;border-radius:11px;margin-bottom:14px;overflow:hidden">'
      + '<div style="background:linear-gradient(135deg,' + col + ',' + col + 'bb);padding:10px 14px;display:flex;align-items:center;gap:10px">'
      + '<div style="width:34px;height:34px;border-radius:50%;background:rgba(255,255,255,.25);color:#fff;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:900">' + initials(n) + '</div>'
      + '<div><div style="color:#fff;font-weight:800;font-size:14px">' + esc(n) + (isTop?' 👑':'') + '</div>'
      + '<div style="color:rgba(255,255,255,.8);font-size:12px">' + ents.length + ' acts · ❤️ ' + sh + ' · 🍎 ' + sa + '</div></div>'
      + '</div>'
      + '<div style="padding:11px 14px;display:flex;gap:14px;align-items:flex-start">'
      + '<div style="flex-shrink:0">' + miniTreeHTML(ents) + '</div>'
      + '<div style="flex:1;min-width:0">'
      + (stop ? '<div style="font-size:12px;color:#6b7280;margin-bottom:7px">Most practised: <strong style="color:#2d6a3f">' + esc(stop[0]) + '</strong> (' + stop[1] + '×)</div>' : '')
      + '<div style="font-size:12px;color:#6b7280;margin-bottom:3px"><strong>Recent acts:</strong></div>'
      + recentRows
      + '</div></div></div>';
  }

  var reportHTML = '<!DOCTYPE html>\n'
    + '<html lang="en"><head><meta charset="UTF-8"/>'
    + '<title>Kindness Tree Report ' + activeYear + '</title>'
    + '<link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800;900&family=Lora:wght@400;600&display=swap" rel="stylesheet"/>'
    + '<style>'
    + '*{box-sizing:border-box;margin:0;padding:0}'
    + 'body{font-family:Nunito,sans-serif;color:#1e1e1e;background:#fff;font-size:14px;line-height:1.6}'
    + '.page{max-width:780px;margin:0 auto;padding:36px 28px}'
    + '@media print{'
    + '.no-print{display:none!important}'
    + 'h2{break-before:page}'
    + 'h2:first-of-type{break-before:avoid}'
    + '}'
    + '.cover{background:linear-gradient(160deg,#1e3a2f,#2d6a3f 60%,#4a9b61);color:#fff;border-radius:14px;padding:44px 36px;margin-bottom:28px;text-align:center}'
    + '.stitle{font-family:Lora,serif;font-size:19px;font-weight:600;color:#2d6a3f;margin:28px 0 14px;padding-bottom:7px;border-bottom:2px solid #d4edda}'
    + '.sgrid4{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:20px}'
    + '.sbox{background:#f4f7f2;border-radius:11px;padding:13px;text-align:center;border:1px solid #e2e8e0}'
    + '.hgrid{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:20px}'
    + '.hbx{border-radius:11px;padding:12px 14px;border:1px solid}'
    + '.bgrid{display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-bottom:20px}'
    + '.bcard{background:#f4f7f2;border-radius:11px;padding:14px;border:1px solid #e2e8e0}'
    + '.seegrid{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;margin-bottom:20px}'
    + '.seec{border-radius:11px;padding:13px;text-align:center}'
    + '.pbtn{display:block;margin:0 auto 28px;background:#2d6a3f;color:#fff;border:none;border-radius:28px;padding:11px 28px;font-family:Nunito,sans-serif;font-weight:800;font-size:14px;cursor:pointer;box-shadow:0 4px 14px rgba(45,106,63,.3)}'
    + '</style></head><body><div class="page">'

    + '<div class="no-print" style="text-align:center;margin-bottom:20px;background:#f0faf3;border-radius:11px;padding:14px">'
    + '<p style="font-size:14px;color:#2d6a3f;font-weight:700;margin-bottom:9px">Your report is ready! Save as PDF to share with your principal.</p>'
    + '<button class="pbtn" onclick="window.print()">Save as PDF (Ctrl+P / Cmd+P)</button>'
    + '</div>'

    + '<div class="cover">'
    + '<div style="font-size:48px;margin-bottom:10px">🌳</div>'
    + '<h1 style="font-family:Lora,serif;font-size:28px;font-weight:600;margin-bottom:6px">Kindness Tree — Evaluation Report</h1>'
    + '<div style="font-size:14px;opacity:.8;margin-bottom:20px">SEE Learning Professional Development · School Year ' + activeYear + '</div>'
    + '<div style="display:flex;justify-content:center;gap:20px;flex-wrap:wrap;font-size:13px">'
    + '<span style="background:rgba(255,255,255,.15);border:1px solid rgba(255,255,255,.25);border-radius:18px;padding:4px 13px">📅 ' + today + '</span>'
    + '<span style="background:rgba(255,255,255,.15);border:1px solid rgba(255,255,255,.25);border-radius:18px;padding:4px 13px">👦 ' + students.length + ' students</span>'
    + '<span style="background:rgba(255,255,255,.15);border:1px solid rgba(255,255,255,.25);border-radius:18px;padding:4px 13px">❤️🍎 ' + total + ' acts</span>'
    + '</div></div>'

    + (msg ? '<div style="background:#f0faf3;border-left:4px solid #2d6a3f;border-radius:0 11px 11px 0;padding:14px 18px;margin-bottom:22px;font-size:14px;line-height:1.7">' + esc(msg).replace(/\n/g,'<br>') + '</div>' : '')

    + '<h2 class="stitle">📊 Class Summary</h2>'
    + '<div class="sgrid4">'
    + '<div class="sbox"><div style="font-size:30px;font-weight:900;color:#2d6a3f">' + total + '</div><div style="font-size:11px;font-weight:700;color:#6b7280;text-transform:uppercase;letter-spacing:.05em;margin-top:3px">Total acts</div></div>'
    + '<div class="sbox"><div style="font-size:30px;font-weight:900;color:#2563a8">' + students.length + '</div><div style="font-size:11px;font-weight:700;color:#6b7280;text-transform:uppercase;letter-spacing:.05em;margin-top:3px">Students</div></div>'
    + '<div class="sbox"><div style="font-size:30px;font-weight:900;color:#c0395a">' + hearts + '</div><div style="font-size:11px;font-weight:700;color:#6b7280;text-transform:uppercase;letter-spacing:.05em;margin-top:3px">Hearts ❤️</div></div>'
    + '<div class="sbox"><div style="font-size:30px;font-weight:900;color:#e07b2a">' + apples + '</div><div style="font-size:11px;font-weight:700;color:#6b7280;text-transform:uppercase;letter-spacing:.05em;margin-top:3px">Apples 🍎</div></div>'
    + '</div>'

    + '<div class="hgrid">'
    + '<div class="hbx" style="background:#fffbeb;border-color:#fde68a"><div style="font-size:10px;font-weight:800;text-transform:uppercase;letter-spacing:.07em;color:#92400e;margin-bottom:4px">🏆 Kindest student</div><div style="font-size:15px;font-weight:800">' + (topStu?esc(topStu[0]):'—') + '</div><div style="font-size:11px;color:#6b7280;margin-top:2px">' + (topStu?topStu[1]+' acts':'') + '</div></div>'
    + '<div class="hbx" style="background:#f0faf3;border-color:#d4edda"><div style="font-size:10px;font-weight:800;text-transform:uppercase;letter-spacing:.07em;color:#2d6a3f;margin-bottom:4px">⭐ Most practised act</div><div style="font-size:15px;font-weight:800">' + (topT?esc(topT[0]):'—') + '</div><div style="font-size:11px;color:#6b7280;margin-top:2px">' + (topT?topT[1]+' times':'') + '</div></div>'
    + '<div class="hbx" style="background:#fff5f5;border-color:#fecaca"><div style="font-size:10px;font-weight:800;text-transform:uppercase;letter-spacing:.07em;color:#991b1b;margin-bottom:4px">💬 Least seen act</div><div style="font-size:15px;font-weight:800">' + (lowT?esc(lowT[0]):'—') + '</div><div style="font-size:11px;color:#6b7280;margin-top:2px">' + (lowT?lowT[1]+' times':'') + '</div></div>'
    + '<div class="hbx" style="background:#e8f1fb;border-color:#bfdbfe"><div style="font-size:10px;font-weight:800;text-transform:uppercase;letter-spacing:.07em;color:#1d4ed8;margin-bottom:4px">📍 Top location</div><div style="font-size:15px;font-weight:800">' + (topC?esc(topC[0]):'—') + '</div><div style="font-size:11px;color:#6b7280;margin-top:2px">' + (topC?topC[1]+' acts here':'') + '</div></div>'
    + '</div>'

    + '<div class="bgrid">'
    + '<div class="bcard"><h4 style="font-size:11px;font-weight:800;text-transform:uppercase;letter-spacing:.07em;color:#6b7280;margin-bottom:10px">Kindness types</h4>' + barHTML(types,'#4a9b61') + '</div>'
    + '<div class="bcard"><h4 style="font-size:11px;font-weight:800;text-transform:uppercase;letter-spacing:.07em;color:#6b7280;margin-bottom:10px">By location</h4>' + barHTML(ctxs,'#2563a8') + '</div>'
    + '</div>'

    + (missing.length || rare.length ? '<div style="background:#fff5f5;border:1px solid #fecaca;border-radius:11px;padding:14px;margin-bottom:20px">'
    + '<div style="font-size:11px;font-weight:800;text-transform:uppercase;letter-spacing:.07em;color:#991b1b;margin-bottom:7px">Areas for growth</div>'
    + (missing.length ? '<p style="font-size:13px;margin-bottom:5px"><strong>Never seen:</strong> ' + missing.map(function(t){return '<span style="background:#fdeef2;color:#c0395a;border-radius:8px;padding:2px 7px;font-size:12px;font-weight:700;margin:2px">'+t+'</span>';}).join('') + '</p>' : '')
    + (rare.length ? '<p style="font-size:13px"><strong>Seen only once:</strong> ' + rare.map(function(t){return '<span style="background:#fff3e0;color:#e07b2a;border-radius:8px;padding:2px 7px;font-size:12px;font-weight:700;margin:2px">'+t+'</span>';}).join('') + '</p>' : '')
    + '</div>' : '')

    + '<h2 class="stitle">💡 SEE Learning Connection</h2>'
    + '<p style="font-size:13px;color:#6b7280;margin-bottom:14px">The Kindness Tree activity directly addresses SEE Learning\'s three core domains:</p>'
    + '<div class="seegrid">'
    + '<div class="seec" style="background:#e8f1fb;border:1px solid #bfdbfe"><div style="background:#2563a8;color:#fff;border-radius:18px;font-size:11px;font-weight:800;padding:3px 11px;display:inline-block;margin-bottom:7px">Personal</div><p style="font-size:12px;color:#4b5563;line-height:1.5">Students recognise their capacity to act with care and compassion</p></div>'
    + '<div class="seec" style="background:#f0faf3;border:1px solid #d4edda"><div style="background:#2d6a3f;color:#fff;border-radius:18px;font-size:11px;font-weight:800;padding:3px 11px;display:inline-block;margin-bottom:7px">Social</div><p style="font-size:12px;color:#4b5563;line-height:1.5">Sharing, comforting, and including build essential relational skills</p></div>'
    + '<div class="seec" style="background:#fff3e0;border:1px solid #fed7aa"><div style="background:#e07b2a;color:#fff;border-radius:18px;font-size:11px;font-weight:800;padding:3px 11px;display:inline-block;margin-bottom:7px">Systems</div><p style="font-size:12px;color:#4b5563;line-height:1.5">The class tree shows students that kindness has collective community impact</p></div>'
    + '</div>'
    + '<div style="background:#f0faf3;border-radius:11px;padding:14px;margin-bottom:22px;font-size:13px;color:#4b5563;line-height:1.7"><strong style="color:#2d6a3f">Note on PD completion:</strong> While the formal SEE Learning PD modules were not completed within this period due to time constraints, the Kindness Tree initiative demonstrates authentic integration of SEE Learning values into daily classroom practice. The data above provides tangible evidence of a sustained, student-centred approach to social-emotional learning throughout the year.</div>'

    + '<h2 class="stitle">🌳 Individual Student Trees</h2>'
    + '<p style="font-size:13px;color:#6b7280;margin-bottom:14px">Each student maintained their own personal Kindness Tree. Hearts and apples were added each time they demonstrated a kindness act.</p>'
    + stuSections

    + (notes ? '<h2 class="stitle">✍️ Teacher Reflection</h2><div style="background:#f0faf3;border-left:4px solid #2d6a3f;border-radius:0 11px 11px 0;padding:14px 18px;margin-bottom:22px;font-size:14px;line-height:1.7">' + esc(notes).replace(/\n/g,'<br>') + '</div>' : '')

    + '<div style="text-align:center;font-size:12px;color:#9ca3af;margin-top:36px;padding-top:18px;border-top:1px solid #e2e8e0">Kindness Tree Tracker · SEE Learning · ' + activeYear + ' · Generated ' + today + '</div>'
    + '</div></body></html>';

  var w = window.open('', '_blank');
  if (!w) { alert('Pop-up blocked! Please allow pop-ups for this file in your browser and try again.'); return; }
  w.document.write(reportHTML);
  w.document.close();
}

// ── RESET ──────────────────────────────────────────────────
function resetData() {
  if (!confirm("Reload all original class data? Any edits will be lost.")) return;
  try {
    localStorage.clear();
    lsSet("kt_students_2024-2025", KT_STUDENTS);
    lsSet("kt_entries_2024-2025",  KT_ENTRIES);
    lsSet("kt_notes_2024-2025",    "Kindness Tree data covers February through May 2025.");
    lsSet("kt_years",              ["2024-2025"]);
    lsSet("kt_active_year",        "2024-2025");
  } catch(e) {}
  location.reload();
}

// ── INIT ─────────────────────────────────────────────────────
document.getElementById('f-date').value = new Date().toISOString().split('T')[0];
renderRoster();
renderLogChips();
</script>
</body>
</html>
