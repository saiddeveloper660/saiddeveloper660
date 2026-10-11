<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Said Developer | Profile</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;500;700&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #000;
    --panel: rgba(0, 12, 8, 0.82);
    --green: #00ff9c;
    --green-dim: #0a8f5c;
    --text: #c9d1d9;
    --line: rgba(0, 255, 156, 0.35);
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  html { scroll-behavior: smooth; }
  body {
    background: var(--bg);
    color: var(--text);
    font-family: "Fira Code", ui-monospace, Menlo, Consolas, monospace;
    line-height: 1.6;
    min-height: 100vh;
    overflow-x: hidden;
  }
  #rain { position: fixed; inset: 0; z-index: 0; opacity: 0.35; }
  body::after {
    content: ""; position: fixed; inset: 0; z-index: 3; pointer-events: none;
    background: repeating-linear-gradient(0deg, rgba(0,0,0,0.18) 0 1px, transparent 1px 3px);
  }
  main { position: relative; z-index: 2; max-width: 920px; margin: 0 auto; padding: 32px 16px 64px; }

  .window {
    background: var(--panel);
    border: 1px solid var(--line);
    border-radius: 8px;
    margin-bottom: 28px;
    box-shadow: 0 0 24px rgba(0, 255, 156, 0.08);
    backdrop-filter: blur(3px);
  }
  .bar {
    display: flex; align-items: center; gap: 8px;
    padding: 8px 14px; border-bottom: 1px solid var(--line);
    font-size: 12px; color: var(--green-dim);
  }
  .dot { width: 10px; height: 10px; border-radius: 50%; background: var(--green-dim); }
  .dot:nth-child(1) { background: #ff5f56; }
  .dot:nth-child(2) { background: #ffbd2e; }
  .dot:nth-child(3) { background: var(--green); }
  .bar span { margin-left: 8px; }
  .body { padding: 20px; }

  /* hero */
  .hero { text-align: center; padding: 36px 16px 28px; }
  .glitch {
    position: relative; display: inline-block;
    font-size: clamp(32px, 9vw, 68px); font-weight: 700; letter-spacing: 0.04em;
    color: var(--green); text-shadow: 0 0 14px rgba(0,255,156,0.6);
  }
  .glitch::before, .glitch::after {
    content: attr(data-text); position: absolute; inset: 0; overflow: hidden;
  }
  .glitch::before { color: #ff2e63; transform: translate(2px, 0); clip-path: inset(0 0 60% 0); animation: gl1 3.2s infinite steps(1); }
  .glitch::after  { color: #08d9ff; transform: translate(-2px, 0); clip-path: inset(55% 0 0 0); animation: gl2 3.2s infinite steps(1); }
  @keyframes gl1 { 0%,88%,100% { opacity: 0; } 90% { opacity: .9; transform: translate(4px,-1px); } 94% { opacity: .9; transform: translate(-3px,1px); } }
  @keyframes gl2 { 0%,90%,100% { opacity: 0; } 92% { opacity: .9; transform: translate(-4px,1px); } 96% { opacity: .9; transform: translate(3px,-1px); } }

  .typing { min-height: 1.8em; margin-top: 14px; font-size: clamp(14px, 3.6vw, 20px); color: var(--green); font-weight: 500; }
  .caret { display: inline-block; width: 0.6em; height: 1.1em; background: var(--green); vertical-align: text-bottom; margin-left: 2px; animation: blink 1s steps(1) infinite; }
  @keyframes blink { 50% { opacity: 0; } }
  .sub { margin-top: 10px; color: var(--text); font-size: 14px; }

  .badges { display: flex; flex-wrap: wrap; justify-content: center; gap: 10px; margin-top: 20px; }
  .badge {
    color: var(--green); text-decoration: none; font-size: 13px; font-weight: 500;
    border: 1px solid var(--green); padding: 7px 14px; border-radius: 4px; background: #000;
    transition: background .2s, color .2s, box-shadow .2s;
  }
  .badge:hover, .badge:focus-visible { background: var(--green); color: #000; box-shadow: 0 0 14px var(--green); outline: none; }

  h2 { font-size: 15px; font-weight: 500; color: var(--green); margin-bottom: 14px; }
  h2::before { content: "$ "; color: var(--green-dim); }

  pre { font-family: inherit; font-size: 13px; white-space: pre-wrap; word-break: break-word; }
  .prompt { color: var(--green-dim); }
  .cmd { color: var(--green); }

  .sysinfo { overflow-x: auto; }
  .sysinfo pre { color: var(--green); white-space: pre; font-size: 12.5px; min-width: max-content; }

  .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 14px; }
  .card {
    display: block; text-decoration: none; color: var(--text);
    border: 1px solid var(--line); border-radius: 6px; padding: 16px; background: rgba(0,0,0,0.5);
    transition: border-color .2s, box-shadow .2s, transform .2s;
  }
  .card:hover, .card:focus-visible { border-color: var(--green); box-shadow: 0 0 18px rgba(0,255,156,0.25); transform: translateY(-2px); outline: none; }
  .card h3 { color: var(--green); font-size: 15px; margin-bottom: 6px; }
  .card p { font-size: 13px; }
  .card .go { display: inline-block; margin-top: 12px; font-size: 12px; color: var(--green); border: 1px solid var(--green-dim); padding: 3px 10px; border-radius: 3px; }

  .icons, .stats { display: flex; flex-wrap: wrap; justify-content: center; gap: 12px; }
  .stats img, .icons img { max-width: 100%; height: auto; }
  .tags { margin-top: 14px; }

  .closing { text-align: center; }
  .closing .typing { margin: 16px 0 0; }

  @media (max-width: 520px) {
    .body { padding: 14px; }
    pre { font-size: 12px; }
    .sysinfo pre { font-size: 11px; }
  }
  @media (prefers-reduced-motion: reduce) {
    .glitch::before, .glitch::after, .caret { animation: none; }
    .card, .badge { transition: none; }
    #rain { display: none; }
  }
</style>
</head>
<body>
<canvas id="rain" aria-hidden="true"></canvas>

<main>

  <!-- HERO -->
  <section class="window">
    <div class="bar"><i class="dot"></i><i class="dot"></i><i class="dot"></i><span>root@said: ~</span></div>
    <div class="hero">
      <h1 class="glitch" data-text="SAID DEVELOPER">SAID DEVELOPER</h1>
      <div class="typing" id="typing" aria-live="polite"></div>
      <p class="sub">Developer • Open-Source Builder • Security Research Enthusiast<br>Creating practical tools, browser extensions, and privacy-focused projects.</p>
      <div class="badges">
        <a class="badge" href="https://github.com/saiddeveloper660" target="_blank" rel="noopener">GitHub: saiddeveloper660</a>
        <a class="badge" href="https://www.saidddeveloper.com" target="_blank" rel="noopener">Portfolio: Visit</a>
      </div>
    </div>
  </section>

  <!-- WHOAMI -->
  <section class="window">
    <div class="bar"><i class="dot"></i><i class="dot"></i><i class="dot"></i><span>whoami</span></div>
    <div class="body">
      <pre><span class="prompt">┌──(said㉿github)-[~]
└─$</span> <span class="cmd">whoami</span>
Said Developer

<span class="prompt">┌──(said㉿github)-[~]
└─$</span> <span class="cmd">cat mission.txt</span>
Build useful, privacy-aware, open-source software.
Learn continuously. Share knowledge. Make technology accessible.

<span class="prompt">┌──(said㉿github)-[~]
└─$</span> <span class="cmd">cat /etc/rules</span>
Security work is performed only on systems I own
or have explicit permission to test.

<span class="prompt">┌──(said㉿github)-[~]
└─$</span> <span class="caret"></span></pre>
    </div>
  </section>

  <!-- SYSTEM INFO -->
  <section class="window">
    <div class="bar"><i class="dot"></i><i class="dot"></i><i class="dot"></i><span>system-info</span></div>
    <div class="body sysinfo">
      <h2>ls ./system-info</h2>
<pre>┌──────────────────────────────────────────────┐
│  OS        : Linux / Windows                 │
│  SHELL     : bash                            │
│  ROLE      : Developer • Open-Source Builder │
│  FOCUS     : Web • Extensions • Privacy      │
│  LANGS     : HTML  CSS  JS  Python           │
│  STATUS    : [ ONLINE ]                      │
└──────────────────────────────────────────────┘</pre>
    </div>
  </section>

  <!-- PROJECTS -->
  <section class="window">
    <div class="bar"><i class="dot"></i><i class="dot"></i><i class="dot"></i><span>featured-projects</span></div>
    <div class="body">
      <h2>./featured-projects --list</h2>
      <div class="grid">
        <a class="card" href="https://github.com/saiddeveloper660/said-full-screen" target="_blank" rel="noopener">
          <h3>⛶ Said Full Screen</h3>
          <p>A browser extension designed to make browsing more immersive with fullscreen support.</p>
          <span class="go">Explore repository</span>
        </a>
        <a class="card" href="https://github.com/saiddeveloper660/Said-Background-Recorder" target="_blank" rel="noopener">
          <h3>◉ Said Background Recorder</h3>
          <p>A background video recording project. Check the repository for its current capabilities and permissions.</p>
          <span class="go">Explore repository</span>
        </a>
        <a class="card" href="https://github.com/saiddeveloper660/Said-Password-Manager-" target="_blank" rel="noopener">
          <h3>🔐 Said Password Manager</h3>
          <p>A password-management project. See the repository for its current features and security notes.</p>
          <span class="go">Explore repository</span>
        </a>
        <a class="card" href="https://github.com/saiddeveloper660/search-everywhere-pro" target="_blank" rel="noopener">
          <h3>⌕ Search Everywhere Pro</h3>
          <p>A privacy-minded browser extension for searching across multiple websites.</p>
          <span class="go">Explore repository</span>
        </a>
      </div>
    </div>
  </section>

  <!-- TOOLKIT -->
  <section class="window">
    <div class="bar"><i class="dot"></i><i class="dot"></i><i class="dot"></i><span>toolkit.conf</span></div>
    <div class="body">
      <h2>cat toolkit.conf</h2>
      <div class="icons">
        <img src="https://skillicons.dev/icons?i=html,css,js,python,git,github,vscode,linux,bash&theme=dark" alt="Technology icons">
      </div>
      <div class="icons tags">
        <img src="https://img.shields.io/badge/Open%20Source-000000?style=for-the-badge&logo=github&logoColor=00FF9C" alt="Open Source">
        <img src="https://img.shields.io/badge/Web%20Development-000000?style=for-the-badge&logo=googlechrome&logoColor=00FF9C" alt="Web Development">
        <img src="https://img.shields.io/badge/Ethical%20Security-000000?style=for-the-badge&logo=kalilinux&logoColor=00FF9C" alt="Ethical Security">
        <img src="https://img.shields.io/badge/Privacy%20First-000000?style=for-the-badge&logo=torproject&logoColor=00FF9C" alt="Privacy First">
      </div>
    </div>
  </section>

  <!-- STATS -->
  <section class="window">
    <div class="bar"><i class="dot"></i><i class="dot"></i><i class="dot"></i><span>git-log --stats</span></div>
    <div class="body">
      <h2>git log --stats</h2>
      <div class="stats">
        <img height="165" src="https://github-readme-stats.vercel.app/api?username=saiddeveloper660&show_icons=true&hide_border=true&bg_color=000000&title_color=00FF9C&icon_color=00FF9C&text_color=C9D1D9&rank_icon=github" alt="GitHub stats">
        <img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=saiddeveloper660&layout=compact&hide_border=true&bg_color=000000&title_color=00FF9C&text_color=C9D1D9" alt="Top languages">
      </div>
      <div class="stats" style="margin-top:14px">
        <img width="95%" src="https://streak-stats.demolab.com?user=saiddeveloper660&theme=dark&background=000000&hide_border=true&ring=00FF9C&fire=00FF9C&currStreakLabel=00FF9C&currStreakNum=FFFFFF&sideNums=FFFFFF&sideLabels=00FF9C&dates=8B949E" alt="GitHub streak stats">
      </div>
      <div class="stats" style="margin-top:14px">
        <img src="https://github-profile-trophy.vercel.app/?username=saiddeveloper660&theme=matrix&no-frame=true&no-bg=true&margin-w=10&row=1" alt="GitHub trophies">
      </div>
    </div>
  </section>

  <!-- CONTRIBUTIONS -->
  <section class="window">
    <div class="bar"><i class="dot"></i><i class="dot"></i><i class="dot"></i><span>contributions</span></div>
    <div class="body">
      <h2>./contributions --graph</h2>
      <div class="stats">
        <img width="100%" src="https://github-readme-activity-graph.vercel.app/graph?username=saiddeveloper660&bg_color=000000&color=00FF9C&line=00FF9C&point=FFFFFF&area=true&area_color=00FF9C&hide_border=true" alt="GitHub contribution activity graph">
      </div>
    </div>
  </section>

  <!-- CONNECT -->
  <section class="window closing">
    <div class="bar"><i class="dot"></i><i class="dot"></i><i class="dot"></i><span>connect</span></div>
    <div class="body">
      <h2>./connect --open</h2>
      <div class="badges">
        <a class="badge" href="https://github.com/saiddeveloper660" target="_blank" rel="noopener">GitHub: Follow</a>
        <a class="badge" href="https://www.saidddeveloper.com" target="_blank" rel="noopener">Website: saidddeveloper.com</a>
      </div>
      <div class="typing" id="typing2"></div>
    </div>
  </section>

</main>

<script>
  // Typing effect: cycles through lines, types and deletes
  function typer(el, lines, speed, hold) {
    var reduce = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
    if (reduce) { el.textContent = lines[0]; return; }
    var li = 0, ci = 0, deleting = false;
    var caret = document.createElement("span");
    caret.className = "caret";
    var text = document.createElement("span");
    el.appendChild(text); el.appendChild(caret);
    (function tick() {
      var line = lines[li];
      text.textContent = line.slice(0, ci);
      var delay = speed;
      if (!deleting && ci === line.length) { deleting = true; delay = hold; }
      else if (deleting && ci === 0) { deleting = false; li = (li + 1) % lines.length; delay = 350; }
      else { ci += deleting ? -1 : 1; if (deleting) delay = speed / 2; }
      setTimeout(tick, delay);
    })();
  }
  typer(document.getElementById("typing"), [
    "[+] Access granted...",
    "[+] Hi, I'm Said Developer",
    "[+] Open-Source Builder",
    "[+] Developer | Security Enthusiast",
    "[+] Building useful tools for everyone",
    "[+] Privacy first. Always."
  ], 60, 1400);
  typer(document.getElementById("typing2"), [
    "Open to collaboration on useful open-source projects.",
    "$ echo \"Let's build something useful\"",
    "[+] Connection established."
  ], 55, 1500);

  // Matrix rain
  (function () {
    var c = document.getElementById("rain"), ctx = c.getContext("2d");
    var chars = "01アイウエオカキクケコサシスセソ{}<>/;=+*$#".split("");
    var size = 16, cols, drops;
    function resize() {
      c.width = innerWidth; c.height = innerHeight;
      cols = Math.floor(c.width / size);
      drops = Array.from({ length: cols }, function () { return Math.random() * -50; });
    }
    resize(); addEventListener("resize", resize);
    function draw() {
      ctx.fillStyle = "rgba(0,0,0,0.08)";
      ctx.fillRect(0, 0, c.width, c.height);
      ctx.fillStyle = "#00ff9c";
      ctx.font = size + "px 'Fira Code', monospace";
      for (var i = 0; i < cols; i++) {
        ctx.fillText(chars[Math.floor(Math.random() * chars.length)], i * size, drops[i] * size);
        if (drops[i] * size > c.height && Math.random() > 0.975) drops[i] = 0;
        drops[i]++;
      }
    }
    setInterval(draw, 55);
  })();
</script>
</body>
</html>
