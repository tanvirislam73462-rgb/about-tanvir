<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tanvirul Islam — Terminal Profile</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=VT323&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --green: #00ff88;
    --green-dim: #00cc66;
    --green-faint: rgba(0,255,136,0.07);
    --amber: #ffb300;
    --red: #ff4455;
    --bg: #0a0f0a;
    --bg2: #0d140d;
    --border: rgba(0,255,136,0.25);
    --font-mono: 'Share Tech Mono', monospace;
    --font-display: 'VT323', monospace;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--green);
    font-family: var(--font-mono);
    font-size: 15px;
    line-height: 1.7;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* Scanlines overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,0,0,0.18) 2px,
      rgba(0,0,0,0.18) 4px
    );
    pointer-events: none;
    z-index: 999;
  }

  /* CRT vignette */
  body::after {
    content: '';
    position: fixed;
    inset: 0;
    background: radial-gradient(ellipse at center, transparent 60%, rgba(0,0,0,0.7) 100%);
    pointer-events: none;
    z-index: 998;
  }

  /* Noise texture */
  .noise {
    position: fixed;
    inset: 0;
    opacity: 0.03;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
    background-size: 150px;
    pointer-events: none;
    z-index: 997;
  }

  .container {
    max-width: 860px;
    margin: 0 auto;
    padding: 2rem 1.5rem 4rem;
  }

  /* ── HEADER ── */
  .terminal-header {
    border: 1px solid var(--border);
    border-radius: 6px 6px 0 0;
    background: #111a11;
    padding: 0.5rem 1rem;
    display: flex;
    align-items: center;
    gap: 0.6rem;
  }
  .dot { width: 12px; height: 12px; border-radius: 50%; }
  .dot.r { background: var(--red); }
  .dot.y { background: var(--amber); }
  .dot.g { background: var(--green); box-shadow: 0 0 6px var(--green); }
  .term-title {
    margin-left: auto;
    margin-right: auto;
    font-size: 13px;
    color: rgba(0,255,136,0.4);
    letter-spacing: 0.1em;
  }

  .terminal-body {
    border: 1px solid var(--border);
    border-top: none;
    border-radius: 0 0 6px 6px;
    background: var(--bg2);
    padding: 2rem 2.5rem 3rem;
    position: relative;
  }

  /* ── HERO ── */
  .hero {
    margin-bottom: 3rem;
    animation: fadeIn 0.6s ease both;
  }

  .prompt-line {
    color: rgba(0,255,136,0.45);
    font-size: 13px;
    margin-bottom: 0.3rem;
    letter-spacing: 0.05em;
  }

  .prompt-line span { color: var(--amber); }

  .big-name {
    font-family: var(--font-display);
    font-size: clamp(3.5rem, 10vw, 6.5rem);
    line-height: 0.95;
    color: var(--green);
    text-shadow: 0 0 30px rgba(0,255,136,0.5), 0 0 60px rgba(0,255,136,0.15);
    letter-spacing: 0.03em;
    animation: flicker 8s infinite;
    margin-bottom: 0.5rem;
  }

  .tagline {
    font-size: 14px;
    color: var(--amber);
    letter-spacing: 0.08em;
    text-transform: uppercase;
    margin-bottom: 1.5rem;
  }
  .tagline::before { content: '> '; color: var(--green-dim); }

  .bio-text {
    max-width: 560px;
    color: rgba(0,255,136,0.75);
    font-size: 14px;
    line-height: 1.9;
    border-left: 2px solid var(--border);
    padding-left: 1rem;
    margin-bottom: 2rem;
  }

  .status-bar {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    font-size: 13px;
  }
  .status-item {
    display: flex;
    align-items: center;
    gap: 0.4rem;
    color: rgba(0,255,136,0.6);
  }
  .status-item .blink {
    display: inline-block;
    width: 8px; height: 8px;
    background: var(--green);
    border-radius: 50%;
    box-shadow: 0 0 6px var(--green);
    animation: blink 1.4s steps(1) infinite;
  }
  .status-item .blink.amber { background: var(--amber); box-shadow: 0 0 6px var(--amber); }

  /* ── SECTION ── */
  .section {
    margin-top: 2.5rem;
    animation: fadeIn 0.8s ease both;
  }

  .section-label {
    font-size: 11px;
    letter-spacing: 0.2em;
    color: rgba(0,255,136,0.35);
    text-transform: uppercase;
    margin-bottom: 0.8rem;
  }
  .section-label::before { content: '# '; }

  .section-title {
    font-family: var(--font-display);
    font-size: 2.2rem;
    color: var(--green);
    text-shadow: 0 0 20px rgba(0,255,136,0.3);
    margin-bottom: 1.2rem;
    letter-spacing: 0.05em;
  }

  /* ── SKILLS GRID ── */
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 1rem;
  }

  .skill-card {
    border: 1px solid var(--border);
    background: var(--green-faint);
    padding: 1rem 1.2rem;
    border-radius: 4px;
    transition: all 0.2s ease;
    position: relative;
    overflow: hidden;
    cursor: default;
  }
  .skill-card::before {
    content: '';
    position: absolute;
    top: 0; left: -100%;
    width: 60%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(0,255,136,0.07), transparent);
    transition: left 0.4s ease;
  }
  .skill-card:hover::before { left: 150%; }
  .skill-card:hover {
    border-color: var(--green-dim);
    box-shadow: 0 0 20px rgba(0,255,136,0.1);
    transform: translateY(-2px);
  }

  .skill-icon {
    font-family: var(--font-display);
    font-size: 1.6rem;
    color: var(--amber);
    margin-bottom: 0.3rem;
  }
  .skill-name {
    font-size: 13px;
    color: var(--green);
    font-weight: bold;
    margin-bottom: 0.2rem;
  }
  .skill-desc {
    font-size: 11.5px;
    color: rgba(0,255,136,0.5);
  }

  .skill-bar-wrap {
    margin-top: 0.6rem;
    height: 3px;
    background: rgba(0,255,136,0.1);
    border-radius: 2px;
    overflow: hidden;
  }
  .skill-bar {
    height: 100%;
    background: linear-gradient(90deg, var(--green-dim), var(--green));
    box-shadow: 0 0 6px var(--green);
    border-radius: 2px;
    animation: growBar 1.5s ease both;
  }

  /* ── TERMINAL BLOCK ── */
  .term-block {
    border: 1px solid var(--border);
    border-radius: 4px;
    background: rgba(0,0,0,0.4);
    padding: 1.2rem 1.5rem;
    font-size: 13px;
    line-height: 2;
  }
  .term-block .cmd { color: var(--amber); }
  .term-block .out { color: rgba(0,255,136,0.7); padding-left: 1.5rem; }
  .term-block .out::before { content: '→ '; color: var(--green-dim); }
  .term-block .comment { color: rgba(0,255,136,0.3); font-style: italic; }

  /* ── PROJECTS ── */
  .projects-list {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  .project-card {
    border: 1px solid var(--border);
    background: var(--green-faint);
    border-radius: 4px;
    padding: 1.2rem 1.5rem;
    transition: all 0.2s ease;
    display: grid;
    grid-template-columns: 1fr auto;
    align-items: start;
    gap: 1rem;
  }
  .project-card:hover {
    border-color: var(--green-dim);
    box-shadow: 0 0 24px rgba(0,255,136,0.08);
  }
  .project-name {
    font-size: 15px;
    color: var(--green);
    font-weight: bold;
    margin-bottom: 0.3rem;
  }
  .project-name::before { content: '📁 '; }
  .project-desc { font-size: 12.5px; color: rgba(0,255,136,0.6); }
  .project-tag {
    font-size: 11px;
    background: rgba(0,255,136,0.1);
    border: 1px solid var(--border);
    padding: 2px 8px;
    border-radius: 3px;
    color: var(--amber);
    white-space: nowrap;
    align-self: start;
  }

  /* ── CONTACT ── */
  .contact-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 0.8rem;
  }
  .contact-item {
    border: 1px solid var(--border);
    padding: 0.9rem 1.1rem;
    border-radius: 4px;
    background: var(--green-faint);
    transition: all 0.2s;
    text-decoration: none;
    display: block;
  }
  .contact-item:hover {
    border-color: var(--amber);
    box-shadow: 0 0 16px rgba(255,179,0,0.1);
  }
  .contact-label { font-size: 10px; color: rgba(0,255,136,0.4); letter-spacing: 0.15em; text-transform: uppercase; }
  .contact-val { font-size: 14px; color: var(--green); margin-top: 2px; }

  /* ── FOOTER ── */
  .footer {
    margin-top: 3rem;
    text-align: center;
    font-size: 12px;
    color: rgba(0,255,136,0.2);
    letter-spacing: 0.1em;
  }
  .footer span { color: var(--green-dim); }

  /* Cursor blink on name */
  .cursor {
    display: inline-block;
    width: 3px;
    height: 0.85em;
    background: var(--green);
    vertical-align: text-bottom;
    margin-left: 4px;
    animation: blink 0.85s steps(1) infinite;
  }

  /* ── DIVIDER ── */
  .divider {
    border: none;
    border-top: 1px solid var(--border);
    margin: 2.5rem 0;
  }

  /* ── ANIMATIONS ── */
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }
  @keyframes flicker {
    0%,95%,100% { opacity: 1; }
    96% { opacity: 0.85; }
    97% { opacity: 1; }
    98% { opacity: 0.9; }
  }
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(12px); }
    to   { opacity: 1; transform: translateY(0); }
  }
  @keyframes growBar {
    from { width: 0; }
  }
  @keyframes typeIn {
    from { width: 0; }
    to { width: 100%; }
  }

  .delay-1 { animation-delay: 0.1s; }
  .delay-2 { animation-delay: 0.25s; }
  .delay-3 { animation-delay: 0.4s; }
  .delay-4 { animation-delay: 0.55s; }
  .delay-5 { animation-delay: 0.7s; }

  @media (max-width: 600px) {
    .terminal-body { padding: 1.5rem 1.2rem 2rem; }
    .big-name { font-size: 3rem; }
    .project-card { grid-template-columns: 1fr; }
  }
</style>
</head>
<body>
<div class="noise"></div>
<div class="container">

  <!-- Window chrome -->
  <div class="terminal-header">
    <div class="dot r"></div>
    <div class="dot y"></div>
    <div class="dot g"></div>
    <div class="term-title">tanvirul@profile ~ bash</div>
  </div>

  <div class="terminal-body">

    <!-- HERO -->
    <div class="hero">
      <div class="prompt-line"><span>tanvirul@profile</span>:~$ whoami</div>
      <h1 class="big-name">TANVIRUL<br>ISLAM<span class="cursor"></span></h1>
      <p class="tagline">Marketing Undergrad &nbsp;·&nbsp; CA Aspirant &nbsp;·&nbsp; Finance Analyst</p>
      <p class="bio-text">
        A driven business student navigating the intersection of marketing strategy and
        chartered accountancy. I decode financial statements, build models that make numbers
        tell stories, and craft written narratives that move audiences. Currently loading
        the next module of my career stack…
      </p>
      <div class="status-bar">
        <div class="status-item"><div class="blink"></div> Open to opportunities</div>
        <div class="status-item"><div class="blink amber"></div> CA Studies — In Progress</div>
        <div class="status-item">📍 Bangladesh</div>
      </div>
    </div>

    <hr class="divider">

    <!-- SKILLS -->
    <div class="section delay-1">
      <div class="section-label">section</div>
      <div class="section-title">SKILLS.exe</div>

      <div class="skills-grid">

        <div class="skill-card">
          <div class="skill-icon">📊</div>
          <div class="skill-name">Financial Modeling</div>
          <div class="skill-desc">DCF, forecasting, scenario analysis &amp; valuation</div>
          <div class="skill-bar-wrap"><div class="skill-bar" style="width:88%"></div></div>
        </div>

        <div class="skill-card">
          <div class="skill-icon">📄</div>
          <div class="skill-name">Company Report Analysis</div>
          <div class="skill-desc">Reading annual reports, ratios &amp; earnings breakdowns</div>
          <div class="skill-bar-wrap"><div class="skill-bar" style="width:85%"></div></div>
        </div>

        <div class="skill-card">
          <div class="skill-icon">🗂</div>
          <div class="skill-name">Microsoft Office Suite</div>
          <div class="skill-desc">Excel, Word, PowerPoint — advanced level workflows</div>
          <div class="skill-bar-wrap"><div class="skill-bar" style="width:92%"></div></div>
        </div>

        <div class="skill-card">
          <div class="skill-icon">✍️</div>
          <div class="skill-name">Professional Writing</div>
          <div class="skill-desc">Reports, proposals, marketing copy &amp; business docs</div>
          <div class="skill-bar-wrap"><div class="skill-bar" style="width:80%"></div></div>
        </div>

        <div class="skill-card">
          <div class="skill-icon">📈</div>
          <div class="skill-name">Marketing Strategy</div>
          <div class="skill-desc">Market research, consumer behavior &amp; brand planning</div>
          <div class="skill-bar-wrap"><div class="skill-bar" style="width:78%"></div></div>
        </div>

        <div class="skill-card">
          <div class="skill-icon">🧾</div>
          <div class="skill-name">Accounting & CA</div>
          <div class="skill-desc">Financial accounting, auditing concepts &amp; taxation</div>
          <div class="skill-bar-wrap"><div class="skill-bar" style="width:70%"></div></div>
        </div>

      </div>
    </div>

    <hr class="divider">

    <!-- ABOUT / TERMINAL BLOCK -->
    <div class="section delay-2">
      <div class="section-label">section</div>
      <div class="section-title">./about_me</div>

      <div class="term-block">
        <div><span class="cmd">$ cat profile.txt</span></div>
        <div class="out">Marketing undergraduate with a passion for financial analysis</div>
        <div class="out">Pursuing CA — bridging the gap between business & numbers</div>
        <div class="out">Strong written communicator across academic & professional contexts</div>
        <div class="out">Excel power-user: PivotTables, VLOOKUP, dynamic dashboards</div>
        <div class="out">Believe good storytelling is the heart of great financial reporting</div>
        <br>
        <div><span class="cmd">$ cat goals.txt</span></div>
        <div class="out">Become a qualified Chartered Accountant</div>
        <div class="out">Combine marketing insights with financial acumen</div>
        <div class="out">Work in corporate finance, investment analysis, or consulting</div>
        <div class="comment"># currently compiling…</div>
      </div>
    </div>

    <hr class="divider">

    <!-- PROJECTS -->
    <div class="section delay-3">
      <div class="section-label">section</div>
      <div class="section-title">PROJECTS.log</div>

      <div class="projects-list">
        <div class="project-card">
          <div>
            <div class="project-name">Financial Statement Deep Dive</div>
            <div class="project-desc">Comprehensive ratio analysis &amp; commentary on a publicly listed company's annual report, highlighting red flags and growth signals.</div>
          </div>
          <div class="project-tag">Excel · Analysis</div>
        </div>
        <div class="project-card">
          <div>
            <div class="project-name">Marketing Plan — Consumer Brand</div>
            <div class="project-desc">Full go-to-market strategy including segmentation, targeting, positioning, and a 12-month promotional roadmap.</div>
          </div>
          <div class="project-tag">Marketing · Writing</div>
        </div>
        <div class="project-card">
          <div>
            <div class="project-name">DCF Valuation Model</div>
            <div class="project-desc">Built a discounted cash flow model with sensitivity tables to value a mid-cap company, with scenario analysis for bull/bear cases.</div>
          </div>
          <div class="project-tag">Excel · Finance</div>
        </div>
      </div>
    </div>

    <hr class="divider">

    <!-- CONTACT -->
    <div class="section delay-4">
      <div class="section-label">section</div>
      <div class="section-title">CONTACT.sh</div>

      <div class="contact-grid">
        <a class="contact-item" href="mailto:your@email.com">
          <div class="contact-label">Email</div>
          <div class="contact-val">your@email.com</div>
        </a>
        <a class="contact-item" href="https://linkedin.com/in/yourprofile" target="_blank">
          <div class="contact-label">LinkedIn</div>
          <div class="contact-val">/in/tanvirulislam</div>
        </a>
        <a class="contact-item" href="https://github.com/yourusername" target="_blank">
          <div class="contact-label">GitHub</div>
          <div class="contact-val">github/tanvirul</div>
        </a>
        <a class="contact-item" href="#">
          <div class="contact-label">Location</div>
          <div class="contact-val">Bangladesh 🇧🇩</div>
        </a>
      </div>
    </div>

    <!-- FOOTER -->
    <div class="footer" style="margin-top:3rem">
      <span>©</span> 2025 Tanvirul Islam &nbsp;·&nbsp; Built with terminal energy &amp; ☕
      <br><br>
      <span style="letter-spacing:0.2em">█▓▒░ EOF ░▒▓█</span>
    </div>

  </div><!-- /terminal-body -->
</div><!-- /container -->
</body>
</html>
