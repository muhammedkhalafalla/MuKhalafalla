<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mohammed Khalafalla — IT Architect & Cybersecurity Engineer</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;700;800;900&family=JetBrains+Mono:wght@300;400;500;600&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #02040A;
  --bg2: #060D1A;
  --cyan: #00D9FF;
  --gold: #FFD166;
  --purple: #8B5CF6;
  --red: #FF4D6D;
  --green: #06D6A0;
  --white: #EEF2FF;
  --muted: #6B7280;
  --card: rgba(6,13,26,0.85);
  --border: rgba(0,217,255,0.18);
}
*{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;}
body{background:var(--bg);color:var(--white);font-family:'DM Sans',sans-serif;overflow-x:hidden;cursor:none;}

/* ── CUSTOM CURSOR ── */
#cur{position:fixed;width:12px;height:12px;background:var(--cyan);border-radius:50%;pointer-events:none;z-index:9999;mix-blend-mode:difference;transition:transform .1s;}
#cur2{position:fixed;width:44px;height:44px;border:1.5px solid rgba(0,217,255,.5);border-radius:50%;pointer-events:none;z-index:9998;transition:all .18s cubic-bezier(.175,.885,.32,1.275);}
body:hover #cur{transform:scale(1);}
a:hover~#cur,button:hover~#cur{transform:scale(2.5);}

/* ── CANVAS BACKGROUND ── */
#bg-canvas{position:fixed;inset:0;z-index:0;opacity:.55;}

/* ── LOADING SCREEN ── */
#loader{position:fixed;inset:0;background:var(--bg);z-index:10000;display:flex;flex-direction:column;align-items:center;justify-content:center;font-family:'JetBrains Mono',monospace;}
#loader-bar{width:300px;height:2px;background:rgba(0,217,255,.15);margin-top:24px;border-radius:2px;overflow:hidden;}
#loader-fill{width:0%;height:100%;background:linear-gradient(90deg,var(--cyan),var(--purple));border-radius:2px;transition:width .05s linear;}
#loader-text{color:var(--cyan);font-size:13px;margin-top:12px;letter-spacing:2px;}
#loader-logo{font-family:'Orbitron',monospace;font-size:clamp(24px,5vw,42px);font-weight:900;letter-spacing:4px;background:linear-gradient(135deg,var(--cyan),var(--purple),var(--gold));-webkit-background-clip:text;color:transparent;animation:pulse2 1.5s ease-in-out infinite;}
@keyframes pulse2{0%,100%{opacity:1;}50%{opacity:.6;}}

/* ── WRAPPER ── */
#app{position:relative;z-index:2;opacity:0;transition:opacity .6s ease;}
#app.ready{opacity:1;}

/* ── NAV ── */
nav{position:fixed;top:0;left:0;right:0;z-index:100;padding:18px 48px;display:flex;align-items:center;justify-content:space-between;backdrop-filter:blur(20px);background:rgba(2,4,10,.7);border-bottom:1px solid var(--border);}
.nav-logo{font-family:'Orbitron',monospace;font-weight:900;font-size:16px;letter-spacing:3px;color:var(--cyan);}
.nav-links{display:flex;gap:32px;}
.nav-links a{font-size:12px;letter-spacing:2px;text-transform:uppercase;color:var(--muted);text-decoration:none;transition:.2s;font-family:'JetBrains Mono',monospace;font-weight:500;}
.nav-links a:hover{color:var(--cyan);}
.nav-status{display:flex;align-items:center;gap:8px;font-size:11px;font-family:'JetBrains Mono',monospace;color:var(--green);}
.status-dot{width:7px;height:7px;background:var(--green);border-radius:50%;animation:blink 2s ease-in-out infinite;}
@keyframes blink{0%,100%{opacity:1;}50%{opacity:.3;}}

/* ── HERO ── */
#hero{min-height:100vh;display:flex;align-items:center;padding:120px 48px 60px;position:relative;overflow:hidden;}
.hero-grid{display:grid;grid-template-columns:1fr 420px;gap:80px;align-items:center;max-width:1400px;margin:0 auto;width:100%;}
.hero-eyebrow{font-family:'JetBrains Mono',monospace;font-size:12px;letter-spacing:3px;color:var(--cyan);text-transform:uppercase;display:flex;align-items:center;gap:12px;margin-bottom:24px;}
.hero-eyebrow::before{content:'';display:block;width:40px;height:1px;background:var(--cyan);}
.hero-name{font-family:'Orbitron',monospace;font-size:clamp(38px,5.5vw,76px);font-weight:900;line-height:1.05;letter-spacing:-1px;margin-bottom:8px;}
.hero-name span{display:block;}
.hero-name .first{color:var(--white);}
.hero-name .last{background:linear-gradient(135deg,var(--cyan) 0%,var(--purple) 50%,var(--gold) 100%);-webkit-background-clip:text;color:transparent;}
.hero-title{font-family:'JetBrains Mono',monospace;font-size:14px;color:var(--muted);letter-spacing:2px;margin:20px 0 32px;display:flex;align-items:center;gap:10px;}
.hero-title span{color:var(--gold);font-weight:600;}
.hero-desc{font-size:16px;line-height:1.75;color:#9CA3AF;max-width:560px;margin-bottom:48px;}
.hero-ctas{display:flex;gap:16px;flex-wrap:wrap;}
.btn-primary{padding:14px 32px;background:var(--cyan);color:var(--bg);font-weight:700;font-size:12px;letter-spacing:2px;text-transform:uppercase;border:none;border-radius:2px;cursor:none;text-decoration:none;display:inline-flex;align-items:center;gap:10px;transition:.25s;font-family:'JetBrains Mono',monospace;clip-path:polygon(0 0,calc(100% - 10px) 0,100% 10px,100% 100%,0 100%);}
.btn-primary:hover{background:var(--white);transform:translateY(-2px);box-shadow:0 16px 40px rgba(0,217,255,.3);}
.btn-outline{padding:14px 32px;background:transparent;color:var(--white);font-weight:600;font-size:12px;letter-spacing:2px;text-transform:uppercase;border:1px solid rgba(255,255,255,.2);border-radius:2px;cursor:none;text-decoration:none;display:inline-flex;align-items:center;gap:10px;transition:.25s;font-family:'JetBrains Mono',monospace;clip-path:polygon(0 0,calc(100% - 10px) 0,100% 10px,100% 100%,0 100%);}
.btn-outline:hover{border-color:var(--cyan);color:var(--cyan);transform:translateY(-2px);}
/* hero card */
.hero-card{background:rgba(6,13,26,.9);border:1px solid var(--border);border-radius:4px;padding:36px;position:relative;overflow:hidden;}
.hero-card::before{content:'';position:absolute;top:0;left:0;right:0;height:2px;background:linear-gradient(90deg,var(--cyan),var(--purple),var(--gold));}
.hero-avatar{width:90px;height:90px;border-radius:3px;background:linear-gradient(135deg,var(--cyan),var(--purple));display:flex;align-items:center;justify-content:center;font-family:'Orbitron',monospace;font-weight:900;font-size:28px;margin-bottom:20px;position:relative;}
.avatar-ring{position:absolute;inset:-4px;border-radius:5px;border:1px solid var(--cyan);animation:ring-pulse 3s ease-in-out infinite;}
@keyframes ring-pulse{0%,100%{opacity:.5;transform:scale(1);}50%{opacity:1;transform:scale(1.03);}}
.hero-card h3{font-family:'Orbitron',monospace;font-size:14px;font-weight:700;margin-bottom:4px;letter-spacing:1px;}
.hero-card p{font-size:12px;color:var(--muted);margin-bottom:20px;font-family:'JetBrains Mono',monospace;}
.hero-stats{display:grid;grid-template-columns:1fr 1fr;gap:12px;}
.hstat{background:rgba(0,217,255,.06);border:1px solid rgba(0,217,255,.12);border-radius:3px;padding:14px;text-align:center;}
.hstat-num{font-family:'Orbitron',monospace;font-size:22px;font-weight:900;color:var(--cyan);}
.hstat-lbl{font-size:10px;color:var(--muted);letter-spacing:1px;text-transform:uppercase;font-family:'JetBrains Mono',monospace;margin-top:3px;}
.card-tags{display:flex;flex-wrap:wrap;gap:6px;margin-top:20px;}
.ctag{padding:4px 10px;background:rgba(139,92,246,.15);border:1px solid rgba(139,92,246,.3);border-radius:2px;font-size:10px;font-family:'JetBrains Mono',monospace;color:var(--purple);letter-spacing:1px;}
.ctag.cyan{background:rgba(0,217,255,.1);border-color:rgba(0,217,255,.25);color:var(--cyan);}
.ctag.gold{background:rgba(255,209,102,.1);border-color:rgba(255,209,102,.25);color:var(--gold);}

/* scroll indicator */
.scroll-ind{position:absolute;bottom:40px;left:50%;transform:translateX(-50%);display:flex;flex-direction:column;align-items:center;gap:8px;font-family:'JetBrains Mono',monospace;font-size:10px;letter-spacing:2px;color:var(--muted);}
.scroll-line{width:1px;height:60px;background:linear-gradient(to bottom,var(--cyan),transparent);animation:scroll-anim 2s ease-in-out infinite;}
@keyframes scroll-anim{0%{transform:scaleY(0);transform-origin:top;}50%{transform:scaleY(1);transform-origin:top;}51%{transform-origin:bottom;}100%{transform:scaleY(0);transform-origin:bottom;}}

/* ── SECTION LAYOUT ── */
section{padding:100px 48px;max-width:1400px;margin:0 auto;}
.section-header{margin-bottom:64px;}
.section-label{font-family:'JetBrains Mono',monospace;font-size:11px;letter-spacing:3px;color:var(--cyan);text-transform:uppercase;display:flex;align-items:center;gap:12px;margin-bottom:16px;}
.section-label::after{content:'';flex:1;height:1px;background:var(--border);}
.section-title{font-family:'Orbitron',monospace;font-size:clamp(28px,4vw,48px);font-weight:900;line-height:1.1;letter-spacing:-1px;}

/* ── EXPERIENCE ── */
.exp-grid{display:grid;gap:0;}
.exp-item{display:grid;grid-template-columns:200px 1fr;gap:0;position:relative;}
.exp-item::before{content:'';position:absolute;left:199px;top:24px;bottom:0;width:1px;background:var(--border);}
.exp-item:last-child::before{display:none;}
.exp-time{padding:0 40px 60px 0;text-align:right;}
.exp-year{font-family:'JetBrains Mono',monospace;font-size:12px;color:var(--cyan);letter-spacing:1px;font-weight:600;}
.exp-duration{font-size:11px;color:var(--muted);margin-top:4px;font-family:'JetBrains Mono',monospace;}
.exp-content{padding:0 0 60px 48px;position:relative;}
.exp-dot{position:absolute;left:-7px;top:8px;width:13px;height:13px;background:var(--bg);border:2px solid var(--cyan);border-radius:50%;box-shadow:0 0 15px rgba(0,217,255,.5);}
.exp-dot.active{background:var(--cyan);}
.exp-company{font-size:12px;color:var(--muted);letter-spacing:1px;font-family:'JetBrains Mono',monospace;text-transform:uppercase;margin-bottom:6px;}
.exp-role{font-family:'Orbitron',monospace;font-size:18px;font-weight:700;margin-bottom:16px;letter-spacing:.5px;}
.exp-list{list-style:none;display:flex;flex-direction:column;gap:8px;}
.exp-list li{font-size:14px;line-height:1.65;color:#9CA3AF;padding-left:20px;position:relative;}
.exp-list li::before{content:'▸';position:absolute;left:0;color:var(--cyan);font-size:12px;}
.exp-badge{display:inline-flex;align-items:center;gap:6px;padding:4px 12px;border-radius:2px;font-size:10px;font-family:'JetBrains Mono',monospace;letter-spacing:1px;border:1px solid rgba(6,214,160,.3);background:rgba(6,214,160,.08);color:var(--green);margin-bottom:12px;}

/* ── SKILLS ── */
.skills-wrap{display:grid;grid-template-columns:1fr 1fr;gap:48px;align-items:start;}
.skill-category{margin-bottom:36px;}
.skill-cat-label{font-family:'JetBrains Mono',monospace;font-size:11px;letter-spacing:2px;color:var(--muted);text-transform:uppercase;margin-bottom:20px;display:flex;align-items:center;gap:10px;}
.skill-cat-label::before{content:'//';color:var(--cyan);font-weight:700;}
.skill-row{margin-bottom:14px;}
.skill-name{font-size:13px;font-family:'JetBrains Mono',monospace;display:flex;justify-content:space-between;margin-bottom:7px;color:var(--white);}
.skill-pct{color:var(--cyan);}
.skill-bar-bg{height:3px;background:rgba(255,255,255,.07);border-radius:3px;overflow:hidden;}
.skill-bar{height:100%;border-radius:3px;background:linear-gradient(90deg,var(--cyan),var(--purple));transform-origin:left;transform:scaleX(0);transition:transform 1.2s cubic-bezier(.16,1,.3,1);}
.skill-bar.gold{background:linear-gradient(90deg,var(--gold),#FF6B35);}
.skill-bar.green{background:linear-gradient(90deg,var(--green),var(--cyan));}
/* hexagons for tools */
.hex-grid{display:flex;flex-wrap:wrap;gap:12px;}
.hex-item{padding:8px 16px;border:1px solid var(--border);border-radius:2px;font-size:11px;font-family:'JetBrains Mono',monospace;color:var(--muted);letter-spacing:1px;transition:.2s;cursor:none;position:relative;overflow:hidden;}
.hex-item::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,rgba(0,217,255,.1),rgba(139,92,246,.1));opacity:0;transition:.2s;}
.hex-item:hover{color:var(--white);border-color:rgba(0,217,255,.4);}
.hex-item:hover::before{opacity:1;}

/* ── CERTS ── */
.certs-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:16px;}
.cert-card{background:var(--card);border:1px solid var(--border);border-radius:3px;padding:24px;position:relative;overflow:hidden;transition:.3s;cursor:none;}
.cert-card::after{content:'';position:absolute;bottom:0;left:0;right:0;height:2px;background:linear-gradient(90deg,transparent,var(--cyan),transparent);opacity:0;transition:.3s;}
.cert-card:hover{border-color:rgba(0,217,255,.4);transform:translateY(-3px);}
.cert-card:hover::after{opacity:1;}
.cert-icon{width:42px;height:42px;border-radius:2px;display:flex;align-items:center;justify-content:center;font-size:18px;margin-bottom:14px;background:rgba(0,217,255,.1);border:1px solid rgba(0,217,255,.2);}
.cert-name{font-family:'JetBrains Mono',monospace;font-size:13px;font-weight:600;margin-bottom:4px;color:var(--white);}
.cert-issuer{font-size:11px;color:var(--muted);letter-spacing:.5px;}
.cert-year{font-family:'JetBrains Mono',monospace;font-size:10px;color:var(--cyan);margin-top:10px;}

/* ── PROJECTS ── */
.projects-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:20px;}
.proj-card{background:var(--card);border:1px solid var(--border);border-radius:3px;padding:28px;position:relative;overflow:hidden;transition:.35s;cursor:none;}
.proj-card::before{content:'';position:absolute;top:0;left:0;bottom:0;width:2px;background:linear-gradient(to bottom,var(--cyan),var(--purple));opacity:0;transition:.3s;}
.proj-card:hover{border-color:rgba(0,217,255,.3);transform:translateY(-4px);box-shadow:0 24px 60px rgba(0,0,0,.5);}
.proj-card:hover::before{opacity:1;}
.proj-num{font-family:'Orbitron',monospace;font-size:48px;font-weight:900;color:rgba(0,217,255,.07);position:absolute;top:12px;right:20px;line-height:1;}
.proj-icon{font-size:24px;margin-bottom:16px;}
.proj-title{font-family:'Orbitron',monospace;font-size:15px;font-weight:700;margin-bottom:10px;letter-spacing:.5px;line-height:1.3;}
.proj-desc{font-size:13px;color:#9CA3AF;line-height:1.65;margin-bottom:16px;}
.proj-tags{display:flex;flex-wrap:wrap;gap:6px;}
.ptag{font-size:10px;font-family:'JetBrains Mono',monospace;padding:3px 8px;border-radius:2px;letter-spacing:.5px;}
.ptag.c{background:rgba(0,217,255,.1);border:1px solid rgba(0,217,255,.2);color:var(--cyan);}
.ptag.p{background:rgba(139,92,246,.1);border:1px solid rgba(139,92,246,.2);color:var(--purple);}
.ptag.g{background:rgba(6,214,160,.1);border:1px solid rgba(6,214,160,.2);color:var(--green);}
.ptag.o{background:rgba(255,209,102,.1);border:1px solid rgba(255,209,102,.2);color:var(--gold);}

/* ── METRICS BAND ── */
.metrics-band{background:var(--bg2);border-top:1px solid var(--border);border-bottom:1px solid var(--border);padding:60px 48px;}
.metrics-inner{display:grid;grid-template-columns:repeat(4,1fr);gap:0;max-width:1400px;margin:0 auto;}
.metric{text-align:center;padding:0 40px;position:relative;}
.metric+.metric::before{content:'';position:absolute;left:0;top:10%;bottom:10%;width:1px;background:var(--border);}
.metric-num{font-family:'Orbitron',monospace;font-size:clamp(40px,5vw,68px);font-weight:900;line-height:1;margin-bottom:8px;background:linear-gradient(135deg,var(--cyan),var(--purple));-webkit-background-clip:text;color:transparent;}
.metric-unit{font-family:'Orbitron',monospace;font-size:20px;color:var(--gold);}
.metric-lbl{font-size:13px;color:var(--muted);letter-spacing:1px;font-family:'JetBrains Mono',monospace;}

/* ── CONTACT ── */
.contact-grid{display:grid;grid-template-columns:1fr 1fr;gap:48px;}
.contact-left p{font-size:16px;color:#9CA3AF;line-height:1.75;margin-bottom:40px;}
.contact-items{display:flex;flex-direction:column;gap:20px;}
.contact-item{display:flex;align-items:center;gap:16px;padding:18px 20px;background:var(--card);border:1px solid var(--border);border-radius:3px;transition:.2s;text-decoration:none;}
.contact-item:hover{border-color:rgba(0,217,255,.4);}
.contact-icon{width:42px;height:42px;background:rgba(0,217,255,.1);border:1px solid rgba(0,217,255,.2);border-radius:2px;display:flex;align-items:center;justify-content:center;font-size:16px;flex-shrink:0;}
.contact-info span{display:block;}
.contact-label{font-size:10px;font-family:'JetBrains Mono',monospace;color:var(--muted);letter-spacing:1px;text-transform:uppercase;}
.contact-value{font-size:14px;color:var(--white);font-family:'JetBrains Mono',monospace;margin-top:2px;}
.contact-right{background:var(--card);border:1px solid var(--border);border-radius:3px;padding:40px;position:relative;overflow:hidden;}
.contact-right::before{content:'';position:absolute;top:0;left:0;right:0;height:2px;background:linear-gradient(90deg,var(--cyan),var(--purple),var(--gold));}
.terminal-header{display:flex;align-items:center;gap:8px;margin-bottom:24px;}
.t-dot{width:10px;height:10px;border-radius:50%;}
.t-red{background:#FF5F57;} .t-yellow{background:#FFBD2E;} .t-green{background:#28C840;}
.terminal-body{font-family:'JetBrains Mono',monospace;font-size:13px;line-height:1.8;}
.t-comment{color:var(--muted);}
.t-key{color:var(--cyan);}
.t-val{color:var(--gold);}
.t-str{color:var(--green);}
.t-cursor{display:inline-block;width:8px;height:14px;background:var(--cyan);vertical-align:middle;animation:blink 1s step-end infinite;}
.available-badge{margin-top:28px;display:inline-flex;align-items:center;gap:8px;padding:10px 20px;background:rgba(6,214,160,.08);border:1px solid rgba(6,214,160,.25);border-radius:2px;font-family:'JetBrains Mono',monospace;font-size:12px;color:var(--green);letter-spacing:1px;}

/* ── FOOTER ── */
footer{border-top:1px solid var(--border);padding:40px 48px;display:flex;align-items:center;justify-content:space-between;max-width:100%;}
.footer-logo{font-family:'Orbitron',monospace;font-size:13px;font-weight:900;color:var(--cyan);letter-spacing:3px;}
.footer-copy{font-family:'JetBrains Mono',monospace;font-size:11px;color:var(--muted);letter-spacing:1px;}
.footer-links{display:flex;gap:24px;}
.footer-links a{font-family:'JetBrains Mono',monospace;font-size:11px;color:var(--muted);text-decoration:none;transition:.2s;letter-spacing:1px;}
.footer-links a:hover{color:var(--cyan);}

/* ── GLITCH ── */
.glitch{position:relative;}
.glitch::after{content:attr(data-text);position:absolute;inset:0;background:var(--bg);clip-path:polygon(0 45%,100% 45%,100% 55%,0 55%);animation:glitch-anim 5s infinite;color:var(--cyan);opacity:.6;}
@keyframes glitch-anim{0%,94%,100%{transform:none;opacity:0;}95%{transform:translate(-2px,0);opacity:.6;}97%{transform:translate(2px,0);opacity:.6;}99%{transform:translate(0,2px);opacity:.6;}}

/* ── HIGHLIGHT ── */
.highlight{color:var(--cyan);}

/* ── FADE REVEAL ── */
.reveal{opacity:0;transform:translateY(30px);transition:opacity .8s ease,transform .8s ease;}
.reveal.visible{opacity:1;transform:none;}

/* ── RESPONSIVE ── */
@media(max-width:1024px){
  .hero-grid,.skills-wrap,.contact-grid{grid-template-columns:1fr;}
  .hero-card{display:none;}
  .projects-grid{grid-template-columns:1fr 1fr;}
  .metrics-inner{grid-template-columns:1fr 1fr;gap:40px;}
  .metric+.metric::before{display:none;}
}
@media(max-width:768px){
  section,nav,footer{padding-left:24px;padding-right:24px;}
  nav{padding-top:16px;padding-bottom:16px;}
  .nav-links{display:none;}
  .projects-grid{grid-template-columns:1fr;}
  .exp-item{grid-template-columns:1fr;}
  .exp-time{text-align:left;padding-bottom:8px;}
  .exp-item::before{display:none;}
  .exp-content{padding-left:20px;}
  .metrics-inner{grid-template-columns:1fr 1fr;}
  body{cursor:auto;}
  #cur,#cur2{display:none;}
}
</style>
</head>
<body>

<canvas id="bg-canvas"></canvas>
<div id="cur"></div>
<div id="cur2"></div>

<!-- LOADING SCREEN -->
<div id="loader">
  <div id="loader-logo">MK</div>
  <div id="loader-bar"><div id="loader-fill"></div></div>
  <div id="loader-text">INITIALIZING SYSTEM...</div>
</div>

<div id="app">

<!-- NAV -->
<nav>
  <div class="nav-logo">MuKhalafalla</div>
  <div class="nav-links">
    <a href="#experience">Experience</a>
    <a href="#skills">Skills</a>
    <a href="#projects">Projects</a>
    <a href="#certs">Certifications</a>
    <a href="#contact">Contact</a>
  </div>
  <div class="nav-status"><div class="status-dot"></div>Available for Opportunities</div>
</nav>

<!-- HERO -->
<div id="hero">
  <div class="hero-grid">
    <div>
      <div class="hero-eyebrow">IT Architect & Cybersecurity Engineer</div>
      <div class="hero-name">
        <span class="first">MOHAMMED</span>
        <span class="last glitch" data-text="KHALAFALLA">KHALAFALLA</span>
      </div>
      <div class="hero-title">
        <span id="typed-title"></span>
      </div>
      <p class="hero-desc">
        Results-driven IT Manager with <span class="highlight">6+ years</span> of hands-on expertise spanning system administration, infrastructure architecture, and cybersecurity — primarily within hospitality. Building high-performance, zero-trust environments from the ground up.
      </p>
      <div class="hero-ctas">
        <a href="#contact" class="btn-primary">⚡ Initiate Contact</a>
        <a href="#projects" class="btn-outline">// View Projects</a>
      </div>
    </div>

    <div class="hero-card">
      <div class="hero-avatar">
        <div class="avatar-ring"></div>
        MK
      </div>
      <h3>Mohammed Khalafalla</h3>
      <p>IT Manager @ Swiss International Al Taif</p>
      <div class="hero-stats">
        <div class="hstat"><div class="hstat-num">6+</div><div class="hstat-lbl">Years XP</div></div>
        <div class="hstat"><div class="hstat-num">60%</div><div class="hstat-lbl">Cost Cut</div></div>
        <div class="hstat"><div class="hstat-num">10+</div><div class="hstat-lbl">Certifications</div></div>
        <div class="hstat"><div class="hstat-num">4</div><div class="hstat-lbl">Companies</div></div>
      </div>
      <div class="card-tags">
        <span class="ctag cyan">FortiGate</span>
        <span class="ctag">VMware ESXi</span>
        <span class="ctag gold">OPERA Cloud</span>
        <span class="ctag cyan">Active Directory</span>
        <span class="ctag">Veeam</span>
        <span class="ctag">Python</span>
      </div>
    </div>
  </div>

  <div class="scroll-ind">
    <div class="scroll-line"></div>
    <span>SCROLL</span>
  </div>
</div>

<!-- METRICS BAND -->
<div class="metrics-band reveal">
  <div class="metrics-inner">
    <div class="metric">
      <div class="metric-num"><span class="count" data-target="60">0</span><span class="metric-unit">%</span></div>
      <div class="metric-lbl">Telecom Cost Reduction</div>
    </div>
    <div class="metric">
      <div class="metric-num"><span class="count" data-target="5">0</span><span class="metric-unit">+</span></div>
      <div class="metric-lbl">Years of Experience</div>
    </div>
    <div class="metric">
      <div class="metric-num"><span class="count" data-target="10">0</span><span class="metric-unit">+</span></div>
      <div class="metric-lbl">Certifications Earned</div>
    </div>
    <div class="metric">
      <div class="metric-num"><span class="count" data-target="3">0</span><span class="metric-unit">✕</span></div>
      <div class="metric-lbl">Chess Champion 🏆</div>
    </div>
  </div>
</div>

<!-- EXPERIENCE -->
<section id="experience">
  <div class="section-header reveal">
    <div class="section-label">Work History</div>
    <h2 class="section-title">Battle-Tested<br><span style="color:var(--cyan)">Experience</span></h2>
  </div>
  <div class="exp-grid">

    <div class="exp-item reveal">
      <div class="exp-time">
        <div class="exp-year">2024</div>
        <div class="exp-duration">Aug 2024 → Present</div>
      </div>
      <div class="exp-content">
        <div class="exp-dot active"></div>
        <div class="exp-badge">● Currently Active</div>
        <div class="exp-company">Swiss International Al Taif Hotel · Taif, KSA</div>
        <div class="exp-role">IT Manager</div>
        <ul class="exp-list">
          <li>Designed and deployed the hotel's Full Domain Controller System — eliminated external vendor costs, enforced zero-trust access management & Group Policy hardening.</li>
          <li>Architected cost-effective high-speed Guest Wi-Fi infrastructure; migrated critical hotel systems to wired backbone — improving stability and data throughput significantly.</li>
          <li>Led integration of Sun System & Material Control for automated financial operations and procurement management across all hotel departments.</li>
          <li>Deployed FortiGate Firewall with structured ACLs, advanced file-sharing policies, and IDS/IPS rules — achieving 99.9% cybersecurity compliance.</li>
          <li>Optimized telecom infrastructure: reduced telephone lines from 15 → 6, delivering a <strong>60% cost reduction</strong> with zero degradation in service quality.</li>
          <li>Managed OPERA Cloud PMS, Micros POS, and all hospitality IT systems ensuring seamless 24/7 operations for staff and guests.</li>
        </ul>
      </div>
    </div>

    <div class="exp-item reveal">
      <div class="exp-time">
        <div class="exp-year">2023</div>
        <div class="exp-duration">Nov 2023 → Jun 2024</div>
      </div>
      <div class="exp-content">
        <div class="exp-dot"></div>
        <div class="exp-company">Backbone Group · Part-Time</div>
        <div class="exp-role">Cybersecurity Engineer</div>
        <ul class="exp-list">
          <li>Designed, implemented, and managed enterprise cybersecurity toolsets including next-generation firewalls, IDS/IPS, and antivirus solutions for commercial clients.</li>
          <li>Delivered comprehensive Trend Micro product support (Apex One, Apex Central, Deep Security, DDx) across the Middle East region — ensuring robust threat protection at scale.</li>
        </ul>
      </div>
    </div>

    <div class="exp-item reveal">
      <div class="exp-time">
        <div class="exp-year">2023</div>
        <div class="exp-duration">Aug 2023 → May 2024</div>
      </div>
      <div class="exp-content">
        <div class="exp-dot"></div>
        <div class="exp-company">ElManara Flour Company</div>
        <div class="exp-role">System Administrator</div>
        <ul class="exp-list">
          <li>Installed, configured, and hardened VMware ESXi servers with Sophos Firewall solutions — building a resilient virtualized infrastructure.</li>
          <li>Managed user access controls, maintained file servers, and configured virtual storage environments for system stability and data integrity.</li>
          <li>Proactively monitored network activity to identify and mitigate security threats before impact.</li>
        </ul>
      </div>
    </div>

    <div class="exp-item reveal">
      <div class="exp-time">
        <div class="exp-year">2021</div>
        <div class="exp-duration">Apr 2021 → Jun 2023</div>
      </div>
      <div class="exp-content">
        <div class="exp-dot"></div>
        <div class="exp-company">Blue Reef Resort</div>
        <div class="exp-role">Assistant IT Manager</div>
        <ul class="exp-list">
          <li>Migrated physical servers to VMware ESXi 6 virtualized environment — significantly improving performance, redundancy, and disaster recovery capabilities.</li>
          <li>Upgraded firewall infrastructure from pfSense → Sophos XG, enhancing network security posture.</li>
          <li>Implemented Veeam Backup & Recovery solution and led a full Wi-Fi system overhaul using Ubiquiti mesh technology.</li>
          <li>Enhanced hotel CCTV infrastructure for advanced security monitoring coverage.</li>
        </ul>
      </div>
    </div>

    <div class="exp-item reveal">
      <div class="exp-time">
        <div class="exp-year">2020</div>
        <div class="exp-duration">Sep 2020 → Mar 2021</div>
      </div>
      <div class="exp-content">
        <div class="exp-dot"></div>
        <div class="exp-company">Telecom Egypt (WE)</div>
        <div class="exp-role">IT Support Specialist</div>
        <ul class="exp-list">
          <li>Delivered end-user support via phone, email, and in-person for hardware and software resolution across diverse enterprise environments.</li>
          <li>Assisted in system installations, upgrades, and routine maintenance ensuring continuous operational performance.</li>
        </ul>
      </div>
    </div>

  </div>
</section>

<!-- SKILLS -->
<section id="skills" style="background:var(--bg2);max-width:100%;padding:100px 0;">
  <div style="max-width:1400px;margin:0 auto;padding:0 48px;">
    <div class="section-header reveal">
      <div class="section-label">Core Competencies</div>
      <h2 class="section-title">Technical <span style="color:var(--cyan)">Arsenal</span></h2>
    </div>
    <div class="skills-wrap">
      <div>
        <div class="skill-category reveal">
          <div class="skill-cat-label">Networking & Security</div>
          <div class="skill-row"><div class="skill-name"><span>FortiGate / Fortinet Suite</span><span class="skill-pct">95%</span></div><div class="skill-bar-bg"><div class="skill-bar" data-w="95"></div></div></div>
          <div class="skill-row"><div class="skill-name"><span>Sophos Firewall / XG</span><span class="skill-pct">90%</span></div><div class="skill-bar-bg"><div class="skill-bar" data-w="90"></div></div></div>
          <div class="skill-row"><div class="skill-name"><span>TCP/IP · DNS · DHCP · VPN</span><span class="skill-pct">92%</span></div><div class="skill-bar-bg"><div class="skill-bar" data-w="92"></div></div></div>
          <div class="skill-row"><div class="skill-name"><span>IDS / IPS · Zero Trust</span><span class="skill-pct">85%</span></div><div class="skill-bar-bg"><div class="skill-bar" data-w="85"></div></div></div>
          <div class="skill-row"><div class="skill-name"><span>Trend Micro (Apex One / Deep Security)</span><span class="skill-pct">88%</span></div><div class="skill-bar-bg"><div class="skill-bar" data-w="88"></div></div></div>
        </div>
        <div class="skill-category reveal">
          <div class="skill-cat-label">Virtualization & Infrastructure</div>
          <div class="skill-row"><div class="skill-name"><span>VMware ESXi / vSphere / vCenter</span><span class="skill-pct">90%</span></div><div class="skill-bar-bg"><div class="skill-bar gold" data-w="90"></div></div></div>
          <div class="skill-row"><div class="skill-name"><span>Windows Server / Active Directory</span><span class="skill-pct">93%</span></div><div class="skill-bar-bg"><div class="skill-bar gold" data-w="93"></div></div></div>
          <div class="skill-row"><div class="skill-name"><span>Linux Administration</span><span class="skill-pct">80%</span></div><div class="skill-bar-bg"><div class="skill-bar gold" data-w="80"></div></div></div>
          <div class="skill-row"><div class="skill-name"><span>Veeam Backup & Disaster Recovery</span><span class="skill-pct">87%</span></div><div class="skill-bar-bg"><div class="skill-bar gold" data-w="87"></div></div></div>
        </div>
      </div>
      <div>
        <div class="skill-category reveal">
          <div class="skill-cat-label">Hospitality IT Systems</div>
          <div class="skill-row"><div class="skill-name"><span>OPERA Cloud PMS</span><span class="skill-pct">92%</span></div><div class="skill-bar-bg"><div class="skill-bar green" data-w="92"></div></div></div>
          <div class="skill-row"><div class="skill-name"><span>Micros POS</span><span class="skill-pct">88%</span></div><div class="skill-bar-bg"><div class="skill-bar green" data-w="88"></div></div></div>
          <div class="skill-row"><div class="skill-name"><span>Sun System / Material Control</span><span class="skill-pct">85%</span></div><div class="skill-bar-bg"><div class="skill-bar green" data-w="85"></div></div></div>
        </div>
        <div class="skill-category reveal">
          <div class="skill-cat-label">Automation & Scripting</div>
          <div class="skill-row"><div class="skill-name"><span>PowerShell</span><span class="skill-pct">85%</span></div><div class="skill-bar-bg"><div class="skill-bar" data-w="85"></div></div></div>
          <div class="skill-row"><div class="skill-name"><span>Python (Automation / Scripting)</span><span class="skill-pct">78%</span></div><div class="skill-bar-bg"><div class="skill-bar" data-w="78"></div></div></div>
          <div class="skill-row"><div class="skill-name"><span>Bash Scripting</span><span class="skill-pct">80%</span></div><div class="skill-bar-bg"><div class="skill-bar" data-w="80"></div></div></div>
        </div>
        <div class="skill-category reveal">
          <div class="skill-cat-label">Tools & Platforms</div>
          <div class="hex-grid">
            <div class="hex-item">Ubiquiti</div><div class="hex-item">pfSense</div><div class="hex-item">CCNA</div>
            <div class="hex-item">MCSA</div><div class="hex-item">CompTIA A+</div><div class="hex-item">Group Policy</div>
            <div class="hex-item">SIEM</div><div class="hex-item">FortiAP</div><div class="hex-item">VLAN</div>
            <div class="hex-item">VoIP</div><div class="hex-item">CCTV Systems</div><div class="hex-item">QoS</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- PROJECTS -->
<section id="projects">
  <div class="section-header reveal">
    <div class="section-label">Key Initiatives</div>
    <h2 class="section-title">Signature <span style="color:var(--cyan)">Projects</span></h2>
  </div>
  <div class="projects-grid">

    <div class="proj-card reveal">
      <div class="proj-num">01</div>
      <div class="proj-icon">🖥️</div>
      <div class="proj-title">Hotel Domain Controller & Zero-Trust Deployment</div>
      <p class="proj-desc">Designed and deployed the entire Active Directory & GPO infrastructure at Swiss International Al Taif Hotel — eliminating third-party vendor dependency and saving significant outsourcing costs. Centralized authentication, enforced zero-trust policies, and streamlined all user access management.</p>
      <div class="proj-tags"><span class="ptag c">Windows Server</span><span class="ptag p">Active Directory</span><span class="ptag g">Zero Trust</span><span class="ptag o">Cost Optimization</span></div>
    </div>

    <div class="proj-card reveal">
      <div class="proj-num">02</div>
      <div class="proj-icon">🌐</div>
      <div class="proj-title">Enterprise Guest Wi-Fi Architecture</div>
      <p class="proj-desc">Engineered a high-performance guest Wi-Fi network with VLAN segmentation, captive portal authentication, and QoS prioritization. Migrated all critical hotel systems to wired backbone — improving stability, data transfer speed, and network security posture while reducing operational expenses.</p>
      <div class="proj-tags"><span class="ptag c">Ubiquiti</span><span class="ptag p">FortiAP</span><span class="ptag g">VLAN</span><span class="ptag o">QoS</span></div>
    </div>

    <div class="proj-card reveal">
      <div class="proj-num">03</div>
      <div class="proj-icon">📡</div>
      <div class="proj-title">Telecom Optimization — 60% Cost Reduction</div>
      <p class="proj-desc">Audited and restructured the hotel's entire telecommunication infrastructure. Reduced telephone lines from 15 → 6, implemented intelligent call routing and VoIP optimization — delivering 60% annual cost savings with zero degradation to internal or guest-facing communication quality.</p>
      <div class="proj-tags"><span class="ptag o">VoIP</span><span class="ptag g">Cost Engineering</span><span class="ptag c">Infrastructure</span></div>
    </div>

    <div class="proj-card reveal">
      <div class="proj-num">04</div>
      <div class="proj-icon">🔥</div>
      <div class="proj-title">FortiGate Security Hardening & Compliance</div>
      <p class="proj-desc">Implemented full FortiGate firewall deployment with advanced access control lists, structured security policies, IDS/IPS rules, and file-sharing governance. Achieved 99.9% cybersecurity compliance and significantly reduced attack surface across all hotel network segments.</p>
      <div class="proj-tags"><span class="ptag c">FortiGate</span><span class="ptag p">IDS/IPS</span><span class="ptag g">Compliance</span><span class="ptag o">Security Policy</span></div>
    </div>

    <div class="proj-card reveal">
      <div class="proj-num">05</div>
      <div class="proj-icon">☁️</div>
      <div class="proj-title">Physical-to-Virtual ESXi Migration</div>
      <p class="proj-desc">Led a full P2V migration from legacy physical servers to VMware ESXi 6 virtualized environment at Blue Reef Resort — dramatically improving system performance, reliability, and disaster recovery readiness. Complemented with Veeam Backup implementation for business continuity.</p>
      <div class="proj-tags"><span class="ptag c">VMware ESXi</span><span class="ptag p">Veeam</span><span class="ptag g">P2V Migration</span><span class="ptag o">DR</span></div>
    </div>

    <div class="proj-card reveal">
      <div class="proj-num">06</div>
      <div class="proj-icon">⚙️</div>
      <div class="proj-title">Sun System & Material Control Integration</div>
      <p class="proj-desc">Played a central role in configuring and integrating Sun System financial software and Material Control procurement platform — enabling automated financial operations, real-time inventory management, and seamless cross-departmental data flow throughout the hotel.</p>
      <div class="proj-tags"><span class="ptag c">Sun System</span><span class="ptag p">Material Control</span><span class="ptag g">ERP Integration</span><span class="ptag o">Automation</span></div>
    </div>

    <!-- NEW PROJECT: Multi-Branch VPN & SD-WAN Fabric -->
    <div class="proj-card reveal">
      <div class="proj-num">07</div>
      <div class="proj-icon">🔗</div>
      <div class="proj-title">Multi-Branch VPN & SD-WAN Fabric</div>
      <p class="proj-desc">Architected a secure SD-WAN overlay connecting 4 hotel branches with site-to-site VPN tunnels and dynamic routing (BGP/OSPF). Implemented QoS policies prioritizing VoIP and critical ERP traffic, reducing inter-branch latency by 40% and ensuring 99.99% uptime for voice and data.</p>
      <div class="proj-tags"><span class="ptag c">SD-WAN</span><span class="ptag p">Site-to-Site VPN</span><span class="ptag g">VoIP QoS</span><span class="ptag o">BGP/OSPF</span></div>
    </div>

    <!-- NEW PROJECT: Unified VoIP & Telephony Migration -->
    <div class="proj-card reveal">
      <div class="proj-num">08</div>
      <div class="proj-icon">📞</div>
      <div class="proj-title">Unified VoIP & Telephony Migration</div>
      <p class="proj-desc">Designed and deployed a centralized VoIP PBX (3CX/Asterisk) across all branches, integrating legacy POTS lines with SIP trunks. Enabled unified extension dialing, call recording, and softphone roaming — reduced long-distance costs by 65% and improved internal voice collaboration.</p>
      <div class="proj-tags"><span class="ptag c">VoIP PBX</span><span class="ptag p">SIP Trunking</span><span class="ptag g">3CX</span><span class="ptag o">Unified Comms</span></div>
    </div>

    <!-- NEW PROJECT: Centralized Server & Storage Replication -->
    <div class="proj-card reveal">
      <div class="proj-num">09</div>
      <div class="proj-icon">🗄️</div>
      <div class="proj-title">Centralized Server & Storage Replication</div>
      <p class="proj-desc">Consolidated 12 physical servers into 3 clustered hypervisors (VMware vSAN) across two data centers. Implemented synchronous replication for mission-critical VMs and Veeam Backup & Replication for offsite DR. Achieved RPO of 15 minutes and RTO under 2 hours for all branch servers.</p>
      <div class="proj-tags"><span class="ptag c">vSAN</span><span class="ptag p">Hyper-V Replica</span><span class="ptag g">Veeam B&R</span><span class="ptag o">DR Orchestration</span></div>
    </div>

  </div>
</section>

<!-- CERTIFICATIONS -->
<section id="certs" style="background:var(--bg2);max-width:100%;padding:100px 0;">
  <div style="max-width:1400px;margin:0 auto;padding:0 48px;">
    <div class="section-header reveal">
      <div class="section-label">Qualifications</div>
      <h2 class="section-title">Certifications & <span style="color:var(--cyan)">Education</span></h2>
    </div>
    <div class="certs-grid">
      <div class="cert-card reveal"><div class="cert-icon">🛡️</div><div class="cert-name">Fortinet Certified Associate (FCA)</div><div class="cert-issuer">Fortinet · Cybersecurity</div><div class="cert-year">May 2025</div></div>
      <div class="cert-card reveal"><div class="cert-icon">🔐</div><div class="cert-name">Fortinet Certified Fundamentals (FCF)</div><div class="cert-issuer">Fortinet · Cybersecurity</div><div class="cert-year">May 2025</div></div>
      <div class="cert-card reveal"><div class="cert-icon">🌐</div><div class="cert-name">Cisco Certified Network Associate (CCNA)</div><div class="cert-issuer">Cisco Systems · Networking</div><div class="cert-year">Active</div></div>
      <div class="cert-card reveal"><div class="cert-icon">🪟</div><div class="cert-name">Microsoft Certified Solutions Associate (MCSA)</div><div class="cert-issuer">Microsoft · Systems Admin</div><div class="cert-year">Active</div></div>
      <div class="cert-card reveal"><div class="cert-icon">💻</div><div class="cert-name">VMware Essentials (vSphere & ESXi)</div><div class="cert-issuer">VMware · Virtualization</div><div class="cert-year">Active</div></div>
      <div class="cert-card reveal"><div class="cert-icon">☁️</div><div class="cert-name">Veeam Backup & Recovery</div><div class="cert-issuer">Veeam · Disaster Recovery</div><div class="cert-year">Active</div></div>
      <div class="cert-card reveal"><div class="cert-icon">🔒</div><div class="cert-name">Google Cybersecurity Certificate</div><div class="cert-issuer">Google · Apr 2024</div><div class="cert-year">Apr 2024</div></div>
      <div class="cert-card reveal"><div class="cert-icon">🔥</div><div class="cert-name">Sophos Firewall — Threat Protection</div><div class="cert-issuer">Sophos · Network Security</div><div class="cert-year">Active</div></div>
      <div class="cert-card reveal"><div class="cert-icon">🖥️</div><div class="cert-name">CompTIA A+ — IT Hardware & Networking</div><div class="cert-issuer">CompTIA</div><div class="cert-year">Active</div></div>
      <div class="cert-card reveal"><div class="cert-icon">🧬</div><div class="cert-name">Trend Micro Suite (Apex One, Deep Security)</div><div class="cert-issuer">Trend Micro · Security</div><div class="cert-year">Active</div></div>
      <div class="cert-card reveal"><div class="cert-icon">🎓</div><div class="cert-name">B.Sc. Information Technology & Computer Science</div><div class="cert-issuer">Sinai University · 2016–2020</div><div class="cert-year">2020</div></div>
      <div class="cert-card reveal" style="border-color:rgba(255,209,102,.3);background:rgba(255,209,102,.04);">
        <div class="cert-icon" style="background:rgba(255,209,102,.1);border-color:rgba(255,209,102,.3);">♟️</div>
        <div class="cert-name" style="color:var(--gold)">3× University Chess Champion</div>
        <div class="cert-issuer">Sinai University</div>
        <div class="cert-year" style="color:var(--gold)">2018 · 2019 · 2020</div>
      </div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="section-header reveal">
    <div class="section-label">Get In Touch</div>
    <h2 class="section-title">Let's Build Something <span style="color:var(--cyan)">Extraordinary</span></h2>
  </div>
  <div class="contact-grid">
    <div class="contact-left reveal">
      <p>Currently based in Taif, Saudi Arabia with a transferable IT Engineer visa. Open to senior IT management roles, cybersecurity contracts, and infrastructure architecture projects across the region.</p>
      <div class="contact-items">
        <a class="contact-item" href="tel:+966547706541">
          <div class="contact-icon">📱</div>
          <div class="contact-info">
            <span class="contact-label">Phone / WhatsApp</span>
            <span class="contact-value">+966 54 770 6541</span>
          </div>
        </a>
        <a class="contact-item" href="mailto:Eng.muhammedkh@gmail.com">
          <div class="contact-icon">✉️</div>
          <div class="contact-info">
            <span class="contact-label">Email</span>
            <span class="contact-value">Eng.muhammedkh@gmail.com</span>
          </div>
        </a>
        <a class="contact-item" href="https://www.mukhalafalla.com" target="_blank">
          <div class="contact-icon">🌐</div>
          <div class="contact-info">
            <span class="contact-label">Portfolio Website</span>
            <span class="contact-value">www.mukhalafalla.com</span>
          </div>
        </a>
        <a class="contact-item" href="https://linkedin.com/in/mohammed-khalafalla-cyber" target="_blank">
          <div class="contact-icon">💼</div>
          <div class="contact-info">
            <span class="contact-label">LinkedIn</span>
            <span class="contact-value">/in/mohammed-khalafalla-cyber</span>
          </div>
        </a>
      </div>
    </div>
    <div class="contact-right reveal">
      <div class="terminal-header">
        <div class="t-dot t-red"></div>
        <div class="t-dot t-yellow"></div>
        <div class="t-dot t-green"></div>
      </div>
      <div class="terminal-body">
        <div><span class="t-comment">// candidate.profile.json</span></div>
        <div>&nbsp;</div>
        <div>{</div>
        <div>&nbsp;&nbsp;<span class="t-key">"name"</span>: <span class="t-str">"Mohammed Khalafalla"</span>,</div>
        <div>&nbsp;&nbsp;<span class="t-key">"role"</span>: <span class="t-str">"IT Manager & Cybersecurity Engineer"</span>,</div>
        <div>&nbsp;&nbsp;<span class="t-key">"location"</span>: <span class="t-str">"Taif, Saudi Arabia"</span>,</div>
        <div>&nbsp;&nbsp;<span class="t-key">"visa"</span>: <span class="t-str">"IT Engineer | Transferable"</span>,</div>
        <div>&nbsp;&nbsp;<span class="t-key">"languages"</span>: [<span class="t-str">"Arabic"</span>, <span class="t-str">"English (C2)"</span>, <span class="t-str">"Italian"</span>],</div>
        <div>&nbsp;&nbsp;<span class="t-key">"experience_years"</span>: <span class="t-val">5</span>,</div>
        <div>&nbsp;&nbsp;<span class="t-key">"specialization"</span>: <span class="t-str">"Hospitality IT + Cybersecurity"</span>,</div>
        <div>&nbsp;&nbsp;<span class="t-key">"status"</span>: <span class="t-str">"open_to_opportunities"</span></div>
        <div>} <span class="t-cursor"></span></div>
      </div>
      <div class="available-badge">
        <div class="status-dot"></div>
        AVAILABLE FOR HIRE — Q2 2026
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-logo">MK.SYS</div>
  <div class="footer-copy">© 2026 MOHAMMED KHALAFALLA — All Systems Operational</div>
  <div class="footer-links">
    <a href="https://www.mukhalafalla.com">mukhalafalla.com</a>
    <a href="mailto:Eng.muhammedkh@gmail.com">Email</a>
    <a href="tel:+966547706541">+966 54 770 6541</a>
  </div>
</footer>

</div><!-- /app -->

<script>
// ── CURSOR ──
const cur = document.getElementById('cur'), cur2 = document.getElementById('cur2');
let mx=0,my=0,cx=0,cy=0;
document.addEventListener('mousemove',e=>{mx=e.clientX;my=e.clientY;cur.style.left=mx-6+'px';cur.style.top=my-6+'px';});
setInterval(()=>{cx+=(mx-cx)*.15;cy+=(my-cy)*.15;cur2.style.left=cx-22+'px';cur2.style.top=cy-22+'px';},16);

// ── CIRCUIT CANVAS BACKGROUND ──
const canvas=document.getElementById('bg-canvas');
const ctx=canvas.getContext('2d');
let W,H,particles=[];
function resize(){W=canvas.width=window.innerWidth;H=canvas.height=window.innerHeight;}
resize();window.addEventListener('resize',resize);
class Particle{
  constructor(){this.reset();}
  reset(){this.x=Math.random()*W;this.y=Math.random()*H;this.vx=(Math.random()-.5)*.4;this.vy=(Math.random()-.5)*.2;this.r=Math.random()*1.5+.5;this.a=Math.random()*.4+.1;}
  update(){this.x+=this.vx;this.y+=this.vy;if(this.x<0||this.x>W||this.y<0||this.y>H)this.reset();}
  draw(){ctx.beginPath();ctx.arc(this.x,this.y,this.r,0,Math.PI*2);ctx.fillStyle=`rgba(0,217,255,${this.a})`;ctx.fill();}
}
for(let i=0;i<90;i++)particles.push(new Particle());
function loop(){
  ctx.clearRect(0,0,W,H);
  for(let p of particles){p.update();p.draw();}
  for(let i=0;i<particles.length;i++)
    for(let j=i+1;j<particles.length;j++){
      let d=Math.hypot(particles[i].x-particles[j].x,particles[i].y-particles[j].y);
      if(d<120){ctx.beginPath();ctx.strokeStyle=`rgba(0,150,200,${.08*(1-d/120)})`;ctx.lineWidth=.6;ctx.moveTo(particles[i].x,particles[i].y);ctx.lineTo(particles[j].x,particles[j].y);ctx.stroke();}
    }
  requestAnimationFrame(loop);
}
loop();

// ── LOADER ──
const fill=document.getElementById('loader-fill');
const loaderText=document.getElementById('loader-text');
const messages=['INITIALIZING SYSTEM...','LOADING CREDENTIALS...','ESTABLISHING SECURE TUNNEL...','MOUNTING INFRASTRUCTURE...','ACCESS GRANTED'];
let pct=0;
const interval=setInterval(()=>{
  pct+=Math.random()*4+1;
  if(pct>=100){pct=100;clearInterval(interval);
    loaderText.textContent='ACCESS GRANTED ✓';
    setTimeout(()=>{
      document.getElementById('loader').style.opacity='0';
      document.getElementById('loader').style.transition='opacity .6s';
      setTimeout(()=>{document.getElementById('loader').style.display='none';document.getElementById('app').classList.add('ready');},600);
    },600);
  } else {
    loaderText.textContent=messages[Math.floor(pct/25)]||messages[0];
  }
  fill.style.width=pct+'%';
},60);

// ── TYPED TITLE ──
const titles=['IT Infrastructure Architect','Cybersecurity Engineer','System Administrator','Hospitality IT Manager'];
let ti=0,ci=0,deleting=false;
const titleEl=document.getElementById('typed-title');
function typeEffect(){
  const current=titles[ti];
  if(!deleting){
    titleEl.textContent=current.slice(0,ci+1);
    ci++;
    if(ci===current.length){deleting=true;setTimeout(typeEffect,2000);return;}
  } else {
    titleEl.textContent=current.slice(0,ci-1);
    ci--;
    if(ci===0){deleting=false;ti=(ti+1)%titles.length;}
  }
  setTimeout(typeEffect,deleting?50:80);
}
setTimeout(typeEffect,1800);

// ── INTERSECTION OBSERVER ──
const revealEls=document.querySelectorAll('.reveal');
const obs=new IntersectionObserver(entries=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      e.target.classList.add('visible');
      // skill bars
      e.target.querySelectorAll('.skill-bar').forEach(b=>{b.style.transform=`scaleX(${b.dataset.w/100})`;});
      // counters
      e.target.querySelectorAll('.count').forEach(c=>{
        const target=+c.dataset.target;let current=0;
        const step=target/60;
        const t=setInterval(()=>{current+=step;if(current>=target){current=target;clearInterval(t);}c.textContent=Math.floor(current);},25);
      });
    }
  });
},{threshold:.15});
revealEls.forEach(el=>obs.observe(el));

// skill bars in already-visible areas
document.querySelectorAll('.skill-bar').forEach(b=>{
  const bar=b;
  const parentReveal=bar.closest('.reveal');
  if(!parentReveal){bar.style.transform=`scaleX(${bar.dataset.w/100})`;}
});
</script>
</body>
</html>
