# legacy-website<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Discord Legacy</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;900&display=swap" rel="stylesheet"/>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body { font-family: 'Inter', sans-serif; background: #030812; color: #ffffff; overflow-x: hidden; }

    nav {
      display: flex; align-items: center; justify-content: space-between;
      padding: 20px 60px; background: rgba(3,8,18,0.95);
      backdrop-filter: blur(10px); position: fixed; width: 100%; top: 0;
      z-index: 100; border-bottom: 1px solid rgba(0,150,255,0.1);
    }
    .nav-logo { display: flex; align-items: center; gap: 12px; font-size: 22px; font-weight: 900; letter-spacing: 2px; text-transform: uppercase; }
    .nav-logo img { width: 42px; height: 42px; border-radius: 50%; }
    .nav-links { display: flex; gap: 30px; list-style: none; }
    .nav-links a { color: rgba(255,255,255,0.6); text-decoration: none; font-size: 14px; font-weight: 600; letter-spacing: 1px; text-transform: uppercase; transition: color 0.2s; }
    .nav-links a:hover { color: #00b4ff; }
    .nav-buttons { display: flex; gap: 12px; }
    .btn-join { background: linear-gradient(135deg, #0072ff, #00b4ff); color: white; border: none; padding: 10px 24px; border-radius: 8px; font-size: 14px; font-weight: 700; cursor: pointer; text-decoration: none; transition: all 0.2s; }
    .btn-join:hover { transform: translateY(-1px); box-shadow: 0 6px 20px rgba(0,180,255,0.35); }
    .btn-staff { background: transparent; color: rgba(255,255,255,0.7); border: 1px solid rgba(0,180,255,0.25); padding: 10px 24px; border-radius: 8px; font-size: 14px; font-weight: 700; cursor: pointer; text-decoration: none; transition: all 0.2s; }
    .btn-staff:hover { border-color: #00b4ff; color: #00b4ff; }

    .hero { min-height: 100vh; display: flex; align-items: center; justify-content: center; text-align: center; padding: 120px 40px 80px; position: relative; overflow: hidden; }
    .hero::before { content: ''; position: absolute; width: 700px; height: 700px; background: radial-gradient(circle, rgba(0,114,255,0.12) 0%, transparent 70%); top: 50%; left: 50%; transform: translate(-50%, -50%); pointer-events: none; }
    .hero::after { content: ''; position: absolute; width: 400px; height: 400px; background: radial-gradient(circle, rgba(0,180,255,0.08) 0%, transparent 70%); top: 30%; left: 30%; pointer-events: none; }
    .hero-badge { display: inline-block; background: rgba(0,180,255,0.1); border: 1px solid rgba(0,180,255,0.3); color: #00b4ff; padding: 6px 18px; border-radius: 20px; font-size: 12px; font-weight: 700; letter-spacing: 2px; text-transform: uppercase; margin-bottom: 24px; }
    .hero h1 { font-size: clamp(42px, 7vw, 80px); font-weight: 900; line-height: 1.05; letter-spacing: -1px; margin-bottom: 24px; }
    .hero h1 span { background: linear-gradient(135deg, #0072ff, #00b4ff, #40d9ff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
    .hero p { font-size: 18px; color: rgba(255,255,255,0.5); max-width: 560px; margin: 0 auto 40px; line-height: 1.7; }
    .hero-buttons { display: flex; gap: 16px; justify-content: center; flex-wrap: wrap; }
    .btn-hero-join { background: linear-gradient(135deg, #0072ff, #00b4ff); color: white; padding: 16px 36px; border-radius: 10px; font-size: 16px; font-weight: 700; text-decoration: none; transition: all 0.2s; }
    .btn-hero-join:hover { transform: translateY(-2px); box-shadow: 0 10px 35px rgba(0,180,255,0.4); }
    .btn-hero-learn { background: transparent; color: rgba(255,255,255,0.7); border: 1px solid rgba(0,180,255,0.2); padding: 16px 36px; border-radius: 10px; font-size: 16px; font-weight: 700; text-decoration: none; transition: all 0.2s; }
    .btn-hero-learn:hover { border-color: #00b4ff; color: #00b4ff; }

    .stats-bar { display: flex; justify-content: center; gap: 60px; padding: 40px 60px; background: rgba(0,114,255,0.04); border-top: 1px solid rgba(0,180,255,0.08); border-bottom: 1px solid rgba(0,180,255,0.08); flex-wrap: wrap; }
    .stat-item { text-align: center; }
    .stat-number { font-size: 32px; font-weight: 900; background: linear-gradient(135deg, #0072ff, #00b4ff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
    .stat-label { font-size: 12px; color: rgba(255,255,255,0.35); font-weight: 600; letter-spacing: 1px; text-transform: uppercase; margin-top: 4px; }

    .section { padding: 100px 60px; max-width: 1200px; margin: 0 auto; }
    .section-label { font-size: 12px; font-weight: 700; letter-spacing: 3px; text-transform: uppercase; color: #00b4ff; margin-bottom: 16px; }
    .section-title { font-size: clamp(28px, 4vw, 48px); font-weight: 900; margin-bottom: 16px; letter-spacing: -0.5px; }
    .section-sub { font-size: 16px; color: rgba(255,255,255,0.45); margin-bottom: 60px; max-width: 500px; line-height: 1.6; }

    .ranks-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 16px; }
    .rank-card { background: rgba(255,255,255,0.03); border: 1px solid rgba(0,180,255,0.1); border-radius: 16px; padding: 28px 24px; transition: all 0.3s; position: relative; overflow: hidden; }
    .rank-card::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px; border-radius: 16px 16px 0 0; }
    .rank-card:hover { transform: translateY(-4px); border-color: rgba(0,180,255,0.3); background: rgba(0,180,255,0.05); }
    .rank-legendary::before { background: linear-gradient(90deg, #FFD700, #FFA500); }
    .rank-veteran::before { background: linear-gradient(90deg, #e74c3c, #c0392b); }
    .rank-classic::before { background: linear-gradient(90deg, #0072ff, #00b4ff); }
    .rank-modern::before { background: linear-gradient(90deg, #9b59b6, #8e44ad); }
    .rank-new::before { background: linear-gradient(90deg, #2ecc71, #27ae60); }
    .rank-emoji { font-size: 32px; margin-bottom: 12px; }
    .rank-name { font-size: 18px; font-weight: 900; letter-spacing: 1px; margin-bottom: 6px; }
    .rank-years { font-size: 13px; color: rgba(255,255,255,0.35); font-weight: 600; margin-bottom: 10px; }
    .rank-desc { font-size: 13px; color: rgba(255,255,255,0.5); line-height: 1.5; }

    .features-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; }
    .feature-card { background: rgba(255,255,255,0.03); border: 1px solid rgba(0,180,255,0.1); border-radius: 16px; padding: 32px; transition: all 0.3s; }
    .feature-card:hover { transform: translateY(-4px); border-color: rgba(0,180,255,0.3); background: rgba(0,114,255,0.05); }
    .feature-icon { font-size: 36px; margin-bottom: 16px; }
    .feature-title { font-size: 18px; font-weight: 700; margin-bottom: 10px; }
    .feature-desc { font-size: 14px; color: rgba(255,255,255,0.45); line-height: 1.6; }
    code { background: rgba(0,180,255,0.15); color: #00b4ff; padding: 2px 6px; border-radius: 4px; font-size: 13px; }

    .cta-section { text-align: center; padding: 100px 40px; background: rgba(0,114,255,0.05); border-top: 1px solid rgba(0,180,255,0.12); border-bottom: 1px solid rgba(0,180,255,0.12); }
    .cta-section h2 { font-size: clamp(28px, 4vw, 52px); font-weight: 900; margin-bottom: 16px; letter-spacing: -0.5px; }
    .cta-section p { font-size: 16px; color: rgba(255,255,255,0.45); margin-bottom: 40px; }

    footer { text-align: center; padding: 40px; color: rgba(255,255,255,0.2); font-size: 13px; }
    footer a { color: rgba(0,180,255,0.5); text-decoration: none; }
    footer a:hover { color: #00b4ff; }

    @media (max-width: 768px) {
      nav { padding: 16px 20px; }
      .nav-links { display: none; }
      .section { padding: 60px 20px; }
      .stats-bar { gap: 30px; padding: 30px 20px; }
    }
  </style>
</head>
<body>

  <nav>
    <div class="nav-logo">
      <img src="https://i.imgur.com/NSbMuef.png" alt="Legacy Logo"/>
      LEGACY
    </div>
    <ul class="nav-links">
      <li><a href="#ranks">Ranks</a></li>
      <li><a href="#features">Features</a></li>
      <li><a href="#join">Join</a></li>
    </ul>
    <div class="nav-buttons">
      <a href="https://discord.gg/3XF3uubH" target="_blank" class="btn-join">Join Server</a>
      <a href="https://discord.gg/3XF3uubH" target="_blank" class="btn-staff">Staff Area</a>
    </div>
  </nav>

  <section class="hero">
    <div>
      <div class="hero-badge">🏆 Your history defines your rank</div>
      <h1>Welcome to<br/><span>Discord Legacy</span></h1>
      <p>The only Discord community that ranks members based on their account creation year. Your history speaks for you.</p>
      <div class="hero-buttons">
        <a href="https://discord.gg/3XF3uubH" target="_blank" class="btn-hero-join">Join the Community</a>
        <a href="#ranks" class="btn-hero-learn">Discover Your Rank</a>
      </div>
    </div>
  </section>

  <div class="stats-bar">
    <div class="stat-item"><div class="stat-number">5</div><div class="stat-label">Rank Categories</div></div>
    <div class="stat-item"><div class="stat-number">12</div><div class="stat-label">Year Roles</div></div>
    <div class="stat-item"><div class="stat-number">50+</div><div class="stat-label">Quiz Questions</div></div>
    <div class="stat-item"><div class="stat-number">24/7</div><div class="stat-label">Bot Online</div></div>
  </div>

  <section class="section" id="ranks">
    <div class="section-label">Rank System</div>
    <h2 class="section-title">What's your Legacy rank?</h2>
    <p class="section-sub">Your rank is automatically assigned based on the year your Discord account was created. No choices — your history speaks for you.</p>
    <div class="ranks-grid">
      <div class="rank-card rank-legendary">
        <div class="rank-emoji">🏛️</div>
        <div class="rank-name">LEGENDARY</div>
        <div class="rank-years">2015 — 2016</div>
        <div class="rank-desc">The original Discord pioneers. You were there when it all began.</div>
      </div>
      <div class="rank-card rank-veteran">
        <div class="rank-emoji">⚔️</div>
        <div class="rank-name">VETERAN</div>
        <div class="rank-years">2017 — 2018</div>
        <div class="rank-desc">Battle-hardened veterans who shaped the early Discord culture.</div>
      </div>
      <div class="rank-card rank-classic">
        <div class="rank-emoji">🔵</div>
        <div class="rank-name">CLASSIC</div>
        <div class="rank-years">2019 — 2020</div>
        <div class="rank-desc">The classics. Present during Discord's biggest growth era.</div>
      </div>
      <div class="rank-card rank-modern">
        <div class="rank-emoji">💜</div>
        <div class="rank-name">MODERN</div>
        <div class="rank-years">2021 — 2022</div>
        <div class="rank-desc">Part of the new era that brought Discord to the mainstream.</div>
      </div>
      <div class="rank-card rank-new">
        <div class="rank-emoji">🌿</div>
        <div class="rank-name">NEW</div>
        <div class="rank-years">2023 — 2026</div>
        <div class="rank-desc">The future of Legacy. Your story is just beginning.</div>
      </div>
    </div>
  </section>

  <section class="section" id="features" style="padding-top:0">
    <div class="section-label">Features</div>
    <h2 class="section-title">Everything you need</h2>
    <p class="section-sub">Legacy comes with a fully custom bot built from scratch for this community.</p>
    <div class="features-grid">
      <div class="feature-card">
        <div class="feature-icon">✅</div>
        <div class="feature-title">Auto Verification</div>
        <div class="feature-desc">Use <code>!verify</code> and the bot instantly assigns your year role and category.</div>
      </div>
      <div class="feature-card">
        <div class="feature-icon">🧠</div>
        <div class="feature-title">Daily Quiz</div>
        <div class="feature-desc">A new Discord trivia question every day at 15:00 UTC. Compete for points.</div>
      </div>
      <div class="feature-card">
        <div class="feature-icon">🎂</div>
        <div class="feature-title">Anniversary System</div>
        <div class="feature-desc">The bot automatically celebrates your Discord account anniversary every year.</div>
      </div>
      <div class="feature-card">
        <div class="feature-icon">📊</div>
        <div class="feature-title">Live Statistics</div>
        <div class="feature-desc">See how many members belong to each year and category with <code>!stats</code>.</div>
      </div>
      <div class="feature-card">
        <div class="feature-icon">🛡️</div>
        <div class="feature-title">Anti-Spam Protection</div>
        <div class="feature-desc">Automatic mute for 5 minutes if you spam commands.</div>
      </div>
      <div class="feature-card">
        <div class="feature-icon">🌍</div>
        <div class="feature-title">International Community</div>
        <div class="feature-desc">Members from all over the world united by their Discord history.</div>
      </div>
    </div>
  </section>

  <section class="cta-section" id="join">
    <h2>Ready to discover<br/>your rank?</h2>
    <p>Join Legacy and find out where your Discord history places you.</p>
    <a href="https://discord.gg/3XF3uubH" target="_blank" class="btn-hero-join">Join Discord Legacy</a>
  </section>

  <footer>
    <p>© 2025 Discord Legacy — All rights reserved</p>
    <p style="margin-top:8px">
      <a href="https://discord.gg/3XF3uubH" target="_blank">Discord</a> &nbsp;·&nbsp;
      <a href="mailto:maximilian04wr@gmail.com">Contact</a>
    </p>
  </footer>

</body>
</html>
