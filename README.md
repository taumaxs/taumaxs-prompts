[taumaxs-prompts.html](https://github.com/user-attachments/files/27733053/taumaxs-prompts.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Taumaxs — Prompts IA</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Bebas+Neue&family=Inter:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --orange: #FE5516;
    --dark: #0A0A0A;
    --surface: #111111;
    --surface2: #1A1A1A;
    --border: #2A2A2A;
    --text: #E8E8E8;
    --muted: #666;
    --green: #22C55E;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--dark);
    color: var(--text);
    font-family: 'Inter', sans-serif;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* NOISE OVERLAY */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
    opacity: 0.5;
  }

  .container {
    max-width: 760px;
    margin: 0 auto;
    padding: 0 20px;
    position: relative;
    z-index: 1;
  }

  /* HEADER */
  header {
    padding: 48px 0 32px;
    border-bottom: 1px solid var(--border);
  }

  .brand-line {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 20px;
  }

  .brand-dot {
    width: 10px;
    height: 10px;
    background: var(--orange);
    border-radius: 50%;
    animation: pulse 2s ease-in-out infinite;
  }

  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.5; transform: scale(0.7); }
  }

  .brand-name {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    color: var(--orange);
    letter-spacing: 0.15em;
    text-transform: uppercase;
  }

  h1 {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(42px, 8vw, 72px);
    line-height: 0.95;
    letter-spacing: -0.01em;
    color: var(--text);
    margin-bottom: 16px;
  }

  h1 span {
    color: var(--orange);
  }

  .subtitle {
    font-size: 14px;
    color: var(--muted);
    line-height: 1.6;
    max-width: 500px;
    font-weight: 300;
  }

  /* STEPS LABEL */
  .steps-label {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.2em;
    color: var(--muted);
    text-transform: uppercase;
    padding: 40px 0 24px;
  }

  /* PROMPT CARD */
  .prompt-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    margin-bottom: 16px;
    overflow: hidden;
    transition: border-color 0.2s;
  }

  .prompt-card:hover {
    border-color: #3a3a3a;
  }

  .card-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 20px 24px;
    border-bottom: 1px solid var(--border);
    gap: 16px;
  }

  .card-meta {
    display: flex;
    align-items: center;
    gap: 14px;
    flex: 1;
    min-width: 0;
  }

  .step-badge {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 22px;
    color: var(--orange);
    line-height: 1;
    flex-shrink: 0;
    min-width: 32px;
  }

  .card-info {
    min-width: 0;
  }

  .card-title {
    font-size: 13px;
    font-weight: 500;
    color: var(--text);
    margin-bottom: 3px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .card-tag {
    display: inline-flex;
    align-items: center;
    gap: 4px;
    font-family: 'Space Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--muted);
    background: var(--surface2);
    border: 1px solid var(--border);
    padding: 2px 8px;
    border-radius: 4px;
  }

  .copy-btn {
    display: flex;
    align-items: center;
    gap: 8px;
    background: transparent;
    border: 1px solid var(--border);
    color: var(--muted);
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    padding: 8px 16px;
    border-radius: 6px;
    cursor: pointer;
    transition: all 0.15s ease;
    flex-shrink: 0;
    white-space: nowrap;
  }

  .copy-btn:hover {
    border-color: var(--orange);
    color: var(--orange);
  }

  .copy-btn.copied {
    border-color: var(--green);
    color: var(--green);
    animation: flash 0.3s ease;
  }

  @keyframes flash {
    0% { background: rgba(34, 197, 94, 0.15); }
    100% { background: transparent; }
  }

  .copy-icon {
    width: 12px;
    height: 12px;
    flex-shrink: 0;
  }

  .card-body {
    padding: 20px 24px;
  }

  .prompt-text {
    font-family: 'Space Mono', monospace;
    font-size: 11.5px;
    line-height: 1.75;
    color: #AAA;
    white-space: pre-wrap;
    word-break: break-word;
    max-height: 220px;
    overflow: hidden;
    position: relative;
    transition: max-height 0.4s ease;
  }

  .prompt-text.expanded {
    max-height: 2000px;
  }

  .prompt-text:not(.expanded)::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 60px;
    background: linear-gradient(transparent, var(--surface));
  }

  .expand-btn {
    background: none;
    border: none;
    color: var(--orange);
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    cursor: pointer;
    padding: 12px 0 0;
    display: block;
    transition: opacity 0.15s;
  }

  .expand-btn:hover { opacity: 0.7; }

  /* DIVIDER */
  .divider {
    display: flex;
    align-items: center;
    gap: 16px;
    padding: 16px 0;
  }

  .divider-line {
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  .divider-icon {
    font-size: 16px;
    opacity: 0.3;
  }

  /* CTA */
  .cta-block {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 32px 28px;
    margin: 40px 0 60px;
    position: relative;
    overflow: hidden;
  }

  .cta-block::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, var(--orange), transparent);
    opacity: 0.7;
  }

  .cta-eyebrow {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    color: var(--orange);
    letter-spacing: 0.2em;
    text-transform: uppercase;
    margin-bottom: 12px;
  }

  .cta-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 32px;
    line-height: 1;
    margin-bottom: 12px;
    color: var(--text);
  }

  .cta-text {
    font-size: 13px;
    color: var(--muted);
    line-height: 1.7;
    margin-bottom: 24px;
    font-weight: 300;
  }

  .cta-link {
    display: inline-flex;
    align-items: center;
    gap: 10px;
    background: var(--orange);
    color: #000;
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    font-weight: 700;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    text-decoration: none;
    padding: 14px 24px;
    border-radius: 6px;
    transition: all 0.15s ease;
  }

  .cta-link:hover {
    background: #FF6B2B;
    transform: translateY(-1px);
    box-shadow: 0 8px 24px rgba(254,85,22,0.3);
  }

  .cta-arrow {
    font-size: 14px;
    transition: transform 0.15s;
  }

  .cta-link:hover .cta-arrow {
    transform: translateX(3px);
  }

  /* FOOTER */
  footer {
    border-top: 1px solid var(--border);
    padding: 24px 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 12px;
    flex-wrap: wrap;
  }

  .footer-brand {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 18px;
    color: var(--muted);
    letter-spacing: 0.05em;
  }

  .footer-note {
    font-family: 'Space Mono', monospace;
    font-size: 9px;
    color: #3a3a3a;
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }

  /* COPY ALL */
  .copy-all-wrapper {
    padding: 0 0 28px;
    display: flex;
    justify-content: flex-end;
  }

  .copy-all-btn {
    display: flex;
    align-items: center;
    gap: 8px;
    background: var(--surface2);
    border: 1px solid var(--border);
    color: var(--muted);
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    padding: 10px 18px;
    border-radius: 6px;
    cursor: pointer;
    transition: all 0.15s ease;
  }

  .copy-all-btn:hover {
    border-color: var(--orange);
    color: var(--orange);
  }

  /* ENTRANCE ANIMATION */
  .prompt-card {
    opacity: 0;
    transform: translateY(16px);
    animation: slideUp 0.5s ease forwards;
  }

  .prompt-card:nth-child(1) { animation-delay: 0.1s; }
  .prompt-card:nth-child(2) { animation-delay: 0.22s; }

  @keyframes slideUp {
    to { opacity: 1; transform: translateY(0); }
  }

  @media (max-width: 480px) {
    .card-header { flex-wrap: wrap; }
    .copy-btn { width: 100%; justify-content: center; }
    .footer-note { display: none; }
  }
</style>
</head>
<body>
<div class="container">

  <header>
    <div class="brand-line">
      <div class="brand-dot"></div>
      <span class="brand-name">@taumaxs — Prompts IA</span>
    </div>
    <h1>CRIA<span>TI</span>VIDADE<br>SEM LIMITE</h1>
    <p class="subtitle">Copie os prompts abaixo e use em qualquer gerador de imagem ou vídeo com IA. Cole a sua foto de referência e bora.</p>
  </header>

  <p class="steps-label">// 02 prompts prontos para usar</p>

  <div class="cards-wrapper">

    <!-- CARD 01 -->
    <div class="prompt-card">
      <div class="card-header">
        <div class="card-meta">
          <span class="step-badge">01</span>
          <div class="card-info">
            <div class="card-title">Prompt — Imagem</div>
            <span class="card-tag">🖼️ Pode fazer em qualquer IA de foto</span>
          </div>
        </div>
        <button class="copy-btn" onclick="copyPrompt(this, 'prompt1')">
          <svg class="copy-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <rect x="9" y="9" width="13" height="13" rx="2" ry="2"></rect>
            <path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"></path>
          </svg>
          Copiar
        </button>
      </div>
      <div class="card-body">
        <div class="prompt-text" id="prompt1">Use the uploaded face reference and preserve identity exactly.
Ultra-realistic live TV broadcast screenshot during an international football match between Brazil and France. The man from the reference photo is sitting casually in the stadium crowd wearing a yellow Brazil jersey. He is filmed naturally from far away by a professional sports broadcast camera, with a subtle "caught on camera" expression while looking slightly to the side. Relaxed posture, seated naturally among fans in the stadium stands.
Around him are random football fans only, authentic crowded stadium atmosphere, mixed ages and appearances, some wearing Brazil jerseys, others France jerseys or casual clothing. Nobody posing for the camera. Real televised football vibe.
TV scoreboard overlay in the corner:
BRA 4 x 2 FRA
78:54
Important:
* preserve identity exactly
* telephoto sports broadcast lens
* wide live-TV framing
* NOT selfie
* NOT portrait photography
* imperfect TV framing
* slight motion blur
* subtle TV compression artifacts
* realistic stadium lighting
* natural skin texture
* no beauty filter
* no cinematic grading
* authentic FIFA / sports broadcast aesthetic
* crowd slightly out of focus while subject stays readable
* genuine "camera randomly found this fan in the crowd" feeling
* ultra realistic 4K</div>
        <button class="expand-btn" onclick="toggleExpand(this)">↓ Ver tudo</button>
      </div>
    </div>

    <div class="divider">
      <div class="divider-line"></div>
      <span class="divider-icon">⚡</span>
      <div class="divider-line"></div>
    </div>

    <!-- CARD 02 -->
    <div class="prompt-card">
      <div class="card-header">
        <div class="card-meta">
          <span class="step-badge">02</span>
          <div class="card-info">
            <div class="card-title">Prompt — Vídeo</div>
            <span class="card-tag">🎬 Pode fazer em qualquer IA de vídeo</span>
          </div>
        </div>
        <button class="copy-btn" onclick="copyPrompt(this, 'prompt2')">
          <svg class="copy-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <rect x="9" y="9" width="13" height="13" rx="2" ry="2"></rect>
            <path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"></path>
          </svg>
          Copiar
        </button>
      </div>
      <div class="card-body">
        <div class="prompt-text" id="prompt2">Use the uploaded face reference and preserve the man's identity EXACTLY during the entire video. Facial structure, beard, eyebrows, eye shape, lips, skin tone and hairline must remain fully consistent in every frame. No face morphing, no identity drift, no AI facial changes during zoom or movement.
The camera slowly finds him in the crowd for a few seconds and naturally zooms in slightly. He is seated relaxed, looking toward the event. After noticing the camera on the giant screen, he gives a subtle awkward smile and briefly raises his eyebrows, like someone unexpectedly caught on live TV. Natural blinking and micro facial movements only.
Around him are random spectators reacting naturally to the event, cheering, talking, drinking and moving naturally. Nobody is posing for the camera. Authentic crowded atmosphere.
Important:
* preserve facial identity exactly in all frames
* no face transformation during zoom
* no changing facial proportions
* no AI beauty enhancement
* authentic live broadcast aesthetic
* telephoto sports lens compression
* imperfect TV framing
* subtle handheld broadcast camera movement
* slight motion blur
* subtle digital compression artifacts
* realistic lighting
* natural skin texture
* realistic crowd depth of field
* crowd slightly out of focus while subject remains readable
* genuine "live TV randomly found this person" feeling
* ultra realistic 4K</div>
        <button class="expand-btn" onclick="toggleExpand(this)">↓ Ver tudo</button>
      </div>
    </div>

  </div>

  <!-- CTA -->
  <div class="cta-block">
    <div class="cta-eyebrow">// Quer ir além disso?</div>
    <div class="cta-title">APRENDA CRIATIVIDADE<br>DE VERDADE</div>
    <p class="cta-text">No Efeito Midas você aprende criação de conteúdo, produção de vídeo e como transformar criatividade em resultado — do jeito certo.</p>
    <a href="https://www.efeitomidas.com.br" target="_blank" class="cta-link">
      Quero conhecer o Efeito Midas
      <span class="cta-arrow">→</span>
    </a>
  </div>

  <footer>
    <span class="footer-brand">TAUMAXS</span>
    <span class="footer-note">Aqui o foguete sobe de ré ↑</span>
  </footer>

</div>

<script>
  function copyPrompt(btn, id) {
    const text = document.getElementById(id).innerText;
    navigator.clipboard.writeText(text).then(() => {
      btn.classList.add('copied');
      const original = btn.innerHTML;
      btn.innerHTML = `<svg class="copy-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="20 6 9 17 4 12"></polyline></svg> Copiado!`;
      setTimeout(() => {
        btn.classList.remove('copied');
        btn.innerHTML = original;
      }, 2000);
    });
  }

  function toggleExpand(btn) {
    const text = btn.previousElementSibling;
    const isExpanded = text.classList.toggle('expanded');
    btn.textContent = isExpanded ? '↑ Recolher' : '↓ Ver tudo';
  }
</script>
</body>
</html>
