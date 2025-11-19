---
title: Chatbot
---

<header class="site-header" role="banner">
  <div class="brand">
    <div class="logo" aria-hidden="true">🤖</div>
    <div>
      <h1>Udify Chat</h1>
      <p class="tag">Ask anything — voice & text supported</p>
    </div>
  </div>

  <div class="controls">
    <button id="themeToggle" class="icon-btn" aria-label="Toggle theme">🌙</button>
    <button id="shareBtn" class="icon-btn" aria-label="Share link">🔗</button>
    <button id="infoToggle" class="icon-btn" aria-label="Open info">❔</button>
  </div>
</header>

<div class="layout">
  <aside class="meta" id="metaPanel" aria-hidden="false">
    <div class="meta-inner">
      <h2>About this bot</h2>
      <p>Voice-enabled assistant hosted on Udify. Helpful for quick research, debugging, and casual chat. Uses microphone permission if you allow it.</p>

      <h3>Quick tips</h3>
      <ul>
        <li>Click the mic icon inside the chat to speak.</li>
        <li>Use the theme toggle for dark/light modes.</li>
        <li>On mobile, tap the floating button to open this panel.</li>
      </ul>

      <h3>FAQ</h3>
      <details>
        <summary>Embed blank?</summary>
        If the iframe is blank, the host may block embedding. Try opening the bot link directly to verify.
      </details>

      <div class="meta-footer">
        <small>Made with ❤️ · GitHub Pages</small>
      </div>
    </div>
  </aside>

  <main class="chat-area" id="chatArea" role="main">
    <div class="chat-shell">
      <!-- Visible fixed-size box with native panning inside -->
      <div class="iframe-wrap" id="iframeWrap" tabindex="0" aria-label="Chat iframe wrapper">
        <iframe id="chatFrame"
                src="https://udify.app/chatbot/sI7tIcJbUKYk9pHy"
                title="Udify Chatbot"
                allow="microphone"
                frameborder="0"
                sandbox="allow-scripts allow-same-origin allow-forms">
        </iframe>
      </div>
    </div>
  </main>
</div>

<button id="fab" class="fab" aria-label="Open info">❔</button>

<style>
/* ---------- Change these if you want different sizes ---------- */
:root{
  --embed-width: 1000px;   /* inner iframe width (controls horizontal pan area) */
  --embed-height: 600px;   /* visible box height (same on desktop & mobile) */
  --bg-1: #0f172a; --bg-2: #0b1226;
  --text: #e6eef8; --muted: #9aa6b2; --accent: #60a5fa;
  --glass: rgba(255,255,255,0.06); --radius:14px;
}
[data-theme="light"]{
  --bg-1:#f7f9fc; --bg-2:#eef2fb; --text:#0b1220; --muted:#4b5563; --accent:#2563eb; --glass:rgba(255,255,255,0.7);
}
*{box-sizing:border-box}
html,body{height:100%}
body{
  margin:0; font-family:Inter, system-ui, -apple-system, "Segoe UI", Roboto, Arial;
  color:var(--text);
  background:linear-gradient(160deg,var(--bg-1),var(--bg-2));
  padding:18px; -webkit-font-smoothing:antialiased;
}

/* header & controls */
.site-header{display:flex;justify-content:space-between;align-items:center;max-width:1200px;margin:0 auto 12px;z-index:2}
.brand{display:flex;align-items:center;gap:12px}
.logo{width:48px;height:48px;border-radius:10px;display:grid;place-items:center;font-size:22px;background:linear-gradient(135deg,#1e3a8a,#60a5fa)}
.brand h1{margin:0;font-size:17px;color:var(--text)}
.tag{margin:0;color:var(--muted);font-size:13px}
.controls{display:flex;gap:8px}
.icon-btn{background:var(--glass);border:0;padding:8px 10px;border-radius:10px;cursor:pointer}

/* layout */
.layout{display:grid;grid-template-columns:300px 1fr;gap:18px;max-width:1100px;margin:0 auto;align-items:start;z-index:2}
.meta{background:linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.02));border-radius:12px;padding:16px;color:var(--text);box-shadow:0 8px 24px rgba(2,6,23,0.5);backdrop-filter:blur(6px);border:1px solid rgba(255,255,255,0.03)}
.meta p, .meta ul li, .meta details summary{color:var(--text)}
.meta ul{padding-left:18px;margin:6px 0 12px}
.meta-footer{margin-top:18px;color:var(--muted);font-size:13px}

/* chat card */
.chat-area{display:flex;align-items:flex-start;justify-content:center}
.chat-shell{
  width:100%;
  border-radius:12px;
  padding:10px;
  background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
  box-shadow: 0 14px 32px rgba(2,6,23,0.5);
  border:1px solid rgba(255,255,255,0.03);
  overflow:hidden;
  display:flex; flex-direction:column;
}

/* wrapper: fixed visible box that doesn't grow the page */
.iframe-wrap{
  width:100%;
  height: var(--embed-height);        /* visible box height */
  max-height: var(--embed-height);
  overflow:auto;                      /* enables horizontal & vertical scroll inside the box */
  -webkit-overflow-scrolling: touch;
  border-radius:10px;
  background:transparent;
  outline:none;
  display:block;
}

/* desktop: iframe fills width of container and matches visible height */
.iframe-wrap iframe{
  display:block;
  width:100%;
  height: var(--embed-height);
  border:0;
  border-radius:10px;
  background:transparent;
  max-width:100%;
}

/* mobile: inner iframe becomes wider than wrapper so you can scroll left/right */
@media (max-width:900px){
  body{padding:12px}
  .layout{grid-template-columns:1fr;gap:12px;margin-bottom:80px}
  .meta{
    position:fixed; right:12px; top:68px; width:82%; max-width:420px; transform:translateX(110%); transition:transform .26s cubic-bezier(.2,.9,.3,1);
    box-shadow:0 28px 56px rgba(2,6,23,0.5); display:block; height:calc(100vh - 92px); overflow:auto;
  }
  .meta.open{transform:translateX(0)}
  .chat-shell{padding:8px}

  /* Keep the visible box small (same as desktop). The iframe inside is wider for panning. */
  .iframe-wrap{
    height: var(--embed-height);
    max-height: var(--embed-height);
    overflow:auto;
    -webkit-overflow-scrolling: touch;
    border-radius:8px;
  }

  .iframe-wrap iframe{
    width: var(--embed-width);   /* intentionally wider than wrapper for horizontal pan */
    height: var(--embed-height);
    max-width: none;
    border-radius:6px;
    display:block;
  }

  .fab{display:block}
  .site-header{margin-bottom:8px}
}

/* small desktop tweak */
@media (min-width:1200px){
  .layout{max-width:1200px}
}

/* light-mode tweaks */
[data-theme="light"] .brand h1, [data-theme="light"] .tag{color:var(--text)}
</style>

<script>
/* Theme toggle */
(function(){
  const btn = document.getElementById('themeToggle');
  const stored = localStorage.getItem('theme') || (window.matchMedia && window.matchMedia('(prefers-color-scheme: light)').matches ? 'light' : 'dark');
  if(stored === 'light') document.documentElement.setAttribute('data-theme','light');

  btn.addEventListener('click', ()=>{
    const isDark = document.documentElement.getAttribute('data-theme') !== 'light';
    if(isDark) {
      document.documentElement.setAttribute('data-theme','light');
      localStorage.setItem('theme','light');
      btn.textContent='🌙';
    } else {
      document.documentElement.removeAttribute('data-theme');
      localStorage.setItem('theme','dark');
      btn.textContent='☀️';
    }
  });
})();

/* Info panel toggle & helpers */
(function(){
  const infoToggle = document.getElementById('infoToggle');
  const meta = document.getElementById('metaPanel');
  const fab = document.getElementById('fab');
  const shareBtn = document.getElementById('shareBtn');

  function openMeta() { meta.classList.add('open'); meta.setAttribute('aria-hidden','false'); }
  function closeMeta(){ meta.classList.remove('open'); meta.setAttribute('aria-hidden','true'); }

  infoToggle.addEventListener('click', ()=>{ meta.classList.toggle('open'); const open = meta.classList.contains('open'); meta.setAttribute('aria-hidden', !open); });
  fab.addEventListener('click', openMeta);

  document.addEventListener('click', (e)=>{
    if(window.innerWidth <= 900 && meta.classList.contains('open')){
      const inside = meta.contains(e.target) || e.target.id === 'fab' || e.target.id === 'infoToggle';
      if(!inside) closeMeta();
    }
  });

  shareBtn.addEventListener('click', async ()=>{
    const url = location.href;
    try { await navigator.clipboard.writeText(url); shareBtn.textContent = '✅'; setTimeout(()=> shareBtn.textContent = '🔗', 1400); }
    catch(e){ alert('Copy failed — please copy the URL manually.'); }
  });

  // Keyboard panning for accessibility
  const wrap = document.getElementById('iframeWrap');
  if(wrap) wrap.addEventListener('keydown', (e)=>{
    if(e.key === 'ArrowDown') { wrap.scrollBy({top:100, behavior:'smooth'}); e.preventDefault(); }
    if(e.key === 'ArrowUp') { wrap.scrollBy({top:-100, behavior:'smooth'}); e.preventDefault(); }
    if(e.key === 'ArrowRight') { wrap.scrollBy({left:100, behavior:'smooth'}); e.preventDefault(); }
    if(e.key === 'ArrowLeft') { wrap.scrollBy({left:-100, behavior:'smooth'}); e.preventDefault(); }
  });
})();
</script>
