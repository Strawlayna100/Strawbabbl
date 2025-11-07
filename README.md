# Strawbabbl
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="default">
  <meta name="format-detection" content="telephone=no">
  <title>Strawbabble – The Pure Garden</title>
  <link href="https://fonts.googleapis.com/css2?family=Fredoka+One&family=Comic+Neue:wght@400;700&family=Reenie+Beanie&display=swap" rel="stylesheet">
  <link rel="apple-touch-icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><circle cx='50' cy='50' r='45' fill='%23FF4D6D'/><path d='M35 40c0-3 2-5 5-5s5 2 5 5-2 5-5 5-5-2-5-5m20 0c0-3 2-5 5-5s5 2 5 5-2 5-5 5-5-2-5-5' fill='%2390EE90'/><path d='M45 55c0 5 10 10 10 10s10-5 10-10c0-3-5-5-10-5s-10 2-10 5' fill='white'/></svg>">
  <style>
    :root{
      --sky-day:#A0D8F1;--sky-night:#1C3A6B;--grass:#6BBF5A;--flower:#FFB6C1;--strawberry:#FF4D6D;
      --lbp-blue:#6BB9F0;--lbp-pink:#FF69B4;--dora-purple:#9B59B6;--noggin-orange:#FF7F50;
      --crayola-yellow:#FFD700;--alice-teal:#4ECDC4;--disney-cream:#FFF8E7;--text:#22313F;
      --card:rgba(255,255,255,0.96);--shadow:rgba(0,0,0,0.18);--sun:#FFEB3B;--moon:#F4F1C9;
      --cloud:rgba(255,255,255,0.9);--spring:#B5EAD7;--summer:#90EE90;--autumn:#FFB366;
      --winter:#E0F7FA;--gold:#FFD700;
    }
    *{margin:0;padding:0;box-sizing:border-box;}
    
    /* A11y Fix: Visible focus states for keyboard users */
    *:focus-visible {
      outline: 4px dashed var(--dora-purple);
      outline-offset: 2px;
    }

    body{
      background:linear-gradient(to bottom,var(--sky-day) 0%,var(--spring) 40%,var(--grass) 100%);
      font-family:'Comic Neue',cursive;color:var(--text);overflow:hidden;height:100vh;
      perspective:1600px;transition:background 3s ease;position:relative;
      -webkit-font-smoothing:antialiased;-webkit-tap-highlight-color:transparent;
      touch-action:manipulation;
    }
    /* Seasonal and Day/Night Classes */
    body.night{background:linear-gradient(to bottom,var(--sky-night) 0%,#2C3E50 40%,#1e3a2a 100%);}
    body.summer{--grass:var(--summer);}
    body.autumn{--grass:var(--autumn);}
    body.winter{--grass:var(--winter);background:linear-gradient(to bottom,#87CEEB 0%,#E0F7FA 40%,#FFF 100%);}
    body::before{
      content:'';position:absolute;top:0;left:0;right:0;bottom:0;
      background:radial-gradient(circle at 20% 80%,rgba(255,255,255,0) 0%,var(--sky-day) 100%);
      z-index:-1;
      opacity:0.6;
      transition:opacity 3s ease;
    }
    body.night::before{
      background:radial-gradient(circle at 80% 20%,rgba(0,0,0,0) 0%,var(--sky-night) 100%);
      opacity:0.8;
    }

    /* Sun and Moon */
    .sun, .moon{
      position:absolute;
      width:100px;
      height:100px;
      border-radius:50%;
      top:10%;
      right:10%;
      box-shadow:0 0 40px var(--gold);
      transition:transform 3s ease, background 3s ease;
      z-index:5;
    }
    .sun{
      background:var(--sun);
      transform:translateY(0);
      animation:pulse 4s infinite alternate;
    }
    .moon{
      background:var(--moon);
      transform:translateY(500px);
      box-shadow:0 0 30px #B0C4DE;
    }
    body.night .sun{
      transform:translateY(-500px);
    }
    body.night .moon{
      transform:translateY(0);
    }
    @keyframes pulse{
      from{box-shadow:0 0 20px var(--gold), 0 0 50px rgba(255,215,0,0.5);}
      to{box-shadow:0 0 40px var(--gold), 0 0 80px rgba(255,215,0,0.8);}
    }

    /* === 🌳 Structural Layout Styles === */

    header {
      position: relative;
      text-align: center;
      padding: 20px 0 10px;
      z-index: 10;
    }
    header h1 {
      font-family: 'Fredoka One', cursive;
      font-size: clamp(3rem, 10vw, 5rem);
      color: var(--text);
      text-shadow: 
        4px 4px 0 var(--lbp-pink),
        5px 5px 0 var(--strawberry);
      display: inline-block;
      padding: 0 15px;
      transform: rotate(-2deg);
    }
    
    main#garden {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 90%;
      max-width: 1200px;
      height: 70%;
      z-index: 5;
    }

    /* Control Panel (The Card) */
    aside.controls {
      position: fixed;
      top: 20px;
      right: 20px;
      width: 280px;
      padding: 20px;
      background: var(--card);
      border: 4px solid var(--text);
      border-radius: 15px;
      box-shadow: 10px 10px 0 var(--shadow);
      z-index: 15;
      transition: all 0.3s ease-in-out;
      font-family: 'Comic Neue', cursive;
    }
    @media (max-width: 768px) {
      aside.controls {
        position: fixed;
        top: auto;
        bottom: 0;
        left: 0;
        right: 0;
        width: 100%;
        border-radius: 15px 15px 0 0;
        box-shadow: 0 -5px 15px var(--shadow);
        padding-bottom: env(safe-area-inset-bottom, 20px);
      }
    }
    
    aside.controls h2 {
      font-family: 'Fredoka One', cursive;
      font-size: 1.5rem;
      margin-bottom: 15px;
      color: var(--dora-purple);
      text-align: center;
      border-bottom: 2px dashed var(--noggin-orange);
      padding-bottom: 8px;
    }

    /* General Garden Element Styles */
    .garden-element {
      position: absolute;
      cursor: pointer;
      user-select: none;
      transform-style: preserve-3d;
      transition: transform 0.5s ease;
    }
    .garden-element:hover {
      transform: scale(1.05) translateY(-5px);
      z-index: 7;
    }

    /* Control Group Styles */
    .control-group {
      margin-bottom: 20px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .control-label, .toggle-label {
      font-weight: 700;
      color: var(--text);
      font-size: 1.1rem;
    }
    .control-divider {
      border: none;
      height: 2px;
      background: linear-gradient(to right, transparent, var(--shadow), transparent);
      margin: 15px 0;
    }

    /* A11y: Screen Reader Only (sr-only) */
    .sr-only {
      position: absolute;
      width: 1px;
      height: 1px;
      padding: 0;
      margin: -1px;
      overflow: hidden;
      clip: rect(0, 0, 0, 0);
      white-space: nowrap;
      border-width: 0;
    }

    /* Day/Night Toggle Switch Styles */
    .toggle-switch {
      display: block;
      width: 60px;
      height: 30px;
      background-color: var(--sky-day);
      border-radius: 15px;
      position: relative;
      cursor: pointer;
      border: 2px solid var(--text);
      transition: background-color 0.5s ease;
    }
    .toggle-indicator {
      display: block;
      width: 26px;
      height: 26px;
      background-color: var(--sun);
      border-radius: 50%;
      position: absolute;
      top: 0;
      left: 0;
      box-shadow: 0 2px 4px var(--shadow);
      transform: translateX(0);
      transition: transform 0.5s ease, background-color 0.5s ease;
    }
    #nightMode:checked + .toggle-switch {
      background-color: var(--sky-night);
      border-color: var(--moon);
    }
    #nightMode:checked + .toggle-switch .toggle-indicator {
      transform: translateX(30px);
      background-color: var(--moon);
      box-shadow: 0 2px 4px #B0C4DE;
    }

    /* Season Selector Styles */
    .season-selector {
      display: flex;
      flex-wrap: wrap;
      gap: 5px;
      justify-content: center;
      margin-top: 10px;
    }
    .season-btn {
      flex: 1 1 45%;
      padding: 10px 5px;
      border: 2px solid var(--text);
      border-radius: 8px;
      cursor: pointer;
      font-family: 'Fredoka One', cursive;
      font-size: 0.9rem;
      transition: background-color 0.2s, color 0.2s, transform 0.1s;
      background-color: white;
      color: var(--text);
    }
    .season-btn:active {
      transform: scale(0.98);
    }
    .season-btn[data-season="spring"].active { background-color: var(--spring); color: var(--text); border-color: var(--grass); }
    .season-btn[data-season="summer"].active { background-color: var(--summer); color: var(--text); border-color: var(--grass); }
    .season-btn[data-season="autumn"].active { background-color: var(--autumn); color: white; border-color: #A0522D; }
    .season-btn[data-season="winter"].active { background-color: var(--winter); color: var(--text); border-color: #87CEEB; }
    .season-btn:not(.active):hover, .season-btn:not(.active):focus-visible {
      background-color: var(--disney-cream);
    }
    .season-btn.active {
      box-shadow: 3px 3px 0 var(--text);
      transform: translateY(-2px);
    }

    /* === 🍓 Garden Element Styles (Strawberry) === */
    .strawberry {
      position: absolute;
      width: 40px;
      height: 50px;
      cursor: pointer;
      z-index: 6;
      top: 50%; 
      left: 20%; 
      transform: translate(-50%, -50%) rotate(-5deg);
    }
    .berry-body {
      background: var(--strawberry);
      width: 100%;
      height: 100%;
      border-radius: 45% 45% 40% 40% / 60% 60% 40% 40%;
      border: 3px solid var(--text);
      box-shadow: inset -5px -5px 0px rgba(0,0,0,0.1);
      position: relative;
    }
    .berry-seeds {
      position: absolute;
      top: 30%;
      left: 10%;
      width: 80%;
      height: 60%;
      background: radial-gradient(circle at 10px 10px, rgba(255,255,255,0.7) 1px, transparent 1px);
      background-size: 15px 15px;
      transform: rotate(10deg);
    }
    .berry-leaf {
      position: absolute;
      width: 60px;
      height: 30px;
      background: var(--grass);
      border-radius: 50%;
      top: -10px;
      left: -10px;
      clip-path: polygon(50% 0%, 65% 25%, 100% 30%, 75% 50%, 90% 80%, 50% 60%, 10% 80%, 25% 50%, 0% 30%, 35% 25%);
      border: 2px solid var(--text);
      z-index: 1;
    }

    /* === 🌸 Flower Element Styles === */
    .flower {
      position: absolute;
      width: 50px;
      height: 50px;
      z-index: 5;
      top: 50%;
      left: 78%;
      transform: translate(-50%, -50%) rotate(0deg) scale(1.2);
    }
    .flower-stem {
      position: absolute;
      bottom: -15px;
      left: 50%;
      transform: translateX(-50%);
      width: 4px;
      height: 40px;
      background: #4682B4;
      border-radius: 2px;
      z-index: -1;
    }
    .flower-head {
      position: relative;
    }
    .petal {
      position: absolute;
      width: 25px;
      height: 40px;
      background: var(--flower);
      border-radius: 50%;
      margin-left: -12.5px;
      border: 2px solid var(--text);
    }
    .petal:nth-child(1) { transform: rotate(0deg) translateY(-20px); }
    .petal:nth-child(2) { transform: rotate(45deg) translateY(-20px); }
    .petal:nth-child(3) { transform: rotate(90deg) translateY(-20px); }
    .petal:nth-child(4) { transform: rotate(135deg) translateY(-20px); }
    .petal:nth-child(5) { transform: rotate(180deg) translateY(-20px); }
    .petal:nth-child(6) { transform: rotate(225deg) translateY(-20px); }
    .petal:nth-child(7) { transform: rotate(270deg) translateY(-20px); }
    .petal:nth-child(8) { transform: rotate(315deg) translateY(-20px); }

    .flower-center {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 15px;
      height: 15px;
      background: var(--gold);
      border-radius: 50%;
      border: 2px solid var(--text);
      z-index: 2;
    }

    /* Seasonal Effects */
    body.autumn main#garden::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      /* Tiny SVG for leaf pattern */
      background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="10" height="10"><rect width="10" height="10" fill="none"/><path d="M5 0 L10 5 L5 10 L0 5 Z" fill="%23D2B48C" opacity="0.4"/></svg>') repeat;
      pointer-events: none;
      opacity: 0.5;
      z-index: 1;
    }
    body.winter main#garden::after {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      /* Tiny SVG for snow pattern */
      background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="20" height="20"><g fill="white" opacity="0.6"><circle cx="5" cy="5" r="1"/><circle cx="15" cy="15" r="1.5"/></g></svg>') repeat;
      pointer-events: none;
      z-index: 10;
    }
  </style>
</head>
<body>
  <div class="sun"></div>
  <div class="moon"></div>

  <header role="banner">
    <h1>Strawbabble</h1>
  </header>

  <main id="garden" aria-label="The Pure Garden">
    
    <div class="strawberry garden-element" style="top: 75%; left: 30%; transform: rotate(-8deg) scale(1.1);">
      <div class="berry-leaf"></div>
      <div class="berry-body">
        <div class="berry-seeds"></div>
      </div>
    </div>

    <div class="strawberry garden-element" style="top: 85%; left: 65%; transform: rotate(15deg) scale(0.9);">
      <div class="berry-leaf"></div>
      <div class="berry-body">
        <div class="berry-seeds"></div>
      </div>
    </div>
    
    <div class="flower garden-element" style="top: 50%; left: 78%; transform: rotate(0deg) scale(1.2);">
      <div class="flower-stem"></div>
      <div class="flower-head">
        <div class="petal"></div>
        <div class="petal"></div>
        <div class="petal"></div>
        <div class="petal"></div>
        <div class="petal"></div>
        <div class="petal"></div>
        <div class="petal"></div>
        <div class="petal"></div>
        <div class="flower-center"></div>
      </div>
    </div>

    <div class="flower garden-element" style="top: 65%; left: 15%; transform: rotate(20deg) scale(0.8);">
      <div class="flower-stem"></div>
      <div class="flower-head">
        <div class="petal" style="background: var(--lbp-pink);"></div>
        <div class="petal" style="background: var(--lbp-pink);"></div>
        <div class="petal" style="background: var(--lbp-pink);"></div>
        <div class="petal" style="background: var(--lbp-pink);"></div>
        <div class="petal" style="background: var(--lbp-pink);"></div>
        <div class="petal" style="background: var(--lbp-pink);"></div>
        <div class="petal" style="background: var(--lbp-pink);"></div>
        <div class="petal" style="background: var(--lbp-pink);"></div>
        <div class="flower-center"></div>
      </div>
    </div>

  </main>

  <aside role="complementary" class="controls">
    <h2>Garden Controls</h2>
    
    <div class="control-group">
      <label for="nightMode" class="toggle-label">Day/Night Cycle</label>
      <input type="checkbox" id="nightMode" class="sr-only" aria-checked="false">
      <label for="nightMode" class="toggle-switch" aria-hidden="true">
        <span class="toggle-indicator"></span>
      </label>
    </div>

    <hr class="control-divider">

    <div class="control-group">
      <label class="control-label">Current Season</label>
      <div class="season-selector" role="radiogroup" aria-label="Select the current season">
        <button class="season-btn active" data-season="spring" aria-pressed="true">Spring</button>
        <button class="season-btn" data-season="summer" aria-pressed="false">Summer</button>
        <button class="season-btn" data-season="autumn" aria-pressed="false">Autumn</button>
        <button class="season-btn" data-season="winter" aria-pressed="false">Winter</button>
      </div>
    </div>
    
  </aside>

  <script>
    document.addEventListener('DOMContentLoaded', () => {
      const body = document.body;
      const nightModeToggle = document.getElementById('nightMode');
      const seasonButtons = document.querySelectorAll('.season-btn');
      
      // --- 1. Day/Night Toggle Handler ---
      nightModeToggle.addEventListener('change', (e) => {
        body.classList.toggle('night', e.target.checked);
        e.target.setAttribute('aria-checked', e.target.checked);
      });

      // --- 2. Season Selector Handler ---
      seasonButtons.forEach(button => {
        button.addEventListener('click', () => {
          const selectedSeason = button.getAttribute('data-season');
          
          // 2a. Update the Body Class
          body.classList.remove('spring', 'summer', 'autumn', 'winter');
          
          if (selectedSeason !== 'spring') {
              body.classList.add(selectedSeason);
          }
          
          // 2b. Update Button Active States and ARIA attributes
          seasonButtons.forEach(btn => {
            btn.classList.remove('active');
            btn.setAttribute('aria-pressed', 'false');
          });
          
          button.classList.add('active');
          button.setAttribute('aria-pressed', 'true');
        });
      });
      
      // Ensure initial ARIA status is set
      const initialActiveButton = document.querySelector('.season-btn.active');
      if (initialActiveButton) {
          initialActiveButton.setAttribute('aria-pressed', 'true');
      }
    });
  </script>

</body>
</html>
