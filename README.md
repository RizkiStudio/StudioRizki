
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Rizki Studio</title>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --cream: #2e8949;
      --ink: #1A1410;
      --rust: #C4521A;
      --sage: #7A9E7E;
      --gold: #D4A843;
      --warm-gray: #ffffff;
      --card-bg: #0c9aad;
    }

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body {
      background: var(--cream);
      color: var(--ink);
      font-family: 'DM Sans', sans-serif;
      font-weight: 300;
      overflow-x: hidden;
    }

    /* ── NAV ── */
    nav {
      position: fixed; top: 0; left: 0; right: 0; z-index: 100;
      display: flex; align-items: center; justify-content: space-between;
      padding: 1.25rem 4rem;
      background: rgba(245,240,232,0.92);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid rgba(196,82,26,0.12);
      transition: box-shadow .3s;
    }
    nav.scrolled { box-shadow: 0 2px 30px rgba(26,20,16,.08); }
    .logo {
      font-family: 'Playfair Display', serif;
      font-size: 1.4rem; font-weight: 900;
      color: var(--ink); letter-spacing: -0.02em; cursor: pointer;
    }
    .logo span { color: var(--rust); }
    .nav-links { display: flex; gap: 2.5rem; list-style: none; }
    .nav-links li a {
      font-size: .88rem; font-weight: 500; letter-spacing: .06em;
      text-transform: uppercase; text-decoration: none;
      color: var(--warm-gray); position: relative; padding-bottom: 2px;
      transition: color .25s;
    }
    .nav-links li a::after {
      content: ''; position: absolute; bottom: 0; left: 0;
      width: 0; height: 1.5px; background: var(--rust);
      transition: width .3s ease;
    }
    .nav-links li a:hover, .nav-links li a.active { color: var(--rust); }
    .nav-links li a:hover::after, .nav-links li a.active::after { width: 100%; }
    .menu-toggle { display: none; flex-direction: column; gap: 5px; cursor: pointer; }
    .menu-toggle span { display: block; width: 26px; height: 2px; background: var(--ink); transition: .3s; }

    /* ── PAGES ── */
    .page { display: none; min-height: 100vh; padding-top: 80px; }
    .page.active { display: block; }
    #home { display: none; flex-direction: column; }
    #home.active { display: flex; }
    .page { animation: pagein .4s ease; }
    @keyframes pagein {
      from { opacity: 0; transform: translateY(14px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    /* ── HOME ── */
    .hero {
      min-height: calc(100vh - 80px);
      display: grid; grid-template-columns: 1fr 1fr;
      align-items: center; padding: 6rem 4rem 4rem; gap: 4rem;
      position: relative; overflow: hidden;
    }
    .hero::before {
      content: ''; position: absolute; right: -10%; top: -10%;
      width: 60vw; height: 100vh;
      background: radial-gradient(ellipse at center, rgba(196,82,26,.07) 0%, transparent 70%);
      pointer-events: none;
    }
    .hero-text { position: relative; }
    .hero-eyebrow {
      display: inline-flex; align-items: center; gap: .6rem;
      font-size: .78rem; font-weight: 500; letter-spacing: .14em;
      text-transform: uppercase; color: var(--rust); margin-bottom: 1.5rem;
    }
    .hero-eyebrow::before { content: ''; display: block; width: 30px; height: 1px; background: var(--rust); }
    .hero h1 {
      font-family: 'Playfair Display', serif;
      font-size: clamp(3.2rem, 5.5vw, 5.5rem);
      font-weight: 900; line-height: 1.05; letter-spacing: -0.03em;
      color: var(--ink); margin-bottom: 1.5rem;
    }
    .hero h1 em { font-style: italic; color: var(--rust); }
    .hero-desc { font-size: 1.05rem; line-height: 1.75; color: var(--warm-gray); max-width: 440px; margin-bottom: 2.5rem; }
    .btn-group { display: flex; gap: 1rem; flex-wrap: wrap; }
    .btn {
      display: inline-flex; align-items: center; gap: .5rem;
      padding: .85rem 2rem; font-size: .9rem; font-weight: 500;
      border: none; cursor: pointer; text-decoration: none;
      transition: all .28s ease; letter-spacing: .02em;
    }
    .btn-primary {
      background: var(--rust); color: white;
      clip-path: polygon(0 0, calc(100% - 10px) 0, 100% 10px, 100% 100%, 10px 100%, 0 calc(100% - 10px));
    }
    .btn-primary:hover { background: #a8431a; transform: translateY(-2px); box-shadow: 0 8px 24px rgba(196,82,26,.3); }
    .btn-outline { background: transparent; color: var(--ink); border: 1.5px solid var(--ink); }
    .btn-outline:hover { background: var(--ink); color: var(--cream); }
    .hero-visual { position: relative; display: flex; align-items: center; justify-content: center; }
    .hero-card-stack { position: relative; width: 380px; height: 460px; }
    .hero-card { position: absolute; border-radius: 4px; overflow: hidden; }
    .hero-card:nth-child(1) {
      width: 300px; height: 380px; top: 40px; left: 40px;
      background: linear-gradient(135deg, #C4521A 0%, #8B3510 100%);
      transform: rotate(-4deg); animation: floatA 6s ease-in-out infinite;
    }
    .hero-card:nth-child(2) {
      width: 260px; height: 320px; top: 20px; left: 60px;
      background: linear-gradient(135deg, var(--gold) 0%, #a07a20 100%);
      transform: rotate(2deg); animation: floatB 7s ease-in-out infinite;
    }
    .hero-card:nth-child(3) {
      width: 240px; height: 280px; top: 60px; left: 80px;
      background: linear-gradient(135deg, var(--sage) 0%, #4d7552 100%);
      display: flex; flex-direction: column; align-items: center; justify-content: center; gap: .75rem;
      animation: floatC 5s ease-in-out infinite;
    }
    .hero-card:nth-child(3) .card-icon { font-size: 3.5rem; }
    .hero-card:nth-child(3) p { font-family: 'Playfair Display', serif; color: white; font-size: 1rem; text-align: center; padding: 0 1.5rem; }
    @keyframes floatA { 0%,100% { transform: rotate(-4deg) translateY(0); } 50% { transform: rotate(-4deg) translateY(-12px); } }
    @keyframes floatB { 0%,100% { transform: rotate(2deg) translateY(0); } 50% { transform: rotate(2deg) translateY(-8px); } }
    @keyframes floatC { 0%,100% { transform: translateY(0); } 50% { transform: translateY(-16px); } }

    .stat-strip {
      display: grid; grid-template-columns: repeat(3,1fr);
      border-top: 1px solid rgba(26,20,16,.1); border-bottom: 1px solid rgba(26,20,16,.1);
      margin: 0 4rem;
    }
    .stat-item { padding: 2.5rem; border-right: 1px solid rgba(26,20,16,.1); text-align: center; }
    .stat-item:last-child { border-right: none; }
    .stat-num { font-family: 'Playfair Display', serif; font-size: 3rem; font-weight: 900; color: var(--rust); line-height: 1; margin-bottom: .4rem; }
    .stat-label { font-size: .8rem; letter-spacing: .1em; text-transform: uppercase; color: var(--warm-gray); }

    /* ── SECTION ── */
    .section-wrap { padding: 6rem 4rem; }
    .section-header { margin-bottom: 4rem; }
    .section-tag {
      display: inline-flex; align-items: center; gap: .6rem;
      font-size: .75rem; font-weight: 500; letter-spacing: .14em;
      text-transform: uppercase; color: var(--rust); margin-bottom: 1rem;
    }
    .section-tag::before { content: ''; display: block; width: 20px; height: 1px; background: var(--rust); }
    .section-title { font-family: 'Playfair Display', serif; font-size: clamp(2rem, 3.5vw, 3.2rem); font-weight: 900; line-height: 1.1; letter-spacing: -0.02em; }
    .section-title em { font-style: italic; color: var(--rust); }
    .section-sub { font-size: .95rem; color: var(--warm-gray); line-height: 1.7; max-width: 520px; margin-top: 1rem; }

    .services-grid {
      display: grid; grid-template-columns: repeat(3, 1fr);
      gap: 1.5px; background: rgba(26,20,16,.1); border: 1px solid rgba(26,20,16,.1);
    }
    .service-item {
      background: var(--cream); padding: 3rem 2.5rem;
      transition: background .3s; position: relative; overflow: hidden;
    }
    .service-item::before {
      content: ''; position: absolute; bottom: 0; left: 0; right: 0; height: 3px;
      background: var(--rust); transform: scaleX(0); transform-origin: left; transition: transform .4s ease;
    }
    .service-item:hover { background: var(--card-bg); }
    .service-item:hover::before { transform: scaleX(1); }
    .service-icon { font-size: 2.5rem; margin-bottom: 1.25rem; display: block; }
    .service-item h3 { font-family: 'Playfair Display', serif; font-size: 1.3rem; font-weight: 700; margin-bottom: .75rem; }
    .service-item p { font-size: .9rem; color: var(--warm-gray); line-height: 1.7; }
    .service-item .service-num { position: absolute; top: 2rem; right: 2rem; font-family: 'Playfair Display', serif; font-size: 2rem; font-weight: 900; color: rgba(196,82,26,.12); }

    /* ── PROFIL ── */
    .profile-grid { display: grid; grid-template-columns: 1fr 1.4fr; gap: 5rem; align-items: center; }
    .profile-img-wrap { position: relative; }
    .profile-img-frame { width: 100%; padding-bottom: 120%; background: linear-gradient(135deg, var(--rust) 0%, var(--gold) 100%); position: relative; overflow: hidden; }
    .profile-img-frame::after { content: '🌿'; position: absolute; bottom: 2rem; right: 2rem; font-size: 5rem; opacity: .18; }
    .profile-img-frame .inner { position: absolute; inset: 20px; background: linear-gradient(160deg, rgba(255,255,255,.15) 0%, transparent 100%); display: flex; align-items: center; justify-content: center; }
    .profile-img-frame .inner span { font-size: 5rem; }
    .profile-badge { position: absolute; bottom: -1.5rem; right: -1.5rem; background: var(--ink); color: var(--cream); padding: 1.2rem 1.6rem; font-family: 'Playfair Display', serif; font-size: 1rem; }
    .profile-badge strong { display: block; font-size: 2rem; font-weight: 900; color: var(--gold); }
    .profile-content h2 { font-family: 'Playfair Display', serif; font-size: clamp(2rem, 3vw, 2.8rem); font-weight: 900; margin-bottom: 1.5rem; }
    .profile-content p { color: var(--warm-gray); line-height: 1.8; margin-bottom: 1rem; }
    .values-list { list-style: none; margin-top: 2rem; display: grid; grid-template-columns: 1fr 1fr; gap: .75rem; }
    .values-list li { display: flex; align-items: center; gap: .6rem; font-size: .9rem; font-weight: 500; }
    .values-list li::before { content: '◆'; color: var(--rust); font-size: .5rem; }
    .team-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 2rem; margin-top: 5rem; }
    .team-card { background: var(--card-bg); border: 1px solid rgba(26,20,16,.07); padding: 2rem; transition: transform .3s, box-shadow .3s; text-align: center; }
    .team-card:hover { transform: translateY(-6px); box-shadow: 0 20px 40px rgba(26,20,16,.08); }
    .team-avatar { width: 80px; height: 80px; border-radius: 50%; background: linear-gradient(135deg, var(--rust), var(--gold)); margin: 0 auto 1rem; display: flex; align-items: center; justify-content: center; font-size: 2rem; }
    .team-card h4 { font-family: 'Playfair Display', serif; font-size: 1.1rem; font-weight: 700; }
    .team-card span { font-size: .8rem; color: var(--rust); letter-spacing: .06em; text-transform: uppercase; }

    /* ── SAWERIA ── */
    .saweria-hero {
      text-align: center;
      padding: 4rem 4rem 2rem;
    }
    .saweria-badge {
      display: inline-block;
      background: linear-gradient(135deg, #FF6B35, #FF9500);
      color: white;
      font-size: .75rem; font-weight: 700; letter-spacing: .12em;
      text-transform: uppercase; padding: .4rem 1.2rem;
      margin-bottom: 1.5rem;
    }
    .saweria-hero h2 {
      font-family: 'Playfair Display', serif;
      font-size: clamp(2rem, 4vw, 3.5rem); font-weight: 900;
      line-height: 1.1; margin-bottom: 1rem;
    }
    .saweria-hero h2 em { font-style: italic; color: #FF6B35; }
    .saweria-hero p { color: var(--warm-gray); font-size: 1rem; line-height: 1.75; max-width: 540px; margin: 0 auto 2.5rem; }

    .saweria-main {
      display: grid; grid-template-columns: 1fr 1.2fr;
      gap: 4rem; padding: 0 4rem 6rem; align-items: start;
    }

    .saweria-card {
      background: linear-gradient(145deg, #1a1410 0%, #2d1f0e 100%);
      border: 1px solid rgba(255,107,53,.2);
      padding: 3rem;
      position: relative; overflow: hidden;
      text-align: center;
    }
    .saweria-card::before {
      content: '';
      position: absolute; top: -50%; left: -50%;
      width: 200%; height: 200%;
      background: radial-gradient(circle, rgba(255,107,53,.08) 0%, transparent 60%);
      pointer-events: none;
    }
    .saweria-logo-wrap {
      width: 90px; height: 90px; border-radius: 50%;
      background: linear-gradient(135deg, #FF6B35, #FF9500);
      margin: 0 auto 1.5rem;
      display: flex; align-items: center; justify-content: center;
      font-size: 2.5rem;
      box-shadow: 0 0 30px rgba(255,107,53,.4);
    }
    .saweria-card h3 {
      font-family: 'Playfair Display', serif;
      font-size: 1.6rem; font-weight: 900;
      color: white; margin-bottom: .5rem;
    }
    .saweria-card .saweria-handle {
      font-size: .85rem; color: #FF9500; letter-spacing: .08em;
      text-transform: uppercase; margin-bottom: 2rem;
    }
    .saweria-card p {
      color: rgba(255,255,255,.65); font-size: .9rem; line-height: 1.75;
      margin-bottom: 2rem;
    }
    .btn-saweria {
      display: inline-flex; align-items: center; gap: .6rem;
      background: linear-gradient(135deg, #FF6B35, #FF9500);
      color: white; padding: 1rem 2.5rem;
      font-size: .95rem; font-weight: 600;
      text-decoration: none; border: none; cursor: pointer;
      transition: all .3s; letter-spacing: .02em;
      clip-path: polygon(0 0, calc(100% - 10px) 0, 100% 10px, 100% 100%, 10px 100%, 0 calc(100% - 10px));
    }
    .btn-saweria:hover { transform: translateY(-3px); box-shadow: 0 12px 32px rgba(255,107,53,.45); }

    .saweria-tiers { display: flex; flex-direction: column; gap: 1.25rem; }
    .tier-card {
      background: rgba(26,20,16,.6);
      border: 1px solid rgba(255,107,53,.15);
      padding: 1.75rem 2rem;
      display: flex; align-items: center; gap: 1.5rem;
      transition: all .3s; cursor: pointer;
      position: relative; overflow: hidden;
    }
    .tier-card::after {
      content: ''; position: absolute; left: 0; top: 0; bottom: 0;
      width: 3px; background: linear-gradient(180deg, #FF6B35, #FF9500);
      transform: scaleY(0); transform-origin: bottom; transition: transform .3s;
    }
    .tier-card:hover { border-color: rgba(255,107,53,.4); transform: translateX(6px); }
    .tier-card:hover::after { transform: scaleY(1); }
    .tier-emoji { font-size: 2.2rem; flex-shrink: 0; }
    .tier-info { flex: 1; }
    .tier-info h4 { font-family: 'Playfair Display', serif; font-size: 1.05rem; font-weight: 700; color: white; margin-bottom: .2rem; }
    .tier-info p { font-size: .83rem; color: rgba(255,255,255,.55); line-height: 1.5; }
    .tier-amount {
      font-family: 'Playfair Display', serif;
      font-size: 1.3rem; font-weight: 900;
      color: #FF9500; flex-shrink: 0;
    }

    .saweria-note {
      margin: 0 4rem 4rem;
      background: rgba(255,107,53,.07);
      border: 1px dashed rgba(255,107,53,.3);
      padding: 1.5rem 2rem;
      display: flex; gap: 1rem; align-items: flex-start;
      font-size: .88rem; color: var(--warm-gray); line-height: 1.7;
    }
    .saweria-note span:first-child { font-size: 1.4rem; flex-shrink: 0; }

    /* ── KONTAK ── */
    .contact-layout { display: grid; grid-template-columns: 1fr 1.2fr; gap: 5rem; align-items: start; }
    .contact-info h3 { font-family: 'Playfair Display', serif; font-size: 1.8rem; font-weight: 700; margin-bottom: 1rem; }
    .contact-info p { color: var(--warm-gray); line-height: 1.8; }
    .contact-details { margin-top: 2.5rem; display: flex; flex-direction: column; gap: 1.5rem; }
    .contact-row { display: flex; gap: 1rem; align-items: flex-start; }
    .contact-row-icon { width: 42px; height: 42px; background: var(--ink); display: flex; align-items: center; justify-content: center; font-size: 1rem; flex-shrink: 0; }
    .contact-row-text strong { display: block; font-size: .8rem; letter-spacing: .08em; text-transform: uppercase; color: var(--rust); margin-bottom: .2rem; }
    .contact-row-text span { font-size: .95rem; color: var(--warm-gray); }
    .contact-form { display: flex; flex-direction: column; gap: 1.25rem; }
    .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 1.25rem; }
    .form-group { display: flex; flex-direction: column; gap: .4rem; }
    .form-group label { font-size: .78rem; letter-spacing: .08em; text-transform: uppercase; font-weight: 500; color: var(--warm-gray); }
    .form-group input, .form-group textarea, .form-group select {
      background: var(--card-bg); border: 1px solid rgba(26,20,16,.15);
      padding: .9rem 1.1rem; font-family: 'DM Sans', sans-serif;
      font-size: .9rem; color: var(--ink); outline: none; transition: border-color .25s;
    }
    .form-group input:focus, .form-group textarea:focus, .form-group select:focus { border-color: var(--rust); }
    .form-group textarea { resize: vertical; min-height: 120px; }
    .form-submit .btn-primary { width: 100%; justify-content: center; padding: 1.1rem; }

    .toast { position: fixed; bottom: 2rem; right: 2rem; background: var(--ink); color: var(--cream); padding: 1rem 1.75rem; font-size: .9rem; transform: translateY(120%); opacity: 0; transition: all .4s ease; z-index: 999; }
    .toast.show { transform: translateY(0); opacity: 1; }

    footer { background: var(--ink); color: rgba(245,240,232,.6); padding: 3rem 4rem; display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap; gap: 1rem; font-size: .82rem; }
    footer .logo { color: var(--cream); }
    footer a { color: rgba(245,240,232,.5); text-decoration: none; }
    footer a:hover { color: var(--gold); }

    @media (max-width: 900px) {
      nav { padding: 1rem 1.5rem; }
      .nav-links { display: none; flex-direction: column; gap: 1.5rem; position: absolute; top: 70px; left: 0; right: 0; background: var(--cream); padding: 2rem 1.5rem; border-bottom: 1px solid rgba(26,20,16,.1); }
      .nav-links.open { display: flex; }
      .menu-toggle { display: flex; }
      .hero { grid-template-columns: 1fr; padding: 3rem 1.5rem; text-align: center; }
      .hero-visual { display: none; }
      .stat-strip { margin: 0 1.5rem; grid-template-columns: 1fr; }
      .stat-item { border-right: none; border-bottom: 1px solid rgba(26,20,16,.1); }
      .section-wrap { padding: 4rem 1.5rem; }
      .profile-grid, .contact-layout, .saweria-main { grid-template-columns: 1fr; gap: 3rem; }
      .team-grid { grid-template-columns: 1fr 1fr; }
      .services-grid { grid-template-columns: 1fr; }
      .form-row { grid-template-columns: 1fr; }
      footer { flex-direction: column; text-align: center; padding: 2rem 1.5rem; }
      .btn-group { justify-content: center; }
      .saweria-hero, .saweria-main, .saweria-note { padding-left: 1.5rem; padding-right: 1.5rem; }
      .saweria-note { margin: 0 1.5rem 3rem; }
    }
  </style>
</head>
<body>

<nav id="navbar">
  <div class="logo" onclick="showPage('home')">Rizki Studio<span>.</span></div>
  <ul class="nav-links" id="navLinks">
    <li><a href="#" onclick="showPage('home')" class="active" data-page="home">Home</a></li>
    <li><a href="#" onclick="showPage('profil')" data-page="profil">Profil</a></li>
    <li><a href="#" onclick="showPage('saweria')" data-page="saweria">Dukungan</a></li>
    <li><a href="#" onclick="showPage('kontak')" data-page="kontak">Kontak</a></li>
  </ul>
  <div class="menu-toggle" id="menuToggle">
    <span></span><span></span><span></span>
  </div>
</nav>

<!-- ═══════════════ HOME ═══════════════ -->
<div id="home" class="page active">
  <section class="hero">
    <div class="hero-text">
      <p class="hero-eyebrow">Rizki Studio</p>
      <h1>Wujudkan<br><em>Visi Anda</em><br>Bersama Kami</h1>
      <p class="hero-desc">Saya berkomitmen menghadirkan solusi kreatif dan inovatif untuk bisnis di era digital.</p>
      <div class="btn-group">
        <a href="#" class="btn btn-primary" onclick="showPage('kontak')">Hubungi Kami ›</a>
        <a href="#" class="btn btn-outline" onclick="showPage('saweria')">Dukung Kami ☕</a>
      </div>
    </div>
    <div class="hero-visual">
      <div class="hero-card-stack">
        <div class="hero-card"></div>
        <div class="hero-card"></div>
        <div class="hero-card">
          <span class="card-icon">✦</span>
          <p>Inovasi &<br>Kreativitas</p>
        </div>
      </div>
    </div>
  </section>

  <div class="stat-strip">
    <div class="stat-item">
      <div class="stat-num">0</div>
      <div class="stat-label">Proyek Berjalan</div>
    </div>
    <div class="stat-item">
      <div class="stat-num">100%</div>
      <div class="stat-label">Kepuasan</div>
    </div>
    <div class="stat-item">
      <div class="stat-num">Pemula</div>
      <div class="stat-label">Pengalaman</div>
    </div>
  </div>

  <section class="section-wrap">
    <div class="section-header">
      <p class="section-tag">Mengapa Kami</p>
      <h2 class="section-title">Keunggulan yang<br><em>Membuat Perbedaan</em></h2>
    </div>
    <div class="services-grid">
      <div class="service-item">
        <span class="service-num">01</span>
        <span class="service-icon">🎯</span>
        <h3>Tepat Sasaran</h3>
        <p>Setiap solusi dirancang khusus sesuai kebutuhan unik, bukan pendekatan satu-untuk-semua.</p>
      </div>
      <div class="service-item">
        <span class="service-num">02</span>
        <span class="service-icon">⚡</span>
        <h3>Eksekusi Cepat</h3>
        <p>Menghasilkan output berkualitas dalam waktu singkat.</p>
      </div>
      <div class="service-item">
        <span class="service-num">03</span>
        <span class="service-icon">🤝</span>
        <h3>Kemitraan Sejati</h3>
        <p>Kami tumbuh bersama bisnis Anda.</p>
      </div>
    </div>
  </section>
</div>

<!-- ═══════════════ PROFIL ═══════════════ -->
<div id="profil" class="page">
  <section class="section-wrap">
    <div class="profile-grid">
      <div class="profile-img-wrap">
        <div class="profile-img-frame">
          <div class="inner"><span>🏛️</span></div>
        </div>
        <div class="profile-badge">
          <strong>2026</strong>
          Berdiri Sejak
        </div>
      </div>
      <div class="profile-content">
        <p class="section-tag">Tentang Kami</p>
        <h2>Kami Adalah<br><em>Rizki Studio</em></h2>
        <p>Rizki Studio berdiri dengan misi sederhana namun kuat: menghadirkan solusi kreatif berkualitas tinggi yang benar-benar berdampak bagi viewers dan masyarakat luas.</p>
        <p>Berawal dari semangat kecil, kini kami telah berkembang menjadi studio pengembangan digital.</p>
        <p>Nilai-nilai yang kami pegang teguh sejak awal adalah komitmen kuat memajukan channel, kejujuran dalam setiap proses, dan rasa hormat mendalam kepada viewers serta komunitas.</p>
        <ul class="values-list">
          <li>Integritas & Kejujuran</li>
          <li>Inovasi Berkelanjutan</li>
          <li>Kualitas Terdepan</li>
          <li>Kolaborasi Inklusif</li>
        </ul>
      </div>
    </div>
    <div class="team-grid">
      <div class="team-card">
        <div class="team-avatar">👨‍💼</div>
        <h4>Faozan Rizki Wijaya</h4>
        <span>Pemilik</span>
      </div>
      <div class="team-card">
        <div class="team-avatar">👩‍🎨</div>
        <h4>Faozan Rizki Wijaya</h4>
        <span>Creative Director</span>
      </div>
      <div class="team-card">
        <div class="team-avatar">👨‍💻</div>
        <h4>Faozan Rizki Wijaya</h4>
        <span>Lead Developer</span>
      </div>
    </div>
  </section>
</div>

<!-- ═══════════════ SAWERIA ═══════════════ -->
<div id="saweria" class="page">
  <div class="saweria-hero">
    <div class="saweria-badge">☕ Dukung Kami</div>
    <h2>Traktir Kami<br><em>Kopi & Semangat</em></h2>
    <p>Dukungan kamu sangat berarti bagi perkembangan Rizki Studio. Setiap kontribusi membantu kami terus berkarya dan menciptakan konten yang lebih baik.</p>
  </div>

  <div class="saweria-main">
    <div class="saweria-card">
      <div class="saweria-logo-wrap">☕</div>
      <h3>Rizki Studio</h3>
      <p class="saweria-handle">saweria.com/rizkistudio</p>
      <p>Halo! Terima kasih sudah mengunjungi halaman dukungan kami. Kalau konten kami bermanfaat dan kamu mau support perkembangan kami, kopi virtual dari kamu sangat kami hargai! 🙏</p>
      <a href="https://saweria.co/Zephyrshade" target="_blank" class="btn-saweria">
        ☕ Traktir Kopi di Saweria
      </a>
    </div>

    <div>
      <p style="font-family:'Playfair Display',serif; font-size:1.1rem; font-weight:700; color:white; margin-bottom:1.5rem;">Pilih Dukunganmu</p>
      <div class="saweria-tiers">
        <div class="tier-card" onclick="openSaweria()">
          <span class="tier-emoji">☕</span>
          <div class="tier-info">
            <h4>Secangkir Kopi</h4>
            <p>Traktiran kecil yang bikin semangat terus berkarya</p>
          </div>
          <div class="tier-amount">Rp 10K</div>
        </div>
        <div class="tier-card" onclick="openSaweria()">
          <span class="tier-emoji">🍕</span>
          <div class="tier-info">
            <h4>Semangkuk Mie Ayam</h4>
            <p>Dukungan yang bikin kami makin produktif seharian</p>
          </div>
          <div class="tier-amount">Rp 25K</div>
        </div>
        <div class="tier-card" onclick="openSaweria()">
          <span class="tier-emoji">🚀</span>
          <div class="tier-info">
            <h4>Supporter Setia</h4>
            <p>Kamu adalah pahlawan di balik layar Rizki Studio!</p>
          </div>
          <div class="tier-amount">Rp 50K</div>
        </div>
        <div class="tier-card" onclick="openSaweria()">
          <span class="tier-emoji">💎</span>
          <div class="tier-info">
            <h4>Diamond Supporter</h4>
            <p>Dukungan luar biasa yang tidak akan pernah kami lupakan</p>
          </div>
          <div class="tier-amount">Bebas</div>
        </div>
      </div>
    </div>
  </div>

  <div class="saweria-note">
    <span>💡</span>
    <span>Semua donasi disalurkan langsung untuk pengembangan konten, peralatan produksi, dan operasional Rizki Studio. Nama kamu akan kami sebut di video sebagai bentuk apresiasi! Klik tombol di atas untuk langsung menuju halaman Saweria kami.</span>
  </div>
</div>

<!-- ═══════════════ KONTAK ═══════════════ -->
<div id="kontak" class="page">
  <section class="section-wrap">
    <div class="section-header">
      <p class="section-tag">Hubungi Kami</p>
      <h2 class="section-title">Mari Mulai<br><em>Percakapan</em></h2>
      <p class="section-sub">Kirim pesan dan kami akan merespons secepatnya.</p>
    </div>
    <div class="contact-layout">
      <div class="contact-info">
        <h3>Informasi Kontak</h3>
        <p>Jangan ragu untuk menghubungi kami melalui berbagai saluran yang tersedia.</p>
        <div class="contact-details">
          <div class="contact-row">
            <div class="contact-row-icon">📍</div>
            <div class="contact-row-text">
              <strong>Alamat</strong>
              <span>Indonesia</span>
            </div>
          </div>
          <div class="contact-row">
            <div class="contact-row-icon">📞</div>
            <div class="contact-row-text">
              <strong>Telepon / WhatsApp</strong>
              <span>+62 823-4056-8808</span>
            </div>
          </div>
          <div class="contact-row">
            <div class="contact-row-icon">✉️</div>
            <div class="contact-row-text">
              <strong>Email</strong>
              <span>rizkiofficialacid@gmail.com</span>
            </div>
          </div>
        </div>
      </div>
      <div>
        <div class="contact-form" id="contactForm">
          <div class="form-row">
            <div class="form-group">
              <label>Nama Lengkap</label>
              <input type="text" id="fname" placeholder="Nama kamu" />
            </div>
            <div class="form-group">
              <label>Alamat Email</label>
              <input type="email" id="femail" placeholder="email@kamu.com" />
            </div>
          </div>
          <div class="form-group">
            <label>Nomor Telepon</label>
            <input type="tel" id="fphone" placeholder="+62 8xx xxxx xxxx" />
          </div>
          <div class="form-group">
            <label>Topik</label>
            <select id="fservice">
              <option value="">— Pilih topik —</option>
              <option>Pengembangan Web</option>
              <option>Pengembangan Channel</option>
              <option>Produksi Konten</option>
              <option>Lainnya</option>
            </select>
          </div>
          <div class="form-group">
            <label>Pesan</label>
            <textarea id="fmsg" placeholder="Ceritakan tentang proyek atau pertanyaan kamu…"></textarea>
          </div>
          <div class="form-submit">
            <button class="btn btn-primary" onclick="submitForm()">Kirim Pesan →</button>
          </div>
        </div>
      </div>
    </div>
  </section>
</div>

<footer>
  <div class="logo">Rizki Studio<span style="color:var(--gold)">.</span></div>
  <span>© 2026 Rizki Studio. Semua hak dilindungi.</span>
  <div style="display:flex; gap:1.5rem;">
    <a href="https://www.instagram.com/faozanrizky_?igsh=MXE5anQzYnIxeDRrNQ==">Instagram</a>
    <a href="https://www.tiktok.com/@officialkreator.muda?_r=1&_t=ZS-94WHKwDqJQA">Tiktok</a>
  </div>
</footer>

<div class="toast" id="toast">✓ Pesan berhasil dikirim! Kami akan menghubungi Anda segera.</div>

<script>
  function showPage(id) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    document.querySelectorAll('.nav-links a').forEach(a => {
      a.classList.toggle('active', a.dataset.page === id);
    });
    window.scrollTo({ top: 0, behavior: 'smooth' });
    document.getElementById('navLinks').classList.remove('open');
  }

  window.addEventListener('scroll', () => {
    document.getElementById('navbar').classList.toggle('scrolled', window.scrollY > 10);
  });

  document.getElementById('menuToggle').addEventListener('click', () => {
    document.getElementById('navLinks').classList.toggle('open');
  });

  function openSaweria() {
    window.open('https://saweria.co/Zephyrshade', '_blank');
  }

  function submitForm() {
    const name = document.getElementById('fname').value.trim();
    const email = document.getElementById('femail').value.trim();
    if (!name || !email) {
      alert('Mohon isi nama dan email terlebih dahulu.');
      return;
    }
    const toast = document.getElementById('toast');
    toast.classList.add('show');
    ['fname','femail','fphone','fservice','fmsg'].forEach(id => {
      const el = document.getElementById(id);
      if (el) el.value = '';
    });
    setTimeout(() => toast.classList.remove('show'), 4000);
  }

  document.querySelectorAll('.nav-links a').forEach(a => {
    a.addEventListener('click', e => e.preventDefault());
  });
</script>
</body>
</html>
