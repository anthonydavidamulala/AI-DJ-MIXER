<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AI-DJ — README</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;500;700&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0d1117;
    --bg-panel: #161b22;
    --bg-code: #0d1117;
    --border: #30363d;
    --border-muted: #21262d;
    --green: #1db954;
    --green-dim: #158a3e;
    --green-glow: rgba(29,185,84,0.15);
    --white: #e6edf3;
    --muted: #8b949e;
    --faint: #484f58;
    --accent: #1db954;
    --heading: #f0f6fc;
    --link: #58a6ff;
    --warn: #f0a800;
    --table-head: #161b22;
    --table-row-alt: #0d1117;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg);
    color: var(--white);
    font-family: 'JetBrains Mono', monospace;
    font-size: 14px;
    line-height: 1.7;
    min-height: 100vh;
  }

  /* ── SCANLINE OVERLAY ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,0,0,0.03) 2px,
      rgba(0,0,0,0.03) 4px
    );
    pointer-events: none;
    z-index: 9999;
  }

  /* ── HEADER BAR ── */
  .repo-bar {
    background: var(--bg-panel);
    border-bottom: 1px solid var(--border);
    padding: 12px 24px;
    display: flex;
    align-items: center;
    gap: 10px;
    font-size: 13px;
    color: var(--muted);
    position: sticky;
    top: 0;
    z-index: 100;
  }
  .repo-bar .repo-icon {
    color: var(--muted);
    font-size: 16px;
  }
  .repo-bar .repo-path {
    display: flex;
    align-items: center;
    gap: 6px;
  }
  .repo-bar .repo-path a {
    color: var(--link);
    text-decoration: none;
    font-weight: 500;
  }
  .repo-bar .repo-path a:hover { text-decoration: underline; }
  .repo-bar .sep { color: var(--faint); }
  .repo-bar .repo-name { color: var(--link); font-weight: 700; }
  .repo-bar .spacer { flex: 1; }
  .repo-bar .star-btn {
    background: var(--bg-panel);
    border: 1px solid var(--border);
    color: var(--white);
    padding: 5px 14px;
    border-radius: 6px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    cursor: pointer;
    transition: border-color .15s, background .15s;
    display: flex;
    align-items: center;
    gap: 6px;
  }
  .repo-bar .star-btn:hover { border-color: var(--green); background: var(--green-glow); }

  /* ── MAIN LAYOUT ── */
  .layout {
    max-width: 1012px;
    margin: 0 auto;
    padding: 24px 16px 80px;
    display: grid;
    grid-template-columns: 1fr 280px;
    gap: 24px;
    align-items: start;
  }

  /* ── README BOX ── */
  .readme-box {
    background: var(--bg-panel);
    border: 1px solid var(--border);
    border-radius: 6px;
    overflow: hidden;
  }
  .readme-header {
    background: var(--bg-panel);
    border-bottom: 1px solid var(--border);
    padding: 10px 16px;
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 12px;
    color: var(--muted);
  }
  .readme-header .file-icon { color: var(--green); }
  .readme-header .file-name { color: var(--white); font-weight: 600; }
  .readme-body { padding: 32px 40px; }

  /* ── TYPOGRAPHY ── */
  h1 {
    font-family: 'Syne', sans-serif;
    font-size: 32px;
    font-weight: 800;
    color: var(--heading);
    margin-bottom: 10px;
    display: flex;
    align-items: center;
    gap: 12px;
    border-bottom: none;
    padding-bottom: 0;
  }
  h2 {
    font-family: 'Syne', sans-serif;
    font-size: 20px;
    font-weight: 700;
    color: var(--heading);
    margin: 28px 0 12px;
    padding-bottom: 8px;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    gap: 8px;
  }
  h3 {
    font-family: 'Syne', sans-serif;
    font-size: 15px;
    font-weight: 700;
    color: var(--heading);
    margin: 20px 0 8px;
    display: flex;
    align-items: center;
    gap: 6px;
  }
  p { color: var(--white); margin-bottom: 12px; }
  strong { color: var(--heading); font-weight: 600; }
  hr { border: none; border-top: 1px solid var(--border); margin: 24px 0; }

  /* ── BADGES ── */
  .badges {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    margin-bottom: 20px;
  }
  .badge {
    height: 20px;
    border-radius: 4px;
    font-size: 11px;
    font-weight: 700;
    letter-spacing: 0.5px;
    padding: 0 8px;
    display: inline-flex;
    align-items: center;
    gap: 5px;
    text-transform: uppercase;
  }
  .badge.main { background: var(--green); color: #000; }
  .badge.mit  { background: #158a3e; color: #a0ffb8; }
  .badge.browser { background: #1a2a3a; color: #58a6ff; border: 1px solid #30363d; }
  .badge.none { background: #1a1a1a; color: var(--faint); border: 1px solid #30363d; }

  /* ── LISTS ── */
  ul { padding-left: 20px; margin-bottom: 12px; }
  ul li { margin-bottom: 4px; color: var(--white); }
  ul li::marker { color: var(--green); }

  /* ── CODE BLOCKS ── */
  pre {
    background: var(--bg-code);
    border: 1px solid var(--border-muted);
    border-radius: 6px;
    padding: 16px;
    overflow-x: auto;
    margin: 12px 0;
    position: relative;
  }
  pre code {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12.5px;
    color: #a9b7c6;
    background: none;
    border: none;
    padding: 0;
    line-height: 1.6;
  }
  code {
    background: rgba(110,118,129,0.15);
    border: 1px solid var(--border-muted);
    border-radius: 4px;
    padding: 2px 6px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    color: #ff7b72;
  }
  /* flow diagram colors */
  .flow { color: #a9b7c6; }
  .flow .arrow { color: var(--green); }
  .flow .label { color: #e6edf3; font-weight: 600; }
  .flow .sub { color: var(--muted); }

  /* formula */
  .formula-block {
    background: var(--bg-code);
    border: 1px solid var(--border-muted);
    border-left: 3px solid var(--green);
    border-radius: 6px;
    padding: 12px 16px;
    font-size: 13px;
    color: #79c0ff;
    margin: 12px 0;
    text-align: center;
    letter-spacing: 0.5px;
  }

  /* ── TABLES ── */
  table {
    width: 100%;
    border-collapse: collapse;
    margin: 12px 0;
    font-size: 13px;
  }
  th {
    background: var(--table-head);
    color: var(--muted);
    font-weight: 600;
    text-align: left;
    padding: 8px 12px;
    border: 1px solid var(--border);
    font-size: 11px;
    letter-spacing: 1px;
    text-transform: uppercase;
  }
  td {
    padding: 8px 12px;
    border: 1px solid var(--border);
    color: var(--white);
  }
  tr:nth-child(even) td { background: var(--table-row-alt); }
  td code { font-size: 11px; }

  /* ── BLOCKQUOTE ── */
  blockquote {
    border-left: 3px solid var(--green);
    padding: 8px 16px;
    background: rgba(29,185,84,0.06);
    border-radius: 0 4px 4px 0;
    margin: 12px 0;
    color: var(--muted);
    font-size: 13px;
  }
  blockquote strong { color: var(--green); }

  /* ── STEP LIST ── */
  .steps { counter-reset: step; padding: 0; list-style: none; margin-bottom: 12px; }
  .steps li {
    counter-increment: step;
    display: flex;
    align-items: flex-start;
    gap: 12px;
    margin-bottom: 8px;
    color: var(--white);
  }
  .steps li::before {
    content: counter(step);
    background: var(--green);
    color: #000;
    font-weight: 700;
    font-size: 11px;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    margin-top: 2px;
  }

  /* ── STATUS BADGES IN TABLE ── */
  .status-ok { color: var(--green); font-weight: 600; }

  /* ── SIDEBAR ── */
  .sidebar { display: flex; flex-direction: column; gap: 16px; }
  .sidebar-card {
    background: var(--bg-panel);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 16px;
  }
  .sidebar-card h4 {
    font-family: 'Syne', sans-serif;
    font-size: 12px;
    font-weight: 700;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 2px;
    margin-bottom: 12px;
    padding-bottom: 8px;
    border-bottom: 1px solid var(--border);
  }
  .tag-list { display: flex; flex-wrap: wrap; gap: 6px; }
  .tag {
    background: rgba(29,185,84,0.1);
    border: 1px solid var(--green-dim);
    color: var(--green);
    font-size: 11px;
    padding: 3px 9px;
    border-radius: 12px;
    letter-spacing: 0.5px;
  }
  .stat-row { display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px; font-size: 12px; }
  .stat-row .k { color: var(--muted); }
  .stat-row .v { color: var(--green); font-weight: 700; }
  .lang-bar { margin-top: 4px; }
  .lang-bar-track { background: var(--border); border-radius: 3px; height: 6px; overflow: hidden; display: flex; margin-bottom: 8px; }
  .lang-seg { height: 100%; }
  .lang-labels { display: flex; flex-direction: column; gap: 5px; }
  .lang-label { display: flex; align-items: center; gap: 7px; font-size: 11px; color: var(--muted); }
  .lang-dot { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; }

  /* ── COPY BUTTON ── */
  .copy-wrap { position: relative; }
  .copy-btn {
    position: absolute;
    top: 8px; right: 8px;
    background: var(--bg-panel);
    border: 1px solid var(--border);
    color: var(--muted);
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px;
    letter-spacing: 1px;
    padding: 4px 8px;
    border-radius: 4px;
    cursor: pointer;
    transition: all .15s;
  }
  .copy-btn:hover { border-color: var(--green); color: var(--green); }

  /* ── ANIMATIONS ── */
  .readme-body > * { animation: fadeUp 0.4s ease both; }
  .readme-body > *:nth-child(1) { animation-delay: .05s; }
  .readme-body > *:nth-child(2) { animation-delay: .10s; }
  .readme-body > *:nth-child(3) { animation-delay: .15s; }
  .readme-body > *:nth-child(4) { animation-delay: .20s; }
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(12px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  @media (max-width: 768px) {
    .layout { grid-template-columns: 1fr; }
    .sidebar { order: -1; }
    .readme-body { padding: 20px 16px; }
    h1 { font-size: 24px; }
  }
</style>
</head>
<body>

<!-- REPO BAR -->
<div class="repo-bar">
  <span class="repo-icon">⬡</span>
  <div class="repo-path">
    <a href="#">your-username</a>
    <span class="sep">/</span>
    <span class="repo-name">ai-dj</span>
  </div>
  <span class="spacer"></span>
  <button class="star-btn" onclick="this.textContent='★ Starred!'">☆ Star</button>
</div>

<!-- LAYOUT -->
<div class="layout">

  <!-- README -->
  <div class="readme-box">
    <div class="readme-header">
      <span class="file-icon">📄</span>
      <span class="file-name">README.md</span>
    </div>
    <div class="readme-body">

      <h1>🎧 AI-DJ</h1>

      <p><strong>Fourier-powered song order recommender, auto mixer, and DJ toolkit — runs entirely in the browser.</strong></p>

      <div class="badges">
        <span class="badge main">▶ Fourier + ML + Auto Mix</span>
        <span class="badge mit">MIT License</span>
        <span class="badge browser">🌐 Browser</span>
        <span class="badge none">No Backend</span>
      </div>

      <hr>

      <h2>What It Does</h2>
      <p>AI-DJ analyzes your local audio files using the <strong>Fast Fourier Transform (FFT)</strong> and a <strong>simulated annealing + 2-opt optimization algorithm</strong> to recommend the smoothest possible play order for your music. It then auto-mixes through the playlist with configurable crossfades — all in real time, entirely client-side.</p>

      <hr>

      <h2>Features</h2>

      <h3>🔬 Fourier Intelligence Engine</h3>
      <ul>
        <li>Transforms each audio file from the time domain into the frequency domain using FFT</li>
        <li>Extracts BPM, spectral centroid, dominant frequency, energy, and key from raw audio data</li>
        <li>Displays live time-domain waveform and frequency spectrum side by side</li>
        <li>Explains the underlying DSP math (<code>X(f) = ∫ x(t)e^{-j2πft} dt</code>) with a toggleable breakdown</li>
      </ul>

      <h3>🧠 ML Song Order Recommendation</h3>
      <ul>
        <li>Builds a 3-dimensional feature vector per song: <code>[BPM, energy, spectral centroid]</code></li>
        <li>Uses a <strong>greedy nearest-neighbor</strong> algorithm as the starting solution</li>
        <li>Refines it with <strong>simulated annealing</strong> (3 independent passes) for near-optimal global ordering</li>
        <li>Polishes the result with <strong>2-opt local search</strong> to eliminate suboptimal swaps</li>
        <li>Scores every transition as <code>Smooth / OK / Hard</code> based on BPM delta and spectral similarity</li>
        <li>Displays a similarity matrix and full transition reasoning for each pair</li>
      </ul>

      <h3>⏯️ Auto Mix Engine</h3>
      <ul>
        <li>Plays a configurable segment of each song (offset + duration)</li>
        <li>Schedules crossfades automatically using the Web Audio API</li>
        <li>Dual-deck architecture (Deck A / Deck B) with exponential gain curves for natural-sounding fades</li>
        <li>Configurable: crossfade duration, segment offset, and play duration per track</li>
        <li>Live progress bar with countdown and crossfade status</li>
      </ul>

      <h3>🎚️ 3-Band EQ</h3>
      <ul>
        <li>Bass (lowshelf ~250 Hz), Mid (peaking ~1.2 kHz), Treble (highshelf ~4 kHz)</li>
        <li>Adjustable via vertical sliders, ±18 dB range</li>
        <li>One-click presets: Flat, Bass Boost, Vocal, Club, Acoustic, Electronic</li>
      </ul>

      <h3>🔊 Sound Effects (FX)</h3>
      <ul>
        <li><strong>Reverb</strong> — boosted mid resonance for a spatial effect</li>
        <li><strong>Echo</strong> — delay simulation via mid Q shaping</li>
        <li><strong>Sweep↓ / Sweep↑</strong> — low-pass / high-pass filter sweeps</li>
        <li><strong>Stutter</strong> — rapid gain gating at ~80 ms intervals</li>
        <li><strong>Scratch</strong> — randomized playback rate variation</li>
        <li><strong>Bitcrush</strong> — heavy mid and treble roll-off for lo-fi texture</li>
        <li><strong>Flanger</strong> — narrow peaking filter with high Q</li>
      </ul>

      <h3>🎵 Player</h3>
      <ul>
        <li>Waveform progress bar with seek support</li>
        <li>Volume control via Web Audio master gain node</li>
        <li>Loop, shuffle, previous/next with smooth crossfades on all transitions</li>
        <li>Animated spinning disc tied to playback state</li>
      </ul>

      <hr>

      <h2>How the Algorithm Works</h2>

      <div class="copy-wrap">
        <pre><code class="flow"><span class="label">Audio File</span>
    <span class="arrow">│</span>
    <span class="arrow">▼</span>
<span class="label">FFT Feature Extraction</span>
<span class="sub">(BPM · Energy · Spectral Centroid · Key)</span>
    <span class="arrow">│</span>
    <span class="arrow">▼</span>
<span class="label">Greedy Nearest-Neighbor</span>  <span class="sub">(seed order)</span>
    <span class="arrow">│</span>
    <span class="arrow">▼</span>
<span class="label">Simulated Annealing × 3 runs</span>
<span class="sub">(stochastic global search, T → 0)</span>
    <span class="arrow">│</span>
    <span class="arrow">▼</span>
<span class="label">2-Opt Local Search</span>
<span class="sub">(deterministic, guaranteed local optimum)</span>
    <span class="arrow">│</span>
    <span class="arrow">▼</span>
<span class="label">Best of 3 candidates → Recommended Playlist</span></code></pre>
      </div>

      <p>Transition cost between two songs is a weighted Euclidean distance:</p>
      <div class="formula-block">d(a, b) = √( 2·ΔBPM² + 1·ΔEnergy² + 0.5·ΔCentroid² )</div>

      <hr>

      <h2>Getting Started</h2>
      <p>No build step, no dependencies, no server required.</p>

      <ol class="steps">
        <li>Clone or download the repository</li>
        <li>Open <code>index.html</code> in any modern browser (Chrome, Firefox, Edge, Safari)</li>
        <li>Drag and drop audio files onto the upload zone</li>
        <li>Click <strong>Analyze &amp; Recommend Optimal Play Order</strong></li>
        <li>Click any track to play it, or enable <strong>Auto Mix</strong> for hands-free DJ mode</li>
      </ol>

      <div class="copy-wrap">
        <button class="copy-btn" onclick="navigator.clipboard.writeText('git clone https://github.com/your-username/ai-dj.git\ncd ai-dj\nopen index.html');this.textContent='Copied!'">COPY</button>
        <pre><code>git clone https://github.com/your-username/ai-dj.git
cd ai-dj
open index.html   # or just double-click it</code></pre>
      </div>

      <blockquote><strong>Supported formats:</strong> MP3, WAV, OGG, FLAC, AAC, M4A — anything the browser's <code>decodeAudioData</code> supports.</blockquote>

      <hr>

      <h2>Tech Stack</h2>
      <table>
        <tr><th>Layer</th><th>Technology</th></tr>
        <tr><td>Audio decoding &amp; routing</td><td>Web Audio API (<code>AudioContext</code>, <code>AudioBufferSourceNode</code>)</td></tr>
        <tr><td>Frequency analysis</td><td><code>AnalyserNode</code> + manual FFT (Hanning window)</td></tr>
        <tr><td>Signal processing</td><td><code>BiquadFilterNode</code> (lowshelf, highshelf, peaking, lowpass, highpass)</td></tr>
        <tr><td>Optimization</td><td>Greedy NN + Simulated Annealing + 2-Opt</td></tr>
        <tr><td>Rendering</td><td>Canvas 2D API (live FFT bars, waveform, Fourier panel)</td></tr>
        <tr><td>Fonts</td><td>Space Mono, Bebas Neue (Google Fonts)</td></tr>
        <tr><td>Backend</td><td>None — 100% client-side</td></tr>
      </table>

      <hr>

      <h2>Project Structure</h2>
      <pre><code>ai-dj/
└── index.html      # Entire application — HTML, CSS, and JS in one file</code></pre>

      <hr>

      <h2>Browser Compatibility</h2>
      <table>
        <tr><th>Browser</th><th>Status</th></tr>
        <tr><td>Chrome 90+</td><td><span class="status-ok">✅ Full support</span></td></tr>
        <tr><td>Firefox 88+</td><td><span class="status-ok">✅ Full support</span></td></tr>
        <tr><td>Edge 90+</td><td><span class="status-ok">✅ Full support</span></td></tr>
        <tr><td>Safari 14.1+</td><td><span class="status-ok">✅ Full support</span></td></tr>
      </table>
      <blockquote>Mobile browsers are supported but the interface is optimized for desktop viewports.</blockquote>

      <hr>

      <h2>License</h2>
      <p>MIT — do whatever you want with it.</p>

      <hr>

      <h2>Acknowledgements</h2>
      <p>Built with the <strong>Web Audio API</strong>, raw FFT math, and no external audio libraries.<br>
      Inspired by the signal processing behind real DJ software and music information retrieval (MIR) research.</p>

    </div>
  </div>

  <!-- SIDEBAR -->
  <div class="sidebar">
    <div class="sidebar-card">
      <h4>About</h4>
      <p style="font-size:12px;color:var(--muted);margin-bottom:12px;">Browser-based AI DJ — Fourier analysis, ML ordering, auto crossfade.</p>
      <div class="stat-row"><span class="k">⭐ Stars</span><span class="v">—</span></div>
      <div class="stat-row"><span class="k">🍴 Forks</span><span class="v">—</span></div>
      <div class="stat-row"><span class="k">📦 Size</span><span class="v">Single file</span></div>
    </div>

    <div class="sidebar-card">
      <h4>Topics</h4>
      <div class="tag-list">
        <span class="tag">web-audio-api</span>
        <span class="tag">fft</span>
        <span class="tag">dsp</span>
        <span class="tag">dj</span>
        <span class="tag">music</span>
        <span class="tag">bpm-detection</span>
        <span class="tag">javascript</span>
        <span class="tag">simulated-annealing</span>
        <span class="tag">2-opt</span>
        <span class="tag">no-backend</span>
      </div>
    </div>

    <div class="sidebar-card">
      <h4>Languages</h4>
      <div class="lang-bar">
        <div class="lang-bar-track">
          <div class="lang-seg" style="width:62%;background:#f1e05a;"></div>
          <div class="lang-seg" style="width:28%;background:#563d7c;"></div>
          <div class="lang-seg" style="width:10%;background:#e34c26;"></div>
        </div>
      </div>
      <div class="lang-labels">
        <div class="lang-label"><div class="lang-dot" style="background:#f1e05a;"></div>JavaScript 62%</div>
        <div class="lang-label"><div class="lang-dot" style="background:#563d7c;"></div>CSS 28%</div>
        <div class="lang-label"><div class="lang-dot" style="background:#e34c26;"></div>HTML 10%</div>
      </div>
    </div>
  </div>

</div>
</body>
</html>
