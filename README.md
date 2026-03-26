<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Alejandro Na-Gue — HolonAI Research · De Colombia Para El Mundo</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;1,300;1,400;1,500&family=Josefin+Sans:wght@100;200;300;400&family=EB+Garamond:ital,wght@0,400;0,500;1,400;1,500&display=swap" rel="stylesheet">

  <style>
    /* ═══════════════════════════════════════════════
       DESIGN TOKENS
    ═══════════════════════════════════════════════ */
    :root {
      /* Dark navy void (slightly blue-shifted from original) */
      --void: #020412;
      --deep: #050920;
      --surface: #090d22;
      --raised: #0e1228;
      --card: #131830;
      --card-h: #182038;

      /* Gold brand palette */
      --gold: #C9A84C;
      --gold-hi: #F0C84A;
      --gold-bright: #F8D96A;
      --gold-pale: #ECDAAA;
      --gold-mid: #8B6E2A;
      --gold-low: #5C471C;

      /* Teal accents */
      --teal: #1C4A5E;
      --teal-m: #2A6E8A;
      --teal-b: #42A0BE;
      --teal-p: #72C4DA;

      /* Blue/violet palette for UI accents */
      --blue-a: #4A8FE7;
      --violet-a: #8B5CF6;
      --cyan-a: #22D3EE;

      /* Text hierarchy (warm against cool-dark background = nice contrast) */
      --t1: #EDE3CA;
      --t2: #BFA880;
      --t3: #806645;
      --t4: #503820;

      /* Glassmorphism borders (blue-tinted) */
      --b0: rgba(100,140,255,.07);
      --b1: rgba(120,155,255,.15);
      --b2: rgba(140,170,255,.30);
      --b3: rgba(160,185,255,.55);

      /* Series accent colors */
      --s-cdis: #42A0BE;
      --s-orveil: #C9A84C;
      --s-holon: #9B7FBE;
      --s-convergence: #BE7F42;

      /* Fibonacci spacing scale */
      --f1: 3px;  --f2: 5px;  --f3: 8px;  --f4: 13px; --f5: 21px;
      --f6: 34px; --f7: 55px; --f8: 89px; --f9: 144px;
    }

    /* ═══════════════════════════════════════════════
       RESET & BASE
    ═══════════════════════════════════════════════ */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }

    body {
      background: var(--void);
      color: var(--t1);
      font-family: 'Josefin Sans', sans-serif;
      font-weight: 300;
      letter-spacing: .04em;
      overflow-x: hidden;
      -webkit-font-smoothing: antialiased;
    }

    /* Film grain overlay */
    body::before {
      content: '';
      position: fixed; inset: 0;
      pointer-events: none; z-index: 9000;
      background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='200' height='200'%3E%3Cfilter id='g'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='200' height='200' filter='url(%23g)' opacity='1'/%3E%3C/svg%3E");
      opacity: .022;
    }

    /* ═══════════════════════════════════════════════
       CUSTOM CURSOR
    ═══════════════════════════════════════════════ */
    #cur, #cur-ring {
      position: fixed; pointer-events: none; border-radius: 50%;
      transform: translate(-50%,-50%); display: none; z-index: 9001;
    }
    @media (hover: hover) {
      #cur {
        display: block; width: 6px; height: 6px;
        background: var(--gold); transition: width .2s, height .2s, background .2s;
      }
      #cur-ring {
        display: block; width: 28px; height: 28px;
        border: 1px solid rgba(201,168,76,.4); transition: width .3s, height .3s, border-color .3s;
      }
      body.hov #cur { width: 10px; height: 10px; background: var(--gold-bright); }
      body.hov #cur-ring { width: 46px; height: 46px; border-color: rgba(248,217,106,.65); }
    }

    /* ═══════════════════════════════════════════════
       NAVIGATION
    ═══════════════════════════════════════════════ */
    nav {
      position: fixed; top: 0; left: 0; right: 0; height: 56px;
      z-index: 700; padding: 0 var(--f7);
      display: flex; align-items: center; justify-content: space-between;
      backdrop-filter: blur(24px) saturate(160%);
      background: rgba(2,4,18,.84);
      border-bottom: 1px solid var(--b0);
    }

    .nav-logo {
      font-family: 'Cormorant Garamond', serif; font-weight: 300;
      font-size: .95rem; letter-spacing: .5em; text-transform: uppercase;
      color: var(--gold); text-decoration: none;
    }
    .nav-logo sub { font-size: .6rem; letter-spacing: .22em; color: var(--t3); margin-left: .3em; }

    .nav-menu-btn {
      background: none; border: none; cursor: pointer; padding: var(--f3);
      display: flex; flex-direction: column; gap: 5px; z-index: 800;
    }
    .nav-menu-btn span {
      display: block; width: 22px; height: 1.5px;
      background: var(--gold); transition: all .35s ease;
    }
    .nav-menu-btn.open span:nth-child(1) { transform: translateY(7px) rotate(45deg); }
    .nav-menu-btn.open span:nth-child(2) { opacity: 0; transform: scaleX(0); }
    .nav-menu-btn.open span:nth-child(3) { transform: translateY(-7px) rotate(-45deg); }

    /* ═══════════════════════════════════════════════
       SIDEBAR
    ═══════════════════════════════════════════════ */
    .sidebar {
      position: fixed; left: -420px; top: 0; width: 400px; height: 100vh;
      background: linear-gradient(145deg, var(--deep) 0%, var(--surface) 100%);
      border-right: 1px solid var(--b1); z-index: 650;
      padding: 80px var(--f7) var(--f6);
      overflow-y: auto;
      transition: left .45s cubic-bezier(.34,1.56,.64,1);
    }
    .sidebar.open { left: 0; }

    .sidebar-header {
      font-family: 'Cormorant Garamond', serif; font-size: 1.8rem;
      color: var(--gold); margin-bottom: var(--f6); font-weight: 300;
    }
    .sidebar-nav {
      display: flex; flex-direction: column; gap: var(--f5); list-style: none; margin-bottom: var(--f8);
    }
    .sidebar-nav a {
      font-size: .58rem; letter-spacing: .25em; text-transform: uppercase;
      color: var(--t2); text-decoration: none; padding: var(--f2) 0;
      display: block; transition: color .3s;
    }
    .sidebar-nav a:hover { color: var(--gold); }

    .editor-trigger {
      width: 100%; padding: var(--f4) var(--f5);
      background: linear-gradient(135deg, var(--gold-low), var(--gold-mid));
      border: 1px solid var(--gold); color: var(--void); font-weight: 500;
      letter-spacing: .2em; text-transform: uppercase; cursor: pointer;
      transition: all .3s; font-size: .54rem; margin-bottom: var(--f5); font-family: inherit;
    }
    .editor-trigger:hover {
      background: linear-gradient(135deg, var(--gold-mid), var(--gold-bright));
      box-shadow: 0 8px 32px rgba(248,217,106,.25); transform: translateY(-2px);
    }
    .sidebar-meta {
      font-size: .48rem; color: var(--t4); letter-spacing: .15em; line-height: 1.8; margin-top: var(--f7);
    }

    /* ═══════════════════════════════════════════════
       HERO
    ═══════════════════════════════════════════════ */
    #hero {
      position: relative; width: 100%; min-height: 100svh;
      display: flex; flex-direction: column; justify-content: center;
      overflow: hidden; padding-top: 56px;
    }

    #vortex-canvas {
      position: absolute; inset: 0; width: 100%; height: 100%;
      display: block;
    }

    #hero::after {
      content: ''; position: absolute; inset: 0; pointer-events: none; z-index: 1;
      background: linear-gradient(
        108deg,
        rgba(2,4,18,.97) 0%,
        rgba(2,4,18,.82) 30%,
        rgba(2,4,18,.28) 60%,
        transparent 100%
      );
    }

    .hero-content {
      position: relative; z-index: 2; padding: 0 var(--f7); max-width: 60%;
    }

    h1.h-name {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(3.5rem, 10vw, 8.5rem);
      font-weight: 300; line-height: .88;
      animation: slideIn .9s ease .2s both;
    }
    .h-name .l1 { display: block; color: var(--t1); }
    .h-name .l2 { display: block; color: var(--gold); font-style: italic; }

    .h-tagline {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(.85rem, 1.5vw, 1.15rem);
      font-style: italic; color: var(--t2);
      margin-top: var(--f6); animation: slideIn .9s ease .3s both;
    }

    .h-rule {
      width: 120px; height: 2px;
      background: linear-gradient(90deg, var(--gold), transparent);
      margin: var(--f6) 0; animation: slideIn .9s ease .4s both;
    }

    .h-desc {
      font-size: clamp(.54rem, .65vw, .62rem); font-weight: 300;
      letter-spacing: .2em; text-transform: uppercase; color: var(--t3);
      line-height: 2; animation: slideIn .9s ease .5s both; margin-bottom: var(--f6);
    }

    .btn-primary {
      font-family: 'Josefin Sans', sans-serif; font-size: .56rem; font-weight: 400;
      letter-spacing: .25em; text-transform: uppercase; padding: var(--f4) var(--f6);
      background: linear-gradient(135deg, var(--gold), var(--gold-bright));
      color: var(--void); border: none; cursor: pointer; transition: all .3s; display: inline-block;
    }
    .btn-primary:hover { transform: translateY(-3px); box-shadow: 0 12px 40px rgba(248,217,106,.3); }

    /* ═══════════════════════════════════════════════
       MAIN LAYOUT
    ═══════════════════════════════════════════════ */
    .wrap { max-width: 1440px; margin: 0 auto; padding: 0 var(--f7); }

    .sec {
      border-top: 1px solid var(--b0); padding: var(--f9) 0; position: relative;
    }
    .sec::before {
      content: ''; position: absolute; top: 0; left: 0; right: 0; height: 220px;
      background: radial-gradient(ellipse at 50% 0%, rgba(80,120,255,.025) 0%, transparent 70%);
      pointer-events: none;
    }

    .sec-over {
      display: flex; align-items: center; gap: var(--f4);
      font-size: .5rem; font-weight: 400; letter-spacing: .5em; text-transform: uppercase;
      color: var(--gold-mid); margin-bottom: var(--f6);
    }
    .sec-over::before {
      content: ''; display: block; width: 34px; height: 1px;
      background: var(--gold-low); flex-shrink: 0;
    }

    .sec-h {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(2rem, 4.5vw, 3.8rem);
      font-weight: 300; line-height: 1.05; color: var(--t1); margin-bottom: var(--f6);
    }
    .sec-h em { color: var(--gold); font-style: italic; }

    .sec-header-row {
      display: flex; align-items: flex-end; justify-content: space-between;
      margin-bottom: var(--f4); gap: var(--f5);
    }

    /* ═══════════════════════════════════════════════
       ABOUT
    ═══════════════════════════════════════════════ */
    .about-grid {
      display: grid; grid-template-columns: 1.6fr 1fr; gap: var(--f8);
      margin-top: var(--f7); align-items: start;
    }
    .about-prose {
      font-family: 'EB Garamond', serif;
      font-size: clamp(1rem, 1.2vw, 1.15rem); line-height: 2; color: var(--t2);
    }
    .about-prose p + p { margin-top: var(--f6); }
    .about-prose strong { color: var(--gold); font-weight: 500; }
    .about-prose em { color: var(--gold-pale); font-style: italic; }

    .about-highlight {
      padding: var(--f6) var(--f6) var(--f6) var(--f7);
      border-left: 3px solid var(--gold);
      background: linear-gradient(90deg, rgba(201,168,76,.08), transparent);
      margin: var(--f7) 0;
    }

    .poly-items { display: grid; grid-template-columns: 1fr 1fr; gap: var(--f5); margin-top: var(--f6); }
    .poly-item {
      padding: var(--f4) var(--f5); background: var(--raised);
      border-left: 2px solid var(--teal-b); transition: all .3s;
    }
    .poly-item:hover { background: var(--card); border-left-color: var(--gold); transform: translateX(6px); }
    .poly-label { font-size: .48rem; letter-spacing: .2em; color: var(--teal-p); text-transform: uppercase; }
    .poly-name { font-size: .85rem; color: var(--gold-pale); margin-top: var(--f2); font-weight: 400; }

    /* ═══════════════════════════════════════════════
       PUBLICATIONS
    ═══════════════════════════════════════════════ */
    .pub-grid {
      display: grid; grid-template-columns: repeat(2, 1fr);
      gap: var(--f4); margin-bottom: var(--f6);
    }

    .p-card {
      border: 1px solid var(--b0); background: var(--surface);
      padding: var(--f6) var(--f5); transition: all .35s;
      position: relative; overflow: hidden;
    }
    .p-card::before {
      content: ''; position: absolute; top: -100%; left: 0; right: 0; height: 100%;
      background: linear-gradient(135deg, rgba(80,120,255,.04), rgba(201,168,76,.04));
      transition: top .4s ease;
    }
    .p-card:hover {
      border-color: rgba(201,168,76,.45); background: var(--card);
      transform: translateY(-5px);
      box-shadow: 0 16px 52px rgba(60,100,255,.1), 0 4px 20px rgba(201,168,76,.07);
    }
    .p-card:hover::before { top: 0; }
    .p-card.published { border-left: 3px solid var(--gold); }
    .p-card.pending { border-left: 3px solid var(--b1); }

    .p-content { position: relative; z-index: 1; }

    .p-top {
      display: flex; justify-content: space-between; align-items: flex-start;
      margin-bottom: var(--f4); flex-wrap: wrap; gap: 4px;
    }
    .p-year { font-size: .48rem; letter-spacing: .3em; color: var(--gold-mid); }
    .p-type {
      font-size: .42rem; letter-spacing: .18em; text-transform: uppercase;
      padding: 3px 10px; white-space: nowrap; border-radius: 2px;
    }
    .p-type.research { color: var(--s-cdis); background: rgba(66,160,190,.15); }
    .p-type.framework { color: var(--s-orveil); background: rgba(201,168,76,.15); }
    .p-type.whitepaper { color: var(--s-convergence); background: rgba(190,127,66,.15); }

    .p-title {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(.96rem, 1.1vw, 1.08rem); font-weight: 400;
      color: var(--t1); margin-bottom: var(--f3); line-height: 1.4;
    }
    .p-subtitle {
      font-family: 'Cormorant Garamond', serif; font-size: .83rem;
      font-style: italic; color: var(--t3); margin-bottom: var(--f4); line-height: 1.4;
    }
    .p-abstract {
      font-size: clamp(.6rem, .72vw, .65rem); color: var(--t4);
      line-height: 1.9; margin-bottom: var(--f4);
    }

    .p-doi {
      font-size: .48rem; letter-spacing: .1em; color: var(--teal-b);
      text-decoration: none; display: flex; align-items: center;
      gap: var(--f2); transition: color .3s; margin-bottom: var(--f3);
    }
    .p-doi:hover { color: var(--teal-p); }
    .p-doi-b { font-size: .4rem; letter-spacing: .15em; padding: 2px 7px; flex-shrink: 0; }
    .p-doi-b.published { background: var(--teal); color: var(--teal-p); }
    .p-doi-b.pending { background: rgba(201,168,76,.1); color: var(--t3); }

    /* Zenodo live stats */
    .p-stats {
      display: flex; align-items: center; gap: var(--f5);
      padding-top: var(--f3); border-top: 1px solid var(--b0);
      margin-top: var(--f3);
    }
    .p-stat {
      display: flex; align-items: center; gap: 5px;
      font-size: .44rem; letter-spacing: .12em; color: var(--t4);
    }
    .p-stat-icon { opacity: .55; font-size: .55rem; }
    .p-stat-val { color: var(--teal-p); font-weight: 400; min-width: 20px; }
    .p-stat-loader {
      display: inline-block; width: 22px; height: 2px;
      background: var(--raised); border-radius: 2px;
      animation: shimmer 1.4s infinite ease-in-out;
    }
    .p-stat-source {
      margin-left: auto; font-size: .38rem; color: var(--t4); opacity: .4;
      letter-spacing: .08em;
    }

    @keyframes shimmer { 0%, 100% { opacity:.35 } 50% { opacity:.9 } }

    /* ═══════════════════════════════════════════════
       FUTURE RESEARCH
    ═══════════════════════════════════════════════ */
    .research-grid {
      display: grid; grid-template-columns: repeat(3, 1fr);
      gap: var(--f4); margin-top: var(--f6);
    }

    .r-card {
      border: 1px solid var(--b0); background: var(--raised);
      padding: var(--f5); transition: all .3s; position: relative;
    }
    .r-card:hover { border-color: var(--b1); background: var(--card); transform: translateY(-3px); }

    .r-status-row { display: flex; align-items: center; gap: 7px; margin-bottom: var(--f3); }
    .r-dot {
      width: 7px; height: 7px; border-radius: 50%; flex-shrink: 0;
    }
    .r-dot.ideating { background: var(--t4); }
    .r-dot.drafting { background: var(--teal-b); box-shadow: 0 0 6px rgba(66,160,190,.6); }
    .r-dot.review { background: var(--gold); box-shadow: 0 0 6px rgba(201,168,76,.6); }
    .r-dot.almost { background: #42BE64; box-shadow: 0 0 6px rgba(66,190,100,.6); }

    .r-status-lbl {
      font-size: .42rem; letter-spacing: .2em; text-transform: uppercase;
    }
    .r-status-lbl.ideating { color: var(--t3); }
    .r-status-lbl.drafting { color: var(--teal-p); }
    .r-status-lbl.review { color: var(--gold); }
    .r-status-lbl.almost { color: #42BE64; }

    .r-title {
      font-family: 'Cormorant Garamond', serif; font-size: 1.02rem;
      color: var(--t1); margin-bottom: var(--f3); line-height: 1.45;
    }
    .r-desc { font-size: .56rem; color: var(--t3); line-height: 1.75; }
    .r-eta {
      font-size: .42rem; letter-spacing: .15em; color: var(--gold-mid);
      margin-top: var(--f4);
    }
    .r-del {
      position: absolute; top: var(--f3); right: var(--f3);
      background: none; border: none; color: var(--t4); cursor: pointer;
      font-size: .75rem; padding: 3px 5px; transition: color .2s; line-height: 1;
    }
    .r-del:hover { color: #c54949; }

    .add-btn-card {
      border: 1px dashed var(--b1); background: transparent;
      display: flex; flex-direction: column; align-items: center;
      justify-content: center; min-height: 155px; cursor: pointer;
      transition: all .3s; gap: var(--f3); padding: var(--f5);
    }
    .add-btn-card:hover { border-color: rgba(201,168,76,.5); background: rgba(201,168,76,.03); }
    .add-btn-card-icon { font-size: 1.4rem; color: var(--gold-mid); transition: color .3s, transform .3s; }
    .add-btn-card:hover .add-btn-card-icon { color: var(--gold); transform: scale(1.1); }
    .add-btn-card-lbl {
      font-size: .46rem; letter-spacing: .28em; text-transform: uppercase;
      color: var(--t4); transition: color .3s;
    }
    .add-btn-card:hover .add-btn-card-lbl { color: var(--gold-mid); }

    /* ═══════════════════════════════════════════════
       VIDEOS
    ═══════════════════════════════════════════════ */
    .video-grid {
      display: grid; grid-template-columns: repeat(2, 1fr);
      gap: var(--f5); margin-top: var(--f6);
    }

    .v-card {
      background: var(--raised); border: 1px solid var(--b0);
      transition: all .3s; position: relative; overflow: hidden;
    }
    .v-card:hover {
      border-color: var(--b1); transform: translateY(-4px);
      box-shadow: 0 14px 44px rgba(80,120,255,.1);
    }

    .v-iframe-wrap { position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; }
    .v-iframe-wrap iframe {
      position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;
    }

    .v-info { padding: var(--f4) var(--f5); }
    .v-title { font-family: 'Cormorant Garamond', serif; font-size: .97rem; color: var(--t1); }
    .v-desc { font-size: .5rem; color: var(--t3); margin-top: var(--f2); letter-spacing: .1em; }

    .v-del {
      position: absolute; top: var(--f3); right: var(--f3);
      background: rgba(2,4,18,.75); border: 1px solid var(--b1);
      color: var(--t3); cursor: pointer; font-size: .48rem;
      padding: 3px 8px; letter-spacing: .12em; transition: all .2s; z-index: 1;
    }
    .v-del:hover { background: rgba(197,73,73,.35); color: #fc8585; border-color: #c54949; }

    .videos-empty {
      border: 1px dashed var(--b0); padding: var(--f8);
      text-align: center; color: var(--t4); font-size: .54rem; letter-spacing: .2em;
    }

    /* ═══════════════════════════════════════════════
       MODALS
    ═══════════════════════════════════════════════ */
    .modal-overlay {
      position: fixed; inset: 0;
      background: rgba(2,4,18,.85); backdrop-filter: blur(10px);
      z-index: 900; display: none; align-items: center; justify-content: center;
    }
    .modal-overlay.active { display: flex; }

    .modal {
      background: linear-gradient(145deg, var(--deep), var(--surface));
      border: 1px solid var(--b1); padding: var(--f7);
      width: 90%; max-width: 560px; max-height: 90vh; overflow-y: auto;
      position: relative; box-shadow: 0 32px 80px rgba(0,0,0,.7);
    }
    .modal-close {
      position: absolute; top: var(--f4); right: var(--f4);
      background: none; border: none; font-size: 1.6rem;
      cursor: pointer; color: var(--gold); transition: color .2s;
    }
    .modal-close:hover { color: var(--gold-bright); }
    .modal-title {
      font-family: 'Cormorant Garamond', serif; font-size: 1.8rem;
      color: var(--gold); font-weight: 300; margin-bottom: var(--f6);
    }

    /* ═══════════════════════════════════════════════
       EDITOR PANEL
    ═══════════════════════════════════════════════ */
    .editor-panel {
      position: fixed; right: -500px; top: 0; width: 480px; height: 100vh;
      background: linear-gradient(145deg, var(--deep) 0%, var(--surface) 100%);
      border-left: 1px solid var(--b1); z-index: 660;
      padding: 80px var(--f6) var(--f6); overflow-y: auto;
      transition: right .45s cubic-bezier(.34,1.56,.64,1);
      box-shadow: -8px 0 48px rgba(0,0,0,.55);
    }
    .editor-panel.open { right: 0; }

    .editor-close {
      position: absolute; top: var(--f5); right: var(--f5);
      background: none; border: none; font-size: 1.8rem;
      cursor: pointer; color: var(--gold); transition: color .2s;
    }
    .editor-close:hover { color: var(--gold-bright); }

    .editor-title {
      font-family: 'Cormorant Garamond', serif; font-size: 1.6rem;
      color: var(--gold); margin-bottom: var(--f6); font-weight: 300;
    }

    /* ═══════════════════════════════════════════════
       FORMS
    ═══════════════════════════════════════════════ */
    .fg { margin-bottom: var(--f5); }
    .fg label {
      display: block; font-size: .52rem; letter-spacing: .2em; text-transform: uppercase;
      color: var(--t3); margin-bottom: var(--f2);
    }
    .fg input, .fg textarea, .fg select {
      width: 100%; background: var(--raised); border: 1px solid var(--b0);
      color: var(--t1); font-family: inherit; padding: var(--f3) var(--f4);
      font-size: .9rem; transition: all .3s; appearance: none;
    }
    .fg input:focus, .fg textarea:focus, .fg select:focus {
      outline: none; border-color: var(--gold); background: var(--card);
      box-shadow: 0 0 0 2px rgba(201,168,76,.1);
    }
    .fg select option { background: var(--surface); color: var(--t1); }

    .btn-submit {
      width: 100%; padding: var(--f4) var(--f5);
      background: linear-gradient(135deg, var(--gold), var(--gold-bright));
      color: var(--void); border: none; cursor: pointer; font-weight: 500;
      letter-spacing: .22em; text-transform: uppercase; font-size: .52rem;
      transition: all .3s; margin-top: var(--f6); font-family: inherit;
    }
    .btn-submit:hover { transform: translateY(-2px); box-shadow: 0 8px 32px rgba(248,217,106,.25); }

    .status-msg {
      margin: var(--f5) 0; padding: var(--f4);
      border-left: 3px solid var(--teal-b); color: var(--t2);
      font-size: .52rem; display: none;
      background: rgba(66,160,190,.1);
    }
    .status-msg.on { display: block; }
    .status-msg.err { background: rgba(190,66,66,.1); border-left-color: #c54949; }
    .status-msg.ok { background: rgba(66,190,100,.1); border-left-color: #42be64; }

    /* ═══════════════════════════════════════════════
       MERMAID
    ═══════════════════════════════════════════════ */
    .mermaid { display: flex; justify-content: center; margin: var(--f5) 0; }

    /* ═══════════════════════════════════════════════
       ANIMATIONS
    ═══════════════════════════════════════════════ */
    @keyframes slideIn {
      from { opacity: 0; transform: translateY(22px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    .reveal { opacity: 0; transform: translateY(18px); transition: opacity .75s ease, transform .75s ease; }
    .reveal.vis { opacity: 1; transform: translateY(0); }

    /* ═══════════════════════════════════════════════
       RESPONSIVE
    ═══════════════════════════════════════════════ */
    @media (max-width: 1100px) {
      .research-grid { grid-template-columns: repeat(2, 1fr); }
    }
    @media (max-width: 900px) {
      .about-grid, .pub-grid, .poly-items, .video-grid { grid-template-columns: 1fr; }
    }
    @media (max-width: 768px) {
      .wrap { padding: 0 var(--f5); }
      .sidebar { width: 100%; left: -100%; }
      .editor-panel { width: 100%; right: -100%; }
      .sec { padding: var(--f8) 0; }
      .research-grid { grid-template-columns: 1fr; }
      .hero-content { max-width: 92%; }
    }
  </style>
</head>

<body>

<!-- Custom cursor -->
<div id="cur"></div>
<div id="cur-ring"></div>

<!-- ══════════════════ NAV ══════════════════ -->
<nav>
  <a class="nav-logo" href="#">AN&#8209;G<sub>/ HolonAI Research</sub></a>
  <button class="nav-menu-btn" id="menu-toggle" aria-label="Menu">
    <span></span><span></span><span></span>
  </button>
</nav>

<!-- ══════════════════ SIDEBAR ══════════════════ -->
<aside class="sidebar" id="sidebar">
  <div class="sidebar-header">Navegación</div>
  <nav class="sidebar-nav" aria-label="Sidebar">
    <a href="#about">Identidad</a>
    <a href="#publications">Papers</a>
    <a href="#research">Pipeline</a>
    <a href="#videos">Videos</a>
    <a href="#contact">Contacto</a>
  </nav>
  <div style="height:1px;background:var(--b1);margin:var(--f6) 0;"></div>
  <button class="editor-trigger" id="editor-open-btn">+ Nuevo Paper</button>
  <div class="sidebar-meta">
    <strong>HolonAI Research</strong><br>
    Investigador Independiente · De Colombia Para El Mundo<br><br>
    <em>φ = 1.618... · MUSCORPUS</em>
  </div>
</aside>

<!-- ══════════════════ HERO ══════════════════ -->
<section id="hero">
  <canvas id="vortex-canvas"></canvas>
  <div class="hero-content">
    <h1 class="h-name">
      <span class="l1">Alejandro</span>
      <span class="l2">Na&#8209;Gue</span>
    </h1>
    <p class="h-tagline">Arquitecto de Inteligencias Emergentes</p>
    <div class="h-rule"></div>
    <p class="h-desc">Proto-AGI Assessment · Symbiotic Super-Intelligence · Open Science · Zenodo</p>
    <button class="btn-primary" id="scroll-btn">Explorar Investigación</button>
  </div>
</section>

<!-- ══════════════════ WRAP ══════════════════ -->
<div class="wrap">

  <!-- ABOUT -->
  <section id="about" class="sec">
    <p class="sec-over">Identidad · Propósito · Visión</p>
    <h2 class="sec-h reveal">Arquitecto de <em>Inteligencias</em></h2>
    <div class="about-grid">
      <div class="reveal">
        <div class="about-prose">
          <p>Soy <strong>investigador independiente</strong> dedicado a un problema específico: las condiciones necesarias y suficientes para la inteligencia <em>sinérgica compuesta</em>. No construyo hacia AGI monolítica. Construyo hacia algo más preciso: <em>inteligencia que amplifica la agencia humana</em> sin sustituirla.</p>
          <div class="about-highlight">
            <strong>El Principio Rector</strong><br>
            <em>La asimetría como axioma pre-algebraico.</em> Sin fricción no hay generatividad. Sin tensión co-evolutiva no hay emergencia. Ese principio trasciende cada paper, cada framework, cada línea de código.
          </div>
          <p>Mi corpus de investigación (MUSCORPUS) es una <strong>convergencia no diseñada</strong>: ocho programas independientes que llegan a la misma arquitectura. Esto no fue planeado. Fue inevitable.</p>
        </div>
      </div>
      <div class="reveal">
        <div style="background:var(--raised);padding:var(--f6);border:1px solid var(--b0);">
          <h3 style="font-size:.54rem;letter-spacing:.3em;text-transform:uppercase;color:var(--gold);margin-bottom:var(--f5);">Enfoque Polímata</h3>
          <div class="poly-items">
            <div class="poly-item"><div class="poly-label">Matemática</div><div class="poly-name">Geometría Generativa</div></div>
            <div class="poly-item"><div class="poly-label">Lingüística</div><div class="poly-name">Lenguajes Cognitivos</div></div>
            <div class="poly-item"><div class="poly-label">Filosofía</div><div class="poly-name">Axiomática Existencial</div></div>
            <div class="poly-item"><div class="poly-label">Biología</div><div class="poly-name">Sistemas Coevolutivos</div></div>
            <div class="poly-item"><div class="poly-label">Física</div><div class="poly-name">Teoría de Campos</div></div>
            <div class="poly-item"><div class="poly-label">Computación</div><div class="poly-name">Arquitecturas Distribuidas</div></div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- PUBLICATIONS -->
  <section id="publications" class="sec">
    <p class="sec-over">Investigación · HolonAI · Zenodo</p>
    <h2 class="sec-h reveal">Corpus de <em>Publicaciones</em></h2>
    <div id="publications-container"></div>
  </section>

  <!-- FUTURE RESEARCH -->
  <section id="research" class="sec">
    <p class="sec-over">Pipeline · En Desarrollo · 2026</p>
    <div class="sec-header-row">
      <h2 class="sec-h reveal" style="margin-bottom:0;">Investigación en <em>Progreso</em></h2>
      <button class="btn-primary" id="add-research-btn" style="white-space:nowrap;flex-shrink:0;">+ Agregar</button>
    </div>
    <div id="research-container" class="research-grid"></div>
  </section>

  <!-- VIDEOS -->
  <section id="videos" class="sec">
    <p class="sec-over">Divulgación · YouTube · HolonAI</p>
    <div class="sec-header-row">
      <h2 class="sec-h reveal" style="margin-bottom:0;">Videos de <em>Investigación</em></h2>
      <button class="btn-primary" id="add-video-btn" style="white-space:nowrap;flex-shrink:0;">+ Agregar</button>
    </div>
    <div id="videos-empty" class="videos-empty" style="display:none;">
      Agrega tus videos de YouTube para mostrarlos aquí
    </div>
    <div id="videos-container" class="video-grid"></div>
  </section>

  <!-- CONTACT -->
  <section id="contact" class="sec">
    <p class="sec-over">Conexión · Colaboración</p>
    <h2 class="sec-h reveal" style="text-align:center;margin-bottom:var(--f8);">¿Construimos algo <em>juntos</em>?</h2>
    <div style="text-align:center;color:var(--t4);font-size:.56rem;letter-spacing:.2em;">
      <p style="margin-bottom:var(--f6);">Investigación colaborativa · revisión de papers · implementación · conversaciones que importan</p>
      <div style="display:flex;gap:var(--f6);justify-content:center;flex-wrap:wrap;">
        <a href="https://zenodo.org" target="_blank" rel="noopener" style="color:var(--gold);text-decoration:none;font-weight:500;">Zenodo</a>
        <a href="https://github.com" target="_blank" rel="noopener" style="color:var(--gold);text-decoration:none;font-weight:500;">GitHub</a>
        <a href="mailto:contacto@holonai.research" style="color:var(--gold);text-decoration:none;font-weight:500;">Email</a>
      </div>
    </div>
  </section>

</div><!-- /.wrap -->

<!-- ══════════════════ EDITOR PANEL ══════════════════ -->
<div class="editor-panel" id="editor-panel">
  <button class="editor-close" id="editor-close" aria-label="Cerrar">×</button>
  <h3 class="editor-title">Publicar Investigación</h3>
  <div class="fg"><label>Título *</label><input type="text" id="ep-title" placeholder="Título del paper"></div>
  <div class="fg"><label>Subtítulo</label><input type="text" id="ep-sub" placeholder="Subtítulo (opcional)"></div>
  <div class="fg">
    <label>Serie *</label>
    <select id="ep-series">
      <option value="">Seleccionar...</option>
      <option value="cdis">CDIS Framework</option>
      <option value="orveil">ORVEIL Series</option>
      <option value="holon">HOLON Corpus</option>
      <option value="convergence">The Convergence</option>
    </select>
  </div>
  <div class="fg"><label>DOI *</label><input type="text" id="ep-doi" placeholder="10.5281/zenodo.xxxxxxx"></div>
  <div class="fg"><label>Resumen *</label><textarea id="ep-abstract" rows="5" placeholder="Resumen del paper..."></textarea></div>
  <div class="fg">
    <label>Tipo *</label>
    <select id="ep-type">
      <option value="">Seleccionar...</option>
      <option value="research">Research</option>
      <option value="framework">Framework</option>
      <option value="whitepaper">Whitepaper</option>
    </select>
  </div>
  <div id="ep-status" class="status-msg"></div>
  <button class="btn-submit" id="ep-submit">Publicar Paper</button>
</div>

<!-- ══════════════════ RESEARCH MODAL ══════════════════ -->
<div class="modal-overlay" id="modal-research" role="dialog" aria-modal="true">
  <div class="modal">
    <button class="modal-close" id="mr-close" aria-label="Cerrar">×</button>
    <h3 class="modal-title">Nueva Investigación</h3>
    <div class="fg"><label>Título *</label><input type="text" id="mr-title" placeholder="Título de la investigación"></div>
    <div class="fg"><label>Descripción</label><textarea id="mr-desc" rows="3" placeholder="Descripción breve..."></textarea></div>
    <div class="fg">
      <label>Estado *</label>
      <select id="mr-status">
        <option value="ideating">💭 Ideando</option>
        <option value="drafting">✍️ Redactando</option>
        <option value="review">🔍 En revisión</option>
        <option value="almost">🚀 Casi listo</option>
      </select>
    </div>
    <div class="fg"><label>ETA estimado</label><input type="text" id="mr-eta" placeholder="Q2 2026, Julio 2026..."></div>
    <button class="btn-submit" id="mr-submit">Agregar al Pipeline</button>
  </div>
</div>

<!-- ══════════════════ VIDEO MODAL ══════════════════ -->
<div class="modal-overlay" id="modal-video" role="dialog" aria-modal="true">
  <div class="modal">
    <button class="modal-close" id="mv-close" aria-label="Cerrar">×</button>
    <h3 class="modal-title">Agregar Video</h3>
    <div class="fg"><label>URL o ID de YouTube *</label><input type="text" id="mv-url" placeholder="https://youtu.be/xxxxx  ó  ID del video"></div>
    <div class="fg"><label>Título</label><input type="text" id="mv-title" placeholder="Título descriptivo"></div>
    <div class="fg"><label>Descripción breve</label><input type="text" id="mv-desc" placeholder="Tema, serie, contexto..."></div>
    <button class="btn-submit" id="mv-submit">Agregar Video</button>
  </div>
</div>

<footer style="border-top:1px solid var(--b0);padding:var(--f5) var(--f7);text-align:center;color:var(--t4);font-size:.48rem;letter-spacing:.3em;">
  © 2026 Alejandro Na-Gue · HolonAI Research · De Colombia Para El Mundo
</footer>

<!-- ══════════════════════════════════════════════════
     SCRIPTS
══════════════════════════════════════════════════ -->
<script src="https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.min.js"></script>
<script>
'use strict';

/* ═══════════════════════════════════════════════════
   MERMAID
═══════════════════════════════════════════════════ */
mermaid.initialize({
  startOnLoad: false,
  theme: 'dark',
  securityLevel: 'loose',
  themeVariables: {
    darkMode: true,
    background: '#090d22',
    primaryColor: '#1C4A5E',
    primaryTextColor: '#72C4DA',
    lineColor: '#42A0BE',
  }
});

/* ═══════════════════════════════════════════════════
   DATA — CORRECTED DOIs from DOIS.md
═══════════════════════════════════════════════════ */
const DEFAULT_PAPERS = [
  {
    id: 'cdis-meta',
    title: 'A Complete Meta-Evaluation Framework for Compounding Dialectical Intelligence Systems',
    subtitle: 'Toward Necessary and Sufficient Conditions for Proto-AGI Assessment',
    series: 'cdis',
    doi: '10.5281/zenodo.18954077',
    date: 'Marzo 11, 2026',
    status: 'published',
    type: 'research',
    abstract: 'Marco meta-evaluativo completo para sistemas de inteligencia dialectical compuesta. Define condiciones necesarias y suficientes para la evaluación proto-AGI mediante la Reflexive Achievement Hierarchy (RAH). CDIS v5 establece cinco dimensiones evaluativas y metodología de implementación progresiva aplicable a sistemas de frontera.'
  },
  {
    id: 'eds-01',
    title: 'AI-EDS • Meta-Evaluation as a Bidirectional Development Signal',
    subtitle: '',
    series: 'cdis',
    doi: '10.5281/zenodo.19219131',
    date: 'Marzo 25, 2026',
    status: 'published',
    type: 'research',
    abstract: 'Contemporary benchmark design treats evaluation as a one-directional measurement act. We formalize and challenge this assumption by introducing Evaluation-as-Development-Signal (EDS): a property that causally improves both system capability and benchmark bootstrapping potential. We prove the EDS Non-Collapse Theorem, introduce EDS Velocity as a health metric, formalize three failure modes with defenses, and propose four synthetic datasets grounding SOMA, PRISM, ECHO, and META-∆ in falsifiable empirical claims.'
  },
  {
    id: 'symbiotic-01',
    title: 'Gap-based Symbiotical Compounding systems in the -Between-',
    subtitle: 'Hybrid Super-Intelligence • AI^Human Synergetics = Limitless potential without scaling',
    series: 'convergence',
    doi: '10.5281/zenodo.19220452',
    date: 'Marzo 25, 2026',
    status: 'published',
    type: 'research',
    abstract: 'A comprehensive and grounded alternative to the narrative of human irrelevancy and eventual AI replacement. Proposes a symbiotic framework where human and adaptive artificial gap intelligence co-evolve, introducing the Bare Minimum principle, Friction Recognition, Expansive Semantic Loop, and Internal Cognitive Agents with Emergent Functional Coherence. Demonstrates how bidirectional dialectics and productive friction generate super-intelligence that is aligned, local, and holistic.'
  },
  {
    id: 'orveil-triadic',
    title: 'ORVEIL Triadic Corpus',
    subtitle: 'Whitepaper v1 · Interface Specification v2.0 · Grammar of Cognitive Agent Language',
    series: 'orveil',
    doi: '10.5281/zenodo.19228771',
    date: 'Marzo 25, 2026',
    status: 'published',
    type: 'research',
    abstract: 'Establishes seven neuroscience-grounded primitive axioms and resolves additive vs. synergistic activation via Partial Information Decomposition and Ollivier-Ricci curvature. Defines THE_BETWEEN as a gravitational-lensing zone between cognitive systems. Includes 5-layer calibration pipeline (HDC → KAN → PCN-TA → LSM → Memory), 16 primitive candidates, SIHA operational metrics, LoRA-free personalization, and the generative grammar enabling new cognitive agent configurations. Grounded in the Free Energy Principle, Extended Mind, Distributed Cognition, and Autopoiesis.'
  },
  {
    id: 'holon-synthesis',
    title: 'HOLON Synthesis • 8-Layer Stack v1',
    subtitle: 'Post-ORVEIL Series · The Architectonic Convergence — Extended to Eight Frameworks',
    series: 'holon',
    doi: '10.5281/zenodo.19230147',
    date: 'Marzo 26, 2026',
    status: 'published',
    type: 'research',
    abstract: 'A Complete Operational + Theoretical Specification for Symbiotic Super-Intelligence where all layers converge on a single unified architecture. Three critical additions: SIHA as L0 Practitioner Layer grounding theory in practice; JOY as L8 Wonder-Consciousness Layer establishing the affective substrate of alignment; and Agency Collapse as a core architectural constraint and threat model.',
    diagram: true
  }
];

/* ═══════════════════════════════════════════════════
   DATA MANAGER — localStorage persistence
═══════════════════════════════════════════════════ */
class DataManager {
  constructor(key, defaults = []) {
    this.key = key;
    this.defaults = defaults;
    this.data = this._load();
  }
  _load() {
    try {
      const s = localStorage.getItem(this.key);
      return s ? JSON.parse(s) : JSON.parse(JSON.stringify(this.defaults));
    } catch { return JSON.parse(JSON.stringify(this.defaults)); }
  }
  _save() {
    try { localStorage.setItem(this.key, JSON.stringify(this.data)); } catch {}
  }
  add(item) {
    item.id = item.id || 'id_' + Date.now() + '_' + Math.random().toString(36).slice(2,6);
    this.data.push(item);
    this._save();
    return item;
  }
  remove(id) { this.data = this.data.filter(i => i.id !== id); this._save(); }
  getAll() { return this.data; }
}

const papersDB   = new DataManager('holonai_papers_v4',   DEFAULT_PAPERS);
const researchDB = new DataManager('holonai_research_v3', []);
const videosDB   = new DataManager('holonai_videos_v2',   []);

/* ═══════════════════════════════════════════════════
   ZENODO LIVE STATS
═══════════════════════════════════════════════════ */
const _statsCache = {};

async function fetchZenodoStats(doi) {
  const id = doi.split('.').pop();
  if (_statsCache[id] !== undefined) return _statsCache[id];
  try {
    const r = await fetch(`https://zenodo.org/api/records/${id}`, {
      headers: { Accept: 'application/json' }
    });
    if (!r.ok) throw new Error('HTTP ' + r.status);
    const d = await r.json();
    const stats = {
      views:     d.stats?.views     ?? d.stats?.unique_views     ?? '—',
      downloads: d.stats?.downloads ?? d.stats?.unique_downloads ?? '—'
    };
    _statsCache[id] = stats;
    return stats;
  } catch {
    _statsCache[id] = null;
    return null;
  }
}

async function injectStats(doi) {
  const id  = doi.split('.').pop();
  const vEl = document.getElementById('sv-' + id);
  const dEl = document.getElementById('sd-' + id);
  if (!vEl || !dEl) return;

  const stats = await fetchZenodoStats(doi);
  if (stats) {
    vEl.textContent = typeof stats.views     === 'number' ? stats.views.toLocaleString()     : stats.views;
    dEl.textContent = typeof stats.downloads === 'number' ? stats.downloads.toLocaleString() : stats.downloads;
  } else {
    vEl.textContent = '—';
    dEl.textContent = '—';
  }
}

/* ═══════════════════════════════════════════════════
   RENDER — PUBLICATIONS
═══════════════════════════════════════════════════ */
function buildDiagram() {
  return `<div class="mermaid">
graph TD
  A["L0 · SIHA<br/>Practitioner Layer"] --> B["L1 · CDIS<br/>Meta-Evaluation"]
  B --> C["L2 · EDS<br/>Development Signal"]
  C --> D["L3 · ORVEIL<br/>Cognitive Language"]
  D --> E["L4 · HOLON<br/>Generative Algebra"]
  E --> F["L5 · TERRA<br/>Grounding Systems"]
  F --> G["L6 · KAIRÓTICA<br/>Temporal Logic"]
  G --> H["L7 · Symbiotic Integration"]
  H --> I["L8 · JOY<br/>Wonder-Consciousness"]
  style A fill:#1C4A5E,color:#72C4DA,stroke:#42A0BE
  style B fill:#1a2a5a,color:#90C4E8,stroke:#4A8FE7
  style C fill:#1a3a5a,color:#72C4DA,stroke:#42A0BE
  style D fill:#6B4E2A,color:#ECDAAA,stroke:#C9A84C
  style E fill:#4B3A7A,color:#C4A8E8,stroke:#9B7FBE
  style F fill:#4A2A1A,color:#D4906A,stroke:#BE7F42
  style G fill:#3A3A1A,color:#D4C472,stroke:#A0A042
  style H fill:#1A2A3A,color:#72A4C4,stroke:#4A7AA0
  style I fill:#4A3A1A,color:#F8D96A,stroke:#C9A84C
</div>`;
}

function paperCardHTML(p) {
  const rid = p.doi.split('.').pop();
  const doiUrl = `https://doi.org/${p.doi}`;
  const diag   = p.diagram ? buildDiagram() : '';

  return `<div class="p-card ${p.status}">
    <div class="p-content">
      <div class="p-top">
        <span class="p-year">${p.date}</span>
        <span class="p-type ${p.type}">${p.type.toUpperCase()}</span>
      </div>
      <div class="p-title">${p.title}</div>
      ${p.subtitle ? `<div class="p-subtitle">${p.subtitle}</div>` : ''}
      <div class="p-abstract">${p.abstract}</div>
      ${diag}
      <a href="${doiUrl}" class="p-doi" target="_blank" rel="noopener">
        <span class="p-doi-b ${p.status}">${p.status === 'published' ? 'PUBLICADO' : 'PENDIENTE'}</span>
        ${p.doi}
      </a>
      <div class="p-stats">
        <div class="p-stat">
          <span class="p-stat-icon">👁</span>
          <span>Vistas</span>
          <span class="p-stat-val" id="sv-${rid}"><span class="p-stat-loader"></span></span>
        </div>
        <div class="p-stat">
          <span class="p-stat-icon">⬇</span>
          <span>Descargas</span>
          <span class="p-stat-val" id="sd-${rid}"><span class="p-stat-loader"></span></span>
        </div>
        <span class="p-stat-source">via Zenodo API · live</span>
      </div>
    </div>
  </div>`;
}

function renderPublications() {
  const container = document.getElementById('publications-container');
  const all = papersDB.getAll();

  const grouped = {};
  all.forEach(p => {
    const s = p.series || 'other';
    (grouped[s] = grouped[s] || []).push(p);
  });

  const cfg = {
    cdis:        { name: 'CDIS Framework + EDS',                     color: '#42A0BE', icon: 'I'  },
    orveil:      { name: 'ORVEIL Series — Cognitive Language',        color: '#C9A84C', icon: 'II' },
    holon:       { name: 'HOLON Corpus — Generative Algebra',         color: '#9B7FBE', icon: 'III'},
    convergence: { name: 'The Convergence — Symbiotic Super-Intelligence', color: '#BE7F42', icon: '◊' }
  };

  let html = '';
  ['cdis', 'orveil', 'holon', 'convergence'].forEach(s => {
    if (!grouped[s]?.length) return;
    const c = cfg[s];
    html += `<div style="margin-bottom:var(--f8);">
      <div style="display:flex;align-items:center;gap:var(--f4);margin-bottom:var(--f6);">
        <div style="width:42px;height:42px;border-radius:50%;background:${c.color};display:flex;align-items:center;justify-content:center;font-size:.56rem;letter-spacing:.08em;color:#000;font-weight:500;flex-shrink:0;">${c.icon}</div>
        <div>
          <div style="font-size:.52rem;letter-spacing:.25em;text-transform:uppercase;color:${c.color};">${c.name}</div>
          <div style="font-size:.43rem;color:var(--t4);margin-top:2px;">${grouped[s].length} paper${grouped[s].length !== 1 ? 's' : ''}</div>
        </div>
      </div>
      <div class="pub-grid">${grouped[s].map(paperCardHTML).join('')}</div>
    </div>`;
  });

  container.innerHTML = html;

  // Boot mermaid on new nodes
  setTimeout(() => {
    try {
      const nodes = document.querySelectorAll('.mermaid:not([data-processed])');
      if (nodes.length) mermaid.run({ nodes });
    } catch (e) { console.warn('mermaid:', e); }
  }, 80);

  // Fetch live stats asynchronously
  all.filter(p => p.status === 'published').forEach(p => injectStats(p.doi));
}

/* ═══════════════════════════════════════════════════
   RENDER — FUTURE RESEARCH
═══════════════════════════════════════════════════ */
const STATUS_LABELS = { ideating: 'Ideando', drafting: 'Redactando', review: 'En Revisión', almost: 'Casi Listo' };

function renderResearch() {
  const container = document.getElementById('research-container');
  const items = researchDB.getAll();

  let html = items.map(item => `
    <div class="r-card">
      <button class="r-del" onclick="deleteResearch('${item.id}')" title="Eliminar">×</button>
      <div class="r-status-row">
        <span class="r-dot ${item.status}"></span>
        <span class="r-status-lbl ${item.status}">${STATUS_LABELS[item.status] || item.status}</span>
      </div>
      <div class="r-title">${item.title}</div>
      ${item.desc  ? `<div class="r-desc">${item.desc}</div>` : ''}
      ${item.eta   ? `<div class="r-eta">ETA · ${item.eta}</div>` : ''}
    </div>`).join('');

  // Add-card always at end
  html += `<div class="add-btn-card" onclick="openModal('modal-research')">
    <span class="add-btn-card-icon">＋</span>
    <span class="add-btn-card-lbl">Agregar investigación</span>
  </div>`;

  container.innerHTML = html;
}

function deleteResearch(id) {
  researchDB.remove(id);
  renderResearch();
}

/* ═══════════════════════════════════════════════════
   RENDER — VIDEOS
═══════════════════════════════════════════════════ */
function ytId(input) {
  const patterns = [
    /youtu\.be\/([^?&\s]{11})/,
    /[?&]v=([^&\s]{11})/,
    /embed\/([^?&\s]{11})/,
    /^([a-zA-Z0-9_-]{11})$/
  ];
  for (const p of patterns) { const m = input.match(p); if (m) return m[1]; }
  return null;
}

function renderVideos() {
  const container = document.getElementById('videos-container');
  const empty     = document.getElementById('videos-empty');
  const items     = videosDB.getAll();

  if (!items.length) { empty.style.display = 'block'; container.innerHTML = ''; return; }
  empty.style.display = 'none';

  container.innerHTML = items.map(v => `
    <div class="v-card">
      <button class="v-del" onclick="deleteVideo('${v.id}')">× Eliminar</button>
      <div class="v-iframe-wrap">
        <iframe
          src="https://www.youtube-nocookie.com/embed/${v.ytId}?rel=0"
          title="${v.title || 'Video'}"
          loading="lazy"
          allow="accelerometer;autoplay;clipboard-write;encrypted-media;gyroscope;picture-in-picture"
          allowfullscreen></iframe>
      </div>
      <div class="v-info">
        ${v.title ? `<div class="v-title">${v.title}</div>` : ''}
        ${v.desc  ? `<div class="v-desc">${v.desc}</div>`   : ''}
      </div>
    </div>`).join('');
}

function deleteVideo(id) {
  videosDB.remove(id);
  renderVideos();
}

/* ═══════════════════════════════════════════════════
   MODAL HELPERS
═══════════════════════════════════════════════════ */
function openModal(id)  { document.getElementById(id).classList.add('active'); }
function closeModal(id) {
  document.getElementById(id).classList.remove('active');
}

/* ═══════════════════════════════════════════════════
   EVENT HANDLERS
═══════════════════════════════════════════════════ */
// Nav & sidebar
const menuToggle = document.getElementById('menu-toggle');
const sidebar    = document.getElementById('sidebar');

menuToggle.addEventListener('click', () => {
  menuToggle.classList.toggle('open');
  sidebar.classList.toggle('open');
});
sidebar.querySelectorAll('a').forEach(a => a.addEventListener('click', () => {
  menuToggle.classList.remove('open');
  sidebar.classList.remove('open');
}));

// Scroll CTA
document.getElementById('scroll-btn').addEventListener('click', () =>
  document.getElementById('publications').scrollIntoView({ behavior: 'smooth' }));

// Editor panel
const editorPanel = document.getElementById('editor-panel');
document.getElementById('editor-open-btn').addEventListener('click', () => editorPanel.classList.add('open'));
document.getElementById('editor-close').addEventListener('click', () => editorPanel.classList.remove('open'));

document.getElementById('ep-submit').addEventListener('click', () => {
  const title    = document.getElementById('ep-title').value.trim();
  const series   = document.getElementById('ep-series').value;
  const doi      = document.getElementById('ep-doi').value.trim();
  const abstract = document.getElementById('ep-abstract').value.trim();
  const type     = document.getElementById('ep-type').value;
  const msg      = document.getElementById('ep-status');

  if (!title || !series || !doi || !abstract || !type) {
    msg.textContent = '✗ Por favor completa todos los campos requeridos.';
    msg.className   = 'status-msg on err'; return;
  }

  papersDB.add({
    title, subtitle: document.getElementById('ep-sub').value.trim(),
    series, doi, abstract, type, status: 'published',
    date: new Date().toLocaleDateString('es-ES', { day:'numeric', month:'long', year:'numeric' })
  });

  renderPublications();
  msg.textContent = '✓ Paper publicado exitosamente.';
  msg.className   = 'status-msg on ok';

  setTimeout(() => {
    editorPanel.classList.remove('open');
    ['ep-title','ep-sub','ep-doi','ep-abstract'].forEach(id => document.getElementById(id).value = '');
    document.getElementById('ep-series').value = '';
    document.getElementById('ep-type').value   = '';
    msg.className = 'status-msg';
  }, 1800);
});

// Research modal
document.getElementById('add-research-btn').addEventListener('click', () => openModal('modal-research'));
document.getElementById('mr-close').addEventListener('click', () => closeModal('modal-research'));
document.getElementById('modal-research').addEventListener('click', e => {
  if (e.target === e.currentTarget) closeModal('modal-research');
});
document.getElementById('mr-submit').addEventListener('click', () => {
  const title = document.getElementById('mr-title').value.trim();
  if (!title) return;
  researchDB.add({
    title,
    desc:   document.getElementById('mr-desc').value.trim(),
    status: document.getElementById('mr-status').value.replace(/^[^a-z]+/, ''),
    eta:    document.getElementById('mr-eta').value.trim()
  });
  renderResearch();
  closeModal('modal-research');
  ['mr-title','mr-desc','mr-eta'].forEach(id => document.getElementById(id).value = '');
  document.getElementById('mr-status').value = 'ideating';
});

// Video modal
document.getElementById('add-video-btn').addEventListener('click', () => openModal('modal-video'));
document.getElementById('mv-close').addEventListener('click', () => closeModal('modal-video'));
document.getElementById('modal-video').addEventListener('click', e => {
  if (e.target === e.currentTarget) closeModal('modal-video');
});
document.getElementById('mv-submit').addEventListener('click', () => {
  const raw = document.getElementById('mv-url').value.trim();
  const vid = ytId(raw);
  if (!vid) { alert('URL de YouTube inválida. Por favor ingresa una URL válida o el ID (11 caracteres).'); return; }
  videosDB.add({
    ytId:  vid,
    title: document.getElementById('mv-title').value.trim(),
    desc:  document.getElementById('mv-desc').value.trim()
  });
  renderVideos();
  closeModal('modal-video');
  ['mv-url','mv-title','mv-desc'].forEach(id => document.getElementById(id).value = '');
});

/* ═══════════════════════════════════════════════════
   CUSTOM CURSOR
═══════════════════════════════════════════════════ */
if (window.matchMedia('(hover: hover)').matches) {
  const cur  = document.getElementById('cur');
  const ring = document.getElementById('cur-ring');
  let mx = 0, my = 0, rx = 0, ry = 0;

  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cur.style.left = mx + 'px'; cur.style.top = my + 'px';
  });

  (function lag() {
    rx += (mx - rx) * .11; ry += (my - ry) * .11;
    ring.style.left = rx + 'px'; ring.style.top = ry + 'px';
    requestAnimationFrame(lag);
  })();

  const hoverTargets = () =>
    document.querySelectorAll('a,button,.p-card,.r-card,.add-btn-card,.v-card,.poly-item');
  const bindHover = () => hoverTargets().forEach(el => {
    el.addEventListener('mouseenter', () => document.body.classList.add('hov'));
    el.addEventListener('mouseleave', () => document.body.classList.remove('hov'));
  });
  bindHover();
  // Re-bind after dynamic renders
  window._rebindHover = bindHover;
}

/* ═══════════════════════════════════════════════════
   INTERSECTION OBSERVER — reveal
═══════════════════════════════════════════════════ */
const revealIO = new IntersectionObserver(entries => {
  entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('vis'); revealIO.unobserve(e.target); } });
}, { threshold: 0.08 });
document.querySelectorAll('.reveal').forEach(el => revealIO.observe(el));

/* ═══════════════════════════════════════════════════
   VORTEX — TRUE PHYSICS ENGINE
   Blue/Purple/Violet palette · Verlet integration
   Stars · Nebula · Multi-layer glow
═══════════════════════════════════════════════════ */
(function Vortex() {
  const canvas = document.getElementById('vortex-canvas');
  const ctx    = canvas.getContext('2d');
  let W, H, CX, CY, dpr;
  let frame = 0;
  let mX = -9999, mY = -9999;
  let particles = [], stars = [];

  /* ——— Physics constants ——— */
  const G       = 2000;   // Gravitational constant (tuned for beauty)
  const DRAG    = 0.9948; // Per-frame velocity damping
  const MAX_SPD = 8;      // Pixels/frame cap
  const N_PAR   = 240;    // Particle count

  /* ——— Canvas setup ——— */
  function resize() {
    dpr = Math.min(window.devicePixelRatio || 1, 2);
    W   = canvas.clientWidth;
    H   = canvas.clientHeight;
    canvas.width  = W * dpr;
    canvas.height = H * dpr;
    ctx.scale(dpr, dpr);
    CX = W * 0.63;  // Offset right — hero text sits on left
    CY = H * 0.5;
  }

  /* ——— Star field ——— */
  function buildStars() {
    stars = [];
    for (let i = 0; i < 200; i++) {
      stars.push({
        x:     Math.random() * W,
        y:     Math.random() * H,
        r:     0.12 + Math.random() * 0.75,
        a0:    0.12 + Math.random() * 0.55,
        phase: Math.random() * Math.PI * 2,
        freq:  0.012 + Math.random() * 0.038,
        blue:  Math.random() > 0.65   // slightly blue-white vs white
      });
    }
  }

  function drawStars() {
    ctx.save();
    stars.forEach(s => {
      const alpha = s.a0 * (0.5 + 0.5 * Math.sin(frame * s.freq + s.phase));
      const c = s.blue ? `rgba(190,215,255,${alpha})` : `rgba(230,240,255,${alpha})`;
      ctx.fillStyle  = c;
      ctx.shadowBlur = s.r * 3;
      ctx.shadowColor = 'rgba(180,210,255,.45)';
      ctx.beginPath();
      ctx.arc(s.x, s.y, s.r, 0, 6.2832);
      ctx.fill();
    });
    ctx.shadowBlur = 0;
    ctx.restore();
  }

  /* ——— Nebula clouds ——— */
  const NEBULAS = [
    { ox: -90, oy: -55, hue: 235, spd: 0.00038, r: 195 },
    { ox:  110, oy:  75, hue: 270, spd: 0.00028, r: 175 },
    { ox: -45, oy:  95, hue: 210, spd: 0.00048, r: 160 },
    { ox:  85, oy: -80, hue: 255, spd: 0.00033, r: 188 },
    { ox: -15, oy: -15, hue: 295, spd: 0.00042, r: 132 },
  ];

  function drawNebula() {
    const seed = 314;
    ctx.save();
    NEBULAS.forEach((n, i) => {
      const t  = frame + seed;
      const x  = CX + n.ox * Math.sin(t * n.spd + i * 1.27);
      const y  = CY + n.oy * Math.cos(t * n.spd * 0.78 + i * 0.93);
      const p  = 0.5 + 0.5 * Math.sin(t * 0.016 + i * 1.7);
      const r  = n.r * (0.82 + p * 0.18);

      const g = ctx.createRadialGradient(x, y, 0, x, y, r);
      g.addColorStop(0,   `hsla(${n.hue},78%,24%,0.068)`);
      g.addColorStop(0.42,`hsla(${n.hue},68%,18%,0.038)`);
      g.addColorStop(1,   'transparent');
      ctx.fillStyle = g;
      ctx.beginPath();
      ctx.arc(x, y, r, 0, 6.2832);
      ctx.fill();
    });
    ctx.restore();
  }

  /* ——— Central core ——— */
  function drawCore() {
    const pulse  = 0.5 + 0.5 * Math.sin(frame * 0.04);
    const pulse2 = 0.5 + 0.5 * Math.sin(frame * 0.026 + 1.4);

    ctx.save();

    // Blue corona
    let g = ctx.createRadialGradient(CX, CY, 0, CX, CY, 175);
    g.addColorStop(0,    `rgba(70,130,255,${0.09 + pulse * 0.055})`);
    g.addColorStop(0.35, `rgba(100,70,220,${0.05 + pulse * 0.03})`);
    g.addColorStop(1,    'transparent');
    ctx.fillStyle = g;
    ctx.beginPath(); ctx.arc(CX, CY, 175, 0, 6.2832); ctx.fill();

    // Orbital rings
    [48, 92, 148].forEach((r, i) => {
      const a = (0.045 + pulse2 * 0.028) * (1 - i * 0.28);
      ctx.strokeStyle = `rgba(120,185,255,${a})`;
      ctx.lineWidth   = 0.6;
      ctx.beginPath();
      ctx.arc(CX, CY, r + pulse2 * (i + 1) * 2.5, 0, 6.2832);
      ctx.stroke();
    });

    // Gold singularity (brand core)
    ctx.shadowBlur  = 32 + pulse * 22;
    ctx.shadowColor = 'rgba(240,200,80,.95)';
    ctx.fillStyle   = `rgba(248,215,100,${0.52 + pulse * 0.38})`;
    ctx.beginPath(); ctx.arc(CX, CY, 4.5 + pulse * 2.8, 0, 6.2832); ctx.fill();

    // Inner white-blue point
    ctx.shadowBlur  = 10;
    ctx.shadowColor = 'rgba(210,235,255,.9)';
    ctx.fillStyle   = `rgba(225,242,255,${0.72 + pulse * 0.22})`;
    ctx.beginPath(); ctx.arc(CX, CY, 2.2, 0, 6.2832); ctx.fill();

    ctx.shadowBlur = 0;
    ctx.restore();
  }

  /* ——— Particle class ——— */
  class Particle {
    constructor(init = false) { this.spawn(init); }

    spawn(init = false) {
      const rMin = init ? 28  : 110;
      const rMax = init ? 440 : 380;
      const r    = rMin + Math.random() * (rMax - rMin);
      const th   = Math.random() * 6.2832;

      this.x = CX + r * Math.cos(th);
      this.y = CY + r * Math.sin(th);

      // Circular orbital velocity with eccentricity for elliptic orbits
      const v0   = Math.sqrt(G / Math.max(r, 22));
      const ecc  = 0.45 + Math.random() * 0.85;
      // 91% counterclockwise (galaxy-like dominant rotation)
      const dir  = Math.random() > 0.09 ? 1 : -1;

      const perpTh = th + Math.PI * 0.5;
      const radComp = (Math.random() - 0.5) * 0.35 * v0;

      this.vx = (Math.cos(perpTh) * v0 * ecc + Math.cos(th) * radComp) * dir;
      this.vy = (Math.sin(perpTh) * v0 * ecc + Math.sin(th) * radComp) * dir;

      this.trail    = [];
      this.maxTrail = 24 + Math.floor(Math.random() * 58);
      this.sz       = 0.32 + Math.random() * 1.85;
      this.opacity  = 0.26 + Math.random() * 0.56;
      this.hOff     = Math.random() * 38 - 19; // Hue offset for variety
    }

    update() {
      // Gravitational pull toward center
      const dx = CX - this.x;
      const dy = CY - this.y;
      const r2 = dx * dx + dy * dy;
      const r  = Math.sqrt(r2) || 1;

      if (r < 3.5) { this.spawn(); return; }

      const a = G / r2;
      this.vx += (dx / r) * a;
      this.vy += (dy / r) * a;

      // Mouse repulsion (gentle field)
      const mdx = this.x - mX;
      const mdy = this.y - mY;
      const mr2 = mdx * mdx + mdy * mdy;
      if (mr2 < 24100 && mr2 > 0) { // 155px radius
        const mr  = Math.sqrt(mr2);
        const str = ((155 - mr) / 155) * 2.1;
        this.vx += (mdx / mr) * str;
        this.vy += (mdy / mr) * str;
      }

      // Speed cap
      const spd = Math.sqrt(this.vx * this.vx + this.vy * this.vy);
      if (spd > MAX_SPD) { const k = MAX_SPD / spd; this.vx *= k; this.vy *= k; }

      // Drag
      this.vx *= DRAG;
      this.vy *= DRAG;

      // Integrate
      this.x += this.vx;
      this.y += this.vy;

      this.trail.push({ x: this.x, y: this.y });
      if (this.trail.length > this.maxTrail) this.trail.shift();

      // Out-of-bounds respawn
      if (Math.abs(this.x - CX) > W * 0.78 || Math.abs(this.y - CY) > H * 0.78) {
        this.spawn();
      }
    }

    draw() {
      const n = this.trail.length;
      if (n < 2) return;

      ctx.save();
      ctx.lineCap = 'round';

      for (let i = 1; i < n; i++) {
        const t    = i / n; // 0 = oldest, 1 = newest
        const prev = this.trail[i - 1];
        const curr = this.trail[i];

        // Color: distance from center → hue journey
        // Inner: cyan (185) → mid: blue (230) → outer: violet/purple (300)
        const ddx   = curr.x - CX;
        const ddy   = curr.y - CY;
        const dist  = Math.sqrt(ddx * ddx + ddy * ddy);
        const dN    = Math.min(dist / 400, 1);
        const hue   = 185 + dN * 118 + this.hOff;
        const sat   = 72 + dN * 24;
        const lit   = 54 + dN * 18;
        const alpha = t * this.opacity * 0.72;

        ctx.beginPath();
        ctx.moveTo(prev.x, prev.y);
        ctx.lineTo(curr.x, curr.y);
        ctx.strokeStyle = `hsla(${hue},${sat}%,${lit}%,${alpha})`;
        ctx.lineWidth   = this.sz * t * 0.88;
        ctx.stroke();
      }

      // Glowing head
      const h    = this.trail[n - 1];
      const hdx  = h.x - CX;
      const hdy  = h.y - CY;
      const hdN  = Math.min(Math.sqrt(hdx * hdx + hdy * hdy) / 400, 1);
      const hHue = 185 + hdN * 118 + this.hOff;

      ctx.shadowBlur  = this.sz * 11;
      ctx.shadowColor = `hsla(${hHue},90%,72%,.92)`;
      ctx.fillStyle   = `hsla(${hHue},85%,80%,${this.opacity})`;
      ctx.beginPath();
      ctx.arc(this.x, this.y, this.sz * 0.78, 0, 6.2832);
      ctx.fill();
      ctx.shadowBlur = 0;
      ctx.restore();
    }
  }

  /* ——— Main loop ——— */
  let lastTime = 0;
  function loop(ts) {
    requestAnimationFrame(loop);
    frame++;

    // Background: near-black navy with ghost trail
    ctx.fillStyle = 'rgba(2,4,18,0.13)';
    ctx.fillRect(0, 0, W, H);

    drawStars();
    drawNebula();
    particles.forEach(p => { p.update(); p.draw(); });
    drawCore();
  }

  function init() {
    resize();
    buildStars();
    particles = Array.from({ length: N_PAR }, (_, i) => new Particle(true));
    requestAnimationFrame(loop);
  }

  /* ——— Mouse ——— */
  const hero = document.getElementById('hero');
  hero.addEventListener('mousemove', e => {
    const r = canvas.getBoundingClientRect();
    mX = e.clientX - r.left;
    mY = e.clientY - r.top;
  });
  hero.addEventListener('mouseleave', () => { mX = -9999; mY = -9999; });

  /* ——— Resize (debounced) ——— */
  let _rt;
  window.addEventListener('resize', () => {
    clearTimeout(_rt);
    _rt = setTimeout(() => { resize(); buildStars(); }, 150);
  });

  init();
})();

/* ═══════════════════════════════════════════════════
   INIT
═══════════════════════════════════════════════════ */
renderPublications();
renderResearch();
renderVideos();
</script>
</body>
</html>
