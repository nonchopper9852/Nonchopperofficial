<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Nonchopper | Official Portfolio</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;600&family=Noto+Sans+JP:wght@300;400;500&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg-deep: #05070e;
      --bg-card: rgba(14, 20, 38, 0.65);
      --accent-cyan: #5ce1e6;
      --accent-violet: #9d7bff;
      --text-main: #eef2ff;
      --text-muted: #94a3b8;
      --border-glow: rgba(92, 225, 230, 0.25);
    }
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      background-color: var(--bg-deep);
      color: var(--text-main);
      font-family: 'Noto Sans JP', sans-serif;
      line-height: 1.8;
      overflow-x: hidden;
    }
    canvas#bg-canvas {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      z-index: -1;
      pointer-events: none;
    }
    header {
      position: fixed;
      top: 0; width: 100%;
      padding: 1.2rem 5%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: rgba(5, 7, 14, 0.75);
      backdrop-filter: blur(10px);
      border-bottom: 1px solid rgba(255,255,255,0.06);
      z-index: 100;
    }
    .logo {
      font-family: 'Cinzel', serif;
      font-size: 1.4rem;
      letter-spacing: 0.18em;
      color: var(--text-main);
      text-decoration: none;
    }
    nav a {
      color: var(--text-muted);
      text-decoration: none;
      margin-left: 1.8rem;
      font-size: 0.85rem;
      letter-spacing: 0.1em;
      transition: color 0.3s;
    }
    nav a:hover { color: var(--accent-cyan); }
    .hero {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      padding: 0 1.5rem;
    }
    .hero-sub {
      font-size: 0.85rem;
      letter-spacing: 0.35em;
      color: var(--accent-cyan);
      margin-bottom: 1rem;
      text-transform: uppercase;
    }
    .hero h1 {
      font-family: 'Cinzel', serif;
      font-size: clamp(2.4rem, 6vw, 4.5rem);
      letter-spacing: 0.2em;
      font-weight: 400;
      margin-bottom: 1.2rem;
      text-shadow: 0 0 30px rgba(92, 225, 230, 0.3);
    }
    .hero p {
      max-width: 600px;
      color: var(--text-muted);
      font-size: 0.95rem;
      font-weight: 300;
    }
    section {
      max-width: 1080px;
      margin: 0 auto;
      padding: 6rem 1.5rem;
    }
    h2 {
      font-family: 'Cinzel', serif;
      font-size: 1.8rem;
      letter-spacing: 0.2em;
      text-align: center;
      margin-bottom: 3rem;
      font-weight: 400;
    }
    h2 span {
      display: block;
      font-family: 'Noto Sans JP', sans-serif;
      font-size: 0.75rem;
      color: var(--accent-cyan);
      letter-spacing: 0.25em;
      margin-top: 0.4rem;
    }
    .concept-box {
      background: var(--bg-card);
      border: 1px solid var(--border-glow);
      border-radius: 12px;
      padding: 2.5rem;
      text-align: center;
      backdrop-filter: blur(8px);
    }
    .works-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 1.8rem;
    }
    .work-card {
      background: var(--bg-card);
      border: 1px solid rgba(255,255,255,0.08);
      border-radius: 12px;
      overflow: hidden;
      transition: transform 0.3s, border-color 0.3s;
    }
    .work-card:hover {
      transform: translateY(-5px);
      border-color: var(--accent-cyan);
    }
    .work-art {
      height: 220px;
      display: flex;
      align-items: center;
      justify-content: center;
      position: relative;
      overflow: hidden;
    }
    .art-1 { background: radial-gradient(circle at 30% 30%, #1e3a8a, #090d16 70%); }
    .art-2 { background: radial-gradient(circle at 70% 40%, #4c1d95, #090d16 70%); }
    .art-3 { background: radial-gradient(circle at 50% 60%, #0e7490, #090d16 70%); }
    .moon-circle {
      width: 90px; height: 90px;
      border-radius: 50%;
      border: 1px solid rgba(255,255,255,0.6);
      box-shadow: 0 0 25px rgba(92,225,230,0.4);
    }
    .work-info { padding: 1.4rem; }
    .work-info h3 { font-size: 1.1rem; font-weight: 500; margin-bottom: 0.4rem; }
    .work-info p { font-size: 0.85rem; color: var(--text-muted); }
    .links-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 1.2rem;
    }
    .link-card {
      display: block;
      background: var(--bg-card);
      border: 1px solid rgba(255,255,255,0.1);
      padding: 1.4rem;
      border-radius: 10px;
      text-decoration: none;
      color: var(--text-main);
      transition: all 0.3s;
    }
    .link-card:hover {
      border-color: var(--accent-cyan);
      background: rgba(92, 225, 230, 0.08);
    }
    .link-card strong { display: block; font-size: 1rem; margin-bottom: 0.2rem; }
    .link-card span { font-size: 0.8rem; color: var(--text-muted); }
    footer {
      text-align: center;
      padding: 3rem 1rem;
      font-size: 0.8rem;
      color: var(--text-muted);
      border-top: 1px solid rgba(255,255,255,0.06);
    }
  </style>
</head>
<body>
  <canvas id="bg-canvas"></canvas>
  <header>
    <a href="#" class="logo">NONCHOPPER</a>
    <nav>
      <a href="#concept">CONCEPT</a>
      <a href="#works">WORKS</a>
      <a href="#links">LINKS</a>
    </nav>
  </header>

  <div class="hero">
    <div class="hero-sub">Digital Artist &amp; Designer</div>
    <h1>NONCHOPPER</h1>
    <p>写真の断片に光と抽象の線を重ね、現実と幻想の狭間を描く。<br>人間の感情や二面性、そして「結び付き」をテーマに表現を紡ぐ。</p>
  </div>

  <section id="concept">
    <h2>CONCEPT<span>作品世界について</span></h2>
    <div class="concept-box">
      <p>日常の風景や写真の断片に、デジタルの光とラインをレイヤーとして重ねることで、<br>目に見える現実の奥に潜む感情や孤独、つながりの輪郭を可視化しています。</p>
    </div>
  </section>

  <section id="works">
    <h2>SELECTED WORKS<span>代表シリーズ</span></h2>
    <div class="works-grid">
      <div class="work-card">
        <div class="work-art art-1"><div class="moon-circle"></div></div>
        <div class="work-info">
          <h3>格子の月 / 内に居たのはどっち？</h3>
          <p>閉じ込めたものと守られていたものの境界を問うシリーズ。</p>
        </div>
      </div>
      <div class="work-card">
        <div class="work-art art-2"><div class="moon-circle" style="border-radius:12px; transform:rotate(45deg);"></div></div>
        <div class="work-info">
          <h3>横顔 -二面性- / 残響</h3>
          <p>光と影のコントラストで心の揺らぎを捉えたデジタルアート。</p>
        </div>
      </div>
      <div class="work-card">
        <div class="work-art art-3"><div class="moon-circle" style="border-style:dashed;"></div></div>
        <div class="work-info">
          <h3>結び付き / 空論の世界</h3>
          <p>ネットネイティブ時代のつながりと孤独を描く最新コレクション。</p>
        </div>
      </div>
    </div>
  </section>

  <section id="links">
    <h2>PLATFORMS &amp; SNS<span>活動リンク・作品販売</span></h2>
    <div class="links-grid">
      <a href="https://www.instagram.com/non_chopper_/" target="_blank" rel="noopener" class="link-card">
        <strong>Instagram</strong>
        <span>@non_chopper_ / 最新作品・リール</span>
      </a>
      <a href="https://note.com/" target="_blank" rel="noopener" class="link-card">
        <strong>note</strong>
        <span>制作秘話・エッセイ・連載小説</span>
      </a>
      <a href="https://nonchopper-portfolio.my.canva.site/nonchopper" target="_blank" rel="noopener" class="link-card">
        <strong>Archive Portfolio</strong>
        <span>過去の展示履歴・アーカイブ</span>
      </a>
      <a href="https://thebase.com/" target="_blank" rel="noopener" class="link-card">
        <strong>Official Shop (BASE)</strong>
        <span>ジークレー作品・アクリルスタンド販売</span>
      </a>
    </div>
  </section>

  <footer>
    &copy; 2026 Nonchopper. All Rights Reserved.
  </footer>

  <script>
    const canvas = document.getElementById('bg-canvas');
    const ctx = canvas.getContext('2d');
    let w, h, particles = [];
    function resize() {
      w = canvas.width = window.innerWidth;
      h = canvas.height = window.innerHeight;
    }
    window.addEventListener('resize', resize);
    resize();
    for (let i = 0; i < 45; i++) {
      particles.push({
        x: Math.random() * w,
        y: Math.random() * h,
        vx: (Math.random() - 0.5) * 0.4,
        vy: (Math.random() - 0.5) * 0.4,
        r: Math.random() * 2 + 0.5
      });
    }
    function draw() {
      ctx.clearRect(0, 0, w, h);
      ctx.strokeStyle = 'rgba(92, 225, 230, 0.12)';
      ctx.fillStyle = 'rgba(157, 123, 255, 0.5)';
      particles.forEach((p, i) => {
        p.x += p.vx; p.y += p.vy;
        if (p.x < 0 || p.x > w) p.vx *= -1;
        if (p.y < 0 || p.y > h) p.vy *= -1;
        ctx.beginPath();
        ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
        ctx.fill();
        for (let j = i + 1; j < particles.length; j++) {
          const dx = p.x - particles[j].x;
          const dy = p.y - particles[j].y;
          if (Math.hypot(dx, dy) < 140) {
            ctx.beginPath();
            ctx.moveTo(p.x, p.y);
            ctx.lineTo(particles[j].x, particles[j].y);
            ctx.stroke();
          }
        }
      });
      requestAnimationFrame(draw);
    }
    draw();
  </script>
</body>
</html>
