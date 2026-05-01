
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>Aetbar Management System — GUI</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<style>
/* ═══════════════════════════════════════════════════════
   RESET & ROOT VARIABLES
═══════════════════════════════════════════════════════ */
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
:root{
  --g:#1D9E75;--gd:#0F6E56;--gl:#E1F5EE;--gll:#F0FAF6;
  --pur:#7C3AED;--purl:#EDE9FE;
  --ora:#F97316;--oral:#FFF0E6;
  --pin:#EC4899;--pinl:#FCE7F3;
  --amb:#EF9F27;--ambl:#FAEEDA;
  --red:#E24B4A;--redl:#FCEBEB;
  --blu:#378ADD;--blul:#E6F1FB;
  --teal:#0EA5E9;--teall:#E0F2FE;
  --bg:#0D1117;--card:#161B22;--card2:#21262D;
  --border:#30363D;--border2:#484F58;
  --txt:#E6EDF3;--txt2:#8B949E;--txt3:#6E7681;
  --sidebar:240px;
}
html,body{height:100%;font-family:'Plus Jakarta Sans',sans-serif;background:var(--bg);color:var(--txt);overflow:hidden}

/* ═══════════════════════════════════════════════════════
   LAYOUT
═══════════════════════════════════════════════════════ */
.app-shell{display:flex;height:100vh;overflow:hidden}

/* ═══════════════════════════════════════════════════════
   SIDEBAR
═══════════════════════════════════════════════════════ */
.sidebar{
  width:var(--sidebar);flex-shrink:0;
  background:var(--card);
  border-right:1px solid var(--border);
  display:flex;flex-direction:column;
  height:100vh;overflow:hidden;
}
.sidebar-logo{
  padding:20px 16px 16px;
  border-bottom:1px solid var(--border);
  display:flex;align-items:center;gap:10px;
}
.sidebar-logo .logo-icon{
  width:38px;height:38px;border-radius:10px;
  background:linear-gradient(135deg,var(--g),var(--teal));
  display:flex;align-items:center;justify-content:center;
  font-size:18px;flex-shrink:0;
}
.sidebar-logo h2{font-size:16px;font-weight:800;color:var(--txt)}
.sidebar-logo p{font-size:10px;color:var(--txt2);margin-top:1px}

.sidebar-user{
  padding:12px 14px;border-bottom:1px solid var(--border);
  background:var(--card2);
}
.su-name{font-size:13px;font-weight:700;color:var(--txt)}
.su-role{font-size:10px;color:var(--g);font-weight:600;margin-top:2px;text-transform:uppercase;letter-spacing:.5px}
.su-badge{
  display:inline-flex;align-items:center;gap:4px;
  margin-top:6px;background:rgba(29,158,117,.15);
  color:var(--g);font-size:10px;font-weight:700;
  padding:2px 8px;border-radius:20px;border:1px solid rgba(29,158,117,.3);
}

.sidebar-nav{flex:1;overflow-y:auto;padding:10px 8px}
.sidebar-nav::-webkit-scrollbar{width:0}
.nav-section{
  font-size:9px;font-weight:700;color:var(--txt3);
  padding:10px 8px 4px;letter-spacing:1.2px;text-transform:uppercase;
}
.nav-item{
  display:flex;align-items:center;gap:10px;
  padding:9px 12px;border-radius:9px;cursor:pointer;
  color:var(--txt2);font-size:13px;font-weight:500;
  transition:all .15s;margin-bottom:1px;
  border:1px solid transparent;
}
.nav-item:hover{background:var(--card2);color:var(--txt)}
.nav-item.active{
  background:rgba(29,158,117,.15);color:var(--g);
  font-weight:700;border-color:rgba(29,158,117,.3);
}
.nav-item .ni{font-size:15px;width:20px;text-align:center;flex-shrink:0}
.nav-badge{
  margin-left:auto;background:var(--red);color:#fff;
  font-size:9px;font-weight:700;padding:1px 6px;
  border-radius:10px;min-width:18px;text-align:center;
}
.nav-badge.green{background:var(--g)}

.sidebar-footer{
  padding:12px 14px;border-top:1px solid var(--border);
  font-size:11px;color:var(--txt3);
}

/* ═══════════════════════════════════════════════════════
   MAIN CONTENT AREA
═══════════════════════════════════════════════════════ */
.main{flex:1;display:flex;flex-direction:column;overflow:hidden;background:var(--bg)}

.topbar{
  background:var(--card);border-bottom:1px solid var(--border);
  padding:0 24px;height:56px;display:flex;align-items:center;
  justify-content:space-between;flex-shrink:0;
}
.topbar h2{font-size:15px;font-weight:800;color:var(--txt)}
.topbar-right{display:flex;align-items:center;gap:10px}
.tb-btn{
  background:var(--card2);border:1px solid var(--border);
  color:var(--txt2);padding:6px 12px;border-radius:8px;
  font-size:12px;font-weight:600;cursor:pointer;font-family:inherit;
  transition:all .15s;
}
.tb-btn:hover{border-color:var(--g);color:var(--g)}
.tb-date{font-size:11px;color:var(--txt3);font-weight:500}

.content{flex:1;overflow-y:auto;padding:0}
.content::-webkit-scrollbar{width:6px}
.content::-webkit-scrollbar-track{background:var(--card)}
.content::-webkit-scrollbar-thumb{background:var(--border2);border-radius:3px}

/* ═══════════════════════════════════════════════════════
   PAGES
═══════════════════════════════════════════════════════ */
.page{display:none;padding:24px;animation:fadeIn .2s ease}
.page.active{display:block}
@keyframes fadeIn{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:translateY(0)}}

/* ═══════════════════════════════════════════════════════
   STAT CARDS
═══════════════════════════════════════════════════════ */
.stat-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:14px;margin-bottom:22px}
.stat-card{
  background:var(--card);border:1px solid var(--border);
  border-radius:14px;padding:18px;position:relative;overflow:hidden;
  transition:border-color .2s;cursor:default;
}
.stat-card:hover{border-color:var(--border2)}
.stat-card::before{
  content:'';position:absolute;left:0;top:0;
  width:3px;height:100%;border-radius:3px 0 0 3px;
}
.stat-card.green::before{background:linear-gradient(180deg,var(--g),var(--teal))}
.stat-card.amber::before{background:linear-gradient(180deg,var(--amb),var(--ora))}
.stat-card.blue::before{background:linear-gradient(180deg,var(--blu),var(--pur))}
.stat-card.red::before{background:linear-gradient(180deg,var(--red),var(--pin))}
.stat-card .sl{font-size:10px;font-weight:700;color:var(--txt2);text-transform:uppercase;letter-spacing:.5px}
.stat-card .sn{font-size:26px;font-weight:800;margin:6px 0 4px}
.stat-card .sc{font-size:11px;font-weight:500}
.stat-card .si{font-size:26px;position:absolute;top:14px;right:14px;opacity:.12}

/* ═══════════════════════════════════════════════════════
   CARDS / PANELS
═══════════════════════════════════════════════════════ */
.card{
  background:var(--card);border:1px solid var(--border);
  border-radius:14px;overflow:hidden;margin-bottom:18px;
}
.card-header{
  padding:14px 18px;border-bottom:1px solid var(--border);
  display:flex;align-items:center;justify-content:space-between;
  background:var(--card2);
}
.card-header h3{font-size:14px;font-weight:700;color:var(--txt)}
.card-body{padding:18px}

/* ═══════════════════════════════════════════════════════
   TABLES
═══════════════════════════════════════════════════════ */
.table-wrap{overflow-x:auto}
table{width:100%;border-collapse:collapse;font-size:12px}
th{
  background:var(--card2);font-size:10px;font-weight:700;
  color:var(--txt2);text-transform:uppercase;letter-spacing:.5px;
  padding:10px 14px;text-align:left;border-bottom:1px solid var(--border);
  white-space:nowrap;
}
td{
  padding:11px 14px;border-bottom:1px solid var(--border);
  color:var(--txt);vertical-align:middle;
}
tr:last-child td{border-bottom:none}
tr:hover td{background:rgba(255,255,255,.02)}

/* ═══════════════════════════════════════════════════════
   BADGES
═══════════════════════════════════════════════════════ */
.badge{
  font-size:10px;font-weight:700;padding:3px 9px;
  border-radius:20px;display:inline-block;white-space:nowrap;
}
.bg{background:rgba(29,158,117,.15);color:#4ADE80;border:1px solid rgba(29,158,117,.3)}
.ba{background:rgba(239,159,39,.15);color:#FCD34D;border:1px solid rgba(239,159,39,.3)}
.bb{background:rgba(55,138,221,.15);color:#93C5FD;border:1px solid rgba(55,138,221,.3)}
.br{background:rgba(226,75,74,.15);color:#FCA5A5;border:1px solid rgba(226,75,74,.3)}
.bw{background:rgba(255,255,255,.06);color:var(--txt2);border:1px solid var(--border)}
.bpur{background:rgba(124,58,237,.15);color:#C4B5FD;border:1px solid rgba(124,58,237,.3)}

/* ═══════════════════════════════════════════════════════
   BUTTONS
═══════════════════════════════════════════════════════ */
.btn{
  padding:9px 18px;border-radius:9px;font-family:inherit;
  font-weight:700;font-size:13px;cursor:pointer;border:none;
  transition:all .15s;display:inline-flex;align-items:center;gap:6px;
}
.btn-g{background:linear-gradient(135deg,var(--g),var(--gd));color:#fff;box-shadow:0 3px 10px rgba(29,158,117,.3)}
.btn-g:hover{transform:translateY(-1px);box-shadow:0 5px 16px rgba(29,158,117,.4)}
.btn-o{background:transparent;color:var(--g);border:1.5px solid var(--g)}
.btn-o:hover{background:rgba(29,158,117,.1)}
.btn-r{background:rgba(226,75,74,.15);color:#FCA5A5;border:1.5px solid rgba(226,75,74,.3)}
.btn-r:hover{background:rgba(226,75,74,.25)}
.btn-sm{padding:5px 12px;font-size:11px;border-radius:7px}
.btn-icon{width:32px;height:32px;padding:0;justify-content:center;font-size:14px}

/* ═══════════════════════════════════════════════════════
   FORMS
═══════════════════════════════════════════════════════ */
.form-grid{display:grid;grid-template-columns:1fr 1fr;gap:14px}
.form-group{display:flex;flex-direction:column;gap:5px}
.form-group.full{grid-column:1/-1}
.flabel{font-size:10px;font-weight:700;color:var(--txt2);text-transform:uppercase;letter-spacing:.5px}
.finput{
  background:var(--card2);border:1.5px solid var(--border);
  color:var(--txt);border-radius:9px;padding:9px 12px;
  font-family:inherit;font-size:13px;outline:none;
  transition:border .15s;width:100%;
}
.finput:focus{border-color:var(--g);box-shadow:0 0 0 3px rgba(29,158,117,.1)}
.finput::placeholder{color:var(--txt3)}
select.finput{appearance:none;cursor:pointer}
textarea.finput{resize:vertical;min-height:80px}

/* ═══════════════════════════════════════════════════════
   ALERTS / NOTICES
═══════════════════════════════════════════════════════ */
.alert{
  border-radius:10px;padding:12px 14px;font-size:12px;
  display:flex;gap:10px;align-items:flex-start;margin-bottom:16px;
  line-height:1.5;
}
.alert-g{background:rgba(29,158,117,.12);border:1px solid rgba(29,158,117,.3);color:#4ADE80}
.alert-r{background:rgba(226,75,74,.12);border:1px solid rgba(226,75,74,.3);color:#FCA5A5}
.alert-a{background:rgba(239,159,39,.12);border:1px solid rgba(239,159,39,.3);color:#FCD34D}
.alert-b{background:rgba(55,138,221,.12);border:1px solid rgba(55,138,221,.3);color:#93C5FD}

/* ═══════════════════════════════════════════════════════
   MODAL
═══════════════════════════════════════════════════════ */
.overlay{
  display:none;position:fixed;inset:0;
  background:rgba(0,0,0,.7);z-index:200;
  align-items:center;justify-content:center;padding:16px;
  backdrop-filter:blur(4px);
}
.overlay.open{display:flex}
.modal{
  background:var(--card);border:1px solid var(--border);
  border-radius:18px;width:100%;max-width:520px;
  max-height:90vh;overflow-y:auto;
  box-shadow:0 24px 80px rgba(0,0,0,.5);
  animation:modalIn .25s cubic-bezier(.34,1.56,.64,1);
}
.modal::-webkit-scrollbar{width:0}
@keyframes modalIn{from{opacity:0;transform:scale(.92)}to{opacity:1;transform:scale(1)}}
.modal-header{
  padding:18px 22px;border-bottom:1px solid var(--border);
  display:flex;align-items:center;justify-content:space-between;
}
.modal-header h3{font-size:16px;font-weight:800}
.modal-close{
  background:var(--card2);border:1px solid var(--border);
  color:var(--txt2);width:30px;height:30px;border-radius:8px;
  cursor:pointer;font-size:16px;display:flex;align-items:center;
  justify-content:center;transition:all .15s;
}
.modal-close:hover{background:rgba(226,75,74,.2);color:var(--red);border-color:var(--red)}
.modal-body{padding:22px}
.modal-footer{
  padding:16px 22px;border-top:1px solid var(--border);
  display:flex;gap:10px;justify-content:flex-end;
}

/* ═══════════════════════════════════════════════════════
   TOAST
═══════════════════════════════════════════════════════ */
.toast{
  position:fixed;bottom:24px;right:24px;z-index:999;
  padding:12px 18px;border-radius:12px;font-size:13px;
  font-weight:600;display:flex;align-items:center;gap:10px;
  box-shadow:0 8px 30px rgba(0,0,0,.4);
  transform:translateY(80px);transition:transform .3s cubic-bezier(.34,1.56,.64,1);
  max-width:360px;line-height:1.4;
}
.toast.show{transform:translateY(0)}
.toast.success{background:rgba(29,158,117,.9);color:#fff;border:1px solid var(--g)}
.toast.error{background:rgba(226,75,74,.9);color:#fff;border:1px solid var(--red)}
.toast.info{background:rgba(55,138,221,.9);color:#fff;border:1px solid var(--blu)}
.toast.warn{background:rgba(239,159,39,.9);color:#fff;border:1px solid var(--amb)}

/* ═══════════════════════════════════════════════════════
   WORKER AVATAR
═══════════════════════════════════════════════════════ */
.wkav{
  width:34px;height:34px;border-radius:50%;
  display:flex;align-items:center;justify-content:center;
  font-size:11px;font-weight:800;flex-shrink:0;
}

/* ═══════════════════════════════════════════════════════
   SEARCH / FILTER BAR
═══════════════════════════════════════════════════════ */
.filter-bar{
  display:flex;gap:10px;margin-bottom:16px;flex-wrap:wrap;
  align-items:center;
}
.search-input{
  background:var(--card2);border:1.5px solid var(--border);
  color:var(--txt);border-radius:9px;padding:8px 12px;
  font-family:inherit;font-size:13px;outline:none;
  transition:border .15s;flex:1;min-width:200px;
}
.search-input:focus{border-color:var(--g)}
.search-input::placeholder{color:var(--txt3)}
.filter-chip{
  padding:6px 14px;border-radius:20px;font-size:11px;
  font-weight:700;cursor:pointer;border:1px solid var(--border);
  background:var(--card2);color:var(--txt2);transition:all .15s;
  white-space:nowrap;
}
.filter-chip:hover,.filter-chip.active{
  background:rgba(29,158,117,.15);color:var(--g);
  border-color:rgba(29,158,117,.4);
}

/* ═══════════════════════════════════════════════════════
   PROGRESS / STATS BARS
═══════════════════════════════════════════════════════ */
.prog-bar{height:6px;background:var(--card2);border-radius:3px;overflow:hidden;flex:1}
.prog-fill{height:100%;border-radius:3px;transition:width .5s ease}

/* ═══════════════════════════════════════════════════════
   MINI CARDS (for dashboard)
═══════════════════════════════════════════════════════ */
.mini-cards{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;margin-bottom:18px}
.mini-card{
  background:var(--card2);border:1px solid var(--border);
  border-radius:12px;padding:14px;cursor:pointer;
  transition:border-color .15s;
}
.mini-card:hover{border-color:var(--border2)}
.mini-card .mc-title{font-size:11px;color:var(--txt2);font-weight:600;margin-bottom:4px}
.mini-card .mc-val{font-size:18px;font-weight:800;color:var(--txt)}

/* ═══════════════════════════════════════════════════════
   LOGIN SCREEN
═══════════════════════════════════════════════════════ */
.login-screen{
  display:flex;align-items:center;justify-content:center;
  height:100vh;background:var(--bg);
  background-image:radial-gradient(ellipse at 20% 50%, rgba(29,158,117,.08) 0%, transparent 60%),
                   radial-gradient(ellipse at 80% 20%, rgba(14,165,233,.06) 0%, transparent 50%);
}
.login-box{
  background:var(--card);border:1px solid var(--border);
  border-radius:20px;padding:36px;width:100%;max-width:400px;
  box-shadow:0 24px 80px rgba(0,0,0,.5);
}
.login-logo{
  text-align:center;margin-bottom:28px;
}
.login-logo .icon{
  width:60px;height:60px;background:linear-gradient(135deg,var(--g),var(--teal));
  border-radius:16px;display:flex;align-items:center;justify-content:center;
  font-size:28px;margin:0 auto 12px;box-shadow:0 8px 24px rgba(29,158,117,.4);
}
.login-logo h1{font-size:24px;font-weight:800;color:var(--txt)}
.login-logo p{font-size:13px;color:var(--txt2);margin-top:4px}

/* ═══════════════════════════════════════════════════════
   CHART BARS (simple CSS chart)
═══════════════════════════════════════════════════════ */
.chart-wrap{display:flex;align-items:flex-end;gap:8px;height:100px;padding:0 4px}
.chart-bar{
  flex:1;border-radius:4px 4px 0 0;min-width:20px;
  cursor:pointer;transition:opacity .15s;position:relative;
}
.chart-bar:hover{opacity:.8}
.chart-label{
  position:absolute;bottom:-20px;left:0;right:0;
  text-align:center;font-size:9px;color:var(--txt3);white-space:nowrap;
}

/* ═══════════════════════════════════════════════════════
   EXCEPTION LOG
═══════════════════════════════════════════════════════ */
.exc-item{
  background:rgba(226,75,74,.06);border:1px solid rgba(226,75,74,.2);
  border-radius:10px;padding:12px 14px;margin-bottom:10px;
}
.exc-item .exc-type{font-size:11px;font-weight:700;color:#FCA5A5;margin-bottom:4px}
.exc-item .exc-msg{font-size:12px;color:var(--txt2);line-height:1.5}
.exc-item .exc-time{font-size:10px;color:var(--txt3);margin-top:5px}

/* ═══════════════════════════════════════════════════════
   MISC
═══════════════════════════════════════════════════════ */
.divider{height:1px;background:var(--border);margin:16px 0}
.online-dot{width:8px;height:8px;background:#22C55E;border-radius:50%;flex-shrink:0;box-shadow:0 0 6px #22C55E}
.empty-state{
  text-align:center;padding:48px 20px;color:var(--txt3);
}
.empty-state .es-ico{font-size:44px;margin-bottom:12px;display:block}
.empty-state p{font-size:14px;font-weight:600;color:var(--txt2)}
.empty-state span{font-size:12px;color:var(--txt3)}
.page-title{font-size:20px;font-weight:800;margin-bottom:4px}
.page-sub{font-size:13px;color:var(--txt2);margin-bottom:20px}
.two-col{display:grid;grid-template-columns:1fr 1fr;gap:18px}
.three-col{display:grid;grid-template-columns:1fr 1fr 1fr;gap:14px}
.flex-row{display:flex;align-items:center;gap:10px}
</style>
</head>
<body>

<div class="toast" id="toast"></div>

<!-- ════════════════════════════════════════════════════════════
  LOGIN SCREEN
════════════════════════════════════════════════════════════ -->
<div class="login-screen" id="login-screen">
  <div class="login-box">
    <div class="login-logo">
      <div class="icon">🏠</div>
      <h1>Aetbar</h1>
      <p>Management System — GUI</p>
    </div>
    <div id="login-alert"></div>
    <div class="form-group" style="margin-bottom:14px">
      <label class="flabel">Phone / Username</label>
      <input class="finput" id="li-phone" placeholder="03001234567 or admin" type="text" onkeydown="if(event.key==='Enter')doLogin()">
    </div>
    <div class="form-group" style="margin-bottom:20px">
      <label class="flabel">Password</label>
      <input class="finput" id="li-pass" placeholder="Your password" type="password" onkeydown="if(event.key==='Enter')doLogin()">
    </div>
    <button class="btn btn-g" style="width:100%;padding:12px;font-size:14px;justify-content:center" onclick="doLogin()">
      Login to Aetbar →
    </button>
    <div style="margin-top:18px;background:var(--card2);border:1px solid var(--border);border-radius:10px;padding:12px">
      <div style="font-size:10px;font-weight:700;color:var(--txt2);text-transform:uppercase;letter-spacing:.5px;margin-bottom:8px">Default Credentials</div>
      <div style="font-size:12px;color:var(--txt2);line-height:1.8">
        Employer → <span style="color:var(--g);font-weight:700">03001234567</span> / <span style="color:var(--g);font-weight:700">1234</span><br>
        Admin &nbsp;&nbsp;&nbsp;→ <span style="color:var(--amb);font-weight:700">admin</span> / <span style="color:var(--amb);font-weight:700">admin123</span>
      </div>
    </div>
  </div>
</div>

<!-- ════════════════════════════════════════════════════════════
  MAIN APP SHELL
════════════════════════════════════════════════════════════ -->
<div class="app-shell" id="app-shell" style="display:none">

  <!-- SIDEBAR -->
  <aside class="sidebar">
    <div class="sidebar-logo">
      <div class="logo-icon">🏠</div>
      <div><h2>Aetbar</h2><p>Management GUI</p></div>
    </div>
    <div class="sidebar-user">
      <div class="su-name" id="sb-name">Ahmed Raza</div>
      <div class="su-role" id="sb-role">Employer</div>
      <div class="su-badge"><span>●</span> <span id="sb-status">Online</span></div>
    </div>
    <nav class="sidebar-nav" id="sidebar-nav">
      <!-- populated by JS based on role -->
    </nav>
    <div class="sidebar-footer">
      <div style="font-size:11px;color:var(--txt2)">Sultan Ali — 0331-5506907</div>
      <div style="font-size:10px;color:var(--txt3);margin-top:2px">Aetbar v1.0 · Pakistan 🇵🇰</div>
    </div>
  </aside>

  <!-- MAIN -->
  <main class="main">
    <div class="topbar">
      <h2 id="page-title">Dashboard</h2>
      <div class="topbar-right">
        <span class="tb-date" id="tb-date"></span>
        <button class="tb-btn" onclick="loadData();toast('Data refreshed from CSV files','info')">↻ Refresh</button>
        <button class="tb-btn" onclick="doLogout()">Logout</button>
      </div>
    </div>

    <div class="content" id="content">

      <!-- ════ DASHBOARD ════ -->
      <div class="page active" id="p-dashboard">
        <div style="padding:24px 24px 0">
          <div class="page-title">Dashboard</div>
          <div class="page-sub" id="dash-welcome">Welcome back!</div>
        </div>
        <div style="padding:0 24px 24px">
          <div class="stat-grid" id="stat-grid">
            <div class="stat-card green"><div class="sl">Total Workers</div><div class="sn" id="s-workers" style="color:#4ADE80">—</div><div class="sc" style="color:#4ADE80">Platform workers</div><div class="si">👷</div></div>
            <div class="stat-card amber"><div class="sl">Verified</div><div class="sn" id="s-verified" style="color:#FCD34D">—</div><div class="sc" style="color:#FCD34D">Police cleared</div><div class="si">✓</div></div>
            <div class="stat-card blue"><div class="sl">Bookings</div><div class="sn" id="s-bookings" style="color:#93C5FD">—</div><div class="sc" style="color:#93C5FD">Total bookings</div><div class="si">📅</div></div>
            <div class="stat-card red"><div class="sl">Users</div><div class="sn" id="s-users" style="color:#FCA5A5">—</div><div class="sc" style="color:#FCA5A5">Registered</div><div class="si">👥</div></div>
          </div>

          <div class="two-col">
            <!-- Recent Bookings -->
            <div class="card">
              <div class="card-header"><h3>Recent Bookings</h3><button class="btn btn-sm bw" onclick="goTo('p-bookings')">View All</button></div>
              <div class="table-wrap"><table><thead><tr><th>Worker</th><th>Service</th><th>Amount</th><th>Status</th></tr></thead>
              <tbody id="dash-bookings"><tr><td colspan="4" style="text-align:center;color:var(--txt3);padding:20px">Loading...</td></tr></tbody></table></div>
            </div>
            <!-- Pending Verifications -->
            <div class="card">
              <div class="card-header"><h3>Pending Verifications</h3><span class="badge br" id="pend-count">0</span></div>
              <div id="dash-pending"><div class="empty-state"><span class="es-ico">✅</span><p>All clear!</p><span>No pending verifications</span></div></div>
            </div>
          </div>

          <!-- Services Chart -->
          <div class="card">
            <div class="card-header"><h3>Workers by Category</h3></div>
            <div class="card-body">
              <div id="cat-chart" style="display:flex;flex-direction:column;gap:10px"></div>
            </div>
          </div>
        </div>
      </div>

      <!-- ════ WORKERS ════ -->
      <div class="page" id="p-workers">
        <div style="padding:24px">
          <div class="page-title">Workers</div>
          <div class="page-sub">All workers registered on the platform</div>
          <div class="filter-bar">
            <input class="search-input" id="w-search" placeholder="Search by name, category or city..." oninput="renderWorkers()">
            <select class="search-input" id="w-cat" onchange="renderWorkers()" style="flex:0;width:160px">
              <option value="">All Categories</option>
              <option>Maid</option><option>Cook</option><option>Electrician</option>
              <option>Plumber</option><option>Security</option><option>Labourer</option>
              <option>Carpenter</option><option>Painter</option><option>Baby Sitter</option><option>Clothes</option>
            </select>
            <select class="search-input" id="w-status" onchange="renderWorkers()" style="flex:0;width:130px">
              <option value="">All Status</option>
              <option value="1">Verified</option>
              <option value="0">Pending</option>
            </select>
            <button class="btn btn-g btn-sm" onclick="openAddWorkerModal()">+ Add Worker</button>
          </div>
          <div class="card">
            <div class="table-wrap"><table>
              <thead><tr><th>Worker</th><th>Category</th><th>City / Area</th><th>Phone</th><th>Rate/Day</th><th>Rating</th><th>Jobs</th><th>Status</th><th>Actions</th></tr></thead>
              <tbody id="workers-tbody"></tbody>
            </table></div>
          </div>
        </div>
      </div>

      <!-- ════ BOOKINGS ════ -->
      <div class="page" id="p-bookings">
        <div style="padding:24px">
          <div class="page-title">Bookings</div>
          <div class="page-sub">All booking records with full details</div>
          <div class="filter-bar">
            <input class="search-input" id="b-search" placeholder="Search by worker name or service..." oninput="renderBookings()">
            <select class="search-input" id="b-status" onchange="renderBookings()" style="flex:0;width:140px">
              <option value="">All Status</option>
              <option>pending</option><option>active</option>
              <option>completed</option><option>cancelled</option>
            </select>
            <button class="btn btn-g btn-sm" onclick="openNewBookingModal()">+ New Booking</button>
          </div>
          <div class="three-col" id="booking-stats" style="margin-bottom:18px"></div>
          <div class="card">
            <div class="table-wrap"><table>
              <thead><tr><th>ID</th><th>Worker</th><th>Service</th><th>Package</th><th>Amount</th><th>Start Date</th><th>End Date</th><th>Status</th><th>Payment</th><th>Actions</th></tr></thead>
              <tbody id="bookings-tbody"></tbody>
            </table></div>
          </div>
        </div>
      </div>

      <!-- ════ USERS ════ -->
      <div class="page" id="p-users">
        <div style="padding:24px">
          <div class="page-title">Users</div>
          <div class="page-sub">All registered employer accounts</div>
          <div class="filter-bar">
            <input class="search-input" id="u-search" placeholder="Search by name or phone..." oninput="renderUsers()">
          </div>
          <div class="card">
            <div class="table-wrap"><table>
              <thead><tr><th>ID</th><th>Name</th><th>Phone</th><th>City/Area</th><th>Role</th><th>Wallet</th><th>Member Since</th><th>Bookings</th></tr></thead>
              <tbody id="users-tbody"></tbody>
            </table></div>
          </div>
        </div>
      </div>

      <!-- ════ VERIFICATION ════ -->
      <div class="page" id="p-verify">
        <div style="padding:24px">
          <div class="page-title">Verification Queue</div>
          <div class="page-sub">Review and approve worker CNIC & police clearance documents</div>
          <div id="verify-list"></div>
        </div>
      </div>

      <!-- ════ EXCEPTIONS LOG ════ -->
      <div class="page" id="p-exceptions">
        <div style="padding:24px">
          <div class="page-title">Exception Log</div>
          <div class="page-sub">All errors and exceptions that have occurred in this session</div>
          <div class="flex-row" style="margin-bottom:16px">
            <div id="exc-count" class="badge br">0 exceptions</div>
            <button class="btn btn-sm" style="background:var(--card2);color:var(--txt2);border:1px solid var(--border);margin-left:auto" onclick="clearExceptions()">Clear Log</button>
          </div>
          <div id="exc-list">
            <div class="empty-state"><span class="es-ico">✅</span><p>No exceptions</p><span>All operations completed successfully</span></div>
          </div>
        </div>
      </div>

      <!-- ════ MY BOOKINGS (employer) ════ -->
      <div class="page" id="p-my-bookings">
        <div style="padding:24px">
          <div class="page-title">My Bookings</div>
          <div class="page-sub">Your personal booking history and active jobs</div>
          <div class="filter-bar">
            <span class="filter-chip active" onclick="filterMyBookings('all',this)">All</span>
            <span class="filter-chip" onclick="filterMyBookings('pending',this)">Pending</span>
            <span class="filter-chip" onclick="filterMyBookings('active',this)">Active</span>
            <span class="filter-chip" onclick="filterMyBookings('completed',this)">Completed</span>
            <span class="filter-chip" onclick="filterMyBookings('cancelled',this)">Cancelled</span>
            <button class="btn btn-g btn-sm" onclick="openNewBookingModal()" style="margin-left:auto">+ Book a Worker</button>
          </div>
          <div class="card">
            <div class="table-wrap"><table>
              <thead><tr><th>ID</th><th>Worker</th><th>Service</th><th>Amount</th><th>Start</th><th>End</th><th>Address</th><th>Status</th><th>Actions</th></tr></thead>
              <tbody id="my-bookings-tbody"></tbody>
            </table></div>
          </div>
        </div>
      </div>

      <!-- ════ SEARCH WORKERS (employer) ════ -->
      <div class="page" id="p-search">
        <div style="padding:24px">
          <div class="page-title">Find a Worker</div>
          <div class="page-sub">Search and browse all verified workers near you</div>
          <div class="filter-bar">
            <input class="search-input" id="s-query" placeholder="Name, category, city..." oninput="renderSearch()">
            <select class="search-input" id="s-sort" onchange="renderSearch()" style="flex:0;width:170px">
              <option value="rating">Top Rated First</option>
              <option value="price_low">Lowest Price</option>
              <option value="price_high">Highest Price</option>
              <option value="jobs">Most Jobs Done</option>
            </select>
          </div>
          <div id="search-chips" class="filter-bar" style="margin-top:-6px"></div>
          <div id="search-results" style="display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:14px"></div>
        </div>
      </div>

      <!-- ════ WALLET (employer) ════ -->
      <div class="page" id="p-wallet">
        <div style="padding:24px">
          <div class="page-title">My Wallet</div>
          <div class="page-sub">Manage your Aetbar wallet balance and transactions</div>
          <div class="two-col" style="margin-bottom:18px">
            <div style="background:linear-gradient(135deg,var(--gd),var(--g));border-radius:18px;padding:24px;color:#fff;box-shadow:0 8px 28px rgba(29,158,117,.3)">
              <div style="font-size:10px;opacity:.7;font-weight:700;letter-spacing:.8px;text-transform:uppercase">AETBAR WALLET</div>
              <div id="wallet-bal" style="font-size:34px;font-weight:800;margin:8px 0;letter-spacing:-1px">Rs 0</div>
              <div style="font-size:12px;opacity:.7" id="wallet-user">Available balance</div>
              <div style="display:flex;gap:10px;margin-top:16px">
                <button class="btn" style="background:rgba(255,255,255,.2);color:#fff;border:1px solid rgba(255,255,255,.3);font-size:12px;padding:8px 16px" onclick="openTopupModal()">+ Add Money</button>
              </div>
            </div>
            <div class="card" style="margin:0">
              <div class="card-header"><h3>Quick Stats</h3></div>
              <div class="card-body" id="wallet-stats" style="display:grid;gap:12px"></div>
            </div>
          </div>
          <div class="card">
            <div class="card-header"><h3>Transaction History</h3></div>
            <div class="table-wrap"><table>
              <thead><tr><th>Booking ID</th><th>Service</th><th>Amount</th><th>Payment Method</th><th>Status</th><th>Date</th></tr></thead>
              <tbody id="txn-tbody"></tbody>
            </table></div>
          </div>
        </div>
      </div>

      <!-- ════ PROFILE ════ -->
      <div class="page" id="p-profile">
        <div style="padding:24px">
          <div class="page-title">My Profile</div>
          <div class="page-sub">Your account information and settings</div>
          <div class="two-col">
            <div class="card" style="margin:0">
              <div class="card-header"><h3>Account Details</h3><button class="btn btn-sm btn-o" onclick="openChangePassModal()">Change Password</button></div>
              <div class="card-body" id="profile-details"></div>
            </div>
            <div class="card" style="margin:0">
              <div class="card-header"><h3>Booking Summary</h3></div>
              <div class="card-body" id="profile-stats"></div>
            </div>
          </div>
        </div>
      </div>

    </div><!-- end content -->
  </main>
</div><!-- end app-shell -->

<!-- ════════════════════════════════════════════════════════════
  MODALS
════════════════════════════════════════════════════════════ -->

<!-- Add Worker Modal -->
<div class="overlay" id="m-add-worker">
  <div class="modal">
    <div class="modal-header"><h3>Add New Worker</h3><button class="modal-close" onclick="closeModal('m-add-worker')">✕</button></div>
    <div class="modal-body">
      <div id="aw-alert"></div>
      <div class="form-grid">
        <div class="form-group"><label class="flabel">Full Name</label><input class="finput" id="aw-name" placeholder="Worker full name"></div>
        <div class="form-group"><label class="flabel">Category</label>
          <select class="finput" id="aw-cat"><option>Maid</option><option>Cook</option><option>Electrician</option><option>Plumber</option><option>Security</option><option>Labourer</option><option>Carpenter</option><option>Painter</option><option>Baby Sitter</option><option>Clothes</option></select>
        </div>
        <div class="form-group"><label class="flabel">City</label><input class="finput" id="aw-city" placeholder="e.g. Islamabad"></div>
        <div class="form-group"><label class="flabel">Area / Sector</label><input class="finput" id="aw-area" placeholder="e.g. G-10"></div>
        <div class="form-group"><label class="flabel">Phone Number</label><input class="finput" id="aw-phone" placeholder="03XXXXXXXXX" type="tel"></div>
        <div class="form-group"><label class="flabel">Daily Rate (Rs)</label><input class="finput" id="aw-rate" placeholder="e.g. 800" type="number"></div>
      </div>
      <div class="alert alert-a" style="margin-top:10px"><span>⚠️</span><div>New workers start as <strong>Pending Verification</strong>. Go to Verification Queue to approve them.</div></div>
    </div>
    <div class="modal-footer"><button class="btn btn-o" onclick="closeModal('m-add-worker')">Cancel</button><button class="btn btn-g" onclick="doAddWorker()">Add Worker</button></div>
  </div>
</div>

<!-- Booking Detail Modal -->
<div class="overlay" id="m-booking-detail">
  <div class="modal" style="max-width:600px">
    <div class="modal-header"><h3 id="bd-title">Booking Details</h3><button class="modal-close" onclick="closeModal('m-booking-detail')">✕</button></div>
    <div class="modal-body" id="bd-body"></div>
    <div class="modal-footer" id="bd-footer"></div>
  </div>
</div>

<!-- New Booking Modal -->
<div class="overlay" id="m-new-booking">
  <div class="modal" style="max-width:580px">
    <div class="modal-header"><h3>Book a Worker</h3><button class="modal-close" onclick="closeModal('m-new-booking')">✕</button></div>
    <div class="modal-body">
      <div id="nb-alert"></div>
      <div class="form-grid">
        <div class="form-group full"><label class="flabel">Select Worker</label>
          <select class="finput" id="nb-worker" onchange="updateBookingPrice()">
            <option value="">-- Choose a worker --</option>
          </select>
        </div>
        <div class="form-group"><label class="flabel">Package</label>
          <select class="finput" id="nb-pkg" onchange="updateBookingPrice()">
            <option value="Daily">Daily</option>
            <option value="Weekly">Weekly (30% off)</option>
            <option value="Monthly">Monthly (42% off)</option>
          </select>
        </div>
        <div class="form-group"><label class="flabel">Payment Method</label>
          <select class="finput" id="nb-pay">
            <option>Easypaisa</option><option>JazzCash</option>
            <option>Cash</option><option>Wallet</option>
          </select>
        </div>
        <div class="form-group"><label class="flabel">Start Date (DD-MM-YYYY)</label><input class="finput" id="nb-start" placeholder="25-01-2025"></div>
        <div class="form-group"><label class="flabel">End Date (DD-MM-YYYY)</label><input class="finput" id="nb-end" placeholder="31-01-2025"></div>
        <div class="form-group full"><label class="flabel">Full Address</label><input class="finput" id="nb-addr" placeholder="House no., Street, Sector, City"></div>
        <div class="form-group full"><label class="flabel">Special Notes</label><textarea class="finput" id="nb-notes" placeholder="Any special instructions for the worker..."></textarea></div>
      </div>
      <div id="nb-price-box" style="background:var(--card2);border:1px solid var(--border);border-radius:10px;padding:14px;margin-top:10px;display:flex;justify-content:space-between;align-items:center">
        <span style="font-size:13px;color:var(--txt2)">Estimated Total:</span>
        <span id="nb-price" style="font-size:20px;font-weight:800;color:var(--g)">Rs —</span>
      </div>
    </div>
    <div class="modal-footer"><button class="btn btn-o" onclick="closeModal('m-new-booking')">Cancel</button><button class="btn btn-g" onclick="doNewBooking()">Confirm Booking</button></div>
  </div>
</div>

<!-- Top-up Modal -->
<div class="overlay" id="m-topup">
  <div class="modal" style="max-width:400px">
    <div class="modal-header"><h3>Add Money to Wallet</h3><button class="modal-close" onclick="closeModal('m-topup')">✕</button></div>
    <div class="modal-body">
      <div id="tu-alert"></div>
      <div class="form-group" style="margin-bottom:14px"><label class="flabel">Amount (Rs)</label><input class="finput" id="tu-amount" placeholder="Minimum Rs 100" type="number" min="100"></div>
      <div class="form-group"><label class="flabel">Payment Method</label>
        <select class="finput" id="tu-method"><option>Easypaisa</option><option>JazzCash</option><option>Bank Transfer</option></select>
      </div>
      <div class="alert alert-a" style="margin-top:12px"><span>📱</span><div>Send to Aetbar Easypaisa: <strong>0331-5506907</strong> then enter amount above.</div></div>
    </div>
    <div class="modal-footer"><button class="btn btn-o" onclick="closeModal('m-topup')">Cancel</button><button class="btn btn-g" onclick="doTopup()">Add Money</button></div>
  </div>
</div>

<!-- Change Password Modal -->
<div class="overlay" id="m-change-pass">
  <div class="modal" style="max-width:400px">
    <div class="modal-header"><h3>Change Password</h3><button class="modal-close" onclick="closeModal('m-change-pass')">✕</button></div>
    <div class="modal-body">
      <div id="cp-alert"></div>
      <div class="form-group" style="margin-bottom:14px"><label class="flabel">Current Password</label><input class="finput" id="cp-old" type="password" placeholder="Current password"></div>
      <div class="form-group"><label class="flabel">New Password</label><input class="finput" id="cp-new" type="password" placeholder="Minimum 4 characters"></div>
    </div>
    <div class="modal-footer"><button class="btn btn-o" onclick="closeModal('m-change-pass')">Cancel</button><button class="btn btn-g" onclick="doChangePass()">Update Password</button></div>
  </div>
</div>

<!-- Worker Profile Modal -->
<div class="overlay" id="m-worker-profile">
  <div class="modal" style="max-width:500px">
    <div class="modal-header"><h3 id="wp-title">Worker Profile</h3><button class="modal-close" onclick="closeModal('m-worker-profile')">✕</button></div>
    <div class="modal-body" id="wp-body"></div>
    <div class="modal-footer" id="wp-footer"></div>
  </div>
</div>

<script>
// ════════════════════════════════════════════════════════════
//  DATABASE  — localStorage (mirrors C++ CSV files)
// ════════════════════════════════════════════════════════════
const DB = {
  get: k => { try { return JSON.parse(localStorage.getItem('aetbar_gui_'+k)) } catch { return null } },
  set: (k,v) => localStorage.setItem('aetbar_gui_'+k, JSON.stringify(v)),
  getWorkers()  { return this.get('workers')  || [] },
  getUsers()    { return this.get('users')    || [] },
  getBookings() { return this.get('bookings') || [] },
  setWorkers(v) { this.set('workers',v) },
  setUsers(v)   { this.set('users',v) },
  setBookings(v){ this.set('bookings',v) }
};

// ════════════════════════════════════════════════════════════
//  EXCEPTION LOG  (mirrors C++ exception system)
// ════════════════════════════════════════════════════════════
const ExceptionLog = {
  entries: [],
  log(type, message, context='') {
    const entry = { type, message, context, time: new Date().toLocaleTimeString() };
    this.entries.unshift(entry);
    if (this.entries.length > 100) this.entries.pop();
    updateExceptionBadge();
  },
  clear() { this.entries = []; updateExceptionBadge(); }
};

// Exception classes (mirrors C++ classes)
class AetbarException extends Error {
  constructor(msg) { super(msg); this.name = 'AetbarException'; }
}
class InvalidCredentialsException extends AetbarException {
  constructor() { super('Invalid phone number or password. Please try again.'); this.name = 'InvalidCredentialsException'; }
}
class DuplicatePhoneException extends AetbarException {
  constructor(phone) { super(`Phone ${phone} is already registered.`); this.name = 'DuplicatePhoneException'; }
}
class ValidationException extends AetbarException {
  constructor(field, reason) { super(`Validation error — ${field}: ${reason}`); this.name = 'ValidationException'; }
}
class InsufficientBalanceException extends AetbarException {
  constructor(needed, available) { super(`Insufficient balance. Need Rs ${needed}, have Rs ${available}.`); this.name = 'InsufficientBalanceException'; }
}
class WorkerNotFoundException extends AetbarException {
  constructor(id) { super(`Worker ID ${id} not found.`); this.name = 'WorkerNotFoundException'; }
}
class WorkerNotVerifiedException extends AetbarException {
  constructor(name) { super(`Worker '${name}' is not verified. Only verified workers can be booked.`); this.name = 'WorkerNotVerifiedException'; }
}
class WorkerUnavailableException extends AetbarException {
  constructor(name) { super(`Worker '${name}' is currently unavailable.`); this.name = 'WorkerUnavailableException'; }
}
class InvalidDateException extends AetbarException {
  constructor(date) { super(`Invalid date '${date}'. Use DD-MM-YYYY format e.g. 25-01-2025`); this.name = 'InvalidDateException'; }
}
class InvalidBookingActionException extends AetbarException {
  constructor(action, status) { super(`Cannot ${action} a booking that is already '${status}'.`); this.name = 'InvalidBookingActionException'; }
}
class UnauthorizedException extends AetbarException {
  constructor() { super('Admin privileges required for this action.'); this.name = 'UnauthorizedException'; }
}
class BookingNotFoundException extends AetbarException {
  constructor(id) { super(`Booking ID ${id} not found.`); this.name = 'BookingNotFoundException'; }
}

// Validation helpers (mirrors C++ validate functions)
function validateDate(date) {
  if (!date || date.length !== 10) throw new InvalidDateException(date || '(empty)');
  const parts = date.split('-');
  if (parts.length !== 3) throw new InvalidDateException(date);
  const [d,m,y] = parts.map(Number);
  if (d<1||d>31||m<1||m>12||y<2024||y>2030) throw new InvalidDateException(date);
  return true;
}
function validatePhone(phone) {
  const clean = phone.replace(/-/g,'').trim();
  if (clean.length !== 11 || clean[0] !== '0' || !/^\d+$/.test(clean))
    throw new ValidationException('phone','Must be 11 digits starting with 0');
  return clean;
}
function validateRequired(value, field, minLen=1) {
  if (!value || value.trim().length < minLen)
    throw new ValidationException(field, `Must be at least ${minLen} character(s)`);
  return value.trim();
}
function validateNumber(value, field, min=0) {
  const n = parseFloat(value);
  if (isNaN(n) || n < min)
    throw new ValidationException(field, `Must be a number of at least ${min}`);
  return n;
}

// ════════════════════════════════════════════════════════════
//  SEED DATA  (same as C++ seed)
// ════════════════════════════════════════════════════════════
function today() {
  const d = new Date();
  const dd = String(d.getDate()).padStart(2,'0');
  const mm = String(d.getMonth()+1).padStart(2,'0');
  return `${dd}-${mm}-${d.getFullYear()}`;
}

const SEED_WORKERS = [
  {id:1,name:'Fatima Khan',  category:'Maid',       city:'Islamabad',area:'G-10',phone:'03119876543',dailyRate:800, rating:4.9,totalJobs:87, verified:true, available:true, joinDate:'15-01-2025'},
  {id:2,name:'Muhammad Ali', category:'Cook',       city:'Islamabad',area:'G-11',phone:'03211112222',dailyRate:1200,rating:4.8,totalJobs:63, verified:true, available:true, joinDate:'15-01-2025'},
  {id:3,name:'Zahid Butt',   category:'Electrician',city:'Islamabad',area:'F-7', phone:'03334445566',dailyRate:2000,rating:4.7,totalJobs:44, verified:true, available:false,joinDate:'15-01-2025'},
  {id:4,name:'Rukhsana Naz', category:'Clothes',    city:'Islamabad',area:'G-9', phone:'03005556677',dailyRate:600, rating:5.0,totalJobs:29, verified:true, available:true, joinDate:'15-01-2025'},
  {id:5,name:'Imran Haider', category:'Security',   city:'Islamabad',area:'I-8', phone:'03123334444',dailyRate:1500,rating:4.6,totalJobs:18, verified:true, available:true, joinDate:'15-01-2025'},
  {id:6,name:'Saba Begum',   category:'Maid',       city:'Lahore',   area:'DHA', phone:'03458889999',dailyRate:900, rating:4.8,totalJobs:120,verified:true, available:true, joinDate:'15-01-2025'},
  {id:7,name:'Asif Khan',    category:'Plumber',    city:'Islamabad',area:'F-8', phone:'03007778888',dailyRate:1800,rating:4.5,totalJobs:32, verified:true, available:true, joinDate:'15-01-2025'},
  {id:8,name:'Tariq Mehmood',category:'Labourer',   city:'Islamabad',area:'G-7', phone:'03219990000',dailyRate:700, rating:4.4,totalJobs:21, verified:true, available:true, joinDate:'15-01-2025'},
  {id:9,name:'Khalid Rehman',category:'Carpenter',  city:'Islamabad',area:'I-10',phone:'03451231234',dailyRate:1600,rating:4.6,totalJobs:38, verified:true, available:false,joinDate:'15-01-2025'},
  {id:10,name:'Shakeel Ahmed',category:'Painter',   city:'Islamabad',area:'G-13',phone:'03009876543',dailyRate:1400,rating:4.5,totalJobs:27, verified:true, available:true, joinDate:'15-01-2025'},
  {id:11,name:'Amna Bibi',   category:'Baby Sitter',city:'Islamabad',area:'F-6', phone:'03116543210',dailyRate:900, rating:4.8,totalJobs:15, verified:true, available:false,joinDate:'15-01-2025'},
  {id:12,name:'Nadia Iqbal', category:'Maid',       city:'Islamabad',area:'I-8', phone:'03005550000',dailyRate:700, rating:0,  totalJobs:0,  verified:false,available:true, joinDate:today()},
];
const SEED_USERS = [
  {id:1,name:'Ahmed Raza',phone:'03001234567',password:'1234',    role:'employer',city:'Islamabad',area:'G-10',walletBalance:5200,joinDate:'15-01-2025'},
  {id:2,name:'Admin',     phone:'admin',       password:'admin123',role:'admin',   city:'Islamabad',area:'F-7', walletBalance:0,   joinDate:'15-01-2025'},
];
const SEED_BOOKINGS = [
  {id:1001,employerId:1,workerId:1,workerName:'Fatima Khan',  service:'Maid - Fatima Khan',   packageType:'Monthly',amount:3200, status:'active',   bookingDate:'15-01-2025',startDate:'17-01-2025',endDate:'16-02-2025',address:'G-10/3, Street 12, Islamabad',  notes:'Focus on kitchen and bathrooms',paymentMethod:'Wallet'},
  {id:1002,employerId:1,workerId:2,workerName:'Muhammad Ali', service:'Cook - Muhammad Ali',   packageType:'Monthly',amount:28000,status:'active',   bookingDate:'15-01-2025',startDate:'17-01-2025',endDate:'16-02-2025',address:'G-10/3, Street 12, Islamabad',  notes:'Lunch and dinner daily',        paymentMethod:'Easypaisa'},
  {id:1003,employerId:1,workerId:3,workerName:'Zahid Butt',   service:'Electrician - Zahid',  packageType:'Daily',  amount:2000, status:'completed', bookingDate:'28-12-2024',startDate:'28-12-2024',endDate:'28-12-2024',address:'G-10/3, Street 12, Islamabad',  notes:'Fan installation in 3 rooms',   paymentMethod:'JazzCash'},
  {id:1004,employerId:1,workerId:5,workerName:'Imran Haider', service:'Security - Imran',     packageType:'Daily',  amount:1500, status:'pending',   bookingDate:today(),     startDate:'25-01-2025',endDate:'25-01-2025',address:'G-10/3, Street 12, Islamabad',  notes:'Night guard duty 10pm-6am',     paymentMethod:'Cash'},
];

function initSeedData() {
  if (!DB.getWorkers().length)  DB.setWorkers(SEED_WORKERS);
  if (!DB.getUsers().length)    DB.setUsers(SEED_USERS);
  if (!DB.getBookings().length) DB.setBookings(SEED_BOOKINGS);
}

// ════════════════════════════════════════════════════════════
//  APP STATE
// ════════════════════════════════════════════════════════════
let appState = {
  user: null,
  myBookingFilter: 'all',
  nextWorkerId: 20,
  nextBookingId: 2000,
};

// ════════════════════════════════════════════════════════════
//  TOAST
// ════════════════════════════════════════════════════════════
function toast(msg, type='success') {
  const el = document.getElementById('toast');
  const icons = {success:'✅',error:'❌',info:'ℹ️',warn:'⚠️'};
  el.innerHTML = `<span>${icons[type]||'ℹ️'}</span><span>${msg}</span>`;
  el.className = `toast show ${type}`;
  setTimeout(() => el.classList.remove('show'), 3500);
}

// ════════════════════════════════════════════════════════════
//  MODAL
// ════════════════════════════════════════════════════════════
function openModal(id)  { document.getElementById(id).classList.add('open') }
function closeModal(id) { document.getElementById(id).classList.remove('open') }

// ════════════════════════════════════════════════════════════
//  NAVIGATION
// ════════════════════════════════════════════════════════════
function goTo(pageId) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  document.getElementById(pageId)?.classList.add('active');
  document.querySelectorAll('.nav-item').forEach(n => {
    if (n.dataset.page === pageId) n.classList.add('active');
  });
  // Update topbar title
  const titles = {
    'p-dashboard':'Dashboard','p-workers':'Workers','p-bookings':'All Bookings',
    'p-users':'Users','p-verify':'Verification Queue','p-exceptions':'Exception Log',
    'p-my-bookings':'My Bookings','p-search':'Search Workers',
    'p-wallet':'My Wallet','p-profile':'My Profile',
  };
  document.getElementById('page-title').textContent = titles[pageId] || 'Aetbar';
  // Render page data
  const renders = {
    'p-dashboard': renderDashboard,
    'p-workers':   renderWorkers,
    'p-bookings':  renderBookings,
    'p-users':     renderUsers,
    'p-verify':    renderVerify,
    'p-exceptions':renderExceptions,
    'p-my-bookings':renderMyBookings,
    'p-search':    renderSearch,
    'p-wallet':    renderWallet,
    'p-profile':   renderProfile,
  };
  if (renders[pageId]) renders[pageId]();
}

function buildNav() {
  const nav = document.getElementById('sidebar-nav');
  const isAdmin = appState.user?.role === 'admin';

  const adminItems = [
    {section:'Overview'},
    {page:'p-dashboard', icon:'📊', label:'Dashboard'},
    {section:'Workers & Users'},
    {page:'p-workers',   icon:'👷', label:'Workers',    badge:() => DB.getWorkers().filter(w=>!w.verified).length, badgeType:'red'},
    {page:'p-bookings',  icon:'📅', label:'All Bookings'},
    {page:'p-users',     icon:'👥', label:'Users'},
    {page:'p-verify',    icon:'🛡️', label:'Verification', badge:() => DB.getWorkers().filter(w=>!w.verified).length, badgeType:'red'},
    {section:'System'},
    {page:'p-exceptions',icon:'⚡', label:'Exception Log', badge:() => ExceptionLog.entries.length, badgeType:'red'},
    {page:'p-profile',   icon:'👤', label:'My Profile'},
  ];

  const employerItems = [
    {section:'Main'},
    {page:'p-dashboard',   icon:'📊', label:'Dashboard'},
    {page:'p-search',      icon:'🔍', label:'Find Workers'},
    {page:'p-my-bookings', icon:'📅', label:'My Bookings', badge:() => DB.getBookings().filter(b=>b.employerId===appState.user.id&&b.status==='pending').length, badgeType:'amber'},
    {section:'Account'},
    {page:'p-wallet',      icon:'💰', label:'My Wallet'},
    {page:'p-profile',     icon:'👤', label:'My Profile'},
    {section:'Dev Info'},
    {page:'p-exceptions',  icon:'⚡', label:'Exception Log'},
  ];

  const items = isAdmin ? adminItems : employerItems;
  nav.innerHTML = items.map(item => {
    if (item.section) return `<div class="nav-section">${item.section}</div>`;
    const badgeCount = item.badge ? item.badge() : 0;
    const badgeHtml = badgeCount > 0
      ? `<span class="nav-badge ${item.badgeType||'red'}">${badgeCount}</span>`
      : '';
    return `<div class="nav-item" data-page="${item.page}" onclick="goTo('${item.page}')">
      <span class="ni">${item.icon}</span>${item.label}${badgeHtml}
    </div>`;
  }).join('');
}

function updateExceptionBadge() {
  const count = ExceptionLog.entries.length;
  document.querySelectorAll('.nav-item').forEach(n => {
    if (n.dataset.page === 'p-exceptions') {
      const old = n.querySelector('.nav-badge');
      if (old) old.remove();
      if (count > 0) {
        n.insertAdjacentHTML('beforeend', `<span class="nav-badge">${count}</span>`);
      }
    }
  });
}

// ════════════════════════════════════════════════════════════
//  AUTH
// ════════════════════════════════════════════════════════════
function doLogin() {
  const phone = document.getElementById('li-phone').value.trim().replace(/-/g,'');
  const pass  = document.getElementById('li-pass').value.trim();
  const alertEl = document.getElementById('login-alert');
  alertEl.innerHTML = '';

  try {
    if (!phone) throw new ValidationException('phone', 'Cannot be empty');
    if (!pass)  throw new ValidationException('password', 'Cannot be empty');

    const users = DB.getUsers();
    const user  = users.find(u => u.phone === phone && u.password === pass);
    if (!user) throw new InvalidCredentialsException();

    appState.user = user;
    ExceptionLog.log('INFO', 'Login successful: ' + user.name, 'Auth');

    // Update sidebar
    document.getElementById('sb-name').textContent  = user.name;
    document.getElementById('sb-role').textContent  = user.role.charAt(0).toUpperCase() + user.role.slice(1);

    // Date
    document.getElementById('tb-date').textContent = today();

    // Build nav & switch to app
    buildNav();
    document.getElementById('login-screen').style.display = 'none';
    document.getElementById('app-shell').style.display    = 'flex';
    goTo('p-dashboard');
    toast(`Welcome back, ${user.name}! 👋`);

  } catch(e) {
    ExceptionLog.log(e.name || 'Exception', e.message, 'Auth → Login');
    alertEl.innerHTML = `<div class="alert alert-r"><span>❌</span><div>${e.message}</div></div>`;
  }
}

function doLogout() {
  appState.user = null;
  document.getElementById('app-shell').style.display   = 'none';
  document.getElementById('login-screen').style.display = 'flex';
  document.getElementById('li-phone').value = '';
  document.getElementById('li-pass').value  = '';
  toast('Logged out successfully', 'info');
}

// ════════════════════════════════════════════════════════════
//  LOAD DATA (reads localStorage — refreshable)
// ════════════════════════════════════════════════════════════
function loadData() {
  buildNav();
  const active = document.querySelector('.page.active');
  if (active) {
    const renders = {
      'p-dashboard':renderDashboard,'p-workers':renderWorkers,
      'p-bookings':renderBookings,'p-users':renderUsers,
      'p-verify':renderVerify,'p-exceptions':renderExceptions,
      'p-my-bookings':renderMyBookings,'p-search':renderSearch,
      'p-wallet':renderWallet,'p-profile':renderProfile,
    };
    if (renders[active.id]) renders[active.id]();
  }
}

// ════════════════════════════════════════════════════════════
//  AVATAR COLOR
// ════════════════════════════════════════════════════════════
const AV_COLORS = [
  ['rgba(29,158,117,.25)','#4ADE80'],['rgba(239,159,39,.25)','#FCD34D'],
  ['rgba(55,138,221,.25)','#93C5FD'],['rgba(236,72,153,.25)','#F9A8D4'],
  ['rgba(124,58,237,.25)','#C4B5FD'],['rgba(14,165,233,.25)','#67E8F9'],
];
function avColor(id) { return AV_COLORS[id % AV_COLORS.length] }
function avHtml(w, size=32) {
  const [bg, fg] = avColor(w.id);
  const initials = w.name.split(' ').map(x=>x[0]).join('').toUpperCase().slice(0,2);
  return `<div class="wkav" style="width:${size}px;height:${size}px;background:${bg};color:${fg};font-size:${size*.32}px">${initials}</div>`;
}

// ════════════════════════════════════════════════════════════
//  BADGE HELPERS
// ════════════════════════════════════════════════════════════
function statusBadge(s) {
  const map={active:'bg',completed:'ba',pending:'bb',cancelled:'br'};
  return `<span class="badge ${map[s]||'bw'}">${s}</span>`;
}
function verBadge(v) {
  return v ? '<span class="badge bg">✓ Verified</span>'
           : '<span class="badge br">⏳ Pending</span>';
}
function availBadge(a) {
  return a ? '<span class="badge bg">Available</span>'
           : '<span class="badge bw">Busy</span>';
}
function stars(r) {
  if (!r) return '<span style="color:var(--txt3);font-size:11px">Unrated</span>';
  return '<span style="color:#FCD34D;font-size:12px">' + '★'.repeat(Math.round(r)) + '</span> '
       + `<span style="font-size:11px;color:var(--txt2)">${r}</span>`;
}

// ════════════════════════════════════════════════════════════
//  DASHBOARD
// ════════════════════════════════════════════════════════════
function renderDashboard() {
  const workers  = DB.getWorkers();
  const users    = DB.getUsers();
  const bookings = DB.getBookings();
  const verified = workers.filter(w=>w.verified).length;
  const pending  = workers.filter(w=>!w.verified).length;
  const revenue  = bookings.filter(b=>b.status==='completed').reduce((s,b)=>s+b.amount*.1,0);

  document.getElementById('s-workers').textContent = workers.length;
  document.getElementById('s-verified').textContent = verified;
  document.getElementById('s-bookings').textContent = bookings.length;
  document.getElementById('s-users').textContent = users.length;

  const u = appState.user;
  document.getElementById('dash-welcome').textContent =
    `Welcome back, ${u.name}! Today is ${today()}. Platform revenue: Rs ${Math.round(revenue).toLocaleString()}`;

  // Recent bookings
  const recent = [...bookings].reverse().slice(0,6);
  document.getElementById('dash-bookings').innerHTML = recent.length
    ? recent.map(b => `<tr>
        <td><div style="display:flex;align-items:center;gap:8px">
          ${(() => { const w = workers.find(x=>x.id===b.workerId)||{}; return avHtml(w||{id:0,name:b.workerName||'?'},28) })()}
          <span>${b.workerName}</span></div></td>
        <td style="color:var(--txt2)">${b.service.split('-')[0].trim()}</td>
        <td style="color:var(--g);font-weight:700">Rs ${b.amount.toLocaleString()}</td>
        <td>${statusBadge(b.status)}</td>
      </tr>`).join('')
    : '<tr><td colspan="4" class="empty-state" style="padding:20px">No bookings yet</td></tr>';

  // Pending verifications
  const pendingW = workers.filter(w=>!w.verified);
  document.getElementById('pend-count').textContent = pending + ' pending';
  document.getElementById('dash-pending').innerHTML = pendingW.length
    ? pendingW.slice(0,4).map(w => `
      <div style="display:flex;align-items:center;gap:12px;padding:12px 18px;border-bottom:1px solid var(--border)">
        ${avHtml(w,36)}
        <div style="flex:1">
          <div style="font-size:13px;font-weight:700">${w.name}</div>
          <div style="font-size:11px;color:var(--txt2)">${w.category} · ${w.city}</div>
        </div>
        <button class="btn btn-g btn-sm" onclick="verifyWorker(${w.id})">✓ Verify</button>
      </div>`).join('')
    : '<div class="empty-state"><span class="es-ico">✅</span><p>All clear!</p><span>No pending verifications</span></div>';

  // Category chart
  const cats = {};
  workers.filter(w=>w.verified).forEach(w => cats[w.category] = (cats[w.category]||0)+1);
  const max = Math.max(...Object.values(cats), 1);
  const colors = ['var(--g)','var(--amb)','var(--blu)','var(--pur)','var(--red)','var(--teal)','var(--ora)','var(--pin)'];
  document.getElementById('cat-chart').innerHTML = Object.entries(cats)
    .sort((a,b)=>b[1]-a[1])
    .map(([cat,count], i) => `
    <div style="display:flex;align-items:center;gap:12px">
      <div style="font-size:12px;color:var(--txt2);width:110px">${cat}</div>
      <div class="prog-bar"><div class="prog-fill" style="width:${count/max*100}%;background:${colors[i%colors.length]}"></div></div>
      <div style="font-size:12px;font-weight:700;color:var(--txt);width:20px;text-align:right">${count}</div>
    </div>`).join('');
}

// ════════════════════════════════════════════════════════════
//  WORKERS
// ════════════════════════════════════════════════════════════
function renderWorkers() {
  const q      = (document.getElementById('w-search')?.value||'').toLowerCase();
  const cat    = document.getElementById('w-cat')?.value || '';
  const status = document.getElementById('w-status')?.value ?? '';

  let workers = DB.getWorkers().filter(w => {
    const mq = !q || w.name.toLowerCase().includes(q) || w.category.toLowerCase().includes(q) || w.city.toLowerCase().includes(q);
    const mc = !cat || w.category === cat;
    const ms = status === '' || String(w.verified ? 1 : 0) === status;
    return mq && mc && ms;
  });

  document.getElementById('workers-tbody').innerHTML = workers.length
    ? workers.map(w => `<tr>
        <td><div style="display:flex;align-items:center;gap:10px">${avHtml(w)}
          <div><div style="font-size:13px;font-weight:700">${w.name}</div>
          <div style="font-size:10px;color:var(--txt3)">ID #${w.id} · Since ${w.joinDate}</div></div></div></td>
        <td>${w.category}</td>
        <td>${w.city} / ${w.area}</td>
        <td style="color:var(--txt2)">${w.phone}</td>
        <td style="color:var(--g);font-weight:700">Rs ${w.dailyRate.toLocaleString()}</td>
        <td>${stars(w.rating)}</td>
        <td>${w.totalJobs}</td>
        <td>${verBadge(w.verified)} ${availBadge(w.available)}</td>
        <td>
          <div style="display:flex;gap:6px">
            <button class="btn btn-o btn-sm" onclick="openWorkerProfile(${w.id})">View</button>
            ${!w.verified ? `<button class="btn btn-g btn-sm" onclick="verifyWorker(${w.id})">✓ Verify</button>` : ''}
            <button class="btn btn-sm" style="background:rgba(255,255,255,.06);color:var(--txt2);border:1px solid var(--border)" onclick="toggleAvailability(${w.id})">${w.available?'Set Busy':'Set Free'}</button>
          </div>
        </td>
      </tr>`).join('')
    : '<tr><td colspan="9"><div class="empty-state" style="padding:32px"><span class="es-ico">🔍</span><p>No workers found</p></div></td></tr>';
}

function verifyWorker(id) {
  try {
    const workers = DB.getWorkers();
    const w = workers.find(x => x.id === id);
    if (!w) throw new WorkerNotFoundException(id);
    if (w.verified) { toast(`${w.name} is already verified`, 'warn'); return; }
    w.verified = true;
    DB.setWorkers(workers);
    ExceptionLog.log('INFO', `Worker '${w.name}' verified`, 'Admin → Verify');
    toast(`${w.name} is now verified! ✅`);
    buildNav();
    loadData();
  } catch(e) {
    ExceptionLog.log(e.name, e.message, 'Admin → Verify');
    toast(e.message, 'error');
  }
}

function toggleAvailability(id) {
  try {
    const workers = DB.getWorkers();
    const w = workers.find(x => x.id === id);
    if (!w) throw new WorkerNotFoundException(id);
    w.available = !w.available;
    DB.setWorkers(workers);
    ExceptionLog.log('INFO', `${w.name} set to ${w.available?'Available':'Busy'}`, 'Admin → Toggle');
    toast(`${w.name} is now ${w.available ? 'Available' : 'Busy'}`);
    renderWorkers();
  } catch(e) {
    ExceptionLog.log(e.name, e.message, 'Admin → ToggleAvail');
    toast(e.message, 'error');
  }
}

function openAddWorkerModal() {
  try {
    if (appState.user?.role !== 'admin') throw new UnauthorizedException();
    openModal('m-add-worker');
  } catch(e) {
    ExceptionLog.log(e.name, e.message, 'UI → openAddWorker');
    toast(e.message, 'error');
  }
}

function doAddWorker() {
  const alertEl = document.getElementById('aw-alert');
  alertEl.innerHTML = '';
  try {
    const name  = validateRequired(document.getElementById('aw-name').value, 'name', 3);
    const cat   = document.getElementById('aw-cat').value;
    const city  = validateRequired(document.getElementById('aw-city').value, 'city', 2);
    const area  = validateRequired(document.getElementById('aw-area').value, 'area', 2);
    const phone = validatePhone(document.getElementById('aw-phone').value);
    const rate  = validateNumber(document.getElementById('aw-rate').value, 'daily rate', 100);

    const workers = DB.getWorkers();
    const newW = {
      id: Math.max(...workers.map(w=>w.id), 0) + 1,
      name, category:cat, city, area, phone,
      dailyRate:rate, rating:0, totalJobs:0,
      verified:false, available:true, joinDate:today()
    };
    workers.push(newW);
    DB.setWorkers(workers);
    ExceptionLog.log('INFO', `Worker '${name}' added (pending verify)`, 'Admin → AddWorker');
    closeModal('m-add-worker');
    toast(`${name} added! Pending verification.`);
    buildNav();
    renderWorkers();
  } catch(e) {
    ExceptionLog.log(e.name, e.message, 'Admin → AddWorker');
    alertEl.innerHTML = `<div class="alert alert-r"><span>❌</span><div>${e.message}</div></div>`;
  }
}

function openWorkerProfile(id) {
  try {
    const workers = DB.getWorkers();
    const w = workers.find(x => x.id === id);
    if (!w) throw new WorkerNotFoundException(id);
    const [bg, fg] = avColor(w.id);
    const initials = w.name.split(' ').map(x=>x[0]).join('').toUpperCase().slice(0,2);
    document.getElementById('wp-title').textContent = w.name;
    document.getElementById('wp-body').innerHTML = `
      <div style="display:flex;align-items:center;gap:16px;margin-bottom:20px;padding:18px;background:linear-gradient(135deg,rgba(29,158,117,.15),rgba(14,165,233,.1));border-radius:12px;border:1px solid rgba(29,158,117,.2)">
        <div style="width:56px;height:56px;border-radius:50%;background:${bg};color:${fg};display:flex;align-items:center;justify-content:center;font-size:20px;font-weight:800;flex-shrink:0">${initials}</div>
        <div>
          <div style="font-size:17px;font-weight:800">${w.name}</div>
          <div style="font-size:12px;color:var(--txt2);margin-top:3px">${w.category} · ${w.city}, ${w.area}</div>
          <div style="margin-top:8px;display:flex;gap:6px">${verBadge(w.verified)} ${availBadge(w.available)}</div>
        </div>
      </div>
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;font-size:12px">
        ${[['📱 Phone',w.phone],['💰 Daily Rate','Rs '+w.dailyRate.toLocaleString()],['⭐ Rating',w.rating+' / 5.0'],['📋 Jobs Done',w.totalJobs],['🗓️ Member Since',w.joinDate],['📍 Location',w.city+', '+w.area]].map(([l,v])=>`
          <div style="background:var(--card2);border:1px solid var(--border);border-radius:9px;padding:10px">
            <div style="color:var(--txt3);font-size:10px;margin-bottom:3px">${l}</div>
            <div style="font-weight:700;color:var(--txt)">${v}</div>
          </div>`).join('')}
      </div>`;
    document.getElementById('wp-footer').innerHTML = `
      <button class="btn btn-o" onclick="closeModal('m-worker-profile')">Close</button>
      <button class="btn btn-g" onclick="closeModal('m-worker-profile');openNewBookingModal(${id})">Book This Worker</button>`;
    openModal('m-worker-profile');
  } catch(e) {
    ExceptionLog.log(e.name, e.message, 'UI → WorkerProfile');
    toast(e.message, 'error');
  }
}

// ════════════════════════════════════════════════════════════
//  BOOKINGS
// ════════════════════════════════════════════════════════════
function renderBookings() {
  const q      = (document.getElementById('b-search')?.value||'').toLowerCase();
  const status = document.getElementById('b-status')?.value || '';
  const workers = DB.getWorkers();

  let bks = DB.getBookings().filter(b => {
    const mq = !q || b.workerName.toLowerCase().includes(q) || b.service.toLowerCase().includes(q);
    const ms = !status || b.status === status;
    return mq && ms;
  });

  // Stats mini cards
  const all = DB.getBookings();
  const counts = {pending:0,active:0,completed:0,cancelled:0};
  const revenue = all.filter(b=>b.status==='completed').reduce((s,b)=>s+b.amount*.1,0);
  all.forEach(b => counts[b.status] = (counts[b.status]||0)+1);
  document.getElementById('booking-stats').innerHTML = [
    ['Total',all.length,'var(--txt)'],['Active',counts.active,'#4ADE80'],
    ['Completed',counts.completed,'#FCD34D'],['Revenue (10%)','Rs '+Math.round(revenue).toLocaleString(),'#93C5FD'],
  ].map(([l,v,c])=>`
    <div class="mini-card"><div class="mc-title">${l}</div><div class="mc-val" style="color:${c}">${v}</div></div>`).join('');

  document.getElementById('bookings-tbody').innerHTML = bks.length
    ? bks.map(b => {
        const w = workers.find(x=>x.id===b.workerId)||{id:0,name:b.workerName};
        return `<tr>
          <td><span style="font-weight:700;color:var(--g)">#${b.id}</span></td>
          <td><div style="display:flex;align-items:center;gap:8px">${avHtml(w,28)}<span>${b.workerName}</span></div></td>
          <td style="color:var(--txt2)">${b.service.split('-')[0].trim()}</td>
          <td><span class="badge bw">${b.packageType}</span></td>
          <td style="color:var(--g);font-weight:700">Rs ${b.amount.toLocaleString()}</td>
          <td style="color:var(--txt2)">${b.startDate}</td>
          <td style="color:var(--txt2)">${b.endDate}</td>
          <td>${statusBadge(b.status)}</td>
          <td><span class="badge bw">${b.paymentMethod}</span></td>
          <td><button class="btn btn-o btn-sm" onclick="openBookingDetail(${b.id})">Details</button></td>
        </tr>`;
      }).join('')
    : '<tr><td colspan="10"><div class="empty-state" style="padding:32px"><span class="es-ico">📅</span><p>No bookings found</p></div></td></tr>';
}

function openBookingDetail(id) {
  try {
    const bks = DB.getBookings();
    const b = bks.find(x => x.id === id);
    if (!b) throw new BookingNotFoundException(id);
    const workers = DB.getWorkers();
    const w = workers.find(x=>x.id===b.workerId)||{id:0,name:b.workerName};
    document.getElementById('bd-title').textContent = `Booking #${b.id}`;
    document.getElementById('bd-body').innerHTML = `
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;font-size:12px">
        ${[
          ['Worker',`<div style="display:flex;align-items:center;gap:8px">${avHtml(w,24)}<span>${b.workerName}</span></div>`],
          ['Service',b.service],['Package',`<span class="badge bw">${b.packageType}</span>`],
          ['Amount',`<span style="color:var(--g);font-weight:700">Rs ${b.amount.toLocaleString()}</span>`],
          ['Status',statusBadge(b.status)],['Payment',`<span class="badge bw">${b.paymentMethod}</span>`],
          ['Booked On',b.bookingDate],['Start Date',b.startDate],
          ['End Date',b.endDate],['Platform Fee','Rs '+Math.round(b.amount*.1).toLocaleString()],
        ].map(([l,v])=>`
          <div style="background:var(--card2);border:1px solid var(--border);border-radius:9px;padding:10px">
            <div style="color:var(--txt3);font-size:10px;margin-bottom:3px">${l}</div>
            <div style="font-weight:600">${v}</div>
          </div>`).join('')}
        <div style="grid-column:1/-1;background:var(--card2);border:1px solid var(--border);border-radius:9px;padding:10px">
          <div style="color:var(--txt3);font-size:10px;margin-bottom:3px">📍 Address</div>
          <div style="font-weight:600">${b.address}</div>
        </div>
        <div style="grid-column:1/-1;background:var(--card2);border:1px solid var(--border);border-radius:9px;padding:10px">
          <div style="color:var(--txt3);font-size:10px;margin-bottom:3px">📝 Notes</div>
          <div style="font-weight:600;color:var(--txt2)">${b.notes||'None'}</div>
        </div>
      </div>`;
    document.getElementById('bd-footer').innerHTML = `
      <button class="btn btn-o" onclick="closeModal('m-booking-detail')">Close</button>
      ${b.status==='pending'||b.status==='active' ? `<button class="btn btn-g btn-sm" onclick="updateBookingStatus(${b.id},'completed')">Mark Completed</button>` : ''}
      ${b.status!=='completed'&&b.status!=='cancelled' ? `<button class="btn btn-r btn-sm" onclick="updateBookingStatus(${b.id},'cancelled')">Cancel</button>` : ''}`;
    openModal('m-booking-detail');
  } catch(e) {
    ExceptionLog.log(e.name, e.message, 'UI → BookingDetail');
    toast(e.message, 'error');
  }
}

function updateBookingStatus(id, newStatus) {
  try {
    const bks = DB.getBookings();
    const b = bks.find(x => x.id === id);
    if (!b) throw new BookingNotFoundException(id);
    if (b.status === 'completed') throw new InvalidBookingActionException('change', 'completed');
    if (b.status === 'cancelled') throw new InvalidBookingActionException('change', 'cancelled');
    b.status = newStatus;
    if (newStatus === 'completed') {
      const workers = DB.getWorkers();
      const w = workers.find(x=>x.id===b.workerId);
      if (w) { w.totalJobs++; DB.setWorkers(workers); }
    }
    DB.setBookings(bks);
    ExceptionLog.log('INFO', `Booking #${id} → ${newStatus}`, 'BookingAction');
    closeModal('m-booking-detail');
    toast(`Booking #${id} marked as ${newStatus} ✅`);
    loadData();
  } catch(e) {
    ExceptionLog.log(e.name, e.message, 'BookingAction');
    toast(e.message, 'error');
  }
}

function openNewBookingModal(preselectedWorkerId = null) {
  try {
    const workers = DB.getWorkers().filter(w => w.verified && w.available);
    if (!workers.length) throw new AetbarException('No verified workers available right now.');
    const sel = document.getElementById('nb-worker');
    sel.innerHTML = '<option value="">-- Choose a worker --</option>' +
      workers.map(w => `<option value="${w.id}" data-rate="${w.dailyRate}" ${preselectedWorkerId===w.id?'selected':''}>${w.name} — ${w.category} — Rs ${w.dailyRate}/day</option>`).join('');
    if (preselectedWorkerId) updateBookingPrice();
    document.getElementById('nb-alert').innerHTML = '';
    openModal('m-new-booking');
  } catch(e) {
    ExceptionLog.log(e.name, e.message, 'UI → NewBooking');
    toast(e.message, 'error');
  }
}

function updateBookingPrice() {
  const sel = document.getElementById('nb-worker');
  const opt = sel.options[sel.selectedIndex];
  const rate = parseFloat(opt?.dataset?.rate || 0);
  const pkg  = document.getElementById('nb-pkg').value;
  let amount = rate;
  if (pkg === 'Weekly')  amount = Math.round(rate * 5 * 0.7);
  if (pkg === 'Monthly') amount = Math.round(rate * 22 * 0.58);
  document.getElementById('nb-price').textContent = rate ? `Rs ${amount.toLocaleString()}` : 'Rs —';
  return amount;
}

function doNewBooking() {
  const alertEl = document.getElementById('nb-alert');
  alertEl.innerHTML = '';
  try {
    const workerId = parseInt(document.getElementById('nb-worker').value);
    if (!workerId) throw new ValidationException('worker', 'Please select a worker');
    const workers = DB.getWorkers();
    const w = workers.find(x => x.id === workerId);
    if (!w) throw new WorkerNotFoundException(workerId);
    if (!w.verified)  throw new WorkerNotVerifiedException(w.name);
    if (!w.available) throw new WorkerUnavailableException(w.name);

    const pkg     = document.getElementById('nb-pkg').value;
    const pay     = document.getElementById('nb-pay').value;
    const start   = document.getElementById('nb-start').value.trim();
    const end     = document.getElementById('nb-end').value.trim();
    const addr    = validateRequired(document.getElementById('nb-addr').value, 'address', 10);
    const notes   = document.getElementById('nb-notes').value.trim() || 'None';

    validateDate(start);
    validateDate(end);

    const amount  = updateBookingPrice();

    // Check wallet if selected
    const users = DB.getUsers();
    const user  = users.find(u => u.id === appState.user.id);
    if (pay === 'Wallet' && user.walletBalance < amount)
      throw new InsufficientBalanceException(amount, user.walletBalance);

    const bks = DB.getBookings();
    const newId = Math.max(...bks.map(b=>b.id), 1000) + 1;
    bks.push({
      id: newId, employerId: appState.user.id,
      workerId, workerName: w.name,
      service: `${w.category} - ${w.name}`,
      packageType: pkg, amount, status: 'pending',
      bookingDate: today(), startDate: start, endDate: end,
      address: addr, notes, paymentMethod: pay,
    });
    DB.setBookings(bks);

    // Deduct wallet if chosen
    if (pay === 'Wallet') {
      user.walletBalance -= amount;
      appState.user.walletBalance = user.walletBalance;
      DB.setUsers(users);
    }

    ExceptionLog.log('INFO', `Booking #${newId} created for ${w.name}`, 'NewBooking');
    closeModal('m-new-booking');
    toast(`Booking #${newId} confirmed! Worker will respond in 24 hours ✅`);
    buildNav();
    loadData();
  } catch(e) {
    ExceptionLog.log(e.name, e.message, 'NewBooking');
    alertEl.innerHTML = `<div class="alert alert-r"><span>❌</span><div>${e.message}</div></div>`;
  }
}

// ════════════════════════════════════════════════════════════
//  USERS
// ════════════════════════════════════════════════════════════
function renderUsers() {
  try {
    if (appState.user?.role !== 'admin') throw new UnauthorizedException();
    const q = (document.getElementById('u-search')?.value||'').toLowerCase();
    const users = DB.getUsers().filter(u =>
      !q || u.name.toLowerCase().includes(q) || u.phone.includes(q)
    );
    const bks = DB.getBookings();
    document.getElementById('users-tbody').innerHTML = users.length
      ? users.map(u => {
          const ubks = bks.filter(b => b.employerId === u.id);
          return `<tr>
            <td style="color:var(--g);font-weight:700">#${u.id}</td>
            <td><div style="font-size:13px;font-weight:700">${u.name}</div></td>
            <td style="color:var(--txt2)">${u.phone}</td>
            <td style="color:var(--txt2)">${u.city||'—'} / ${u.area||'—'}</td>
            <td><span class="badge ${u.role==='admin'?'bpur':'bw'}">${u.role}</span></td>
            <td style="color:var(--g);font-weight:700">Rs ${(u.walletBalance||0).toLocaleString()}</td>
            <td style="color:var(--txt3)">${u.joinDate||'—'}</td>
            <td>${ubks.length}</td>
          </tr>`;
        }).join('')
      : '<tr><td colspan="8"><div class="empty-state" style="padding:32px">No users found</div></td></tr>';
  } catch(e) {
    ExceptionLog.log(e.name, e.message, 'renderUsers');
    document.getElementById('users-tbody').innerHTML = `<tr><td colspan="8"><div class="alert alert-r">${e.message}</div></td></tr>`;
  }
}

// ════════════════════════════════════════════════════════════
//  VERIFICATION QUEUE
// ════════════════════════════════════════════════════════════
function renderVerify() {
  try {
    if (appState.user?.role !== 'admin') throw new UnauthorizedException();
    const pending = DB.getWorkers().filter(w => !w.verified);
    document.getElementById('verify-list').innerHTML = pending.length
      ? pending.map(w => `
        <div class="card" style="margin-bottom:14px">
          <div class="card-body">
            <div style="display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:12px;margin-bottom:16px">
              <div style="display:flex;align-items:center;gap:14px">
                ${avHtml(w, 52)}
                <div>
                  <div style="font-size:16px;font-weight:800">${w.name}</div>
                  <div style="font-size:12px;color:var(--txt2);margin-top:3px">${w.category} · ${w.city}, ${w.area}</div>
                  <div style="font-size:11px;color:var(--txt3);margin-top:2px">Applied: ${w.joinDate} · Rs ${w.dailyRate}/day</div>
                </div>
              </div>
              <div style="display:flex;gap:10px">
                <button class="btn btn-g" onclick="verifyWorker(${w.id})">✓ Approve</button>
                <button class="btn btn-r" onclick="rejectWorker(${w.id})">✗ Reject</button>
              </div>
            </div>
            <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:8px">
              ${['🪪 CNIC Front','🪪 CNIC Back','🤳 Selfie Photo','📄 Police Cert'].map(d=>`
                <div style="background:var(--card2);border:1px solid var(--border);border-radius:10px;padding:16px;text-align:center;cursor:pointer;transition:border .15s" onmouseover="this.style.borderColor='var(--g)'" onmouseout="this.style.borderColor='var(--border)'">
                  <div style="font-size:28px;margin-bottom:6px">${d.split(' ')[0]}</div>
                  <div style="font-size:10px;color:var(--txt3)">${d.substring(3)}</div>
                </div>`).join('')}
            </div>
          </div>
        </div>`).join('')
      : '<div class="empty-state"><span class="es-ico">✅</span><p>All workers verified</p><span>No pending verifications</span></div>';
  } catch(e) {
    ExceptionLog.log(e.name, e.message, 'renderVerify');
    document.getElementById('verify-list').innerHTML = `<div class="alert alert-r">${e.message}</div>`;
  }
}

function rejectWorker(id) {
  try {
    const workers = DB.getWorkers();
    const w = workers.find(x => x.id === id);
    if (!w) throw new WorkerNotFoundException(id);
    const idx = workers.indexOf(w);
    workers.splice(idx, 1);
    DB.setWorkers(workers);
    ExceptionLog.log('INFO', `Worker '${w.name}' rejected and removed`, 'Admin → Reject');
    toast(`${w.name} rejected and removed from platform`, 'warn');
    buildNav();
    renderVerify();
  } catch(e) {
    ExceptionLog.log(e.name, e.message, 'Admin → Reject');
    toast(e.message, 'error');
  }
}

// ════════════════════════════════════════════════════════════
//  EXCEPTION LOG PAGE
// ════════════════════════════════════════════════════════════
function renderExceptions() {
  const entries = ExceptionLog.entries;
  document.getElementById('exc-count').textContent = `${entries.length} exception${entries.length!==1?'s':''}`;
  document.getElementById('exc-list').innerHTML = entries.length
    ? entries.map(e => `
      <div class="exc-item">
        <div class="exc-type">${e.type}</div>
        <div class="exc-msg">${e.message}</div>
        ${e.context ? `<div style="font-size:10px;color:var(--txt3);margin-top:3px">Context: ${e.context}</div>` : ''}
        <div class="exc-time">⏱ ${e.time}</div>
      </div>`).join('')
    : '<div class="empty-state"><span class="es-ico">✅</span><p>No exceptions</p><span>All operations completed successfully</span></div>';
}

function clearExceptions() {
  ExceptionLog.clear();
  renderExceptions();
  toast('Exception log cleared', 'info');
}

// ════════════════════════════════════════════════════════════
//  MY BOOKINGS (employer)
// ════════════════════════════════════════════════════════════
function filterMyBookings(filter, el) {
  appState.myBookingFilter = filter;
  document.querySelectorAll('#p-my-bookings .filter-chip').forEach(c => c.classList.remove('active'));
  el.classList.add('active');
  renderMyBookings();
}

function renderMyBookings() {
  const uid = appState.user?.id;
  const filter = appState.myBookingFilter;
  const workers = DB.getWorkers();
  let bks = DB.getBookings().filter(b => b.employerId === uid);
  if (filter !== 'all') bks = bks.filter(b => b.status === filter);
  document.getElementById('my-bookings-tbody').innerHTML = bks.length
    ? bks.map(b => {
        const w = workers.find(x=>x.id===b.workerId)||{id:0,name:b.workerName};
        return `<tr>
          <td style="color:var(--g);font-weight:700">#${b.id}</td>
          <td><div style="display:flex;align-items:center;gap:8px">${avHtml(w,28)}<span>${b.workerName}</span></div></td>
          <td style="color:var(--txt2)">${b.service.split('-')[0].trim()}</td>
          <td style="color:var(--g);font-weight:700">Rs ${b.amount.toLocaleString()}</td>
          <td style="color:var(--txt2)">${b.startDate}</td>
          <td style="color:var(--txt2)">${b.endDate}</td>
          <td style="color:var(--txt2);max-width:160px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis">${b.address}</td>
          <td>${statusBadge(b.status)}</td>
          <td>
            <div style="display:flex;gap:6px">
              <button class="btn btn-o btn-sm" onclick="openBookingDetail(${b.id})">Details</button>
              ${b.status==='pending'||b.status==='active' ? `<button class="btn btn-g btn-sm" onclick="updateBookingStatus(${b.id},'completed')">✓ Done</button>` : ''}
              ${b.status!=='completed'&&b.status!=='cancelled' ? `<button class="btn btn-r btn-sm" onclick="updateBookingStatus(${b.id},'cancelled')">Cancel</button>` : ''}
            </div>
          </td>
        </tr>`;
      }).join('')
    : '<tr><td colspan="9"><div class="empty-state" style="padding:32px"><span class="es-ico">📅</span><p>No bookings found</p><span>Use "Book a Worker" to get started</span></div></td></tr>';
}

// ════════════════════════════════════════════════════════════
//  SEARCH PAGE (employer)
// ════════════════════════════════════════════════════════════
function renderSearch() {
  const q    = (document.getElementById('s-query')?.value||'').toLowerCase();
  const sort = document.getElementById('s-sort')?.value || 'rating';

  // Category chips
  const cats = [...new Set(DB.getWorkers().map(w=>w.category))];
  const activeCat = document.querySelector('#search-chips .filter-chip.active');
  const curCat = activeCat ? activeCat.dataset.cat : '';
  document.getElementById('search-chips').innerHTML =
    ['', ...cats].map(c => `<span class="filter-chip ${c===curCat?'active':''}" data-cat="${c}" onclick="setSearchCat(this,'${c}')">${c||'All'}</span>`).join('');

  let workers = DB.getWorkers().filter(w => w.verified);
  if (curCat) workers = workers.filter(w => w.category === curCat);
  if (q) workers = workers.filter(w =>
    w.name.toLowerCase().includes(q) || w.category.toLowerCase().includes(q) || w.city.toLowerCase().includes(q)
  );
  if (sort==='rating')     workers.sort((a,b)=>b.rating-a.rating);
  if (sort==='price_low')  workers.sort((a,b)=>a.dailyRate-b.dailyRate);
  if (sort==='price_high') workers.sort((a,b)=>b.dailyRate-a.dailyRate);
  if (sort==='jobs')       workers.sort((a,b)=>b.totalJobs-a.totalJobs);

  const [bg0,fg0] = avColor(0);
  document.getElementById('search-results').innerHTML = workers.length
    ? workers.map(w => {
        const [bg,fg] = avColor(w.id);
        const initials = w.name.split(' ').map(x=>x[0]).join('').slice(0,2).toUpperCase();
        return `<div style="background:var(--card);border:1px solid var(--border);border-radius:16px;overflow:hidden;cursor:pointer;transition:all .2s" onmouseover="this.style.borderColor='var(--g)'" onmouseout="this.style.borderColor='var(--border)'">
          <div style="background:linear-gradient(135deg,rgba(29,158,117,.2),rgba(14,165,233,.1));padding:16px;display:flex;align-items:center;gap:12px;border-bottom:1px solid var(--border)">
            <div style="width:48px;height:48px;border-radius:50%;background:${bg};color:${fg};display:flex;align-items:center;justify-content:center;font-size:16px;font-weight:800">${initials}</div>
            <div style="flex:1">
              <div style="font-size:14px;font-weight:800">${w.name}</div>
              <div style="font-size:11px;color:var(--txt2);margin-top:2px">${w.category} · ${w.city}, ${w.area}</div>
              <div style="margin-top:5px">${verBadge(w.verified)} ${availBadge(w.available)}</div>
            </div>
          </div>
          <div style="padding:14px">
            <div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;margin-bottom:12px">
              <div style="text-align:center;background:var(--card2);border-radius:8px;padding:8px">
                <div style="font-size:14px;font-weight:800;color:var(--g)">Rs ${w.dailyRate.toLocaleString()}</div>
                <div style="font-size:9px;color:var(--txt3);margin-top:1px">Per day</div>
              </div>
              <div style="text-align:center;background:var(--card2);border-radius:8px;padding:8px">
                <div style="font-size:14px;font-weight:800;color:#FCD34D">${w.rating||'—'}</div>
                <div style="font-size:9px;color:var(--txt3);margin-top:1px">Rating</div>
              </div>
              <div style="text-align:center;background:var(--card2);border-radius:8px;padding:8px">
                <div style="font-size:14px;font-weight:800">${w.totalJobs}</div>
                <div style="font-size:9px;color:var(--txt3);margin-top:1px">Jobs</div>
              </div>
            </div>
            <div style="display:flex;gap:8px">
              <button class="btn btn-o btn-sm" style="flex:1;justify-content:center" onclick="openWorkerProfile(${w.id})">Profile</button>
              <button class="btn btn-g btn-sm" style="flex:1;justify-content:center" onclick="openNewBookingModal(${w.id})">Book Now</button>
            </div>
          </div>
        </div>`;
      }).join('')
    : '<div class="empty-state" style="grid-column:1/-1;padding:48px"><span class="es-ico">🔍</span><p>No workers found</p><span>Try a different search or category</span></div>';
}

function setSearchCat(el, cat) {
  document.querySelectorAll('#search-chips .filter-chip').forEach(c => c.classList.remove('active'));
  el.classList.add('active');
  renderSearch();
}

// ════════════════════════════════════════════════════════════
//  WALLET
// ════════════════════════════════════════════════════════════
function renderWallet() {
  const users = DB.getUsers();
  const user = users.find(u => u.id === appState.user.id) || appState.user;
  document.getElementById('wallet-bal').textContent = `Rs ${(user.walletBalance||0).toLocaleString()}`;
  document.getElementById('wallet-user').textContent = user.name + ' · ' + user.city;

  const myBks = DB.getBookings().filter(b => b.employerId === user.id);
  const spent = myBks.filter(b=>b.status==='completed').reduce((s,b)=>s+b.amount,0);
  document.getElementById('wallet-stats').innerHTML = [
    ['Total Bookings', myBks.length,'var(--g)'],
    ['Total Spent','Rs '+spent.toLocaleString(),'var(--red)'],
    ['Active Jobs', myBks.filter(b=>b.status==='active').length,'var(--amb)'],
  ].map(([l,v,c])=>`
    <div style="background:var(--card2);border:1px solid var(--border);border-radius:10px;padding:12px;display:flex;justify-content:space-between;align-items:center">
      <span style="font-size:12px;color:var(--txt2)">${l}</span>
      <span style="font-size:14px;font-weight:800;color:${c}">${v}</span>
    </div>`).join('');

  document.getElementById('txn-tbody').innerHTML = myBks.length
    ? myBks.map(b => `<tr>
        <td style="color:var(--g);font-weight:700">#${b.id}</td>
        <td style="color:var(--txt2)">${b.service.split('-')[0].trim()}</td>
        <td style="color:var(--red);font-weight:700">-Rs ${b.amount.toLocaleString()}</td>
        <td><span class="badge bw">${b.paymentMethod}</span></td>
        <td>${statusBadge(b.status)}</td>
        <td style="color:var(--txt3)">${b.bookingDate}</td>
      </tr>`).join('')
    : '<tr><td colspan="6"><div class="empty-state" style="padding:24px">No transactions yet</div></td></tr>';
}

function openTopupModal() { document.getElementById('tu-alert').innerHTML=''; openModal('m-topup'); }

function doTopup() {
  const alertEl = document.getElementById('tu-alert');
  alertEl.innerHTML = '';
  try {
    const amount = validateNumber(document.getElementById('tu-amount').value, 'amount', 100);
    const method = document.getElementById('tu-method').value;
    const users = DB.getUsers();
    const user = users.find(u => u.id === appState.user.id);
    if (!user) throw new AetbarException('User not found');
    user.walletBalance = (user.walletBalance || 0) + amount;
    appState.user.walletBalance = user.walletBalance;
    DB.setUsers(users);
    ExceptionLog.log('INFO', `Wallet top-up Rs ${amount} via ${method}`, 'Wallet');
    closeModal('m-topup');
    toast(`Rs ${amount.toLocaleString()} added via ${method} ✅`);
    renderWallet();
  } catch(e) {
    ExceptionLog.log(e.name, e.message, 'Wallet → Topup');
    alertEl.innerHTML = `<div class="alert alert-r"><span>❌</span><div>${e.message}</div></div>`;
  }
}

// ════════════════════════════════════════════════════════════
//  PROFILE
// ════════════════════════════════════════════════════════════
function renderProfile() {
  const users = DB.getUsers();
  const user = users.find(u => u.id === appState.user.id) || appState.user;
  const myBks = DB.getBookings().filter(b => b.employerId === user.id);
  const [bg, fg] = avColor(user.id);
  const initials = user.name.split(' ').map(x=>x[0]).join('').slice(0,2).toUpperCase();

  document.getElementById('profile-details').innerHTML = `
    <div style="display:flex;align-items:center;gap:16px;margin-bottom:20px;padding:18px;background:var(--card2);border-radius:12px;border:1px solid var(--border)">
      <div style="width:56px;height:56px;border-radius:50%;background:${bg};color:${fg};display:flex;align-items:center;justify-content:center;font-size:20px;font-weight:800">${initials}</div>
      <div>
        <div style="font-size:18px;font-weight:800">${user.name}</div>
        <div style="font-size:12px;color:var(--txt2);margin-top:3px">${user.phone}</div>
        <div style="margin-top:6px"><span class="badge ${user.role==='admin'?'bpur':'bw'}">${user.role}</span></div>
      </div>
    </div>
    ${[['📍 City / Area',user.city+' / '+(user.area||'—')],['💰 Wallet Balance','Rs '+(user.walletBalance||0).toLocaleString()],['📅 Member Since',user.joinDate||'—']].map(([l,v])=>`
    <div style="display:flex;justify-content:space-between;align-items:center;padding:11px 0;border-bottom:1px solid var(--border)">
      <span style="font-size:13px;color:var(--txt2)">${l}</span>
      <span style="font-size:13px;font-weight:700">${v}</span>
    </div>`).join('')}`;

  document.getElementById('profile-stats').innerHTML = [
    ['Total Bookings',myBks.length,'var(--g)'],
    ['Active',myBks.filter(b=>b.status==='active').length,'#4ADE80'],
    ['Completed',myBks.filter(b=>b.status==='completed').length,'#FCD34D'],
    ['Cancelled',myBks.filter(b=>b.status==='cancelled').length,'#FCA5A5'],
    ['Total Spent','Rs '+myBks.filter(b=>b.status==='completed').reduce((s,b)=>s+b.amount,0).toLocaleString(),'var(--g)'],
    ['Exception Log',ExceptionLog.entries.length+' entries','var(--red)'],
  ].map(([l,v,c])=>`
    <div style="display:flex;justify-content:space-between;align-items:center;padding:11px 0;border-bottom:1px solid var(--border)">
      <span style="font-size:13px;color:var(--txt2)">${l}</span>
      <span style="font-size:13px;font-weight:700;color:${c}">${v}</span>
    </div>`).join('');
}

function openChangePassModal() { document.getElementById('cp-alert').innerHTML=''; openModal('m-change-pass'); }

function doChangePass() {
  const alertEl = document.getElementById('cp-alert');
  alertEl.innerHTML = '';
  try {
    const oldPass = document.getElementById('cp-old').value.trim();
    const newPass = document.getElementById('cp-new').value.trim();
    const users = DB.getUsers();
    const user = users.find(u => u.id === appState.user.id);
    if (!user || user.password !== oldPass) throw new InvalidCredentialsException();
    if (newPass.length < 4) throw new ValidationException('new password', 'Must be at least 4 characters');
    user.password = newPass;
    appState.user.password = newPass;
    DB.setUsers(users);
    ExceptionLog.log('INFO', 'Password changed by user', 'Profile → ChangePass');
    closeModal('m-change-pass');
    toast('Password updated successfully ✅');
  } catch(e) {
    ExceptionLog.log(e.name, e.message, 'Profile → ChangePass');
    alertEl.innerHTML = `<div class="alert alert-r"><span>❌</span><div>${e.message}</div></div>`;
  }
}

// ════════════════════════════════════════════════════════════
//  INIT
// ════════════════════════════════════════════════════════════
initSeedData();
document.getElementById('tb-date').textContent = today();

// Enter key on login
document.addEventListener('keydown', e => {
  if (e.key === 'Escape') {
    document.querySelectorAll('.overlay.open').forEach(o => o.classList.remove('open'));
  }
});
</script>
</body>
</html>
