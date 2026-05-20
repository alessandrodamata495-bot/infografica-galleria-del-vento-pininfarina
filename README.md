# infografica-galleria-del-vento-pininfarina<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Pininfarina – Il Tempio del Vento: 50 Anni di Innovazione Aerodinamica</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:ital,wght@0,300;0,400;0,500;0,700;1,300&family=DM+Serif+Display:ital@0;1&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #050d1a;
    --surface: #0b1929;
    --surface2: #102035;
    --border: rgba(100,180,255,0.13);
    --accent: #1e9fff;
    --accent2: #f5a623;
    --accent3: #3dffd0;
    --text: #e8f2ff;
    --muted: #7a9bbf;
    --danger: #ff4f4f;
    --card-glow: 0 0 30px rgba(30,159,255,0.12);
    --radius: 18px;
  }
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    font-weight: 300;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* ── BACKGROUND MESH ── */
  body::before {
    content:'';
    position:fixed; inset:0; z-index:0; pointer-events:none;
    background:
      radial-gradient(ellipse 80% 50% at 20% 10%, rgba(30,159,255,0.08) 0%, transparent 60%),
      radial-gradient(ellipse 60% 40% at 80% 80%, rgba(245,166,35,0.06) 0%, transparent 60%),
      radial-gradient(ellipse 40% 30% at 60% 30%, rgba(61,255,208,0.05) 0%, transparent 60%);
  }

  /* ── HEADER ── */
  header {
    position: relative; z-index: 10;
    padding: 60px 40px 40px;
    text-align: center;
    border-bottom: 1px solid var(--border);
    background: linear-gradient(180deg, rgba(5,13,26,0.0) 0%, rgba(5,13,26,0.95) 100%);
  }
  header .eyebrow {
    font-family: 'DM Sans', sans-serif;
    font-size: 11px; font-weight: 500; letter-spacing: 4px;
    text-transform: uppercase; color: var(--accent);
    margin-bottom: 12px;
    display: inline-block;
    border: 1px solid rgba(30,159,255,0.3);
    padding: 4px 14px; border-radius: 20px;
    background: rgba(30,159,255,0.06);
  }
  header h1 {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(2.4rem, 6vw, 5rem);
    letter-spacing: 2px;
    line-height: 1.05;
    background: linear-gradient(135deg, #ffffff 30%, var(--accent) 70%, var(--accent3) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
    margin-bottom: 16px;
  }
  header .subtitle {
    max-width: 700px; margin: 0 auto 30px;
    color: var(--muted); font-size: 1.05rem; line-height: 1.7;
  }
  .stat-bar {
    display: flex; justify-content: center; gap: 40px; flex-wrap: wrap;
    margin-top: 30px;
  }
  .stat-item { text-align:center; }
  .stat-num {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 2.6rem; color: var(--accent2);
    display: block; line-height: 1;
  }
  .stat-label { font-size: 0.72rem; letter-spacing: 2px; color: var(--muted); text-transform: uppercase; }

  /* ── WIND TUNNEL ANIMATION (Göttingen closed-circuit) ── */
  .wind-hero {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px 20px 10px;
    position: relative; z-index: 5;
    width: 100%;
  }
  .wt-svg {
    max-width: 100%;
    height: auto;
    display: block;
    margin: 0 auto;
  }

  /* Tunnel structural elements */
  .wt-duct {
    fill: rgba(30,159,255,0.04);
    stroke: rgba(100,180,255,0.35);
    stroke-width: 1.2;
  }
  .wt-duct-inner {
    fill: none;
    stroke: rgba(100,180,255,0.18);
    stroke-width: 1;
    stroke-dasharray: 3 4;
  }
  .wt-label {
    font-family: 'DM Sans', sans-serif;
    font-size: 9px;
    font-weight: 500;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    fill: var(--muted);
  }
  .wt-label-accent { fill: var(--accent); }

  /* Honeycomb pattern in settling chamber */
  .wt-honeycomb line {
    stroke: rgba(61,255,208,0.45);
    stroke-width: 0.8;
  }
  /* Screens (turbulence reduction) */
  .wt-screen {
    stroke: rgba(61,255,208,0.55);
    stroke-width: 0.7;
  }
  /* Corner turning vanes */
  .wt-vanes path {
    stroke: rgba(245,166,35,0.5);
    stroke-width: 0.9;
    fill: none;
  }

  /* Static fan hub (no rotating blades to avoid visual noise) */
  .wt-fan-hub {
    fill: var(--accent2);
    opacity: 0.85;
  }

  /* Streamlines — different speeds along the circuit
     The path is shared (defined in <defs>), the dashes "scroll" via stroke-dashoffset.
     Speed is faster in test section (visually): we use multiple offset particles. */
  .wt-streamline {
    fill: none;
    stroke-linecap: round;
  }
  .wt-sl-1 {
    stroke: var(--accent);
    stroke-width: 1.6;
    stroke-dasharray: 14 240;
    stroke-dashoffset: 0;
    animation: streamFlow 4s linear infinite;
    opacity: 0.95;
  }
  .wt-sl-2 {
    stroke: var(--accent3);
    stroke-width: 1.4;
    stroke-dasharray: 10 240;
    stroke-dashoffset: -80;
    animation: streamFlow 4s linear infinite;
    opacity: 0.85;
  }
  .wt-sl-3 {
    stroke: var(--accent);
    stroke-width: 1.2;
    stroke-dasharray: 8 240;
    stroke-dashoffset: -160;
    animation: streamFlow 4s linear infinite;
    opacity: 0.7;
  }
  .wt-sl-4 {
    stroke: var(--accent3);
    stroke-width: 1;
    stroke-dasharray: 6 240;
    stroke-dashoffset: -200;
    animation: streamFlow 4s linear infinite;
    opacity: 0.6;
  }
  @keyframes streamFlow {
    to { stroke-dashoffset: -2240; }
  }

  /* Wake (vortices) behind the car */
  .wt-wake {
    fill: none;
    stroke: var(--accent2);
    stroke-width: 1;
    stroke-dasharray: 3 5;
    opacity: 0.6;
    animation: wakeShimmer 1.8s ease-in-out infinite;
  }
  @keyframes wakeShimmer {
    0%, 100% { opacity: 0.3; stroke-dashoffset: 0; }
    50% { opacity: 0.75; stroke-dashoffset: -16; }
  }

  /* Pressure-color gradient stripe on the contractor (high→low static pressure) */
  .wt-pressure-arrow {
    stroke: var(--accent);
    stroke-width: 1;
    fill: none;
    opacity: 0.5;
  }

  /* Velocity indicator near test section */
  .wt-velocity-tag {
    font-family: 'DM Sans', sans-serif;
    font-size: 8.5px;
    font-weight: 700;
    letter-spacing: 1px;
    fill: var(--accent3);
  }

  @media (max-width: 720px) {
    .wt-label, .wt-velocity-tag { font-size: 7px; letter-spacing: 1px; }
  }

  /* ── GRID ── */
  .grid-section {
    position: relative; z-index: 5;
    padding: 50px 40px;
    max-width: 1400px; margin: 0 auto;
  }
  .section-label {
    font-size: 10px; letter-spacing: 4px; text-transform: uppercase;
    color: var(--accent); font-weight: 500;
    margin-bottom: 8px;
  }
  .section-title {
    font-family: 'DM Serif Display', serif;
    font-size: clamp(1.4rem, 3vw, 2rem);
    margin-bottom: 30px;
    color: var(--text);
  }

  .cards-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 22px;
  }

  /* ── CARD ── */
  .card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 28px 26px 24px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
    transition: transform 0.3s cubic-bezier(.22,.68,0,1.2), box-shadow 0.3s ease, border-color 0.3s ease;
    opacity: 0;
    transform: translateY(30px);
  }
  .card.visible { animation: slideUp 0.55s cubic-bezier(.22,.68,0,1.2) forwards; }
  @keyframes slideUp {
    to { opacity:1; transform:translateY(0); }
  }
  .card:hover {
    transform: translateY(-6px) scale(1.015);
    box-shadow: var(--card-glow), 0 20px 60px rgba(0,0,0,0.4);
    border-color: rgba(30,159,255,0.35);
  }
  .card::before {
    content:''; position:absolute; top:0; left:0; right:0; height:3px;
    background: linear-gradient(90deg, var(--card-accent, var(--accent)), transparent);
    opacity:0; transition: opacity 0.3s;
  }
  .card:hover::before { opacity:1; }

  .card-icon {
    width: 52px; height: 52px;
    background: rgba(30,159,255,0.1);
    border-radius: 14px;
    display: flex; align-items: center; justify-content: center;
    margin-bottom: 18px;
    border: 1px solid rgba(30,159,255,0.2);
    transition: background 0.3s, transform 0.3s;
  }
  .card:hover .card-icon { background: rgba(30,159,255,0.18); transform: rotate(-5deg) scale(1.08); }

  .card h3 {
    font-family: 'DM Serif Display', serif;
    font-size: 1.15rem; margin-bottom: 10px; color: var(--text);
  }
  .card p { font-size: 0.88rem; color: var(--muted); line-height: 1.65; }

  .card-tag {
    display: inline-block; margin-top: 16px;
    font-size: 10px; letter-spacing: 2px; text-transform: uppercase;
    color: var(--card-accent, var(--accent));
    border: 1px solid currentColor;
    padding: 3px 10px; border-radius: 20px;
    opacity: 0.75;
  }
  .click-hint {
    position: absolute; bottom: 18px; right: 20px;
    font-size: 10px; color: var(--muted); letter-spacing: 1px;
    opacity: 0; transition: opacity 0.3s;
    display: flex; align-items: center; gap: 4px;
  }
  .card:hover .click-hint { opacity:1; }
  .click-hint::after { content:'→'; }

  /* ── MODAL OVERLAY ── */
  .overlay {
    position: fixed; inset: 0; z-index: 1000;
    background: rgba(2,8,18,0.85);
    backdrop-filter: blur(12px);
    display: flex; align-items: center; justify-content: center;
    padding: 20px;
    opacity: 0; pointer-events: none;
    transition: opacity 0.3s ease;
  }
  .overlay.open { opacity:1; pointer-events: all; }

  .modal {
    background: var(--surface);
    border: 1px solid rgba(100,180,255,0.2);
    border-radius: 24px;
    max-width: 860px; width: 100%;
    max-height: 90vh; overflow-y: auto;
    position: relative;
    transform: scale(0.94) translateY(20px);
    transition: transform 0.35s cubic-bezier(.22,.68,0,1.2);
    scrollbar-width: thin; scrollbar-color: var(--accent) transparent;
  }
  .overlay.open .modal { transform: scale(1) translateY(0); }

  .modal-header {
    padding: 32px 36px 24px;
    border-bottom: 1px solid var(--border);
    position: sticky; top: 0;
    background: var(--surface);
    z-index: 5;
    display: flex; justify-content: space-between; align-items: flex-start;
  }
  .modal-header h2 {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.8rem; letter-spacing: 1px;
    color: var(--text);
  }
  .modal-close {
    background: rgba(255,255,255,0.08);
    border: 1px solid var(--border);
    color: var(--muted); cursor: pointer;
    width: 36px; height: 36px; border-radius: 50%;
    font-size: 1.2rem;
    display: flex; align-items: center; justify-content: center;
    transition: background 0.2s, color 0.2s;
    flex-shrink: 0; margin-left: 20px;
  }
  .modal-close:hover { background: rgba(255,79,79,0.2); color: var(--danger); }

  .modal-body { padding: 32px 36px 40px; }

  /* ── MODAL CONTENT STYLES ── */
  .modal-body h3 {
    font-family: 'DM Serif Display', serif;
    font-size: 1.2rem; color: var(--accent);
    margin: 28px 0 10px;
    padding-bottom: 6px;
    border-bottom: 1px solid var(--border);
  }
  .modal-body h3:first-child { margin-top: 0; }
  .modal-body p {
    font-size: 0.93rem; line-height: 1.8;
    color: rgba(232,242,255,0.85); margin-bottom: 14px;
  }
  .formula-box {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-left: 3px solid var(--accent2);
    border-radius: 12px;
    padding: 18px 22px;
    margin: 16px 0;
    font-family: 'Courier New', monospace;
    font-size: 0.95rem;
    color: var(--accent2);
    overflow-x: auto;
  }
  .formula-box .formula-label {
    font-family: 'DM Sans', sans-serif;
    font-size: 0.72rem; letter-spacing: 2px;
    color: var(--muted); text-transform: uppercase;
    margin-bottom: 8px; display: block;
  }
  .example-box {
    background: rgba(61,255,208,0.05);
    border: 1px solid rgba(61,255,208,0.2);
    border-radius: 12px;
    padding: 20px 22px; margin: 16px 0;
  }
  .example-box .ex-label {
    font-size: 10px; letter-spacing: 3px; text-transform: uppercase;
    color: var(--accent3); margin-bottom: 10px; display: block; font-weight: 500;
  }
  .example-box p { color: rgba(232,242,255,0.9); }
  .info-grid {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 14px; margin: 16px 0;
  }
  .info-cell {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 10px; padding: 14px 16px;
  }
  .info-cell .lbl { font-size: 10px; letter-spacing: 2px; color: var(--muted); text-transform: uppercase; }
  .info-cell .val { font-size: 1.2rem; font-weight: 500; color: var(--accent); margin-top: 4px; }
  .diagram-wrap { margin: 22px 0; text-align: center; }
  .diagram-wrap svg { max-width: 100%; border-radius: 12px; }
  ul.detail-list { padding-left: 0; list-style: none; margin: 12px 0; }
  ul.detail-list li {
    padding: 8px 0 8px 22px; position: relative;
    font-size: 0.9rem; color: rgba(232,242,255,0.85);
    border-bottom: 1px solid rgba(100,180,255,0.06);
    line-height: 1.65;
  }
  ul.detail-list li::before {
    content: '▸'; position: absolute; left: 0;
    color: var(--accent2); font-size: 0.75rem;
  }

  /* ── TIMELINE ── */
  .timeline { margin: 20px 0; }
  .tl-item {
    display: flex; gap: 18px; margin-bottom: 20px; align-items: flex-start;
  }
  .tl-dot {
    width: 12px; height: 12px; border-radius: 50%;
    background: var(--accent); flex-shrink: 0; margin-top: 5px;
    box-shadow: 0 0 10px var(--accent);
  }
  .tl-year { font-family: 'Bebas Neue', sans-serif; font-size: 1.1rem; color: var(--accent2); min-width: 50px; }
  .tl-text { font-size: 0.88rem; color: var(--muted); line-height: 1.6; }

  /* ── FOOTER ── */
  footer {
    position: relative; z-index: 5;
    text-align: center; padding: 40px;
    border-top: 1px solid var(--border);
    color: var(--muted); font-size: 0.8rem;
  }
  footer a { color: var(--accent); text-decoration: none; }

  /* ── RESPONSIVE ── */
  @media (max-width: 700px) {
    header { padding: 40px 20px 30px; }
    .grid-section { padding: 36px 18px; }
    .stat-bar { gap: 24px; }
    .modal-header, .modal-body { padding-left: 22px; padding-right: 22px; }
    .info-grid { grid-template-columns: 1fr; }
    .cards-grid { grid-template-columns: 1fr; }
  }

  /* ── TABS ── */
  .tabs { display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 22px; }
  .tab-btn {
    padding: 7px 16px; border-radius: 20px;
    border: 1px solid var(--border); background: transparent;
    color: var(--muted); font-size: 0.82rem; cursor: pointer;
    transition: all 0.2s; font-family: 'DM Sans', sans-serif;
  }
  .tab-btn.active, .tab-btn:hover {
    background: rgba(30,159,255,0.15); color: var(--accent);
    border-color: rgba(30,159,255,0.4);
  }
  .tab-content { display: none; }
  .tab-content.active { display: block; }

  /* ── NAV ── */
  nav {
    position: sticky; top: 0; z-index: 100;
    background: rgba(5,13,26,0.92); backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
    padding: 0 40px;
    display: flex; align-items: center; gap: 8px; overflow-x: auto;
    scrollbar-width: none;
  }
  nav::-webkit-scrollbar { display: none; }
  .nav-item {
    padding: 14px 16px; white-space: nowrap;
    font-size: 0.82rem; color: var(--muted); cursor: pointer;
    letter-spacing: 0.5px;
    border-bottom: 2px solid transparent;
    transition: color 0.2s, border-color 0.2s;
  }
  .nav-item:hover, .nav-item.active { color: var(--accent); border-color: var(--accent); }
  .nav-logo { font-family: 'Bebas Neue'; font-size: 1.1rem; color: var(--accent); margin-right: 20px; letter-spacing: 2px; flex-shrink:0; }

  /* speed meter animation */
  @keyframes rotateMeter { from { transform: rotate(-90deg); } to { transform: rotate(90deg); } }
  .meter-needle { transform-origin: 150px 150px; animation: rotateMeter 3s ease-in-out infinite alternate; }
</style>
</head>
<body>

<!-- NAV -->
<nav id="mainNav">
  <span class="nav-logo">PININFARINA</span>
  <span class="nav-item" onclick="scrollTo('#storia')">Storia</span>
  <span class="nav-item" onclick="scrollTo('#tecnologie')">Tecnologie Core</span>
  <span class="nav-item" onclick="scrollTo('#aerodinamica')">Aerodinamica</span>
  <span class="nav-item" onclick="scrollTo('#applicazioni')">Applicazioni</span>
  <span class="nav-item" onclick="scrollTo('#risultati')">Risultati</span>
</nav>

<!-- HERO -->
<header>
  <span class="eyebrow">Dal 1972 · Grugliasco, Torino</span>
  <h1>PININFARINA<br>IL TEMPIO DEL VENTO</h1>
  <p class="subtitle">Prima galleria del vento full-scale in Italia. Cinquant'anni di ricerca aerodinamica e aeroacustica al servizio dell'industria automotive, aeronautica e civile.</p>

  <!-- Animated closed-circuit wind tunnel (Göttingen-type, top view) -->
  <div class="wind-hero">
    <svg class="wt-svg" width="1200" height="340" viewBox="0 0 1200 340" xmlns="http://www.w3.org/2000/svg" aria-label="Schema galleria del vento a circuito chiuso tipo Göttingen">
      <defs>
        <!-- Closed-circuit centerline. Flow direction: starts at settling chamber (left),
             goes right through contraction → test section → diffuser → corner1 → down →
             fan → corner2 → left → corner3 → up → corner4 → back to settling chamber. -->
        <path id="wt-circuit"
          d="M 90 90
             L 380 90
             C 460 90 500 100 540 110
             L 720 130
             C 760 138 790 150 810 165
             L 850 195
             C 870 220 870 250 840 270
             L 540 270
             C 460 270 400 270 340 270
             L 160 270
             C 110 270 80 250 80 220
             L 80 130
             C 80 105 82 96 90 90 Z"
          fill="none" stroke="none"/>

        <!-- Pressure gradient for the contractor section -->
        <linearGradient id="contractorGrad" x1="0%" y1="0%" x2="100%" y2="0%">
          <stop offset="0%" stop-color="rgba(245,166,35,0.18)"/>
          <stop offset="100%" stop-color="rgba(61,255,208,0.18)"/>
        </linearGradient>

        <!-- Test section glow -->
        <linearGradient id="testGrad" x1="0%" y1="0%" x2="100%" y2="0%">
          <stop offset="0%" stop-color="rgba(61,255,208,0.10)"/>
          <stop offset="100%" stop-color="rgba(30,159,255,0.06)"/>
        </linearGradient>

        <!-- Diffuser gradient -->
        <linearGradient id="diffuserGrad" x1="0%" y1="0%" x2="100%" y2="0%">
          <stop offset="0%" stop-color="rgba(30,159,255,0.08)"/>
          <stop offset="100%" stop-color="rgba(30,159,255,0.03)"/>
        </linearGradient>
      </defs>

      <!-- ═══════ TUNNEL STRUCTURE (closed circuit, top view) ═══════ -->

      <!-- Settling chamber (top-left, wide) -->
      <path class="wt-duct" d="M 80 60 L 250 60 L 250 120 L 80 120 Z"
            fill="rgba(61,255,208,0.05)"/>

      <!-- Contractor (cone of contraction) — wide → narrow -->
      <path class="wt-duct" d="M 250 60 L 380 75 L 380 105 L 250 120 Z"
            fill="url(#contractorGrad)"/>

      <!-- Test section (open jet style box) -->
      <path class="wt-duct" d="M 380 75 L 560 75 L 560 105 L 380 105 Z"
            fill="url(#testGrad)"
            stroke="rgba(61,255,208,0.6)" stroke-width="1.4"/>

      <!-- Diffuser (narrow → wide, expanding) -->
      <path class="wt-duct" d="M 560 75 L 760 60 L 760 120 L 560 105 Z"
            fill="url(#diffuserGrad)"/>

      <!-- Corner 1 (top-right) — 90° turn down -->
      <path class="wt-duct" d="M 760 60 L 820 60 Q 870 60 870 110 L 870 165 L 810 165 Q 810 130 810 120 L 760 120 Z"
            fill="rgba(30,159,255,0.04)"/>

      <!-- Return leg right (vertical, with fan) -->
      <path class="wt-duct" d="M 810 165 L 870 165 L 870 235 L 810 235 Z"
            fill="rgba(30,159,255,0.05)"/>

      <!-- Corner 2 (bottom-right) — 90° turn left -->
      <path class="wt-duct" d="M 870 235 L 870 250 Q 870 290 820 290 L 760 290 L 760 250 L 810 250 L 810 235 Z"
            fill="rgba(30,159,255,0.04)"/>

      <!-- Return leg bottom (horizontal) -->
      <path class="wt-duct" d="M 200 250 L 760 250 L 760 290 L 200 290 Z"
            fill="rgba(30,159,255,0.05)"/>

      <!-- Corner 3 (bottom-left) — 90° turn up -->
      <path class="wt-duct" d="M 200 250 L 200 290 L 130 290 Q 80 290 80 250 L 80 235 L 140 235 L 140 250 Z"
            fill="rgba(30,159,255,0.04)"/>

      <!-- Return leg left (vertical, going up) -->
      <path class="wt-duct" d="M 80 110 L 140 110 L 140 235 L 80 235 Z"
            fill="rgba(30,159,255,0.05)"/>

      <!-- Corner 4 (top-left) — 90° turn right into settling chamber -->
      <path class="wt-duct" d="M 80 60 L 80 110 L 140 110 L 140 105 Q 140 60 175 60 L 80 60 Z"
            fill="rgba(30,159,255,0.04)"/>

      <!-- Honeycomb (settling chamber) -->
      <g class="wt-honeycomb">
        <line x1="100" y1="65" x2="100" y2="115"/>
        <line x1="110" y1="65" x2="110" y2="115"/>
        <line x1="120" y1="65" x2="120" y2="115"/>
        <line x1="130" y1="65" x2="130" y2="115"/>
        <line x1="140" y1="65" x2="140" y2="115"/>
        <line x1="150" y1="65" x2="150" y2="115"/>
        <line x1="160" y1="65" x2="160" y2="115"/>
        <line x1="170" y1="65" x2="170" y2="115"/>
        <line x1="95" y1="70" x2="180" y2="70"/>
        <line x1="95" y1="80" x2="180" y2="80"/>
        <line x1="95" y1="90" x2="180" y2="90"/>
        <line x1="95" y1="100" x2="180" y2="100"/>
        <line x1="95" y1="110" x2="180" y2="110"/>
      </g>

      <!-- Anti-turbulence screens (after honeycomb) -->
      <line class="wt-screen" x1="200" y1="62" x2="200" y2="118"/>
      <line class="wt-screen" x1="215" y1="62" x2="215" y2="118"/>
      <line class="wt-screen" x1="230" y1="62" x2="230" y2="118"/>

      <!-- Corner 1 turning vanes (top-right) — concentric arcs -->
      <g class="wt-vanes">
        <path d="M 815 70 Q 855 70 855 115"/>
        <path d="M 800 72 Q 845 72 845 117"/>
        <path d="M 785 78 Q 832 78 832 122"/>
        <path d="M 770 82 Q 820 82 820 120"/>
      </g>

      <!-- Corner 2 turning vanes (bottom-right) -->
      <g class="wt-vanes">
        <path d="M 855 235 Q 855 280 815 280"/>
        <path d="M 845 235 Q 845 270 805 270"/>
        <path d="M 832 235 Q 832 258 792 258"/>
        <path d="M 820 235 Q 820 250 780 250"/>
      </g>

      <!-- Corner 3 turning vanes (bottom-left) -->
      <g class="wt-vanes">
        <path d="M 200 280 Q 100 280 100 240"/>
        <path d="M 200 270 Q 110 270 110 240"/>
        <path d="M 200 258 Q 120 258 120 240"/>
        <path d="M 200 250 Q 130 250 130 240"/>
      </g>

      <!-- Corner 4 turning vanes (top-left) -->
      <g class="wt-vanes">
        <path d="M 100 110 Q 100 70 140 70"/>
        <path d="M 110 110 Q 110 80 145 80"/>
        <path d="M 120 110 Q 120 90 150 90"/>
        <path d="M 130 105 Q 130 98 155 98"/>
      </g>

      <!-- ═══════ FAN (axial, on right return leg) — static representation ═══════ -->
      <!-- Fan housing -->
      <rect x="810" y="180" width="60" height="40" fill="rgba(245,166,35,0.08)"
            stroke="rgba(245,166,35,0.5)" stroke-width="1.2"/>
      <!-- Stator vanes (static guide vanes, vertical) -->
      <line x1="820" y1="184" x2="820" y2="216" stroke="rgba(245,166,35,0.45)" stroke-width="0.7"/>
      <line x1="830" y1="184" x2="830" y2="216" stroke="rgba(245,166,35,0.45)" stroke-width="0.7"/>
      <line x1="850" y1="184" x2="850" y2="216" stroke="rgba(245,166,35,0.45)" stroke-width="0.7"/>
      <line x1="860" y1="184" x2="860" y2="216" stroke="rgba(245,166,35,0.45)" stroke-width="0.7"/>
      <!-- Motor strut (central horizontal axis) -->
      <line x1="810" y1="200" x2="870" y2="200"
            stroke="rgba(245,166,35,0.4)" stroke-width="0.8" stroke-dasharray="2 3"/>
      <!-- Central hub -->
      <circle cx="840" cy="200" r="4" class="wt-fan-hub"/>
      <circle cx="840" cy="200" r="7" fill="none" stroke="rgba(245,166,35,0.4)" stroke-width="0.6"/>

      <!-- ═══════ TEST MODEL (automotive silhouette) ═══════ -->
      <g transform="translate(440,82)">
        <!-- Car body, side-view silhouette -->
        <path d="M 2 16 L 8 16 L 14 6 L 32 3 L 50 4 L 62 10 L 70 14 L 70 16 L 76 16 L 76 18 L 2 18 Z"
              fill="rgba(100,180,255,0.22)"
              stroke="rgba(100,180,255,0.7)" stroke-width="0.9"/>
        <!-- Windows -->
        <path d="M 16 8 L 32 5 L 48 6 L 58 11 Z" fill="rgba(30,159,255,0.35)"/>
        <!-- Wheels -->
        <circle cx="16" cy="18" r="3.2" fill="rgba(15,30,50,0.9)"
                stroke="rgba(100,180,255,0.6)" stroke-width="0.7"/>
        <circle cx="58" cy="18" r="3.2" fill="rgba(15,30,50,0.9)"
                stroke="rgba(100,180,255,0.6)" stroke-width="0.7"/>
        <!-- Bilancia steli (sting/balance struts) -->
        <line x1="16" y1="21" x2="16" y2="26" stroke="rgba(245,166,35,0.6)" stroke-width="0.8"/>
        <line x1="58" y1="21" x2="58" y2="26" stroke="rgba(245,166,35,0.6)" stroke-width="0.8"/>
      </g>

      <!-- Wake region behind the car (turbulent recirculation) -->
      <path class="wt-wake" d="M 524 88 Q 540 88 552 92"/>
      <path class="wt-wake" d="M 524 95 Q 545 96 558 95"/>
      <path class="wt-wake" d="M 524 100 Q 540 102 552 99"/>

      <!-- ═══════ STREAMLINES (4 parallel paths along the circuit) ═══════ -->

      <!-- We use 4 offset versions of similar paths to simulate parallel streamlines.
           Each is the same closed-circuit shape, slightly offset perpendicular to the flow. -->

      <!-- Outer streamline (upper trace) -->
      <path class="wt-streamline wt-sl-1"
        d="M 90 78
           L 250 78
           Q 320 78 380 87
           L 540 87
           L 590 87
           Q 660 87 760 78
           Q 850 78 850 165
           L 850 235
           Q 850 280 760 270
           L 200 270
           Q 100 280 100 220
           L 100 130
           Q 100 78 180 78 Z"/>

      <!-- Mid-upper streamline -->
      <path class="wt-streamline wt-sl-2"
        d="M 90 90
           L 250 90
           Q 320 90 380 90
           L 540 90
           Q 660 90 760 90
           Q 840 90 840 165
           L 840 235
           Q 840 270 760 260
           L 200 260
           Q 110 270 110 220
           L 110 130
           Q 110 90 180 90 Z"/>

      <!-- Mid-lower streamline -->
      <path class="wt-streamline wt-sl-3"
        d="M 90 100
           L 250 100
           Q 320 100 380 100
           L 540 100
           Q 660 100 760 100
           Q 830 100 830 165
           L 830 235
           Q 830 260 760 255
           L 200 255
           Q 120 255 120 220
           L 120 130
           Q 120 100 180 100 Z"/>

      <!-- Inner streamline -->
      <path class="wt-streamline wt-sl-4"
        d="M 90 110
           L 250 110
           Q 320 110 380 108
           L 540 108
           Q 660 108 760 110
           Q 820 110 820 165
           L 820 235
           Q 820 250 760 248
           L 200 248
           Q 130 248 130 220
           L 130 130
           Q 130 110 180 110 Z"/>

      <!-- ═══════ LABELS ═══════ -->
      <text class="wt-label wt-label-accent" x="165" y="50" text-anchor="middle">Settling Chamber</text>
      <text class="wt-label" x="315" y="50" text-anchor="middle">Contractor</text>
      <text class="wt-label wt-label-accent" x="470" y="65" text-anchor="middle">Test Section</text>
      <text class="wt-label" x="660" y="50" text-anchor="middle">Diffuser</text>
      <text class="wt-label" x="840" y="170" text-anchor="middle" transform="rotate(-90, 840, 170)">Fan</text>
      <text class="wt-label" x="480" y="310" text-anchor="middle">Return Duct</text>

      <!-- Velocity tag near test section -->
      <text class="wt-velocity-tag" x="470" y="125" text-anchor="middle">V ≈ 250 km/h</text>

      <!-- Flow direction arrow inside settling chamber -->
      <g opacity="0.8">
        <line x1="255" y1="135" x2="370" y2="135" stroke="var(--accent3)" stroke-width="0.8" stroke-dasharray="2 2"/>
        <path d="M 370 135 L 365 132 L 365 138 Z" fill="var(--accent3)"/>
      </g>

      <!-- Pressure arrows (showing static pressure decrease through contractor) -->
      <text class="wt-label" x="315" y="135" text-anchor="middle" style="font-size:7.5px; letter-spacing:0.5px;">p ↓  V ↑</text>
    </svg>
  </div>

  <div class="stat-bar">
    <div class="stat-item"><span class="stat-num">50</span><span class="stat-label">Anni di attività</span></div>
    <div class="stat-item"><span class="stat-num">250</span><span class="stat-label">km/h velocità max</span></div>
    <div class="stat-item"><span class="stat-num">&lt;0.74%</span><span class="stat-label">Turbolenza laminare</span></div>
    <div class="stat-item"><span class="stat-num">1972</span><span class="stat-label">Anno di fondazione</span></div>
  </div>
</header>

<!-- STORIA -->
<section class="grid-section" id="storia">
  <p class="section-label">Sezione 01</p>
  <h2 class="section-title">Eredità & Contesto Storico</h2>
  <div class="cards-grid">
    <div class="card" style="--card-accent:#f5a623" onclick="openModal('storia-fondazione')">
      <div class="card-icon">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none"><circle cx="14" cy="14" r="10" stroke="#f5a623" stroke-width="1.5"/><path d="M14 8 L14 14 L18 16" stroke="#f5a623" stroke-width="1.5" stroke-linecap="round"/></svg>
      </div>
      <h3>Fondazione e Pionierismo</h3>
      <p>Nel 1972 Pininfarina inaugura la prima galleria del vento in Italia, tra le prime sette al mondo, avviando una nuova era per la ricerca aerodinamica europea.</p>
      <span class="card-tag">1972 · Storia</span>
      <span class="click-hint">Approfondisci</span>
    </div>
    <div class="card" style="--card-accent:#1e9fff" onclick="openModal('storia-evoluzione')">
      <div class="card-icon">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none"><polyline points="4,22 10,14 16,18 24,6" stroke="#1e9fff" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/></svg>
      </div>
      <h3>50 Anni di Evoluzione</h3>
      <p>Dall'architettura originale alle successive modernizzazioni, la galleria ha attraverso mezzo secolo di aggiornamenti tecnologici continui.</p>
      <span class="card-tag">Timeline · Evoluzione</span>
      <span class="click-hint">Approfondisci</span>
    </div>
    <div class="card" style="--card-accent:#3dffd0" onclick="openModal('storia-gallerie')">
      <div class="card-icon">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none"><rect x="4" y="10" width="20" height="12" rx="3" stroke="#3dffd0" stroke-width="1.5"/><path d="M10 10 L10 7 Q14 4 18 7 L18 10" stroke="#3dffd0" stroke-width="1.5" stroke-linecap="round"/></svg>
      </div>
      <h3>Tipologie di Gallerie del Vento</h3>
      <p>Gallerie a circuito aperto vs. chiuso, subsoniche, transoniche e supersoniche: principi fisici, pro e contro di ciascuna architettura.</p>
      <span class="card-tag">Fisica · Architettura</span>
      <span class="click-hint">Approfondisci</span>
    </div>
  </div>
</section>

<!-- TECNOLOGIE CORE -->
<section class="grid-section" id="tecnologie">
  <p class="section-label">Sezione 02</p>
  <h2 class="section-title">Tecnologie Core e Innovazione</h2>
  <div class="cards-grid">
    <div class="card" style="--card-accent:#1e9fff" onclick="openModal('gess')">
      <div class="card-icon">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
          <rect x="4" y="16" width="20" height="4" rx="1" fill="rgba(30,159,255,0.2)" stroke="#1e9fff" stroke-width="1.2"/>
          <path d="M8 20 L8 24 M20 20 L20 24" stroke="#1e9fff" stroke-width="1.5" stroke-linecap="round"/>
          <path d="M6 16 Q14 8 22 16" stroke="#1e9fff" stroke-width="1.5" fill="none" stroke-linecap="round"/>
        </svg>
      </div>
      <h3>Ground Effect Simulation (GESS)</h3>
      <p>Rulli e tappeti mobili replicano fedelmente il movimento dell'auto sulla strada, simulando l'effetto suolo con precisione fisica rigorosa.</p>
      <span class="card-tag">GESS · Effetto Suolo</span>
      <span class="click-hint">Approfondisci</span>
    </div>
    <div class="card" style="--card-accent:#f5a623" onclick="openModal('tgs')">
      <div class="card-icon">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
          <path d="M4 14 Q7 8 10 14 Q13 20 16 14 Q19 8 22 14 Q25 20 28 14" stroke="#f5a623" stroke-width="1.5" fill="none" stroke-linecap="round"/>
        </svg>
      </div>
      <h3>Turbulence Generation System (TGS)</h3>
      <p>Ali oscillanti a frequenza variabile simulano raffiche di vento, sorpassi e scie di altri veicoli: il flusso reale in strada è tutt'altro che stazionario.</p>
      <span class="card-tag">TGS · Turbolenza</span>
      <span class="click-hint">Approfondisci</span>
    </div>
    <div class="card" style="--card-accent:#3dffd0" onclick="openModal('aeroacustica')">
      <div class="card-icon">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
          <circle cx="10" cy="14" r="4" stroke="#3dffd0" stroke-width="1.5"/>
          <path d="M16 9 Q21 14 16 19" stroke="#3dffd0" stroke-width="1.5" fill="none" stroke-linecap="round"/>
          <path d="M19 6 Q26 14 19 22" stroke="#3dffd0" stroke-width="1.5" fill="none" stroke-linecap="round" opacity="0.5"/>
        </svg>
      </div>
      <h3>Analisi Aeroacustica</h3>
      <p>Array di microfoni di precisione e camere anecoiche isolano e analizzano le sorgenti di rumore aerodinamico per massimizzare il comfort in abitacolo.</p>
      <span class="card-tag">Acustica · Comfort</span>
      <span class="click-hint">Approfondisci</span>
    </div>
    <div class="card" style="--card-accent:#ff4f4f" onclick="openModal('velocita')">
      <div class="card-icon">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
          <path d="M4 20 Q8 8 14 10 Q20 12 24 4" stroke="#ff4f4f" stroke-width="1.5" fill="none" stroke-linecap="round"/>
          <circle cx="14" cy="10" r="2" fill="#ff4f4f"/>
        </svg>
      </div>
      <h3>Velocità Massima 250 km/h</h3>
      <p>Test ad alta velocità con flussi laminari estremamente precisi: turbolenza residua inferiore allo 0.74%, garanzia di ripetibilità delle misurazioni.</p>
      <span class="card-tag">250 km/h · Laminare</span>
      <span class="click-hint">Approfondisci</span>
    </div>
  </div>
</section>

<!-- AERODINAMICA -->
<section class="grid-section" id="aerodinamica">
  <p class="section-label">Sezione 03</p>
  <h2 class="section-title">Fondamenti di Aerodinamica</h2>
  <div class="cards-grid">
    <div class="card" style="--card-accent:#1e9fff" onclick="openModal('bernoulli')">
      <div class="card-icon">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
          <path d="M4 18 Q10 4 24 12" stroke="#1e9fff" stroke-width="1.5" fill="none" stroke-linecap="round"/>
          <path d="M4 18 Q10 22 24 12" stroke="#1e9fff" stroke-width="1" fill="none" stroke-linecap="round" stroke-dasharray="3 3"/>
        </svg>
      </div>
      <h3>Teorema di Bernoulli & Portanza</h3>
      <p>Il principio fondamentale che collega velocità e pressione del fluido: base teorica per la generazione di portanza su profili alari e veicoli.</p>
      <span class="card-tag">Bernoulli · Portanza</span>
      <span class="click-hint">Approfondisci</span>
    </div>
    <div class="card" style="--card-accent:#f5a623" onclick="openModal('dragcoeff')">
      <div class="card-icon">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
          <rect x="8" y="10" width="12" height="8" rx="4" stroke="#f5a623" stroke-width="1.5"/>
          <path d="M20 14 L26 14 M22 12 L26 14 L22 16" stroke="#f5a623" stroke-width="1.2" stroke-linecap="round"/>
          <path d="M2 10 L6 14 L2 18" stroke="#f5a623" stroke-width="1.2" stroke-linecap="round" opacity="0.5"/>
        </svg>
      </div>
      <h3>Coefficiente di Resistenza (Cx / Cd)</h3>
      <p>Definizione rigorosa del Cd, metodi di misurazione in galleria e impatto diretto su consumo energetico, emissioni e velocità massima.</p>
      <span class="card-tag">Cd · Drag · Resistenza</span>
      <span class="click-hint">Approfondisci</span>
    </div>
    <div class="card" style="--card-accent:#3dffd0" onclick="openModal('strati')">
      <div class="card-icon">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
          <path d="M4 20 L24 20" stroke="#3dffd0" stroke-width="2" stroke-linecap="round"/>
          <path d="M4 16 L22 16" stroke="#3dffd0" stroke-width="1.5" stroke-linecap="round" opacity="0.8"/>
          <path d="M4 12 L20 12" stroke="#3dffd0" stroke-width="1.2" stroke-linecap="round" opacity="0.6"/>
          <path d="M4 8 L16 8" stroke="#3dffd0" stroke-width="1" stroke-linecap="round" opacity="0.4"/>
        </svg>
      </div>
      <h3>Strato Limite e Separazione</h3>
      <p>Dal regime laminare al turbolento: il fenomeno dello strato limite, la separazione del flusso e le sue conseguenze su portanza e resistenza.</p>
      <span class="card-tag">Strato Limite · BL</span>
      <span class="click-hint">Approfondisci</span>
    </div>
    <div class="card" style="--card-accent:#ff4f4f" onclick="openModal('reynolds')">
      <div class="card-icon">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
          <text x="5" y="18" font-size="12" fill="#ff4f4f" font-family="serif" font-style="italic">Re</text>
          <circle cx="20" cy="10" r="5" stroke="#ff4f4f" stroke-width="1.2" fill="none"/>
          <path d="M17 10 Q20 6 23 10 Q20 14 17 10" fill="rgba(255,79,79,0.2)"/>
        </svg>
      </div>
      <h3>Numero di Reynolds e Similitudine</h3>
      <p>Come scalare i risultati da modello in scala reale: il criterio di similitudine dinamica e le sue implicazioni pratiche nei test in galleria.</p>
      <span class="card-tag">Reynolds · Similitudine</span>
      <span class="click-hint">Approfondisci</span>
    </div>
  </div>
</section>

<!-- APPLICAZIONI -->
<section class="grid-section" id="applicazioni">
  <p class="section-label">Sezione 04</p>
  <h2 class="section-title">Oltre l'Automotive — Applicazioni Globali</h2>
  <div class="cards-grid">
    <div class="card" style="--card-accent:#3dffd0" onclick="openModal('aeronautica')">
      <div class="card-icon">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
          <path d="M4 18 L14 6 L24 18" stroke="#3dffd0" stroke-width="1.5" fill="none" stroke-linecap="round"/>
          <path d="M9 14 L14 6 L19 14" stroke="#3dffd0" stroke-width="1" fill="rgba(61,255,208,0.1)" stroke-linecap="round"/>
          <path d="M2 22 L8 22 L12 18 L16 18 L20 22 L26 22" stroke="#3dffd0" stroke-width="1" stroke-linecap="round"/>
        </svg>
      </div>
      <h3>Applicazioni Aeronautiche</h3>
      <p>Test su profili alari, gondole motore, elementi di controllo e componenti UAV: la galleria Pininfarina al servizio dell'ingegneria del volo.</p>
      <span class="card-tag">Aeronautica · Profili Alari</span>
      <span class="click-hint">Approfondisci</span>
    </div>
    <div class="card" style="--card-accent:#1e9fff" onclick="openModal('civile')">
      <div class="card-icon">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
          <rect x="10" y="6" width="8" height="16" stroke="#1e9fff" stroke-width="1.5" fill="rgba(30,159,255,0.1)"/>
          <rect x="4" y="14" width="6" height="8" stroke="#1e9fff" stroke-width="1.2" fill="rgba(30,159,255,0.08)"/>
          <rect x="18" y="10" width="6" height="12" stroke="#1e9fff" stroke-width="1.2" fill="rgba(30,159,255,0.08)"/>
          <path d="M2 22 L26 22" stroke="#1e9fff" stroke-width="1.5" stroke-linecap="round"/>
        </svg>
      </div>
      <h3>Ingegneria Civile e Strutturale</h3>
      <p>Analisi dell'impatto del vento su edifici ad alta quota, ponti sospesi e coperture: prevenzione del flutter e verifica delle norme di sicurezza.</p>
      <span class="card-tag">Edifici · Ponti · Flutter</span>
      <span class="click-hint">Approfondisci</span>
    </div>
    <div class="card" style="--card-accent:#f5a623" onclick="openModal('sport')">
      <div class="card-icon">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
          <circle cx="14" cy="10" r="5" stroke="#f5a623" stroke-width="1.5"/>
          <path d="M10 15 L8 24 M18 15 L20 24 M8 20 L20 20" stroke="#f5a623" stroke-width="1.2" stroke-linecap="round"/>
        </svg>
      </div>
      <h3>Sport e Attrezzature</h3>
      <p>Sci alpino, ciclismo, imbarcazioni a vela: ottimizzazione dell'equipaggiamento sportivo per ridurre la resistenza e migliorare le prestazioni degli atleti.</p>
      <span class="card-tag">Sport · Performance</span>
      <span class="click-hint">Approfondisci</span>
    </div>
  </div>
</section>

<!-- RISULTATI -->
<section class="grid-section" id="risultati">
  <p class="section-label">Sezione 05</p>
  <h2 class="section-title">Parametri Tecnici e Risultati Chiave</h2>
  <div class="cards-grid">
    <div class="card" style="--card-accent:#f5a623" onclick="openModal('misure')">
      <div class="card-icon">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
          <path d="M6 22 L6 8 M6 22 L22 22" stroke="#f5a623" stroke-width="1.5" stroke-linecap="round"/>
          <rect x="8" y="14" width="3" height="8" fill="rgba(245,166,35,0.3)" stroke="#f5a623" stroke-width="1"/>
          <rect x="13" y="10" width="3" height="12" fill="rgba(245,166,35,0.5)" stroke="#f5a623" stroke-width="1"/>
          <rect x="18" y="6" width="3" height="16" fill="rgba(245,166,35,0.7)" stroke="#f5a623" stroke-width="1"/>
        </svg>
      </div>
      <h3>Strumentazione e Misurazioni</h3>
      <p>Bilance aerodinamiche a sei componenti, PIV, LDA e pressure scanning: la metrologia in galleria del vento per misurare forze, momenti e campi di velocità.</p>
      <span class="card-tag">Metrology · PIV · LDA</span>
      <span class="click-hint">Approfondisci</span>
    </div>
    <div class="card" style="--card-accent:#3dffd0" onclick="openModal('cfd')">
      <div class="card-icon">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
          <rect x="4" y="4" width="20" height="20" rx="3" stroke="#3dffd0" stroke-width="1.2" fill="rgba(61,255,208,0.05)"/>
          <path d="M8 20 L12 12 L16 16 L20 8" stroke="#3dffd0" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </div>
      <h3>CFD e Galleria del Vento: Sinergia</h3>
      <p>Come la simulazione numerica (CFD) e i test fisici in galleria si complementano: vantaggi, limiti e best practice nell'approccio ibrido moderno.</p>
      <span class="card-tag">CFD · Simulazione Numerica</span>
      <span class="click-hint">Approfondisci</span>
    </div>
    <div class="card" style="--card-accent:#1e9fff" onclick="openModal('futuro')">
      <div class="card-icon">
        <svg width="28" height="28" viewBox="0 0 28 28" fill="none">
          <circle cx="14" cy="14" r="9" stroke="#1e9fff" stroke-width="1.2" stroke-dasharray="3 2"/>
          <circle cx="14" cy="14" r="4" fill="rgba(30,159,255,0.2)" stroke="#1e9fff" stroke-width="1.5"/>
          <path d="M14 5 L14 2 M14 22 L14 26 M5 14 L2 14 M22 14 L26 14" stroke="#1e9fff" stroke-width="1" stroke-linecap="round"/>
        </svg>
      </div>
      <h3>Il Futuro della Galleria</h3>
      <p>Mobilità elettrica, idrogeno e sostenibilità: come le sfide della transizione energetica stanno ridefinendo il ruolo della galleria del vento nel XXI secolo.</p>
      <span class="card-tag">Futuro · EV · Sostenibilità</span>
      <span class="click-hint">Approfondisci</span>
    </div>
  </div>
</section>

<footer>
  <p>Infografica interattiva · Pininfarina Wind Tunnel · <em>Il Tempio del Vento</em> · 50 anni di eccellenza tecnologica</p>
  <p style="margin-top:8px; opacity:0.5">Contenuto a scopo didattico. Dati tecnici basati su fonti pubbliche Pininfarina.</p>
</footer>

<!-- ═══════════════════ MODAL OVERLAY ═══════════════════ -->
<div class="overlay" id="overlay" onclick="closeModal(event)">
  <div class="modal" id="modal">
    <div class="modal-header">
      <h2 id="modal-title">Titolo</h2>
      <button class="modal-close" onclick="closeModal()">✕</button>
    </div>
    <div class="modal-body" id="modal-body"></div>
  </div>
</div>

<script>
// ═══════ MODAL DATA ═══════
const MODALS = {

'storia-fondazione': {
  title: 'Fondazione e Pionierismo (1972)',
  body: `
    <div class="tabs">
      <button class="tab-btn active" onclick="switchTab(event,'sf-storia')">Storia</button>
      <button class="tab-btn" onclick="switchTab(event,'sf-fisica')">Fisica di Base</button>
      <button class="tab-btn" onclick="switchTab(event,'sf-esempio')">Esempio Pratico</button>
    </div>
    <div id="sf-storia" class="tab-content active">
      <h3>Il Contesto Storico</h3>
      <p>Nel 1972, Pininfarina inaugura a Grugliasco (Torino) la prima galleria del vento full-scale italiana, posizionandosi tra le prime sette strutture di questo tipo a livello mondiale. La decisione nasce dall'esigenza crescente dell'industria automobilistica italiana di disporre di uno strumento di ricerca avanzato per sviluppare veicoli più efficienti e aerodinamicamente ottimizzati.</p>
      <p>Il contesto geopolitico e industriale degli anni '70 — la crisi petrolifera del 1973, la pressione normativa sulle emissioni — rendeva l'aerodinamica non più un lusso sportivo, ma una necessità competitiva per ogni costruttore.</p>
      <div class="timeline">
        <div class="tl-item"><div class="tl-dot"></div><div><span class="tl-year">1972</span><div class="tl-text">Inaugurazione galleria Pininfarina. Prima in Italia, settima al mondo.</div></div></div>
        <div class="tl-item"><div class="tl-dot"></div><div><span class="tl-year">1980s</span><div class="tl-text">Introduzione del tappeto mobile (T-Belt) per simulazione dello scorrimento del suolo.</div></div></div>
        <div class="tl-item"><div class="tl-dot"></div><div><span class="tl-year">1990s</span><div class="tl-text">Estensione alle misurazioni aeroacustiche con camere anecoiche.</div></div></div>
        <div class="tl-item"><div class="tl-dot"></div><div><span class="tl-year">2000s</span><div class="tl-text">Implementazione del Turbulence Generation System (TGS) e del Ground Effect Simulation System (GESS).</div></div></div>
        <div class="tl-item"><div class="tl-dot"></div><div><span class="tl-year">2022</span><div class="tl-text">Celebrazione dei 50 anni. La struttura rimane uno dei più avanzati laboratori aerodinamici d'Europa.</div></div></div>
      </div>
    </div>
    <div id="sf-fisica" class="tab-content">
      <h3>Principio di Funzionamento della Galleria</h3>
      <p>Una galleria del vento è uno strumento di simulazione che inverte il problema fisico: invece di muovere il veicolo nell'aria ferma (come in strada), si muove l'aria attorno a un veicolo fermo. Per il principio di <strong>relatività galileiana</strong>, i due scenari sono fisicamente equivalenti se si rispettano le condizioni di similitudine dinamica.</p>
      <div class="formula-box">
        <span class="formula-label">Equivalenza galileiana</span>
        Il comportamento aerodinamico dipende dalla velocità relativa v<sub>rel</sub> tra veicolo e fluido:<br><br>
        F_drag = ½ · ρ · v² · A · Cd<br><br>
        dove ρ = densità aria [kg/m³], v = velocità [m/s], A = area frontale [m²], Cd = coeff. di resistenza [-]
      </div>
      <h3>Circuito della Galleria</h3>
      <p>La galleria Pininfarina è a <strong>circuito chiuso (Göttingen type)</strong>: l'aria viene accelerata da un ventilatore centrifugo, espansa nella camera di prova, poi raccolta e reimmessa in circolo. Ciò permette di mantenere condizioni ambientali stazionarie e controllate.</p>
    </div>
    <div id="sf-esempio" class="tab-content">
      <div class="example-box">
        <span class="ex-label">Esempio Aeronautico</span>
        <p>Nel contesto aeronautico, la stessa logica si applica ai test su profili alari di alianti o velivoli leggeri. Un aliante Schleicher ASH-31 testato in galleria a scala 1:5 consente di studiare il campo di pressione attorno al profilo a varie incidenze senza dover effettuare costosi voli di prova. La condizione di similitudine richiede che il numero di Reynolds del modello eguali quello del velivolo reale: ciò si ottiene aumentando la velocità di flusso proporzionalmente alla riduzione di scala.</p>
      </div>
    </div>
  `
},

'storia-evoluzione': {
  title: '50 Anni di Evoluzione Tecnologica',
  body: `
    <h3>Architettura della Galleria nel Tempo</h3>
    <p>L'architettura originale della galleria Pininfarina è quella di una galleria di tipo <em>Eiffel</em> modificata in circuito chiuso. Nel corso dei decenni sono state apportate significative modifiche alla camera di prova, al sistema di ventilazione e agli strumenti di misura.</p>
    <div class="info-grid">
      <div class="info-cell"><div class="lbl">Sezione di prova</div><div class="val">Full-scale</div></div>
      <div class="info-cell"><div class="lbl">Velocità max</div><div class="val">250 km/h</div></div>
      <div class="info-cell"><div class="lbl">Turbolenza residua</div><div class="val">&lt; 0.74%</div></div>
      <div class="info-cell"><div class="lbl">Simulazione suolo</div><div class="val">T-Belt 250 km/h</div></div>
    </div>
    <h3>Il Concetto di Camera di Prova</h3>
    <p>La <strong>sezione di prova</strong> (o camera di misura) è la zona dove il flusso è uniforme, stazionario e a bassa turbolenza. La qualità del flusso in questa zona è il parametro più critico di una galleria del vento: viene caratterizzata dall'indice di turbolenza Tu:</p>
    <div class="formula-box">
      <span class="formula-label">Indice di Turbolenza</span>
      Tu = √(u'²) / U∞  × 100 [%]<br><br>
      dove u' = fluttuazione di velocità rms, U∞ = velocità media del flusso<br><br>
      Pininfarina: Tu &lt; 0.74% → qualità "laminare" eccellente
    </div>
    <div class="example-box">
      <span class="ex-label">Esempio Pratico — Confronto con Altre Gallerie</span>
      <p>La galleria ONERA F2 (Francia) ha Tu ≈ 0.1%, usata per ricerca aerospaziale; la galleria FIAT (Orbassano) ha Tu ≈ 1.5%. Il valore Pininfarina &lt;0.74% la posiziona nella fascia alta per uso automotive/aeronautico leggero, con un ottimo compromesso tra costo operativo e qualità del dato.</p>
    </div>
  `
},

'storia-gallerie': {
  title: 'Tipologie di Gallerie del Vento',
  body: `
    <h3>Classificazione per Circuito</h3>
    <ul class="detail-list">
      <li><strong>Circuito aperto (Eiffel)</strong>: l'aria viene aspirata dall'ambiente esterno, accelerata e scaricata all'esterno. Economica da costruire, ma sensibile alle condizioni ambientali e acusticamente rumorosa.</li>
      <li><strong>Circuito chiuso (Göttingen)</strong>: l'aria circola in un anello chiuso. Permette controllo preciso di temperatura, umidità e turbolenza. Costi energetici inferiori nel lungo periodo. La scelta di Pininfarina.</li>
    </ul>
    <h3>Classificazione per Regime di Flusso</h3>
    <div class="diagram-wrap">
      <svg viewBox="0 0 500 200" xmlns="http://www.w3.org/2000/svg" width="500" height="200">
        <rect width="500" height="200" fill="#0b1929" rx="12"/>
        <!-- timeline bar -->
        <rect x="40" y="95" width="420" height="10" rx="5" fill="rgba(30,159,255,0.15)"/>
        <!-- segments -->
        <rect x="40" y="95" width="100" height="10" rx="5" fill="rgba(61,255,208,0.6)"/>
        <rect x="140" y="95" width="120" height="10" fill="rgba(30,159,255,0.6)"/>
        <rect x="260" y="95" width="80" height="10" fill="rgba(245,166,35,0.6)"/>
        <rect x="340" y="95" width="120" height="10" rx="5" fill="rgba(255,79,79,0.6)"/>
        <!-- labels -->
        <text x="90" y="80" fill="#3dffd0" font-size="11" text-anchor="middle" font-family="DM Sans, sans-serif">Subsonico</text>
        <text x="90" y="130" fill="#7a9bbf" font-size="9" text-anchor="middle" font-family="DM Sans, sans-serif">Ma &lt; 0.3</text>
        <text x="200" y="80" fill="#1e9fff" font-size="11" text-anchor="middle" font-family="DM Sans, sans-serif">Subsonico</text>
        <text x="200" y="130" fill="#7a9bbf" font-size="9" text-anchor="middle" font-family="DM Sans, sans-serif">0.3–0.8</text>
        <text x="300" y="80" fill="#f5a623" font-size="11" text-anchor="middle" font-family="DM Sans, sans-serif">Transonico</text>
        <text x="300" y="130" fill="#7a9bbf" font-size="9" text-anchor="middle" font-family="DM Sans, sans-serif">0.8–1.2</text>
        <text x="400" y="80" fill="#ff4f4f" font-size="11" text-anchor="middle" font-family="DM Sans, sans-serif">Supersonico</text>
        <text x="400" y="130" fill="#7a9bbf" font-size="9" text-anchor="middle" font-family="DM Sans, sans-serif">Ma &gt; 1.2</text>
        <!-- Pininfarina marker -->
        <line x1="90" y1="88" x2="90" y2="108" stroke="#3dffd0" stroke-width="2"/>
        <text x="90" y="160" fill="#3dffd0" font-size="9" text-anchor="middle" font-family="DM Sans, sans-serif">▲ Pininfarina</text>
        <text x="90" y="172" fill="#3dffd0" font-size="9" text-anchor="middle" font-family="DM Sans, sans-serif">250 km/h</text>
      </svg>
    </div>
    <p>La galleria Pininfarina opera principalmente in regime subsonico (Ma ≈ 0.05–0.23), ideale per lo sviluppo di veicoli stradali, autobus, treni ad alta velocità e componenti aeronautici leggeri come UAV e alianti.</p>
    <div class="example-box">
      <span class="ex-label">Esempio — Numero di Mach alla Velocità Massima</span>
      <p>A 250 km/h ≈ 69.4 m/s, con la velocità del suono nell'aria a 20°C di circa 343 m/s:<br>
      Ma = 69.4 / 343 ≈ 0.202<br>
      Siamo ben nel regime subsonico incompressibile (Ma &lt; 0.3), dove le variazioni di densità dell'aria sono trascurabili (&lt; 2%) e le equazioni semplificate di Bernoulli si applicano con ottima approssimazione.</p>
    </div>
  `
},

'gess': {
  title: 'Ground Effect Simulation System (GESS)',
  body: `
    <h3>Il Problema dell'Effetto Suolo</h3>
    <p>In una galleria classica, il pavimento è fisso. Ma quando un veicolo si muove sulla strada, il suolo scorre <em>nella stessa direzione</em> del flusso d'aria, e la velocità relativa tra la parte inferiore del veicolo e il suolo è ZERO. Se il pavimento è fisso, si crea uno <strong>strato limite spesso e non realistico</strong> sotto il veicolo, falsando le misurazioni di pressione, portanza verticale e downforce (cruciale per le vetture da corsa).</p>
    <div class="formula-box">
      <span class="formula-label">Condizione al contorno reale (strada)</span>
      v_suolo = v_veicolo  →  v_relativa = 0<br><br>
      Condizione al contorno non corretta (galleria classica):<br>
      v_suolo = 0  →  strato limite non fisico
    </div>
    <h3>La Soluzione: Tappeto Mobile (Moving Belt)</h3>
    <p>Il GESS di Pininfarina utilizza un <strong>tappeto mobile (T-Belt)</strong> che scorre alla stessa velocità del flusso d'aria libero, replicando fedelmente le condizioni di strada. Questo elimina lo strato limite sul suolo nella zona sotto il veicolo, rendendo le misurazioni di portanza e downforce significativamente più accurate.</p>
    <div class="diagram-wrap">
      <svg viewBox="0 0 480 220" xmlns="http://www.w3.org/2000/svg">
        <rect width="480" height="220" fill="#0b1929" rx="12"/>
        <!-- Belt -->
        <rect x="40" y="160" width="400" height="18" rx="4" fill="rgba(30,159,255,0.15)" stroke="#1e9fff" stroke-width="1.2"/>
        <!-- Belt arrows (moving) -->
        <text x="60" y="172" fill="#1e9fff" font-size="10" font-family="monospace">→ → → → → → → → → →</text>
        <text x="40" y="155" fill="#1e9fff" font-size="9" font-family="DM Sans,sans-serif">Moving Belt (T-Belt) v = 250 km/h</text>
        <!-- Car -->
        <path d="M150 140 L160 110 L190 100 L290 100 L320 110 L330 140 Z" fill="rgba(30,159,255,0.12)" stroke="rgba(30,159,255,0.6)" stroke-width="1.5"/>
        <circle cx="180" cy="145" r="12" fill="rgba(30,159,255,0.2)" stroke="#1e9fff" stroke-width="1.2"/>
        <circle cx="300" cy="145" r="12" fill="rgba(30,159,255,0.2)" stroke="#1e9fff" stroke-width="1.2"/>
        <!-- Flow arrows -->
        <path d="M40 130 L140 130" stroke="#3dffd0" stroke-width="1.5" marker-end="url(#arr)" stroke-linecap="round"/>
        <path d="M40 120 L140 120" stroke="#3dffd0" stroke-width="1" marker-end="url(#arr)" stroke-linecap="round" opacity="0.7"/>
        <path d="M345 130 L430 130" stroke="#3dffd0" stroke-width="1.5" marker-end="url(#arr)" stroke-linecap="round"/>
        <defs>
          <marker id="arr" markerWidth="6" markerHeight="6" refX="3" refY="3" orient="auto">
            <path d="M0,0 L6,3 L0,6 Z" fill="#3dffd0"/>
          </marker>
        </defs>
        <text x="40" y="200" fill="#7a9bbf" font-size="10" font-family="DM Sans,sans-serif">Flusso libero U∞</text>
        <text x="200" y="200" fill="#3dffd0" font-size="10" font-family="DM Sans,sans-serif" text-anchor="middle">↑ Pressione reale sotto il veicolo</text>
      </svg>
    </div>
    <div class="example-box">
      <span class="ex-label">Applicazione Aeronautica — Effetto Suolo su Alianti</span>
      <p>Il fenomeno di "ground effect" è critico anche in aviazione: durante le fasi di decollo e atterraggio, l'ala opera in prossimità del suolo. Questo riduce il drag indotto del 30–50% rispetto al volo libero. Misurare correttamente questo effetto in galleria richiede un piano mobile calibrato alla velocità del flusso. I test su modelli di velivoli da addestramento (es. SIAI-Marchetti SF.260) in galleria Pininfarina con T-Belt attivo hanno permesso di caratterizzare l'effetto suolo senza costose campagne di volo.</p>
    </div>
    <h3>Rulli e Cinematica</h3>
    <p>Oltre al tappeto centrale, i <strong>rulli di azionamento delle ruote</strong> permettono di far "girare" le ruote del veicolo alla velocità corrispondente al flusso. Ruote stazionarie in galleria generano vortici parassite all'interno dei passaruota che non esistono in realtà su strada: una fonte di errore sistematico eliminata dal GESS.</p>
  `
},

'tgs': {
  title: 'Turbulence Generation System (TGS)',
  body: `
    <h3>Il Flusso Reale è Tutt'altro che Stazionario</h3>
    <p>In condizioni di circolazione reale, un veicolo incontra costantemente perturbazioni: raffiche di vento laterale, scie di veicoli precedenti, l'aria turbolenta dopo un sorpasso. Testare un veicolo in un flusso stazionario e laminare fornisce solo una parte dell'informazione necessaria per garantire stabilità dinamica e comfort.</p>
    <h3>Come Funziona il TGS</h3>
    <p>Il TGS utilizza <strong>ali oscillanti</strong> posizionate a monte della camera di prova. Queste ali, azionate da attuatori elettrici, battono a frequenze e ampiezze programmabili, inducendo perturbazioni controllate nel flusso che simulano:</p>
    <ul class="detail-list">
      <li>Raffiche di vento laterale (crosswind gusts) a diverse intensità</li>
      <li>Il passaggio nella scia (wake) di un veicolo precedente</li>
      <li>L'uscita dalla scia durante un sorpasso</li>
      <li>Fluttuazioni di pressione dovute a strutture adiacenti (gallerie, ponti)</li>
    </ul>
    <div class="formula-box">
      <span class="formula-label">Intensità di Turbolenza Generata</span>
      Tu_TGS = √( (u'² + v'² + w'²)/3 ) / U∞<br><br>
      Il TGS può generare Tu fino al 5–8%, replicando condizioni di traffico intenso o ambiente urbano ventoso, partendo dalla baseline Tu &lt; 0.74% della galleria.
    </div>
    <h3>Analisi in Frequenza: Lo Spettro di Turbulenza</h3>
    <p>La perturbazione non è solo caratterizzata dall'intensità, ma anche dalla <strong>scala integrale di lunghezza</strong> (L) e dallo spettro energetico (E(k)). Il TGS è progettato per replicare spettri di Von Kármán o Dryden, standard nell'aerodinamica aeronautica:</p>
    <div class="formula-box">
      <span class="formula-label">Spettro di Von Kármán (forma semplificata)</span>
      E(k) = C · (k·L)⁴ / [1 + (k·L)²]^(17/6)<br><br>
      dove k = numero d'onda, L = scala integrale, C = costante di normalizzazione
    </div>
    <div class="example-box">
      <span class="ex-label">Esempio Aeronautico — Gust Load su Velivolo Leggero</span>
      <p>Per un Cessna 172 in volo di crociera a 230 km/h, le raffiche verticali (vertical gusts) rappresentano il carico critico per la struttura alare. I regolamenti EASA CS-23 richiedono di dimostrare la resistenza a raffiche di 15.2 m/s (velocità di crociera) e 7.6 m/s (velocità di progetto massima). Il TGS consente di simulare tali raffiche su modelli scala 1:5 in galleria, validando le analisi strutturali FEM prima della costruzione del prototipo fisico.</p>
    </div>
  `
},

'aeroacustica': {
  title: 'Analisi Aeroacustica Avanzata',
  body: `
    <h3>Origini del Rumore Aerodinamico</h3>
    <p>Il rumore aerodinamico nasce dalla conversione di energia cinetica del flusso in onde di pressione sonora. I meccanismi principali sono:</p>
    <ul class="detail-list">
      <li><strong>Rumore di dipolo</strong>: generato dalla fluttuazione delle forze aerodinamiche su superfici solide (es. specchietti retrovisori, pilastri A, modanature)</li>
      <li><strong>Rumore di monopolo</strong>: sorgenti volumetriche (pulsazioni) — poco rilevante per veicoli stradali</li>
      <li><strong>Rumore di quadrupolo</strong>: turbolenza libera, dominante ad alte velocità (Ma > 0.3)</li>
    </ul>
    <div class="formula-box">
      <span class="formula-label">Legge di Potenza Acustica (dipolo)</span>
      W ∝ ρ · U⁶ · L²<br><br>
      Il rumore aerodinamico da dipolo cresce con la sesta potenza della velocità: raddoppiare la velocità aumenta il rumore di ~18 dB!
    </div>
    <h3>Strumentazione: Antenna a Microfoni</h3>
    <p>Pininfarina utilizza <strong>array di microfoni</strong> (antenna acustica) posizionati attorno alla camera di prova. Tecniche di beamforming elaborano i segnali in ritardo relativo per ottenere <em>mappe di sorgente acustica</em> (acoustic maps), identificando con precisione sub-centimetrica dove si generano i rumori.</p>
    <div class="diagram-wrap">
      <svg viewBox="0 0 480 180" xmlns="http://www.w3.org/2000/svg">
        <rect width="480" height="180" fill="#0b1929" rx="12"/>
        <!-- car -->
        <path d="M180 110 L190 82 L215 72 L265 72 L290 82 L300 110 Z" fill="rgba(61,255,208,0.08)" stroke="rgba(61,255,208,0.4)" stroke-width="1.2"/>
        <!-- noise sources (hot spots) -->
        <circle cx="192" cy="90" r="8" fill="rgba(255,79,79,0.3)" stroke="#ff4f4f" stroke-width="1"/>
        <circle cx="192" cy="90" r="14" fill="rgba(255,79,79,0.1)"/>
        <text x="192" y="68" fill="#ff4f4f" font-size="8" text-anchor="middle" font-family="DM Sans,sans-serif">Pilastro A</text>
        <circle cx="240" cy="76" r="5" fill="rgba(245,166,35,0.3)" stroke="#f5a623" stroke-width="1"/>
        <text x="240" y="64" fill="#f5a623" font-size="8" text-anchor="middle" font-family="DM Sans,sans-serif">Tetto</text>
        <circle cx="298" cy="88" r="10" fill="rgba(255,79,79,0.25)" stroke="#ff4f4f" stroke-width="1"/>
        <text x="298" y="68" fill="#ff4f4f" font-size="8" text-anchor="middle" font-family="DM Sans,sans-serif">Specchietto</text>
        <!-- microphone array -->
        <g opacity="0.7">
          <circle cx="80" cy="50" r="4" fill="#3dffd0"/><circle cx="80" cy="80" r="4" fill="#3dffd0"/>
          <circle cx="80" cy="110" r="4" fill="#3dffd0"/><circle cx="80" cy="140" r="4" fill="#3dffd0"/>
          <text x="80" y="168" fill="#3dffd0" font-size="8" text-anchor="middle" font-family="DM Sans,sans-serif">Array microfoni</text>
        </g>
        <!-- beamforming lines -->
        <line x1="84" y1="50" x2="192" y2="90" stroke="rgba(61,255,208,0.2)" stroke-width="0.8" stroke-dasharray="3 3"/>
        <line x1="84" y1="80" x2="192" y2="90" stroke="rgba(61,255,208,0.2)" stroke-width="0.8" stroke-dasharray="3 3"/>
        <line x1="84" y1="110" x2="298" y2="88" stroke="rgba(61,255,208,0.2)" stroke-width="0.8" stroke-dasharray="3 3"/>
        <line x1="84" y1="140" x2="298" y2="88" stroke="rgba(61,255,208,0.2)" stroke-width="0.8" stroke-dasharray="3 3"/>
        <text x="240" y="155" fill="#7a9bbf" font-size="9" text-anchor="middle" font-family="DM Sans,sans-serif">Mappa di sorgente acustica (beamforming)</text>
      </svg>
    </div>
    <div class="example-box">
      <span class="ex-label">Esempio — Rumore di Cavità in Aeronautica</span>
      <p>Vani del carrello, aperture di rifornimento e intercapedini strutturali generano <em>risonanza di cavità</em> a specifiche frequenze legate alle dimensioni geometriche (oscillatori di Rossiter). Un test aeroacustico su modello in galleria consente di identificare e correggere queste frequenze di risonanza — che possono raggiungere livelli superiori a 130 dB in prossimità delle strutture — prima che diventino un problema certificativo (CS-25 per transport category).</p>
    </div>
  `
},

'velocita': {
  title: 'Velocità Massima 250 km/h e Qualità del Flusso',
  body: `
    <h3>Perché la Qualità del Flusso è Critica</h3>
    <p>La validità di ogni misurazione in galleria del vento dipende direttamente dalla qualità del flusso nella camera di prova. Due parametri chiave sono:</p>
    <ul class="detail-list">
      <li><strong>Uniformità spaziale</strong>: la variazione di velocità nel piano perpendicolare al flusso deve essere &lt; ±0.5%</li>
      <li><strong>Indice di turbolenza Tu</strong>: la componente fluttuante della velocità deve essere &lt; 0.74% per la galleria Pininfarina</li>
    </ul>
    <div class="diagram-wrap">
      <svg viewBox="0 0 460 200" xmlns="http://www.w3.org/2000/svg">
        <rect width="460" height="200" fill="#0b1929" rx="12"/>
        <!-- Gauge/speedometer style -->
        <path d="M100 150 A80 80 0 0 1 260 150" fill="none" stroke="rgba(30,159,255,0.15)" stroke-width="20" stroke-linecap="round"/>
        <path d="M100 150 A80 80 0 0 1 260 150" fill="none" stroke="url(#speedGrad)" stroke-width="20" stroke-linecap="round" stroke-dasharray="251.2" stroke-dashoffset="0"/>
        <defs>
          <linearGradient id="speedGrad" x1="0%" y1="0%" x2="100%" y2="0%">
            <stop offset="0%" stop-color="#3dffd0"/>
            <stop offset="60%" stop-color="#1e9fff"/>
            <stop offset="100%" stop-color="#f5a623"/>
          </linearGradient>
        </defs>
        <!-- needle -->
        <line x1="180" y1="150" x2="120" y2="85" stroke="#f5a623" stroke-width="2.5" stroke-linecap="round" class="meter-needle"/>
        <circle cx="180" cy="150" r="8" fill="#f5a623" opacity="0.8"/>
        <!-- labels -->
        <text x="95" y="172" fill="#7a9bbf" font-size="11" font-family="DM Sans,sans-serif">0</text>
        <text x="170" y="62" fill="#7a9bbf" font-size="11" font-family="DM Sans,sans-serif">125</text>
        <text x="255" y="172" fill="#7a9bbf" font-size="11" font-family="DM Sans,sans-serif">250</text>
        <text x="180" y="140" fill="#f5a623" font-size="22" font-family="Bebas Neue,sans-serif" text-anchor="middle">250</text>
        <text x="180" y="155" fill="#7a9bbf" font-size="10" font-family="DM Sans,sans-serif" text-anchor="middle">km/h</text>
        <!-- Tu indicator -->
        <rect x="310" y="50" width="120" height="100" rx="10" fill="rgba(30,159,255,0.05)" stroke="rgba(30,159,255,0.2)" stroke-width="1"/>
        <text x="370" y="75" fill="#7a9bbf" font-size="10" text-anchor="middle" font-family="DM Sans,sans-serif">Turbolenza Tu</text>
        <text x="370" y="110" fill="#3dffd0" font-size="24" text-anchor="middle" font-family="Bebas Neue,sans-serif">&lt;0.74%</text>
        <text x="370" y="135" fill="#7a9bbf" font-size="9" text-anchor="middle" font-family="DM Sans,sans-serif">qualità laminare</text>
      </svg>
    </div>
    <h3>Come si Ottiene una Bassa Turbolenza</h3>
    <ul class="detail-list">
      <li><strong>Screens e honeycomb</strong>: griglie e celle esagonali posizionate prima dell'ugello convergente per rompere le strutture turbolente di grandi scale e allineare il flusso</li>
      <li><strong>Rapporto di contrazione elevato</strong>: la convergenza geometrica (rapporto 6:1 a 12:1) amplifica la velocità e riduce proporzionalmente le fluttuazioni trasversali</li>
      <li><strong>Ventilatore a pale profilate</strong>: progettato per generare flusso uniforme con minima perturbazione rotazionale</li>
    </ul>
    <div class="example-box">
      <span class="ex-label">Calcolo — Velocità Equivalente per Modello Scalato</span>
      <p>Un modello scala 1:4 di un velivolo da turismo testato a Re costante richiede una velocità in galleria 4× superiore a quella di volo reale. Per un velivolo che vola a 250 km/h, servirebbero 1000 km/h: impossibile a Pininfarina. Si opera quindi a Reynolds ridotto e si applica una correzione di scala basata su correlazioni empiriche di Cd(Re) — procedura standard nelle prove di certificazione EASA.</p>
    </div>
  `
},

'bernoulli': {
  title: 'Teorema di Bernoulli e Generazione di Portanza',
  body: `
    <h3>Equazione di Bernoulli</h3>
    <p>Per un fluido ideale (inviscido, incompressibile) in moto stazionario lungo una linea di flusso, la somma dell'energia cinetica, dell'energia di pressione e dell'energia potenziale rimane costante:</p>
    <div class="formula-box">
      <span class="formula-label">Equazione di Bernoulli</span>
      p + ½ρv² + ρgh = costante<br><br>
      dove:<br>
      p = pressione statica [Pa]<br>
      ρ = densità del fluido [kg/m³]<br>
      v = velocità del fluido [m/s]<br>
      g = accelerazione di gravità [9.81 m/s²]<br>
      h = quota [m]<br><br>
      Per flussi orizzontali (h = cost):<br>
      p + ½ρv² = p₀ = pressione totale (costante)
    </div>
    <h3>Portanza su un Profilo Alare</h3>
    <p>Un profilo alare (airfoil) ha una superficie superiore più curva: il flusso accelera sulla parte superiore (v↑ → p↓) e decelera su quella inferiore (v↓ → p↑). La differenza di pressione genera una <strong>forza risultante verso l'alto: la portanza L</strong>.</p>
    <div class="diagram-wrap">
      <svg viewBox="0 0 480 160" xmlns="http://www.w3.org/2000/svg">
        <rect width="480" height="160" fill="#0b1929" rx="12"/>
        <!-- Airfoil -->
        <path d="M80 80 Q150 50 300 68 Q380 74 400 80 Q380 88 300 94 Q150 110 80 80 Z"
              fill="rgba(30,159,255,0.15)" stroke="#1e9fff" stroke-width="1.5"/>
        <!-- flow lines upper (faster) -->
        <path d="M30 55 Q200 30 430 55" stroke="#3dffd0" stroke-width="1.2" fill="none" stroke-dasharray="5 3" opacity="0.8"/>
        <path d="M30 45 Q200 20 430 45" stroke="#3dffd0" stroke-width="1" fill="none" stroke-dasharray="5 3" opacity="0.6"/>
        <!-- flow lines lower (slower) -->
        <path d="M30 110 Q200 120 430 110" stroke="#f5a623" stroke-width="1.2" fill="none" stroke-dasharray="5 3" opacity="0.8"/>
        <path d="M30 118 Q200 130 430 118" stroke="#f5a623" stroke-width="1" fill="none" stroke-dasharray="5 3" opacity="0.6"/>
        <!-- pressure arrows -->
        <path d="M240 62 L240 50" stroke="#3dffd0" stroke-width="1.5" marker-end="url(#upArr)"/>
        <path d="M240 92 L240 104" stroke="#f5a623" stroke-width="1.5" marker-end="url(#downArr)"/>
        <defs>
          <marker id="upArr" markerWidth="6" markerHeight="6" refX="3" refY="3" orient="auto"><path d="M0,6 L3,0 L6,6 Z" fill="#3dffd0"/></marker>
          <marker id="downArr" markerWidth="6" markerHeight="6" refX="3" refY="3" orient="auto"><path d="M0,0 L3,6 L6,0 Z" fill="#f5a623"/></marker>
        </defs>
        <!-- Lift arrow -->
        <path d="M350 80 L350 48" stroke="white" stroke-width="2" marker-end="url(#liftArr)"/>
        <defs>
          <marker id="liftArr" markerWidth="6" markerHeight="6" refX="3" refY="6" orient="auto"><path d="M0,6 L3,0 L6,6 Z" fill="white"/></marker>
        </defs>
        <text x="362" y="62" fill="white" font-size="11" font-family="DM Sans,sans-serif">L</text>
        <!-- labels -->
        <text x="30" y="40" fill="#3dffd0" font-size="9" font-family="DM Sans,sans-serif">v alta → p bassa</text>
        <text x="30" y="140" fill="#f5a623" font-size="9" font-family="DM Sans,sans-serif">v bassa → p alta</text>
      </svg>
    </div>
    <div class="formula-box">
      <span class="formula-label">Forza di Portanza</span>
      L = ½ · ρ · v² · S · CL<br><br>
      D = ½ · ρ · v² · S · CD   (resistenza aerodinamica)<br><br>
      CL = coefficiente di portanza (dipende da profilo e angolo di attacco α)<br>
      S = superficie alare di riferimento [m²]
    </div>
    <div class="example-box">
      <span class="ex-label">Esempio — Portanza Ala Cessna 172 a V = 150 km/h</span>
      <p>Dati: ρ_aria = 1.225 kg/m³, V = 150 km/h = 41.7 m/s, S = 16.2 m², CL ≈ 0.7 (assetto di crociera)<br>
      L = ½ × 1.225 × 41.7² × 16.2 × 0.7 = ½ × 1.225 × 1739 × 16.2 × 0.7 ≈ 12,150 N ≈ 1238 kg<br>
      Il MTOW del Cessna 172 è circa 1111 kg: il margine di portanza è adeguato per il volo livellato.</p>
    </div>
  `
},

'dragcoeff': {
  title: 'Coefficiente di Resistenza Aerodinamica (Cd)',
  body: `
    <h3>Definizione Rigorosa</h3>
    <p>Il coefficiente di resistenza aerodinamica Cd (o Cx nella nomenclatura europea) è un numero adimensionale che quantifica l'efficienza aerodinamica di un corpo rispetto alla resistenza al moto:</p>
    <div class="formula-box">
      <span class="formula-label">Definizione di Cd</span>
      Cd = D / (½ · ρ · v² · A)<br><br>
      dove:<br>
      D = forza di resistenza aerodinamica misurata [N]<br>
      ρ = densità dell'aria [kg/m³]<br>
      v = velocità del flusso [m/s]<br>
      A = area di riferimento frontale del veicolo [m²]
    </div>
    <h3>Componenti della Resistenza</h3>
    <ul class="detail-list">
      <li><strong>Pressione (form drag)</strong>: differenza di pressione tra fronte e retro del veicolo; dominante nei corpi tozzi</li>
      <li><strong>Attrito (skin friction)</strong>: forze tangenziali dello strato limite sulla superficie; dominante nei corpi snelli</li>
      <li><strong>Indotta (induced drag)</strong>: generata dalla portanza stessa (vortici di estremità); cruciale per le ali</li>
      <li><strong>Interferenza</strong>: interazione tra componenti (ruote, spoiler, giunzioni)</li>
    </ul>
    <div class="info-grid">
      <div class="info-cell"><div class="lbl">Auto berlina moderna</div><div class="val">Cd ≈ 0.22–0.28</div></div>
      <div class="info-cell"><div class="lbl">Autobus</div><div class="val">Cd ≈ 0.35–0.45</div></div>
      <div class="info-cell"><div class="lbl">Profilo NACA 0012 (α=0°)</div><div class="val">Cd ≈ 0.006</div></div>
      <div class="info-cell"><div class="lbl">Boeing 747 (crociera)</div><div class="val">L/D ≈ 17 → Cd ≈ 0.035</div></div>
    </div>
    <div class="example-box">
      <span class="ex-label">Impatto del Cd sul Consumo Energetico</span>
      <p>Per un veicolo elettrico a 130 km/h (A=2.3 m²): ridurre il Cd da 0.30 a 0.23 (−23%) riduce la potenza aerodinamica necessaria di 23%, estendendo l'autonomia di circa 15–18 km/100 km. In aviazione, l'effetto è ancora più marcato: per un Piaggio P.180 Avanti con propulsori spintore, il profilo laminare riduce il drag del 30% rispetto a design convenzionali equivalenti, abbassando il consumo a 390 l/h vs. 520 l/h di concorrenti turboelica comparabili.</p>
    </div>
    <h3>Misurazione in Galleria</h3>
    <p>La forza D viene misurata con una <strong>bilancia aerodinamica a 6 componenti</strong> (3 forze + 3 momenti), montata sotto il pavimento della camera di prova. La precisione tipica è ±0.5 N su veicoli che generano drag di 400–800 N alla velocità di prova.</p>
  `
},

'strati': {
  title: 'Strato Limite e Separazione del Flusso',
  body: `
    <h3>Definizione di Strato Limite</h3>
    <p>Lo strato limite è la regione di flusso in prossimità di una superficie solida dove gli effetti viscosi sono significativi. Al di fuori dello strato limite, il flusso si comporta come fluido ideale (invisicido). Lo spessore δ dello strato limite cresce lungo la superficie nella direzione del flusso.</p>
    <div class="formula-box">
      <span class="formula-label">Spessore Strato Limite Laminare (lastra piana)</span>
      δ(x) = 5.0 · x · Re_x^(-1/2)<br><br>
      Re_x = ρ · U∞ · x / μ  (numero di Reynolds locale)<br><br>
      μ = viscosità dinamica aria ≈ 1.81×10⁻⁵ Pa·s a 20°C
    </div>
    <h3>Transizione Laminare → Turbolento</h3>
    <p>Oltre un valore critico di Re_x (tipicamente 3×10⁵ – 10⁶ per lastra piana liscia), lo strato limite transisce da laminare a turbolento. Il flusso turbolento ha maggiore miscelazione trasversale, profilo di velocità più pieno, ma genera anche maggiore attrito.</p>
    <div class="diagram-wrap">
      <svg viewBox="0 0 480 170" xmlns="http://www.w3.org/2000/svg">
        <rect width="480" height="170" fill="#0b1929" rx="12"/>
        <!-- flat plate -->
        <rect x="30" y="120" width="420" height="6" fill="rgba(30,159,255,0.3)" rx="2"/>
        <!-- laminar BL -->
        <path d="M30 120 Q80 110 120 90" fill="rgba(61,255,208,0.12)" stroke="#3dffd0" stroke-width="1.5"/>
        <!-- turbulent BL -->
        <path d="M120 90 Q200 75 300 60 Q380 48 450 40" fill="rgba(30,159,255,0.08)" stroke="#1e9fff" stroke-width="1.5"/>
        <!-- transition marker -->
        <line x1="120" y1="40" x2="120" y2="125" stroke="#f5a623" stroke-width="1" stroke-dasharray="4 3"/>
        <text x="122" y="38" fill="#f5a623" font-size="9" font-family="DM Sans,sans-serif">Transizione</text>
        <!-- labels -->
        <text x="60" y="100" fill="#3dffd0" font-size="9" font-family="DM Sans,sans-serif">Laminare</text>
        <text x="250" y="55" fill="#1e9fff" font-size="9" font-family="DM Sans,sans-serif">Turbolento</text>
        <!-- flow arrows -->
        <path d="M10 80 L28 80" stroke="#7a9bbf" stroke-width="1.2" marker-end="url(#floArr)"/>
        <path d="M10 70 L28 70" stroke="#7a9bbf" stroke-width="1" marker-end="url(#floArr)" opacity="0.6"/>
        <defs>
          <marker id="floArr" markerWidth="5" markerHeight="5" refX="3" refY="2.5" orient="auto"><path d="M0,0 L5,2.5 L0,5 Z" fill="#7a9bbf"/></marker>
        </defs>
        <!-- U∞ arrow -->
        <text x="5" y="108" fill="#7a9bbf" font-size="8" font-family="DM Sans,sans-serif">U∞ →</text>
        <!-- separation point annotation -->
        <circle cx="360" cy="68" r="5" fill="rgba(255,79,79,0.4)" stroke="#ff4f4f" stroke-width="1.2"/>
        <text x="365" y="60" fill="#ff4f4f" font-size="9" font-family="DM Sans,sans-serif">Possibile sep.</text>
      </svg>
    </div>
    <h3>Separazione del Flusso</h3>
    <p>Se il gradiente di pressione avverso (pressione crescente nella direzione del flusso) è abbastanza forte, il flusso nello strato limite perde quantità di moto e si separa dalla superficie. Questo genera una <strong>scia turbolenta</strong> con forte aumento della resistenza di pressione e, nel caso di un'ala, la perdita della portanza: lo <em>stallo</em>.</p>
    <div class="example-box">
      <span class="ex-label">Esempio — Stallo su Profilo NACA 2412</span>
      <p>Il profilo NACA 2412 (tipico di addestratori come il Piper PA-28) perde bruscamente portanza oltre α_stallo ≈ 16°. In galleria del vento, è possibile osservare con filo di lana (wool tuft test) o visualizzazione PIV il preciso angolo a cui il flusso si separa dal bordo d'attacco. Questo dato calibra i codici CFD e definisce il margine operativo sicuro per il pilota (CS-23 richiede margine minimo di 9 km/h dalla Vs alla velocità di controllo).</p>
    </div>
  `
},

'reynolds': {
  title: 'Numero di Reynolds e Similitudine Dinamica',
  body: `
    <h3>Il Numero di Reynolds</h3>
    <p>Il numero di Reynolds (Re) è il parametro adimensionale fondamentale per caratterizzare il flusso viscoso. Esprime il rapporto tra le forze inerziali e le forze viscose:</p>
    <div class="formula-box">
      <span class="formula-label">Numero di Reynolds</span>
      Re = ρ · U · L / μ = U · L / ν<br><br>
      dove:<br>
      ρ = densità fluido [kg/m³]<br>
      U = velocità caratteristica [m/s]<br>
      L = lunghezza caratteristica [m]<br>
      μ = viscosità dinamica [Pa·s]<br>
      ν = μ/ρ = viscosità cinematica [m²/s] (aria: ~1.5×10⁻⁵ m²/s a 20°C)
    </div>
    <h3>Similitudine Dinamica</h3>
    <p>Per ottenere risultati validi da un modello in scala, il numero di Reynolds del modello deve eguagliare quello del veicolo reale (similitudine dinamica completa). Per un modello 1:n in aria alla stessa densità:</p>
    <div class="formula-box">
      <span class="formula-label">Condizione di Similitudine</span>
      Re_modello = Re_reale<br>
      U_modello · L_modello = U_reale · L_reale<br>
      U_modello = U_reale · n<br><br>
      Modello 1:4 → velocità 4× superiore al reale<br>
      Modello 1:1 (full-scale) → stessa velocità: nessuna correzione
    </div>
    <h3>Vantaggi del Full-Scale Testing</h3>
    <p>La galleria Pininfarina è una galleria <strong>full-scale</strong> (scala 1:1): elimina completamente il problema della similitudine di Reynolds. Nessuna correzione è necessaria per il coefficiente aerodinamico. Questo è il principale vantaggio rispetto alle gallerie su modello in scala ridotta utilizzate in molti centri universitari o nella fase preliminare di progetto.</p>
    <div class="example-box">
      <span class="ex-label">Calcolo — Re Tipici in Aeronautica</span>
      <p>Aliante Schempp-Hirth Discus-2 in volo a 120 km/h, corda alare = 0.8 m:<br>
      Re = (120/3.6 × 0.8) / 1.5×10⁻⁵ = 33.3 × 0.8 / 1.5×10⁻⁵ ≈ 1.78 × 10⁶<br><br>
      Test su modello 1:4 in galleria: corda = 0.2 m → per mantenere lo stesso Re, si deve volare a 480 km/h in galleria: impraticabile a Pininfarina. Il test a Re ridotto introduce correzioni sperimentali al CL e CD documentate in letteratura per i profili laminari serie Wortmann FX.</p>
    </div>
  `
},

'aeronautica': {
  title: 'Applicazioni Aeronautiche',
  body: `
    <h3>Test su Componenti Aeronautici</h3>
    <p>La galleria Pininfarina, pur non essendo dedicata esclusivamente all'aeronautica, ha caratteristiche tecniche — bassa turbolenza, tappeto mobile, sistema TGS, test full-scale — che la rendono adatta a una serie di applicazioni aeronautiche specifiche.</p>
    <ul class="detail-list">
      <li><strong>Profili alari a basso Re</strong>: UAV, alianti, velivoli ultraleggeri (Re = 10⁵–10⁶)</li>
      <li><strong>Gondole motore e nacelle</strong>: test di resistenza e compatibilità del flusso in ingresso</li>
      <li><strong>Superfici di controllo</strong>: alettoni, flap, slat — misura delle derivate aerodinamiche</li>
      <li><strong>Elicotteri e rotori</strong>: test in configurazione di avanzamento (forward flight)</li>
      <li><strong>Ground effect in fase di decollo/atterraggio</strong></li>
    </ul>
    <div class="diagram-wrap">
      <svg viewBox="0 0 480 180" xmlns="http://www.w3.org/2000/svg">
        <rect width="480" height="180" fill="#0b1929" rx="12"/>
        <!-- UAV shape -->
        <path d="M240 90 L180 100 L130 90 L180 80 Z" fill="rgba(61,255,208,0.12)" stroke="#3dffd0" stroke-width="1.2"/>
        <path d="M240 90 L300 100 L350 90 L300 80 Z" fill="rgba(61,255,208,0.12)" stroke="#3dffd0" stroke-width="1.2"/>
        <path d="M220 90 L260 90 L255 72 L225 72 Z" fill="rgba(61,255,208,0.08)" stroke="#3dffd0" stroke-width="1"/>
        <ellipse cx="240" cy="90" rx="25" ry="8" fill="rgba(61,255,208,0.15)" stroke="#3dffd0" stroke-width="1.2"/>
        <!-- flow lines -->
        <path d="M30 70 Q150 60 220 70 Q270 80 430 70" stroke="rgba(61,255,208,0.5)" stroke-width="1" fill="none" stroke-dasharray="5 3"/>
        <path d="M30 80 Q150 75 200 80 Q280 90 430 80" stroke="rgba(61,255,208,0.4)" stroke-width="1.2" fill="none" stroke-dasharray="5 3"/>
        <path d="M30 100 Q150 105 200 100 Q280 95 430 100" stroke="rgba(245,166,35,0.4)" stroke-width="1" fill="none" stroke-dasharray="5 3"/>
        <path d="M30 110 Q150 118 220 110 Q280 102 430 110" stroke="rgba(245,166,35,0.35)" stroke-width="1" fill="none" stroke-dasharray="5 3"/>
        <!-- label -->
        <text x="240" y="160" fill="#3dffd0" font-size="10" text-anchor="middle" font-family="DM Sans,sans-serif">UAV/Drone — test profilo alare a basso Re</text>
        <!-- force arrows -->
        <line x1="240" y1="85" x2="240" y2="55" stroke="white" stroke-width="2"/>
        <text x="248" y="62" fill="white" font-size="10" font-family="DM Sans,sans-serif">L</text>
        <line x1="255" y1="90" x2="290" y2="90" stroke="#ff4f4f" stroke-width="2"/>
        <text x="292" y="94" fill="#ff4f4f" font-size="10" font-family="DM Sans,sans-serif">D</text>
      </svg>
    </div>
    <h3>Normativa di Riferimento</h3>
    <ul class="detail-list">
      <li><strong>EASA CS-23</strong>: Normal, Utility, Aerobatic and Commuter Category Aeroplanes — requisiti aerodinamici per velivoli leggeri</li>
      <li><strong>EASA CS-25</strong>: Large Aeroplanes — test di flutter, stallo, studi di efficienza del profilo</li>
      <li><strong>ECSS-E-HB-10-02</strong>: specifiche per modelli di test in galleria (settore spazio/satellite)</li>
    </ul>
    <div class="example-box">
      <span class="ex-label">Case Study — Ottimizzazione Profilo Aliante</span>
      <p>Un produttore di alianti da competizione (es. Jonker Sailplanes JS3) utilizza la galleria per validare il profilo laminare custom sviluppato con XFOIL/MSES. Il profilo opera a Re ≈ 1.5×10⁶ in crociera. Il test in galleria a v_galleria = 60 m/s su corda di 0.38 m fornisce Re ≈ 1.52×10⁶: ottima corrispondenza senza correzioni. Si misura la polare CL–CD completa (da α = −5° a α = 18°) con una precisione di ΔCd = ±0.0002, impossibile ottenere con solo CFD.</p>
    </div>
  `
},

'civile': {
  title: 'Ingegneria Civile e Strutturale',
  body: `
    <h3>Vento sulle Strutture</h3>
    <p>Le strutture civili — grattacieli, ponti sospesi, coperture — sono soggette a carichi di vento che possono indurre fenomeni di risonanza strutturale o instabilità aeroelastica. Il test in galleria del vento è uno strumento fondamentale per la progettazione di strutture sicure in zone a rischio eolico.</p>
    <h3>Flutter Aeroelastico</h3>
    <p>Il flutter è un fenomeno di instabilità aeroelastica in cui le oscillazioni strutturali vengono alimentate dal flusso d'aria anziché smorzate. Oltre la velocità critica di flutter, le oscillazioni crescono esponenzialmente fino alla rottura. Il caso storico più noto è il crollo del <em>Tacoma Narrows Bridge</em> (1940).</p>
    <div class="formula-box">
      <span class="formula-label">Velocità Critica di Flutter (Sezione 2-DOF)</span>
      V_flutter = b · ω_α · √(2μ · (r_α² - x_α · r_α) / (1 - (ω_h/ω_α)²))<br><br>
      dove b = semispessore della sezione, ω_α = freq. angolare di torsione,<br>
      μ = parametro di massa, r_α = raggio di girazione, x_α = disallineamento CM-EA
    </div>
    <h3>Test Specifici</h3>
    <ul class="detail-list">
      <li><strong>Sezioni di ponti</strong>: modelli bidimensionali (strip model) su molla per misurare flutter e galloping</li>
      <li><strong>Modelli ad alta scala di edifici</strong>: pressure tap sul rivestimento per mappatura dei coefficienti di pressione</li>
      <li><strong>Imbarcazioni a vela</strong>: test su scafi e attrezzature veliche per ottimizzare aerodinamica e stabilità</li>
    </ul>
    <div class="example-box">
      <span class="ex-label">Esempio — Analisi Vento su Torre Alta</span>
      <p>Un grattacielo di 250 m in zona con Vref = 28 m/s (zona eolica 4 italiana, NTC 2018) richiede test in galleria su modello 1:500 a circa v_galleria ≈ 12 m/s per similitudine di Re. Si misurano i coefficienti di pressione esterni Cpe per le 16 direzioni di vento dominante, i carichi globali (forza di trascinamento, momento alla base) e i movimenti di estremità per verificare il comfort degli occupanti (a_rms &lt; 0.1 m/s² per uffici secondo ISO 6897).</p>
    </div>
  `
},

'sport': {
  title: 'Applicazioni Sportive',
  body: `
    <h3>L'Aerodinamica nelle Prestazioni Sportive</h3>
    <p>In molti sport, la resistenza aerodinamica è il principale limite fisico alle prestazioni. Ridurre il Cd anche del 5-10% può significare decimi di secondo decisivi in una gara. Gli atleti d'élite si sottopongono a test in galleria per ottimizzare postura, equipaggiamento e abbigliamento.</p>
    <ul class="detail-list">
      <li><strong>Sci alpino</strong>: posture di discesa (uovo), casco, tuta — riduzione Cd critica per velocità massima</li>
      <li><strong>Ciclismo</strong>: posizione aerodinamica su bici da cronometro, forma del casco, abbigliamento aderente</li>
      <li><strong>Vela</strong>: test su modelli di scafo e appendici (chiglia, timone) per ridurre la resistenza idrodinamica e ottimizzare l'aerodinamica delle vele</li>
      <li><strong>Atletica / bob / skeleton</strong>: riduzione della sezione frontale e ottimizzazione del profilo</li>
    </ul>
    <div class="formula-box">
      <span class="formula-label">Potenza Necessaria per Vincere la Resistenza</span>
      P_aero = D · v = ½ · ρ · v³ · A · Cd<br><br>
      Nota: la potenza cresce con il cubo della velocità!<br>
      Per un ciclista a 50 km/h: ridurre Cd×A del 10% risparmia ~55 W (≈ 10% della potenza totale)
    </div>
    <div class="example-box">
      <span class="ex-label">Esempio — Ottimizzazione Casco da Sci</span>
      <p>Un casco da discesa libera testato in galleria a 120 km/h (velocità tipica di un atleta di Coppa del Mondo) con atleta in posizione "uovo": la forza di drag varia tra 45 N (casco ottimizzato) e 58 N (casco standard). La differenza di 13 N a 120 km/h equivale a ΔP = 13 × (120/3.6) ≈ 433 W. In 90 secondi di gara, questa differenza energetica equivale a circa 39 kJ — sufficiente per creare distacchi di 1–2 secondi tra atleti di pari capacità fisica.</p>
    </div>
  `
},

'misure': {
  title: 'Strumentazione e Tecniche di Misura',
  body: `
    <h3>Bilancia Aerodinamica a 6 Componenti</h3>
    <p>Il cuore della misura in galleria è la <strong>bilancia aerodinamica</strong>: uno strumento che misura contemporaneamente le 3 forze (drag D, lift L, side force Y) e i 3 momenti (rollio, beccheggio, imbardata) agenti sul modello. È montata sotto il piano di prova e collegata al veicolo tramite steli.</p>
    <div class="formula-box">
      <span class="formula-label">Sistema di riferimento SAE (Wind Axes)</span>
      F_D = Drag (resistenza, asse x, parallelo al flusso)<br>
      F_L = Lift (portanza, asse z, perpendicolare al flusso)<br>
      F_Y = Side Force (forza laterale, asse y)<br>
      M_roll = Momento di rollio (intorno all'asse x)<br>
      M_pitch = Momento di beccheggio (intorno all'asse y)<br>
      M_yaw = Momento di imbardata (intorno all'asse z)
    </div>
    <h3>PIV — Particle Image Velocimetry</h3>
    <p>Il PIV è una tecnica ottica non intrusiva per misurare il campo di velocità su un piano illuminato da un laser. Particelle tracer (nebbia di olio, ~1 μm) vengono semine nel flusso e illuminate da due impulsi laser separati da Δt noto. Una CCD registra due fotogrammi; la cross-correlazione statistica fornisce il vettore spostamento (e quindi velocità) su una griglia densa di punti.</p>
    <h3>Hot Wire Anemometry (HWA)</h3>
    <p>Un filo metallico riscaldato (tungsteno, ø 5 μm) immerso nel flusso perde calore proporzionalmente alla velocità. La HWA ha risposta in frequenza di 10–100 kHz, ideale per misurare turbolenza, spettri e fluttuazioni rapide — impossibili con Pitot o PIV convenzionale.</p>
    <div class="example-box">
      <span class="ex-label">Esempio Aeronautico — Misura Campo di Velocità nel Wake di un'Ala</span>
      <p>Con PIV stereoscopico (Stereo-PIV), si misura il campo di velocità tridimensionale nel piano trasversale a valle di un'ala (wake plane). Integrando il deficit di quantità di moto nel wake, si calcola il drag indotto con la formula di Trefftz:<br>
      D_i = ρ/2 · ∬[(U∞ - u)² + v² + w²] dA<br>
      Il confronto con la bilancia fornisce la suddivisione tra drag di pressione e drag indotto, informazione fondamentale per l'ottimizzazione del winglet.</p>
    </div>
  `
},

'cfd': {
  title: 'CFD e Galleria del Vento: Sinergia Moderna',
  body: `
    <h3>Cos'è la CFD</h3>
    <p>La Computational Fluid Dynamics (CFD) risolve numericamente le equazioni di Navier-Stokes per simulare il comportamento di un fluido attorno a un corpo. I principali approcci sono RANS (Reynolds-Averaged Navier-Stokes), LES (Large Eddy Simulation) e DNS (Direct Numerical Simulation).</p>
    <div class="formula-box">
      <span class="formula-label">Equazioni di Navier-Stokes (forma vettoriale)</span>
      ρ · (∂u/∂t + u·∇u) = -∇p + μ·∇²u + f<br><br>
      + equazione di continuità:<br>
      ∇·u = 0  (flusso incompressibile)<br><br>
      RANS introduce il tensore di Reynolds τ_ij = -ρ·u'_i·u'_j che richiede un modello di chiusura (k-ε, k-ω SST, SA...)
    </div>
    <h3>Confronto: CFD vs Galleria del Vento</h3>
    <div class="info-grid">
      <div class="info-cell"><div class="lbl">CFD — Vantaggi</div><div class="val" style="font-size:0.85rem; line-height:1.4">Campo completo, ogni quantità ovunque; parametrico; economico per iterazioni</div></div>
      <div class="info-cell"><div class="lbl">CFD — Limiti</div><div class="val" style="font-size:0.85rem; line-height:1.4">Modelli di turbolenza approx.; mesh-dipendente; separazioni complesse difficili</div></div>
      <div class="info-cell"><div class="lbl">Galleria — Vantaggi</div><div class="val" style="font-size:0.85rem; line-height:1.4">Dati sperimentali veri; effetti non lineari reali; certificabile</div></div>
      <div class="info-cell"><div class="lbl">Galleria — Limiti</div><div class="val" style="font-size:0.85rem; line-height:1.4">Costosa; interferenza pareti; dati puntuali; no visibilità interna al flusso</div></div>
    </div>
    <h3>Il Workflow Ibrido Moderno</h3>
    <p>L'approccio ottimale combina le due metodologie: CFD per l'esplorazione rapida dello spazio di design (centinaia di configurazioni), poi galleria del vento per la validazione dei candidati finali (3–5 configurazioni) e per i test di certificazione.</p>
    <div class="example-box">
      <span class="ex-label">Workflow — Sviluppo Profilo Alare UAV</span>
      <p>1. XFOIL/OpenFOAM: analisi 2D di 50 profili candidati → selezione top 5<br>
      2. CFD 3D (RANS k-ω SST): analisi di ala finita con i 5 profili a Re = 10⁵–3×10⁵<br>
      3. Test in galleria Pininfarina su modello 1:1 del profilo migliore: validazione CL, CD, α_stallo<br>
      4. Correzione del codice CFD (correlation) per uso nei cicli di ottimizzazione futuri<br>
      Risultato: riduzione del tempo di sviluppo del 60% rispetto al solo approccio sperimentale tradizionale.</p>
    </div>
  `
},

'futuro': {
  title: 'Il Futuro della Galleria del Vento',
  body: `
    <h3>La Sfida della Mobilità Elettrica</h3>
    <p>I veicoli elettrici (EV) amplificano l'importanza dell'aerodinamica: senza il rumore del motore termico, i rumori aerodinamici diventano dominanti già a 60 km/h. Inoltre, ogni percento di riduzione del drag si traduce direttamente in autonomia aggiuntiva — una metrica critica per gli EV.</p>
    <ul class="detail-list">
      <li><strong>Thermal management aerodinamico</strong>: batterie e motori elettrici richiedono flussi d'aria specifici per il raffreddamento, in conflitto con l'ottimizzazione del Cd</li>
      <li><strong>Aerodinamica attiva</strong>: spoiler, flap e prese d'aria ad apertura variabile — test di controllo in galleria</li>
      <li><strong>Veicoli a idrogeno</strong>: nuova geometria delle celle a combustibile richiede test di integrazione termofluido</li>
    </ul>
    <h3>eVTOL e Urban Air Mobility</h3>
    <p>I nuovi velivoli a decollo verticale elettrico (eVTOL) — come Lilium Jet, Joby Aviation, Wisk Aero — operano a basso Re e in prossimità del suolo urbano: un contesto dove la galleria Pininfarina ha competenze uniche (ground effect simulation, bassa turbolenza, TGS).</p>
    <div class="formula-box">
      <span class="formula-label">Potenza di Hovering (teoria disco attuatore)</span>
      P_hover = T · v_induced = T · √(T / (2ρA_rotor))<br><br>
      Per minimizzare P_hover (e quindi la batteria necessaria):<br>
      → massimizzare A_rotor (rotori grandi, efficienza energetica ↑)<br>
      → studi in galleria su interazione tra rotori multipli (tip vortex interaction)
    </div>
    <div class="example-box">
      <span class="ex-label">Scenario Futuro — Digital Twin della Galleria</span>
      <p>Il digital twin integra un modello CFD ad alta fedeltà della galleria stessa (geometria, pareti, condizioni di prova) con i dati sperimentali in tempo reale. Ciò permette: correzione automatica degli effetti di interferenza delle pareti, ottimizzazione adattiva delle condizioni di prova, accumulazione di un database strutturato per il machine learning applicato all'aerodinamica. La galleria Pininfarina sta sviluppando questo approccio in collaborazione con i principali OEM europei per ridurre il numero di test fisici necessari nella fase di validazione finale.</p>
    </div>
    <h3>Sostenibilità Energetica della Galleria</h3>
    <p>Una galleria a 250 km/h consuma nell'ordine di 1–3 MW di potenza elettrica durante i test. Le iniziative future includono l'alimentazione da fonti rinnovabili, il recupero energetico dal sistema di frenatura del ventilatore e l'ottimizzazione dei protocolli di prova per ridurre le ore di funzionamento a piena potenza.</p>
  `
}

}; // end MODALS

// ═══════ OPEN / CLOSE ═══════
function openModal(id) {
  const data = MODALS[id];
  if (!data) return;
  document.getElementById('modal-title').textContent = data.title;
  document.getElementById('modal-body').innerHTML = data.body;
  document.getElementById('overlay').classList.add('open');
  document.body.style.overflow = 'hidden';
}

function closeModal(e) {
  if (e && e.target !== document.getElementById('overlay') && e.type !== 'click') return;
  if (e && e.target !== document.getElementById('overlay') && !e.currentTarget?.classList.contains('modal-close')) {
    if (e.type === 'click' && e.target.id !== 'overlay') return;
  }
  document.getElementById('overlay').classList.remove('open');
  document.body.style.overflow = '';
}

document.addEventListener('keydown', e => { if (e.key === 'Escape') { document.getElementById('overlay').classList.remove('open'); document.body.style.overflow=''; } });

// ═══════ TABS ═══════
function switchTab(e, id) {
  const modal = document.getElementById('modal-body');
  modal.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
  modal.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  e.currentTarget.classList.add('active');
}

// ═══════ SCROLL TO ═══════
function scrollTo(sel) {
  const el = document.querySelector(sel);
  if (el) el.scrollIntoView({ behavior: 'smooth', block: 'start' });
}

// ═══════ SCROLL REVEAL ═══════
const observer = new IntersectionObserver((entries) => {
  entries.forEach((entry, i) => {
    if (entry.isIntersecting) {
      const card = entry.target;
      const siblings = [...card.parentElement.children];
      const idx = siblings.indexOf(card);
      setTimeout(() => card.classList.add('visible'), idx * 80);
      observer.unobserve(card);
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.card').forEach(card => observer.observe(card));

// ═══════ NAV ACTIVE ═══════
const sections = document.querySelectorAll('section[id]');
const navItems = document.querySelectorAll('.nav-item');
window.addEventListener('scroll', () => {
  let current = '';
  sections.forEach(s => { if (window.scrollY >= s.offsetTop - 120) current = s.id; });
  navItems.forEach(n => {
    n.classList.remove('active');
    if (n.textContent.toLowerCase().includes(current.substring(0,4))) n.classList.add('active');
  });
}, { passive: true });
</script>
</body>
</html>
