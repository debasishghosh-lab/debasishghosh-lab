<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Debasish Ghosh — AI · ML · Dev</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=Space+Mono:ital,wght@0,400;0,700;1,400&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;1,9..40,300&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #05070f;
    --surface: #0b0f1e;
    --border: #1a2040;
    --accent: #00f7ff;
    --accent2: #ff6b35;
    --accent3: #a855f7;
    --text: #e8eaf6;
    --muted: #5a6380;
    --glow: 0 0 30px rgba(0,247,255,0.15);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    font-weight: 300;
    line-height: 1.7;
    overflow-x: hidden;
  }

  /* ── NOISE TEXTURE ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 1000;
    opacity: 0.4;
  }

  /* ── GRID BG ── */
  .grid-bg {
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(0,247,255,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,247,255,0.03) 1px, transparent 1px);
    background-size: 60px 60px;
    pointer-events: none;
    z-index: 0;
  }

  /* ── HERO GLOW ORBS ── */
  .orb {
    position: fixed;
    border-radius: 50%;
    filter: blur(80px);
    pointer-events: none;
    z-index: 0;
  }
  .orb-1 { width: 600px; height: 600px; background: rgba(0,247,255,0.04); top: -200px; right: -200px; }
  .orb-2 { width: 500px; height: 500px; background: rgba(168,85,247,0.05); bottom: 0; left: -150px; }

  /* ── LAYOUT ── */
  .container {
    max-width: 900px;
    margin: 0 auto;
    padding: 0 32px;
    position: relative;
    z-index: 10;
  }

  /* ── HEADER ── */
  header {
    padding: 80px 0 60px;
    position: relative;
  }

  .eyebrow {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.3em;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 20px;
    opacity: 0;
    animation: fadeUp 0.6s ease forwards 0.1s;
  }

  h1 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(52px, 9vw, 96px);
    font-weight: 800;
    line-height: 0.95;
    letter-spacing: -0.03em;
    margin-bottom: 24px;
    opacity: 0;
    animation: fadeUp 0.6s ease forwards 0.2s;
  }

  h1 .name-first { color: var(--text); }
  h1 .name-last {
    display: block;
    -webkit-text-stroke: 1.5px var(--accent);
    color: transparent;
  }

  .tagline {
    font-family: 'DM Sans', sans-serif;
    font-size: 18px;
    font-weight: 300;
    color: var(--muted);
    margin-bottom: 40px;
    opacity: 0;
    animation: fadeUp 0.6s ease forwards 0.3s;
  }

  .tagline span {
    color: var(--text);
    font-weight: 400;
  }

  .pill-row {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 0.6s ease forwards 0.4s;
  }

  .pill {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    padding: 6px 14px;
    border: 1px solid var(--border);
    border-radius: 100px;
    color: var(--muted);
    background: rgba(255,255,255,0.02);
    letter-spacing: 0.05em;
    transition: all 0.2s;
  }

  .pill:hover {
    border-color: var(--accent);
    color: var(--accent);
    background: rgba(0,247,255,0.04);
  }

  .pill.active {
    border-color: var(--accent);
    color: var(--accent);
    background: rgba(0,247,255,0.06);
  }

  /* ── DIVIDER ── */
  .divider {
    height: 1px;
    background: linear-gradient(90deg, var(--accent) 0%, transparent 100%);
    margin: 60px 0;
    opacity: 0;
    animation: fadeIn 0.8s ease forwards 0.5s;
  }

  /* ── SECTION ── */
  section { margin-bottom: 80px; }

  .section-label {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.4em;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 32px;
    display: flex;
    align-items: center;
    gap: 16px;
  }

  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  h2 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(28px, 4vw, 40px);
    font-weight: 700;
    letter-spacing: -0.02em;
    margin-bottom: 16px;
    line-height: 1.1;
  }

  /* ── ABOUT ── */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 24px;
  }

  .about-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 28px;
    transition: border-color 0.3s, transform 0.3s;
  }

  .about-card:hover {
    border-color: rgba(0,247,255,0.3);
    transform: translateY(-2px);
  }

  .about-card.wide { grid-column: 1 / -1; }

  .card-icon {
    font-size: 28px;
    margin-bottom: 12px;
    display: block;
  }

  .card-label {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.2em;
    color: var(--muted);
    text-transform: uppercase;
    margin-bottom: 6px;
  }

  .card-value {
    font-size: 15px;
    color: var(--text);
    font-weight: 400;
  }

  /* ── PROJECTS ── */
  .project-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 40px;
    margin-bottom: 20px;
    position: relative;
    overflow: hidden;
    transition: border-color 0.3s, transform 0.3s;
  }

  .project-card:hover {
    border-color: rgba(0,247,255,0.25);
    transform: translateY(-3px);
  }

  .project-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent3));
    opacity: 0;
    transition: opacity 0.3s;
  }

  .project-card:hover::before { opacity: 1; }

  .project-card:nth-child(2)::before {
    background: linear-gradient(90deg, var(--accent2), var(--accent3));
  }

  .project-num {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.1em;
    margin-bottom: 16px;
  }

  .project-title {
    font-family: 'Syne', sans-serif;
    font-size: 26px;
    font-weight: 700;
    margin-bottom: 10px;
    letter-spacing: -0.02em;
  }

  .project-sub {
    font-size: 14px;
    color: var(--muted);
    margin-bottom: 20px;
    font-style: italic;
  }

  .project-desc {
    font-size: 15px;
    color: rgba(232,234,246,0.7);
    margin-bottom: 24px;
    line-height: 1.75;
  }

  .feature-list {
    display: flex;
    flex-direction: column;
    gap: 8px;
    margin-bottom: 28px;
  }

  .feature-item {
    display: flex;
    align-items: center;
    gap: 10px;
    font-size: 14px;
    color: var(--muted);
  }

  .feature-item::before {
    content: '▸';
    color: var(--accent);
    font-size: 10px;
    flex-shrink: 0;
  }

  .stack-row {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
  }

  .stack-tag {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    padding: 5px 12px;
    border-radius: 6px;
    background: rgba(0,247,255,0.06);
    border: 1px solid rgba(0,247,255,0.15);
    color: var(--accent);
    letter-spacing: 0.05em;
  }

  .project-card:nth-child(2) .stack-tag {
    background: rgba(255,107,53,0.06);
    border-color: rgba(255,107,53,0.2);
    color: var(--accent2);
  }

  /* ── TECH STACK ── */
  .tech-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
  }

  .tech-group {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 24px;
    transition: border-color 0.3s;
  }

  .tech-group:hover { border-color: rgba(0,247,255,0.2); }

  .tech-group-title {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.3em;
    color: var(--muted);
    text-transform: uppercase;
    margin-bottom: 16px;
  }

  .tech-items {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .tech-item {
    display: flex;
    align-items: center;
    gap: 10px;
    font-size: 14px;
    color: var(--text);
  }

  .tech-dot {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: var(--accent);
    flex-shrink: 0;
  }

  /* ── TECH LOGO GRID ── */
  .tech-logo-section { }

  .tech-category {
    margin-bottom: 32px;
  }

  .tech-category-title {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.35em;
    color: var(--muted);
    text-transform: uppercase;
    margin-bottom: 16px;
  }

  .tech-logo-row {
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
  }

  .tech-logo-chip {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 10px 16px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 10px;
    font-size: 13px;
    color: var(--text);
    font-weight: 400;
    transition: all 0.22s;
    cursor: default;
  }

  .tech-logo-chip:hover {
    border-color: rgba(0,247,255,0.35);
    background: rgba(0,247,255,0.04);
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(0,247,255,0.08);
  }

  .tech-logo-chip img {
    width: 22px;
    height: 22px;
    object-fit: contain;
    display: block;
    filter: brightness(0.9);
    transition: filter 0.2s;
  }

  .tech-logo-chip:hover img { filter: brightness(1.15); }

  /* ── DSA ── */
  .dsa-block {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 40px;
    display: grid;
    grid-template-columns: auto 1fr;
    gap: 40px;
    align-items: center;
  }

  .dsa-count {
    font-family: 'Syne', sans-serif;
    font-size: 80px;
    font-weight: 800;
    -webkit-text-stroke: 2px var(--accent);
    color: transparent;
    line-height: 1;
    white-space: nowrap;
  }

  .dsa-count span {
    font-size: 36px;
    display: block;
    -webkit-text-stroke: 1px var(--accent);
  }

  .dsa-topics {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
  }

  .dsa-topic {
    font-size: 13px;
    color: var(--muted);
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .dsa-topic::before {
    content: '';
    width: 20px;
    height: 1px;
    background: var(--accent);
    display: block;
  }

  /* ── CERTS ── */
  .cert-list {
    display: flex;
    flex-direction: column;
    gap: 12px;
  }

  .cert-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 18px 24px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    transition: border-color 0.2s, transform 0.2s;
  }

  .cert-item:hover {
    border-color: rgba(168,85,247,0.3);
    transform: translateX(4px);
  }

  .cert-name {
    font-size: 14px;
    color: var(--text);
  }

  .cert-org {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    color: var(--accent3);
    letter-spacing: 0.1em;
  }

  /* ── CONNECT ── */
  .connect-row {
    display: flex;
    gap: 16px;
    flex-wrap: wrap;
  }

  .connect-btn {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 14px 24px;
    border: 1px solid var(--border);
    border-radius: 12px;
    text-decoration: none;
    color: var(--text);
    font-family: 'Space Mono', monospace;
    font-size: 12px;
    letter-spacing: 0.05em;
    background: var(--surface);
    transition: all 0.25s;
  }

  .connect-btn:hover {
    border-color: var(--accent);
    color: var(--accent);
    background: rgba(0,247,255,0.04);
    transform: translateY(-2px);
    box-shadow: 0 8px 24px rgba(0,247,255,0.08);
  }

  .connect-btn svg { width: 18px; height: 18px; fill: currentColor; }

  /* ── GITHUB STATS ── */
  .stats-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }

  .stats-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    overflow: hidden;
  }

  .stats-card img {
    width: 100%;
    display: block;
    border-radius: 16px;
  }

  /* ── FOOTER ── */
  footer {
    border-top: 1px solid var(--border);
    padding: 40px 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    color: var(--muted);
  }

  /* ── ANIMATIONS ── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }

  .reveal {
    opacity: 0;
    transform: translateY(24px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }

  .reveal.visible {
    opacity: 1;
    transform: none;
  }

  /* ── CURSOR TRAIL ── */
  .cursor-glow {
    position: fixed;
    width: 300px;
    height: 300px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(0,247,255,0.05) 0%, transparent 70%);
    pointer-events: none;
    transform: translate(-50%, -50%);
    transition: left 0.1s, top 0.1s;
    z-index: 5;
  }

  @media (max-width: 680px) {
    .about-grid { grid-template-columns: 1fr; }
    .about-card.wide { grid-column: 1; }
    .tech-grid { grid-template-columns: 1fr 1fr; }
    .dsa-block { grid-template-columns: 1fr; text-align: center; }
    .dsa-count { font-size: 60px; }
    .dsa-topics { justify-items: center; }
    .stats-grid { grid-template-columns: 1fr; }
    footer { flex-direction: column; gap: 12px; text-align: center; }
  }
</style>
</head>
<body>

<div class="grid-bg"></div>
<div class="orb orb-1"></div>
<div class="orb orb-2"></div>
<div class="cursor-glow" id="cursor"></div>

<div class="container">

  <!-- ── HEADER ── -->
  <header>
    <div class="eyebrow">👋 Hello, World</div>
    <h1>
      <span class="name-first">Debasish</span>
      <span class="name-last">Ghosh</span>
    </h1>
    <p class="tagline">
      <span>AI · Machine Learning · Software Development</span><br>
      B.Tech CSE (AI-ML) @ Sister Nivedita University, Kolkata
    </p>
    <div class="pill-row">
      <span class="pill active">Artificial Intelligence</span>
      <span class="pill">Machine Learning</span>
      <span class="pill">Real-time Web Apps</span>
      <span class="pill">DSA</span>
      <span class="pill">Predictive Systems</span>
    </div>
  </header>

  <div class="divider"></div>

  <!-- ── ABOUT ── -->
  <section class="reveal">
    <div class="section-label">01 — About</div>
    <div class="about-grid">
      <div class="about-card wide">
        <span class="card-icon">⚡</span>
        <div class="card-label">Focus</div>
        <div class="card-value" style="font-size:17px; line-height:1.6;">
          Currently building <strong style="color:var(--accent)">AI-powered predictive systems</strong> and scalable real-time applications — combining machine learning intuition with clean software engineering.
        </div>
      </div>
      <div class="about-card">
        <span class="card-icon">📍</span>
        <div class="card-label">Location</div>
        <div class="card-value">Kolkata, India</div>
      </div>
      <div class="about-card">
        <span class="card-icon">🎓</span>
        <div class="card-label">Degree</div>
        <div class="card-value">B.Tech CSE (AI-ML)</div>
      </div>
    </div>
  </section>

  <!-- ── PROJECTS ── -->
  <section class="reveal">
    <div class="section-label">02 — Featured Projects</div>

    <div class="project-card">
      <div class="project-num">PROJECT 01</div>
      <div class="project-title">PredictOstock</div>
      <div class="project-sub">AI Inventory Forecasting Platform</div>
      <div class="project-desc">
        An AI-powered platform that predicts inventory stockouts by analyzing sales trends and historical data — giving businesses a smarter way to manage stock before problems arise.
      </div>
      <div class="feature-list">
        <div class="feature-item">Sales trend analysis with time-series modeling</div>
        <div class="feature-item">Inventory risk prediction engine</div>
        <div class="feature-item">Data-driven restocking forecasts</div>
        <div class="feature-item">Smart stock management dashboard</div>
      </div>
      <div class="stack-row">
        <span class="stack-tag"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg" style="width:14px;height:14px;vertical-align:middle;margin-right:5px;">Python</span>
        <span class="stack-tag"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/flask/flask-original.svg" style="width:14px;height:14px;vertical-align:middle;margin-right:5px;filter:hue-rotate(180deg) brightness(1.5);">Flask</span>
        <span class="stack-tag"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/react/react-original.svg" style="width:14px;height:14px;vertical-align:middle;margin-right:5px;">React</span>
      </div>
    </div>

    <div class="project-card">
      <div class="project-num">PROJECT 02</div>
      <div class="project-title">CodeCollab</div>
      <div class="project-sub">Real-Time Collaborative Code Editor</div>
      <div class="project-desc">
        A multi-user coding environment where developers can write, edit, and share code together in real time — built for pair programming, interviews, and remote collaboration.
      </div>
      <div class="feature-list">
        <div class="feature-item">Live multi-user editing with conflict resolution</div>
        <div class="feature-item">Real-time synchronization via WebSockets</div>
        <div class="feature-item">File sharing and session management</div>
        <div class="feature-item">Fully responsive interface</div>
      </div>
      <div class="stack-row">
        <span class="stack-tag"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/react/react-original.svg" style="width:14px;height:14px;vertical-align:middle;margin-right:5px;">React</span>
        <span class="stack-tag"><img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/socketio/socketio-original.svg" style="width:14px;height:14px;vertical-align:middle;margin-right:5px;filter:hue-rotate(180deg) brightness(1.5);">Socket.io</span>
      </div>
    </div>
  </section>

  <!-- ── TECH STACK ── -->
  <section class="reveal">
    <div class="section-label">03 — Tech Stack</div>
    <div class="tech-logo-section">

      <div class="tech-category">
        <div class="tech-category-title">Languages</div>
        <div class="tech-logo-row">
          <div class="tech-logo-chip">
            <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg" alt="Python" />
            Python
          </div>
          <div class="tech-logo-chip">
            <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/cplusplus/cplusplus-original.svg" alt="C++" />
            C++
          </div>
          <div class="tech-logo-chip">
            <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/c/c-original.svg" alt="C" />
            C
          </div>
        </div>
      </div>

      <div class="tech-category">
        <div class="tech-category-title">Web Development</div>
        <div class="tech-logo-row">
          <div class="tech-logo-chip">
            <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/react/react-original.svg" alt="React" />
            React
          </div>
          <div class="tech-logo-chip">
            <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg" alt="JavaScript" />
            JavaScript
          </div>
          <div class="tech-logo-chip">
            <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg" alt="HTML5" />
            HTML5
          </div>
          <div class="tech-logo-chip">
            <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/css3/css3-original.svg" alt="CSS3" />
            CSS3
          </div>
        </div>
      </div>

      <div class="tech-category">
        <div class="tech-category-title">Frameworks & Tools</div>
        <div class="tech-logo-row">
          <div class="tech-logo-chip">
            <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/flask/flask-original.svg" alt="Flask" style="filter:invert(1) brightness(0.8);" />
            Flask
          </div>
          <div class="tech-logo-chip">
            <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/git/git-original.svg" alt="Git" />
            Git
          </div>
          <div class="tech-logo-chip">
            <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg" alt="GitHub" style="filter:invert(1) brightness(0.85);" />
            GitHub
          </div>
          <div class="tech-logo-chip">
            <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/socketio/socketio-original.svg" alt="Socket.io" style="filter:invert(1) brightness(0.85);" />
            Socket.io
          </div>
        </div>
      </div>

    </div>
  </section>

  <!-- ── DSA ── -->
  <section class="reveal">
    <div class="section-label">04 — Problem Solving</div>
    <div class="dsa-block">
      <div>
        <div class="dsa-count">120<span>problems+</span></div>
      </div>
      <div>
        <div style="font-size:13px; color:var(--muted); margin-bottom:16px; font-family:'Space Mono',monospace; letter-spacing:0.1em;">SOLVED ON GEEKSFORGEEKS</div>
        <div class="dsa-topics">
          <div class="dsa-topic">Arrays</div>
          <div class="dsa-topic">Linked Lists</div>
          <div class="dsa-topic">Stacks & Queues</div>
          <div class="dsa-topic">Trees & Graphs</div>
          <div class="dsa-topic">Sorting & Searching</div>
          <div class="dsa-topic">Algorithm Design</div>
        </div>
      </div>
    </div>
  </section>

  <!-- ── GITHUB STATS ── -->
  <section class="reveal">
    <div class="section-label">05 — GitHub Analytics</div>
    <div class="stats-grid">
      <div class="stats-card">
        <img src="https://github-readme-stats.vercel.app/api?username=debasishghosh-lab&show_icons=true&theme=tokyonight&hide_border=true&bg_color=0b0f1e&title_color=00f7ff&icon_color=00f7ff&text_color=e8eaf6" alt="GitHub Stats" loading="lazy" />
      </div>
      <div class="stats-card">
        <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=debasishghosh-lab&layout=compact&theme=tokyonight&hide_border=true&bg_color=0b0f1e&title_color=00f7ff&text_color=e8eaf6" alt="Top Languages" loading="lazy" />
      </div>
    </div>
    <div style="margin-top:16px;">
      <div class="stats-card">
        <img src="https://streak-stats.demolab.com/?user=debasishghosh-lab&theme=tokyonight&hide_border=true&background=0b0f1e&stroke=1a2040&ring=00f7ff&fire=ff6b35&currStreakLabel=00f7ff" alt="GitHub Streak" loading="lazy" style="width:100%; border-radius:16px;" />
      </div>
    </div>
  </section>

  <!-- ── CERTIFICATIONS ── -->
  <section class="reveal">
    <div class="section-label">06 — Certifications</div>
    <div class="cert-list">
      <div class="cert-item">
        <div class="cert-name">Foundations of Data Structures and Algorithms</div>
        <div class="cert-org">Univ. of Colorado Boulder</div>
      </div>
      <div class="cert-item">
        <div class="cert-name">Introduction to Artificial Intelligence</div>
        <div class="cert-org">IBM</div>
      </div>
      <div class="cert-item">
        <div class="cert-name">Introduction to Generative AI</div>
        <div class="cert-org">Google Cloud</div>
      </div>
      <div class="cert-item">
        <div class="cert-name">Generative AI Applications</div>
        <div class="cert-org">IBM</div>
      </div>
      <div class="cert-item">
        <div class="cert-name">Machine Learning & NLP Basics</div>
        <div class="cert-org">Edureka</div>
      </div>
    </div>
  </section>

  <!-- ── CONNECT ── -->
  <section class="reveal">
    <div class="section-label">07 — Connect</div>
    <h2 style="margin-bottom:24px;">Let's build something together.</h2>
    <div class="connect-row">
      <a href="https://linkedin.com" class="connect-btn" target="_blank">
        <svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
        LinkedIn
      </a>
      <a href="https://github.com/debasishghosh-lab" class="connect-btn" target="_blank">
        <svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/></svg>
        GitHub
      </a>
    </div>
  </section>

  <!-- ── FOOTER ── -->
  <footer>
    <span>Debasish Ghosh © 2025</span>
    <span style="color:var(--accent)">AI · ML · Dev</span>
  </footer>

</div>

<script>
  // Cursor glow
  const cursor = document.getElementById('cursor');
  document.addEventListener('mousemove', e => {
    cursor.style.left = e.clientX + 'px';
    cursor.style.top = e.clientY + 'px';
  });

  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver(entries => {
    entries.forEach((entry, i) => {
      if (entry.isIntersecting) {
        setTimeout(() => entry.target.classList.add('visible'), i * 80);
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.1 });
  reveals.forEach(el => observer.observe(el));
</script>
</body>
</html>
