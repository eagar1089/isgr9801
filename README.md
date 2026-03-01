<!--
  Beach & Sea Glassmorphism Profile README
  Customize: name, title, location, links, projects, tech stack, widgets.
  Notes:
  - GitHub READMEs support a subset of HTML/CSS. Some CSS (e.g., backdrop-filter) may render differently across clients.
  - Keep critical content readable even if effects degrade.
-->

<!-- SEO-ish meta (some renderers ignore, harmless) -->
<meta name="description" content="Beach & Sea themed GitHub profile with bright glassmorphism cards, ocean palette, and modern UI/UX." />
<meta name="theme-color" content="#0A2472" />

<!-- Font Awesome (icons). If blocked, content still works. -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" />

<style>
  /* =========================================================
     BEACH & SEA GLASSMORPHISM THEME
     Palette:
     Deep Ocean #0A2472
     Shallow Aqua #4AD9D9
     Sand #F4E4C1
     Coral #FF6B6B
     Seafoam #9FE6D9
     ========================================================= */

  :root{
    --ocean-deep:#0A2472;
    --ocean-mid:#114B9B;
    --ocean-surf:#4AD9D9;
    --seafoam:#9FE6D9;
    --sand:#F4E4C1;
    --coral:#FF6B6B;
    --glass: rgba(255,255,255,0.26);
    --glass-2: rgba(74,217,217,0.15);
    --glass-border: rgba(255,255,255,0.55);
    --shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
    --shadow-strong: 0 12px 46px 0 rgba(31, 38, 135, 0.52);
    --radius: 20px;
  }

  /* Light/Dark adaptation while preserving beach vibe */
  @media (prefers-color-scheme: dark){
    :root{
      --glass: rgba(10, 36, 114, 0.20);
      --glass-2: rgba(74,217,217,0.12);
      --glass-border: rgba(159,230,217,0.35);
      --shadow: 0 10px 34px 0 rgba(0, 0, 0, 0.45);
      --shadow-strong: 0 14px 52px 0 rgba(0, 0, 0, 0.60);
    }
  }

  /* Container background: sky + sun + sea + sand */
  .beach-wrap{
    position: relative;
    border-radius: 26px;
    padding: 28px 18px;
    overflow: hidden;
    background:
      radial-gradient(600px 300px at 92% 12%, rgba(255, 214, 102, 0.85), rgba(255, 214, 102, 0.00) 60%),
      radial-gradient(420px 240px at 12% 18%, rgba(159,230,217,0.55), rgba(159,230,217,0.00) 70%),
      linear-gradient(180deg, rgba(74,217,217,0.55) 0%, rgba(10,36,114,0.92) 55%, rgba(10,36,114,0.96) 68%, rgba(244,228,193,0.92) 100%);
    border: 1px solid rgba(255,255,255,0.22);
  }

  /* Animated wave bands */
  .wave-band{
    position:absolute;
    left:-10%;
    right:-10%;
    height: 120px;
    opacity: 0.55;
    filter: blur(0px);
    pointer-events:none;
    background: radial-gradient(closest-side, rgba(255,255,255,0.30), rgba(255,255,255,0.00) 70%);
    animation: drift 10s linear infinite;
    mix-blend-mode: soft-light;
  }
  .wave1{ top: 210px; animation-duration: 12s; opacity:0.40; }
  .wave2{ top: 350px; animation-duration: 16s; opacity:0.30; }
  .wave3{ top: 520px; animation-duration: 22s; opacity:0.22; }
  @keyframes drift{
    0% { transform: translateX(-2%) }
    50% { transform: translateX(2%) }
    100% { transform: translateX(-2%) }
  }

  /* Bubble animation (optional, subtle) */
  .bubble{
    position:absolute;
    bottom:-40px;
    width: 10px;
    height: 10px;
    border-radius: 999px;
    background: rgba(255,255,255,0.35);
    box-shadow: 0 0 18px rgba(159,230,217,0.35);
    animation: bubbleUp 9s linear infinite;
    pointer-events:none;
  }
  @keyframes bubbleUp{
    0%   { transform: translateY(0) translateX(0); opacity:0.0; }
    15%  { opacity:0.45; }
    70%  { opacity:0.35; }
    100% { transform: translateY(-760px) translateX(26px); opacity:0.0; }
  }

  /* Glass card base */
  .glass{
    background: var(--glass);
    border: 1px solid var(--glass-border);
    box-shadow: var(--shadow);
    border-radius: var(--radius);
    padding: 25px;
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    position: relative;
    overflow:hidden;
  }

  /* Gradient edge + inner glow */
  .glass::before{
    content:"";
    position:absolute;
    inset:-2px;
    border-radius: calc(var(--radius) + 2px);
    padding: 2px;
    background: linear-gradient(135deg,
      rgba(255,255,255,0.65),
      rgba(74,217,217,0.35),
      rgba(255,107,107,0.28),
      rgba(159,230,217,0.30)
    );
    -webkit-mask:
      linear-gradient(#000 0 0) content-box,
      linear-gradient(#000 0 0);
    -webkit-mask-composite: xor;
            mask-composite: exclude;
    opacity: 0.70;
    pointer-events:none;
  }
  .glass::after{
    content:"";
    position:absolute;
    inset: 0;
    background: radial-gradient(800px 220px at 10% 0%, rgba(255,255,255,0.30), rgba(255,255,255,0.00) 55%);
    opacity: 0.65;
    pointer-events:none;
  }

  /* Hover interaction (touch-friendly) */
  .hover{
    transition: transform .18s ease, box-shadow .18s ease, filter .18s ease;
  }
  .hover:hover{
    transform: scale(1.02);
    box-shadow: var(--shadow-strong);
    filter: saturate(1.06);
  }

  /* Shine sweep on hover */
  .shine{
    position: relative;
  }
  .shine:hover .shine-sweep{
    transform: translateX(140%);
    opacity: 1;
  }
  .shine-sweep{
    position:absolute;
    top:-40%;
    left:-60%;
    width: 60%;
    height: 180%;
    background: linear-gradient(120deg,
      rgba(255,255,255,0.00),
      rgba(255,255,255,0.20),
      rgba(255,255,255,0.00)
    );
    transform: translateX(0%);
    opacity: 0.0;
    transition: transform .70s ease, opacity .50s ease;
    pointer-events:none;
  }

  /* Typography */
  .title{
    font-size: 34px;
    line-height: 1.08;
    margin: 0;
    letter-spacing: 0.4px;
    font-weight: 800;
    color: rgba(255,255,255,0.96);
    text-shadow: 0 10px 30px rgba(0,0,0,0.28);
  }
  .subtitle{
    margin: 8px 0 0 0;
    font-size: 16px;
    letter-spacing: 0.3px;
    color: rgba(255,255,255,0.90);
  }
  .muted{
    color: rgba(255,255,255,0.85);
  }
  .sand{
    color: rgba(244,228,193,0.98);
  }
  .coral{
    color: rgba(255,107,107,0.98);
  }
  .pill{
    display:inline-block;
    padding: 6px 10px;
    border-radius: 999px;
    border: 1px solid rgba(255,255,255,0.45);
    background: rgba(255,255,255,0.14);
    font-size: 12px;
    margin: 4px 6px 0 0;
    white-space: nowrap;
  }

  /* Layout helpers */
  .grid{
    width:100%;
    border-collapse: separate;
    border-spacing: 14px;
  }
  .tight{
    border-spacing: 12px;
  }

  /* Mini glass cards */
  .mini{
    padding: 14px 14px;
    border-radius: 16px;
    background: var(--glass-2);
  }
  .mini strong{ color: rgba(255,255,255,0.95); }
  .mini span{ color: rgba(255,255,255,0.85); font-size: 12px; }

  /* Responsive: stack columns on small screens */
  @media (max-width: 760px){
    .title{ font-size: 28px; }
    .subtitle{ font-size: 14px; }
    .grid{ border-spacing: 10px; }
  }

  /* SVG divider wrapper */
  .divider{
    margin: 10px 0 0 0;
  }

  /* Link buttons */
  .btn{
    display:inline-block;
    padding: 9px 12px;
    border-radius: 14px;
    border: 1px solid rgba(255,255,255,0.55);
    background: rgba(255,255,255,0.16);
    color: rgba(255,255,255,0.95);
    text-decoration: none;
    font-weight: 700;
    transition: transform .18s ease, box-shadow .18s ease, background .18s ease;
  }
  .btn:hover{
    transform: translateY(-1px);
    background: rgba(74,217,217,0.18);
    box-shadow: 0 10px 28px rgba(0,0,0,0.22);
  }
  .btn-coral:hover{
    background: rgba(255,107,107,0.18);
  }

  /* Small section headers */
  .h{
    margin: 0 0 10px 0;
    font-size: 18px;
    color: rgba(255,255,255,0.96);
    letter-spacing: 0.3px;
  }
  .hr{
    height: 1px;
    background: linear-gradient(90deg, rgba(255,255,255,0.05), rgba(255,255,255,0.45), rgba(255,255,255,0.05));
    border: 0;
    margin: 14px 0;
  }

  /* Decorative floaters */
  .floater{
    position:absolute;
    opacity: 0.45;
    filter: drop-shadow(0 14px 22px rgba(0,0,0,0.18));
    animation: floaty 6.5s ease-in-out infinite;
    pointer-events:none;
  }
  .floater.f1{ top: 18px; left: 16px; animation-duration: 7.2s; }
  .floater.f2{ top: 110px; right: 18px; animation-duration: 8.1s; }
  .floater.f3{ bottom: 24px; left: 22px; animation-duration: 9.0s; opacity:0.35; }
  @keyframes floaty{
    0%,100%{ transform: translateY(0px) }
    50%{ transform: translateY(-10px) }
  }

  /* Accessibility: reduce motion */
  @media (prefers-reduced-motion: reduce){
    .wave-band, .bubble, .floater{ animation: none !important; }
    .hover, .btn, .shine-sweep{ transition: none !important; }
  }
</style>

<div class="beach-wrap">

  <!-- Decorative floaters -->
  <div class="floater f1">🐚</div>
  <div class="floater f2">🌺</div>
  <div class="floater f3">⭐</div>

  <!-- Animated waves (soft bands) -->
  <div class="wave-band wave1"></div>
  <div class="wave-band wave2"></div>
  <div class="wave-band wave3"></div>

  <!-- Bubbles -->
  <div class="bubble" style="left:10%; animation-delay:0s; width:8px; height:8px;"></div>
  <div class="bubble" style="left:18%; animation-delay:1.2s; width:12px; height:12px;"></div>
  <div class="bubble" style="left:32%; animation-delay:2.6s; width:7px; height:7px;"></div>
  <div class="bubble" style="left:55%; animation-delay:0.9s; width:10px; height:10px;"></div>
  <div class="bubble" style="left:72%; animation-delay:2.1s; width:9px; height:9px;"></div>
  <div class="bubble" style="left:86%; animation-delay:1.7s; width:13px; height:13px;"></div>

  <!-- =======================================================
       1) HEADER (Top card)
       ======================================================= -->
  <div class="glass hover shine" style="margin: 6px auto 16px auto; max-width: 1060px;">
    <div class="shine-sweep"></div>

    <div align="center">
      <!-- ASCII Wave Art -->
      <pre style="margin:0; font-weight:700; color: rgba(255,255,255,0.90); line-height: 1.05; font-size: 12px; white-space: pre; overflow-x: auto;">
 ~~~  ~~~~   ~~~~~  ~~~~   ~~~  ~~~~~~   ~~~~  ~~~
   ~~~~   ~~~~~~   ~~~~  ~~~~~   ~~~~  ~~~~~
 ~~~~~~  ~~~~   ~~~   ~~~~~~   ~~~~   ~~~~~~
      </pre>

      <h1 class="title" style="font-family: ui-rounded, system-ui, -apple-system, Segoe UI, Roboto, Arial;">
        Hi, I’m <span class="sand">Your Name</span>
      </h1>

      <p class="subtitle">
        <strong class="sand">Software Developer</strong> • <span class="coral">UI/UX</span> • <strong>Open Source</strong>
        <span class="muted">— making products that feel like a perfect beach day</span>
        <br/>
        🌊 🏄‍♂️ 🌴 <span class="muted">Building smooth experiences & making waves in code</span>
        <br/>
        <span class="muted">📍</span> 🐠 <span class="muted">Your City, Your Country</span>
      </p>

      <!-- Wave divider SVG -->
      <div class="divider" style="max-width: 860px; margin: 14px auto 0 auto;">
        <svg width="100%" height="50" viewBox="0 0 1200 120" preserveAspectRatio="none" aria-hidden="true">
          <path d="M0,32 C150,80 350,0 600,38 C850,76 1050,10 1200,44 L1200,120 L0,120 Z"
                fill="rgba(255,255,255,0.18)"></path>
          <path d="M0,52 C140,10 320,110 600,60 C880,10 1060,90 1200,58 L1200,120 L0,120 Z"
                fill="rgba(74,217,217,0.16)"></path>
        </svg>
      </div>

      <p class="muted" style="margin: 8px 0 0 0; font-size: 13px;">
        <em>“I navigate complex problems like tides: steady, curious, and always heading toward clarity.”</em>
      </p>
    </div>
  </div>

  <!-- =======================================================
       2) ABOUT ME
       ======================================================= -->
  <div class="glass hover shine" style="margin: 0 auto 16px auto; max-width: 1060px;">
    <div class="shine-sweep"></div>

    <h2 class="h">🏖️ About Me</h2>
    <p class="muted" style="margin: 0;">
      I’m a developer who loves crafting <strong>clean, buoyant UI</strong> and <strong>reliable systems</strong>.
      My coding journey feels like island-hopping—each project a new shore, each bug a hidden reef, and every release a smooth sail into open water. ⛵
    </p>

    <hr class="hr"/>

    <table class="grid tight">
      <tr>
        <td class="glass mini hover" style="width: 50%; vertical-align: top;">
          <div style="display:flex; gap:10px; align-items:center;">
            <div style="font-size: 18px;">🌊</div>
            <div>
              <strong>Currently sailing through:</strong><br/>
              <span>• Building: <em>your current project</em><br/>• Learning: <em>your next tech</em><br/>• Exploring: <em>design systems / performance</em></span>
            </div>
          </div>
        </td>
        <td class="glass mini hover" style="width: 50%; vertical-align: top;">
          <div style="display:flex; gap:10px; align-items:center;">
            <div style="font-size: 18px;">⚓</div>
            <div>
              <strong>Anchored in:</strong><br/>
              <span>• Frontend craft • API design • Testing • Accessibility • DX</span>
            </div>
          </div>
        </td>
      </tr>
      <tr>
        <td class="glass mini hover" style="vertical-align: top;">
          <div style="display:flex; gap:10px; align-items:center;">
            <div style="font-size: 18px;">🐬</div>
            <div>
              <strong>Fun fact:</strong><br/>
              <span>I refactor like a dolphin swims—fast, graceful, and always surfacing for clean air (readability).</span>
            </div>
          </div>
        </td>
        <td class="glass mini hover" style="vertical-align: top;">
          <div style="display:flex; gap:10px; align-items:center;">
            <div style="font-size: 18px;">🌞</div>
            <div>
              <strong>What I value:</strong><br/>
              <span>Calm UX, crisp code, kind collaboration, and shipping with confidence.</span>
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>

  <!-- =======================================================
       3) SKILLS & TOOLS (mini glass grid)
       ======================================================= -->
  <div class="glass hover shine" style="margin: 0 auto 16px auto; max-width: 1060px;">
    <div class="shine-sweep"></div>

    <h2 class="h">🧜‍♀️ Skills & Tools</h2>
    <p class="muted" style="margin-top:0;">
      A beach bag of tools I bring to each build—picked for performance, polish, and smooth sailing.
    </p>

    <table class="grid" role="presentation">
      <tr>
        <td class="glass mini hover" style="vertical-align: top;">
          <strong><i class="fa-solid fa-code"></i> Languages</strong><br/>
          <span>
            <span class="pill">JavaScript</span>
            <span class="pill">TypeScript</span>
            <span class="pill">Python</span>
            <span class="pill">Go</span>
          </span>
        </td>
        <td class="glass mini hover" style="vertical-align: top;">
          <strong><i class="fa-solid fa-layer-group"></i> Frameworks</strong><br/>
          <span>
            <span class="pill">React</span>
            <span class="pill">Next.js</span>
            <span class="pill">Node.js</span>
            <span class="pill">FastAPI</span>
          </span>
        </td>
        <td class="glass mini hover" style="vertical-align: top;">
          <strong><i class="fa-solid fa-palette"></i> UI/UX</strong><br/>
          <span>
            <span class="pill">Design Systems</span>
            <span class="pill">Tailwind</span>
            <span class="pill">Framer Motion</span>
            <span class="pill">A11y</span>
          </span>
        </td>
      </tr>
      <tr>
        <td class="glass mini hover" style="vertical-align: top;">
          <strong><i class="fa-solid fa-screwdriver-wrench"></i> Tooling</strong><br/>
          <span>
            <span class="pill">Git</span>
            <span class="pill">Docker</span>
            <span class="pill">CI/CD</span>
            <span class="pill">Vite</span>
          </span>
        </td>
        <td class="glass mini hover" style="vertical-align: top;">
          <strong><i class="fa-solid fa-database"></i> Data</strong><br/>
          <span>
            <span class="pill">PostgreSQL</span>
            <span class="pill">Redis</span>
            <span class="pill">Prisma</span>
            <span class="pill">ORMs</span>
          </span>
        </td>
        <td class="glass mini hover" style="vertical-align: top;">
          <strong><i class="fa-solid fa-shield-halved"></i> Quality</strong><br/>
          <span>
            <span class="pill">Testing</span>
            <span class="pill">Observability</span>
            <span class="pill">Linting</span>
            <span class="pill">Performance</span>
          </span>
        </td>
      </tr>
    </table>

    <p class="muted" style="margin: 2px 0 0 0; font-size: 12px;">
      Tip: Replace the pills with your actual stack for a sharper “who you are” signal.
    </p>
  </div>

  <!-- =======================================================
       4) GITHUB STATS
       ======================================================= -->
  <div class="glass hover shine" style="margin: 0 auto 16px auto; max-width: 1060px;">
    <div class="shine-sweep"></div>

    <h2 class="h">🌊 GitHub Stats (Making Waves)</h2>
    <p class="muted" style="margin-top:0;">
      Ocean blues + coral accents, served in glass.
    </p>

    <div align="center">
      <!-- GitHub Readme Stats -->
      <img
        alt="GitHub Stats"
        height="165"
        src="https://github-readme-stats.vercel.app/api?username=isgr9801&show_icons=true&rank_icon=github&title_color=4AD9D9&icon_color=FF6B6B&text_color=F4E4C1&bg_color=0A2472&border_color=9FE6D9"
      />
      <img
        alt="Top Languages"
        height="165"
        src="https://github-readme-stats.vercel.app/api/top-langs/?username=isgr9801&layout=compact&title_color=4AD9D9&text_color=F4E4C1&bg_color=0A2472&border_color=9FE6D9"
      />
      <br/>
      <!-- Streak -->
      <img
        alt="GitHub Streak"
        height="165"
        src="https://streak-stats.demolab.com?user=isgr9801&theme=transparent&ring=FF6B6B&fire=FF6B6B&currStreakLabel=4AD9D9&sideLabels=4AD9D9&dates=F4E4C1&stroke=9FE6D9&border=9FE6D9"
      />
      <br/>
      <!-- Trophies -->
      <img
        alt="Trophy Showcase"
        src="https://github-profile-trophy.vercel.app/?username=isgr9801&theme=algolia&no-frame=true&no-bg=true&margin-w=10&margin-h=10&column=6"
      />
    </div>

    <hr class="hr"/>
    <p class="muted" style="margin:0; font-size: 12px;">
      If any widget is down, your README still looks great—these are just the sparkling sea spray on top.
    </p>
  </div>

  <!-- =======================================================
       5) PROJECT SHOWCASE (2-3 featured)
       ======================================================= -->
  <div class="glass hover shine" style="margin: 0 auto 16px auto; max-width: 1060px;">
    <div class="shine-sweep"></div>

    <h2 class="h">🏝️ Project Showcase</h2>
    <p class="muted" style="margin-top:0;">
      Featured builds that (hopefully) feel like a calm shoreline: simple, elegant, and strong underneath.
    </p>

    <table class="grid" role="presentation">
      <tr>
        <td class="glass mini hover" style="vertical-align: top;">
          <h3 style="margin:0; color: rgba(255,255,255,0.96);">🐋 Project One — “Deep Sea Dashboard”</h3>
          <p class="muted" style="margin:8px 0 10px 0;">
            A data experience that dives deep without feeling heavy—smooth charts, crisp filters, and reef-safe performance.
          </p>
          <div>
            <span class="pill">TypeScript</span>
            <span class="pill">React</span>
            <span class="pill">Charts</span>
            <span class="pill">A11y</span>
          </div>
          <p class="muted" style="margin: 10px 0 0 0;">
            Status: <strong class="sand">Smooth sailing</strong> ⛵
          </p>
          <div style="margin-top: 12px;">
            <a class="btn" href="https://github.com/isgr9801" target="_blank" rel="noreferrer noopener">
              🌊 Repo
            </a>
            <a class="btn btn-coral" href="https://example.com" target="_blank" rel="noreferrer noopener">
              🏄 Live
            </a>
          </div>
        </td>

        <td class="glass mini hover" style="vertical-align: top;">
          <h3 style="margin:0; color: rgba(255,255,255,0.96);">🐙 Project Two — “Octo Automations”</h3>
          <p class="muted" style="margin:8px 0 10px 0;">
            GitHub workflows that wrap around repetitive tasks like helpful tentacles—releases, checks, and tidy pipelines.
          </p>
          <div>
            <span class="pill">GitHub Actions</span>
            <span class="pill">CI/CD</span>
            <span class="pill">Docker</span>
            <span class="pill">Quality Gates</span>
          </div>
          <p class="muted" style="margin: 10px 0 0 0;">
            Status: <strong class="coral">Making waves</strong> 🌊
          </p>
          <div style="margin-top: 12px;">
            <a class="btn" href="https://github.com/isgr9801" target="_blank" rel="noreferrer noopener">
              🌊 Repo
            </a>
            <a class="btn btn-coral" href="https://example.com" target="_blank" rel="noreferrer noopener">
              🏖️ Demo
            </a>
          </div>
        </td>
      </tr>

      <tr>
        <td class="glass mini hover" style="vertical-align: top;">
          <h3 style="margin:0; color: rgba(255,255,255,0.96);">🐚 Project Three — “Shell Notes”</h3>
          <p class="muted" style="margin:8px 0 10px 0;">
            A lightweight notes app—quiet UI, strong structure, and quick search that feels like finding seashells at low tide.
          </p>
          <div>
            <span class="pill">Next.js</span>
            <span class="pill">SQLite</span>
            <span class="pill">Search</span>
            <span class="pill">PWA</span>
          </div>
          <p class="muted" style="margin: 10px 0 0 0;">
            Status: <strong class="sand">Smooth sailing</strong> ⚓
          </p>
          <div style="margin-top: 12px;">
            <a class="btn" href="https://github.com/isgr9801" target="_blank" rel="noreferrer noopener">
              🌊 Repo
            </a>
            <a class="btn btn-coral" href="https://example.com" target="_blank" rel="noreferrer noopener">
              🌅 Live
            </a>
          </div>
        </td>

        <td class="glass mini hover" style="vertical-align: top;">
          <h3 style="margin:0; color: rgba(255,255,255,0.96);">🌴 Want yours here?</h3>
          <p class="muted" style="margin:8px 0 10px 0;">
            Pin your best repos on GitHub, then replace these cards with real project links.
          </p>
          <div>
            <span class="pill">Pinned Repos</span>
            <span class="pill">Case Studies</span>
            <span class="pill">Screenshots</span>
          </div>
          <div style="margin-top: 12px;">
            <a class="btn" href="https://github.com/isgr9801?tab=repositories" target="_blank" rel="noreferrer noopener">
              🏝️ Browse Repos
            </a>
          </div>
        </td>
      </tr>
    </table>
  </div>

  <!-- =======================================================
       6) CONTRIBUTIONS / TIDE CHART
       ======================================================= -->
  <div class="glass hover shine" style="margin: 0 auto 16px auto; max-width: 1060px;">
    <div class="shine-sweep"></div>

    <h2 class="h">📈 Tide Chart (Contributions)</h2>
    <p class="muted" style="margin-top:0;">
      Like tides, consistency beats intensity—small waves build strong shores.
    </p>

    <div align="center">
      <!-- Contribution "gradient-ish" via a generator (service-dependent) -->
      <img
        alt="Contribution Graph"
        src="https://github-readme-activity-graph.vercel.app/graph?username=isgr9801&bg_color=0A2472&color=F4E4C1&line=4AD9D9&point=FF6B6B&area=true&area_color=9FE6D9&hide_border=true"
      />
    </div>

    <hr class="hr"/>

    <table class="grid tight" role="presentation">
      <tr>
        <td class="glass mini hover" style="vertical-align: top; width: 50%;">
          <strong>🌊 Current activity</strong><br/>
          <span>
            • Shipping improvements with a “one small wave per day” rhythm<br/>
            • Keeping PRs reviewable and commits tidy
          </span>
        </td>
        <td class="glass mini hover" style="vertical-align: top; width: 50%;">
          <strong>⛵ Tide forecast</strong><br/>
          <span>
            • Next up: documentation polish + test coverage<br/>
            • Longer horizon: performance & DX upgrades
          </span>
        </td>
      </tr>
    </table>
  </div>

  <!-- =======================================================
       7) CONTACT & SOCIALS (horizontal row)
       ======================================================= -->
  <div class="glass hover shine" style="margin: 0 auto 16px auto; max-width: 1060px;">
    <div class="shine-sweep"></div>

    <h2 class="h">📬 Contact & Socials</h2>
    <p class="muted" style="margin-top:0;">
      Let’s build something that feels like summer—bright, calm, and unforgettable. 🌅
    </p>

    <div style="display:flex; flex-wrap: wrap; gap: 10px;">
      <a class="btn" href="https://www.linkedin.com/in/your-handle/" target="_blank" rel="noreferrer noopener">
        <i class="fa-brands fa-linkedin"></i> LinkedIn
      </a>
      <a class="btn" href="https://x.com/your-handle" target="_blank" rel="noreferrer noopener">
        <i class="fa-brands fa-x-twitter"></i> X
      </a>
      <a class="btn" href="https://dev.to/your-handle" target="_blank" rel="noreferrer noopener">
        <i class="fa-brands fa-dev"></i> Blog
      </a>
      <a class="btn btn-coral" href="mailto:you@example.com" target="_blank" rel="noreferrer noopener">
        📯 Email
      </a>
      <a class="btn" href="https://your-portfolio.example" target="_blank" rel="noreferrer noopener">
        🌴 Portfolio
      </a>
      <a class="btn" href="https://github.com/isgr9801" target="_blank" rel="noreferrer noopener">
        <i class="fa-brands fa-github"></i> GitHub
      </a>
    </div>
  </div>

  <!-- =======================================================
       EXTRA: Now Playing (Spotify) + Blog Posts (buoy icons)
       ======================================================= -->
  <div class="glass hover shine" style="margin: 0 auto 16px auto; max-width: 1060px;">
    <div class="shine-sweep"></div>

    <h2 class="h">🎧 Now Playing (Beach / Lo‑fi)</h2>
    <p class="muted" style="margin-top:0;">
      Optional widget. Replace the link to your Spotify “recently played” badge provider of choice.
    </p>

    <div align="center">
      <!-- Example: Spotify GitHub Profile (requires you set up token on their service) -->
      <img
        alt="Spotify Now Playing"
        src="https://spotify-github-profile.kittinanx.com/api/view?uid=YOUR_SPOTIFY_USER_ID&cover_image=true&theme=default&show_offline=false&background_color=0A2472&interchange=false&bar_color=4AD9D9&bar_color_cover=true"
      />
    </div>

    <hr class="hr"/>

    <h2 class="h">🛟 Latest Blog Posts</h2>
    <p class="muted" style="margin-top:0;">
      Add a GitHub Action later to auto-update this list (e.g., from RSS).
    </p>

    <ul class="muted" style="margin: 0; padding-left: 18px;">
      <li>🛟 <a href="https://example.com/post-1" target="_blank" rel="noreferrer noopener" style="color: rgba(244,228,193,0.98);">Designing glassmorphism that stays readable</a></li>
      <li>🛟 <a href="https://example.com/post-2" target="_blank" rel="noreferrer noopener" style="color: rgba(244,228,193,0.98);">Shipping calm UI: motion, contrast, and accessibility</a></li>
      <li>🛟 <a href="https://example.com/post-3" target="_blank" rel="noreferrer noopener" style="color: rgba(244,228,193,0.98);">CI that feels effortless: workflow patterns that scale</a></li>
    </ul>

    <p class="muted" style="margin: 12px 0 0 0; font-size: 12px;">
      <!-- Dynamic content hint -->
      <strong>Dynamic content idea:</strong> Use a workflow that runs daily and rewrites this section from your RSS feed.
    </p>
  </div>

  <!-- =======================================================
       8) FOOTER
       ======================================================= -->
  <div class="glass hover shine" style="margin: 0 auto 6px auto; max-width: 1060px;">
    <div class="shine-sweep"></div>

    <div align="center">
      <h2 class="h" style="margin-bottom: 6px;">🌊 Catch a wave — ride the tide</h2>
      <p class="muted" style="margin: 0 0 12px 0;">
        Thanks for stopping by. If something here inspires you, let’s collaborate. 🐠
      </p>

      <!-- Visitor counter (service-dependent) -->
      <a href="https://github.com/isgr9801" target="_blank" rel="noreferrer noopener" style="text-decoration:none;">
        <img
          alt="Visitor Counter"
          src="https://komarev.com/ghpvc/?username=isgr9801&label=Visitors%20%F0%9F%8C%8A&color=0A2472&style=for-the-badge"
        />
      </a>

      <p class="muted" style="margin: 12px 0 0 0; font-size: 12px;">
        Last updated: <strong class="sand">2026-03-01</strong> 🌅
        <br/>
        <span class="muted">©</span> <span class="sand">Your Name</span> <span class="muted">•</span> <span class="muted">🐟</span> <span class="muted">All rights reserved</span>
      </p>

      <!-- Horizon line -->
      <div style="height:10px; margin-top: 14px; width: min(760px, 96%); border-radius: 999px;
        background: linear-gradient(90deg, rgba(244,228,193,0.0), rgba(244,228,193,0.55), rgba(74,217,217,0.25), rgba(244,228,193,0.0));
        border: 1px solid rgba(255,255,255,0.18);">
      </div>
    </div>
  </div>

</div>

<!--
  Quick Personalization Checklist:
  - Replace "Your Name", title, location
  - Update social links, email, portfolio
  - Replace projects with real repo/demo links
  - (Optional) Add screenshots via <img> in project cards
  - (Optional) Set up RSS-to-README GitHub Action for blog posts
  - (Optional) Configure Spotify widget with your user ID / token
-->
