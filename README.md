<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Scott Sampson — Growth Portfolio</title>
<style>
/* ── RESET & BASE ─────────────────────────────────── */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

:root {
  --bg:     #F4F3F0;
  --bg2:    #ECEAE5;
  --white:  #FFFFFF;
  --ink:    #1A1A18;
  --ink2:   #4A4A46;
  --ink3:   #8A8A84;
  --teal:   #4DB8A0;
  --teal-d: #2E8B78;
  --teal-l: #D6F0EA;
  --amber:  #C8923A;
  --red:    #C0392B;
  --red-l:  #FDECEA;
  --border: #E0E0DC;
  --sans: -apple-system, 'Helvetica Neue', Arial, sans-serif;
  --serif: Georgia, 'Times New Roman', serif;
}

html { scroll-behavior: smooth; }
body { background: #2C2C2A; font-family: var(--sans); color: var(--ink); line-height: 1.5; }

/* ── TOP BAR ──────────────────────────────────────── */
.topbar {
  position: sticky; top: 0; z-index: 200;
  background: var(--ink);
  display: flex; align-items: center; justify-content: space-between;
  padding: 0 28px; height: 52px;
  border-bottom: 1px solid rgba(77,184,160,.2);
}
.topbar-brand { display: flex; align-items: baseline; gap: 10px; }
.topbar-name { font-family: var(--serif); font-size: 16px; color: #fff; font-weight: normal; letter-spacing: -.01em; }
.topbar-role { font-size: 10px; color: rgba(255,255,255,.35); letter-spacing: .08em; text-transform: uppercase; }
.topbar-nav { display: flex; gap: 4px; }
.nav-pill {
  width: 28px; height: 28px; border-radius: 50%;
  background: rgba(255,255,255,.08); border: none;
  color: rgba(255,255,255,.45); font-size: 11px; font-weight: 600;
  cursor: pointer; transition: all .15s; font-family: var(--sans);
  display: flex; align-items: center; justify-content: center;
}
.nav-pill:hover { background: rgba(255,255,255,.18); color: #fff; }
.nav-pill.active { background: var(--teal); color: var(--ink); }
.topbar-right { display: flex; align-items: center; gap: 14px; }
.slide-counter { font-size: 11px; color: rgba(255,255,255,.3); letter-spacing: .04em; }

/* ── SLIDE VIEWPORT ───────────────────────────────── */
.viewport { overflow: hidden; position: relative; }
.slides-track {
  display: flex;
  transition: transform .35s cubic-bezier(.4,0,.2,1);
}

/* ── INDIVIDUAL SLIDE ─────────────────────────────── */
.slide {
  flex-shrink: 0;
  width: 100vw;
  background: var(--bg);
  display: grid;
  grid-template-rows: auto 1fr auto;
  overflow: hidden;
}

/* ── SLIDE HEADER ─────────────────────────────────── */
.s-hdr {
  background: var(--ink);
  padding: 10px 24px 12px;
  display: grid;
  grid-template-columns: 1fr auto;
  grid-template-rows: auto auto auto;
  gap: 0;
  position: relative;
}
.s-num {
  font-size: 9px; font-weight: 600; letter-spacing: .1em;
  text-transform: uppercase; color: var(--teal);
  grid-column: 1; grid-row: 1;
  padding-top: 2px;
}
.s-title {
  font-family: var(--serif); font-size: clamp(18px, 2.2vw, 26px);
  color: #fff; line-height: 1.1; letter-spacing: -.02em;
  grid-column: 1; grid-row: 2; padding: 3px 0 2px;
}
.s-sub {
  font-size: 10px; color: var(--ink3); font-style: italic;
  grid-column: 1; grid-row: 3;
}
.s-badge {
  grid-column: 2; grid-row: 1 / 3; align-self: center;
  background: rgba(77,184,160,.14);
  border: 1px solid rgba(77,184,160,.3);
  border-radius: 20px; padding: 5px 14px;
  font-size: 9px; font-weight: 700;
  color: var(--teal-d); letter-spacing: .06em; text-transform: uppercase;
  white-space: nowrap; margin-left: 20px;
}

/* ── SLIDE BODY ───────────────────────────────────── */
.s-body {
  display: grid;
  grid-template-columns: 1fr 240px;
  gap: 12px;
  padding: 12px 16px 8px;
  min-height: 0;
}

/* ── CHART PANEL ──────────────────────────────────── */
.chart-panel {
  background: var(--white);
  border-radius: 10px; border: 1px solid var(--border);
  padding: 12px 14px 10px;
  display: flex; flex-direction: column; min-height: 0;
  box-shadow: 0 1px 4px rgba(0,0,0,.06);
}
.chart-lbl {
  font-size: 8px; font-weight: 700; letter-spacing: .09em;
  text-transform: uppercase; color: var(--ink3);
  margin-bottom: 6px; flex-shrink: 0;
}
.chart-canvas-wrap { flex: 1; min-height: 0; position: relative; }
canvas { display: block; width: 100% !important; height: 100% !important; }
.legend-row {
  display: flex; gap: 12px; flex-wrap: wrap;
  margin-top: 7px; padding-top: 7px;
  border-top: 1px solid var(--border);
  flex-shrink: 0;
}
.leg-item { display: flex; align-items: center; gap: 5px; font-size: 9px; color: var(--ink3); }
.leg-swatch { width: 16px; height: 2px; flex-shrink: 0; }
.ann-note {
  margin-top: 6px; padding: 5px 9px; border-radius: 5px;
  font-size: 8.5px; font-weight: 500; line-height: 1.45; flex-shrink: 0;
}
.ann-red { background: var(--red-l); border: 1px solid rgba(192,57,43,.22); color: var(--red); }

/* ── CONTEXT PANEL ────────────────────────────────── */
.ctx-panel { display: flex; flex-direction: column; gap: 8px; min-height: 0; }

.insight-box {
  background: var(--ink); border-radius: 9px;
  padding: 11px 13px; flex-shrink: 0;
}
.insight-lbl {
  font-size: 8px; font-weight: 700; letter-spacing: .1em;
  text-transform: uppercase; color: var(--teal); margin-bottom: 5px;
}
.insight-txt {
  font-size: 9.5px; color: rgba(232,232,228,.88);
  line-height: 1.6; font-weight: 300;
}
.insight-txt strong { color: #fff; font-weight: 600; }

.metrics-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 6px; flex-shrink: 0; }
.metric-card {
  background: var(--bg2); border-radius: 7px;
  padding: 7px 9px; text-align: center;
}
.metric-val {
  font-family: var(--serif);
  font-size: clamp(14px, 1.6vw, 20px);
  color: var(--teal-d); line-height: 1; margin-bottom: 3px;
}
.metric-lbl { font-size: 8px; color: var(--ink3); line-height: 1.3; }

.bullets-box {
  background: var(--white); border: 1px solid var(--border);
  border-radius: 9px; padding: 10px 12px;
  flex: 1; min-height: 0; overflow: hidden;
}
.bullets-lbl {
  font-size: 8px; font-weight: 700; letter-spacing: .09em;
  text-transform: uppercase; color: var(--ink3); margin-bottom: 7px;
}
.bullets-list { list-style: none; display: flex; flex-direction: column; gap: 6px; }
.bullets-list li {
  display: flex; gap: 7px;
  font-size: 9px; color: var(--ink2); line-height: 1.5;
}
.bullets-list li::before {
  content: ''; width: 5px; height: 5px; border-radius: 50%;
  background: var(--teal); flex-shrink: 0; margin-top: 4px;
}

/* ── FOOTER ───────────────────────────────────────── */
.s-ftr {
  background: #ECECEA; border-top: 1px solid var(--border);
  display: flex; align-items: center; justify-content: space-between;
  padding: 0 16px; height: 26px; flex-shrink: 0;
}
.s-ftr span { font-size: 8.5px; color: var(--ink3); }
.s-ftr .ftr-role { color: var(--teal); font-weight: 600; }

/* ── ARROW BUTTONS ────────────────────────────────── */
.arrow {
  position: fixed; top: 50%; transform: translateY(-50%);
  width: 40px; height: 40px; border-radius: 50%;
  background: rgba(26,26,24,.7); border: 1px solid rgba(255,255,255,.15);
  color: rgba(255,255,255,.7); font-size: 16px;
  cursor: pointer; transition: all .15s; z-index: 100;
  display: flex; align-items: center; justify-content: center;
  backdrop-filter: blur(4px);
}
.arrow:hover { background: rgba(77,184,160,.8); color: var(--ink); border-color: var(--teal); }
.arrow:disabled { opacity: .2; cursor: default; pointer-events: none; }
.arrow-l { left: 12px; }
.arrow-r { right: 12px; }

/* ── RESPONSIVE ───────────────────────────────────── */
@media (max-width: 600px) {
  .s-body { grid-template-columns: 1fr; }
  .ctx-panel { display: none; }
  .s-badge { display: none; }
}
@media (max-width: 420px) {
  .topbar-nav { display: none; }
}
</style>
</head>
<body>

<!-- TOP BAR -->
<div class="topbar">
  <div class="topbar-brand">
    <span class="topbar-name">Scott Sampson</span>
    <span class="topbar-role">Growth Portfolio</span>
  </div>
  <div class="topbar-nav" id="nav-dots"></div>
  <div class="topbar-right">
    <span class="slide-counter" id="counter">1 / 5</span>
  </div>
</div>

<!-- VIEWPORT -->
<div class="viewport" id="viewport">
<div class="slides-track" id="track">

<!-- ════════════════════════════════════════
     SLIDE 1 — From flat to flywheel
═════════════════════════════════════════ -->
<div class="slide">
  <div class="s-hdr">
    <div class="s-num">01 / 05 · Revenue growth</div>
    <div class="s-title">From flat to flywheel</div>
    <div class="s-sub">Indexed ARR trajectory across three consecutive engagements · Entry = 100 per engagement</div>
    <div class="s-badge">15-year track record</div>
  </div>
  <div class="s-body">
    <div class="chart-panel">
      <div class="chart-lbl">Indexed ARR · Entry = 100 · Each line = one engagement</div>
      <div class="chart-canvas-wrap"><canvas id="c1"></canvas></div>
      <div class="legend-row">
        <div class="leg-item"><div class="leg-swatch" style="background:#4DB8A0"></div>Omnipresent</div>
        <div class="leg-item"><div class="leg-swatch" style="background:#2E8B78"></div>Personio</div>
        <div class="leg-item"><div class="leg-swatch" style="background:#8AC4B8;border-top:2px dashed #8AC4B8;height:0"></div>Civica (ongoing)</div>
        <div class="leg-item" style="font-style:italic">↑ dashed lines = decision points</div>
      </div>
    </div>
    <div class="ctx-panel">
      <div class="insight-box">
        <div class="insight-lbl">The insight</div>
        <div class="insight-txt">In every engagement, growth accelerated after the same intervention: <strong>find the hidden constraint, fix it fast</strong>, then let compounding do the rest.</div>
      </div>
      <div class="metrics-grid">
        <div class="metric-card"><div class="metric-val">3×</div><div class="metric-lbl">Revenue in 12 months</div></div>
        <div class="metric-card"><div class="metric-val">160%</div><div class="metric-lbl">ARR YoY (Personio)</div></div>
        <div class="metric-card"><div class="metric-val">112%</div><div class="metric-lbl">Growth from flat</div></div>
        <div class="metric-card"><div class="metric-val">5×</div><div class="metric-lbl">ARR (legal tech)</div></div>
      </div>
      <div class="bullets-box">
        <div class="bullets-lbl">What drove this</div>
        <ul class="bullets-list">
          <li>Each engagement started with a diagnostic period — no levers pulled until the real constraint was identified</li>
          <li>Growth accelerated when ICP, messaging, and channel were aligned simultaneously, not sequentially</li>
          <li>Cost efficiency improved alongside growth — revenue compounded, headcount did not</li>
        </ul>
      </div>
    </div>
  </div>
  <div class="s-ftr">
    <span>Scott Sampson</span><span class="ftr-role">Director of Growth · Voy</span><span>March 2025</span>
  </div>
</div>

<!-- ════════════════════════════════════════
     SLIDE 2 — Scaling output faster
═════════════════════════════════════════ -->
<div class="slide">
  <div class="s-hdr">
    <div class="s-num">02 / 05 · Team efficiency</div>
    <div class="s-title">Scaling output faster than headcount</div>
    <div class="s-sub">Revenue productivity per FTE vs. team index · Personio · Indexed, entry = 100</div>
    <div class="s-badge">Personio · 2023–2025</div>
  </div>
  <div class="s-body">
    <div class="chart-panel">
      <div class="chart-lbl">Rev / FTE index vs. Headcount index · Personio engagement</div>
      <div class="chart-canvas-wrap"><canvas id="c2"></canvas></div>
      <div class="legend-row">
        <div class="leg-item"><div class="leg-swatch" style="background:#4DB8A0"></div>Revenue / FTE index</div>
        <div class="leg-item"><div class="leg-swatch" style="background:#C8923A"></div>Headcount index</div>
      </div>
    </div>
    <div class="ctx-panel">
      <div class="insight-box">
        <div class="insight-lbl">The insight</div>
        <div class="insight-txt">Productivity per FTE grew <strong>4.2× faster than headcount</strong> — the commercial model scaled through better process, not more people.</div>
      </div>
      <div class="metrics-grid">
        <div class="metric-card"><div class="metric-val">4.2×</div><div class="metric-lbl">Productivity / FTE</div></div>
        <div class="metric-card"><div class="metric-val">50%</div><div class="metric-lbl">CAC payback cut</div></div>
        <div class="metric-card"><div class="metric-val">3×</div><div class="metric-lbl">CVR improvement</div></div>
        <div class="metric-card"><div class="metric-val">2.1×</div><div class="metric-lbl">ACV growth</div></div>
      </div>
      <div class="bullets-box">
        <div class="bullets-lbl">What drove this</div>
        <ul class="bullets-list">
          <li>Upmarket repositioning unlocked ACV 2.1× while maintaining conversion velocity</li>
          <li>CAC halved through channel mix optimisation — spend shifted to highest-payback channels</li>
          <li>Revenue motion systemised: reduced ramp time, removed manual funnel steps</li>
        </ul>
      </div>
    </div>
  </div>
  <div class="s-ftr">
    <span>Scott Sampson</span><span class="ftr-role">Director of Growth · Voy</span><span>March 2025</span>
  </div>
</div>

<!-- ════════════════════════════════════════
     SLIDE 3 — Funnel before and after
═════════════════════════════════════════ -->
<div class="slide">
  <div class="s-hdr">
    <div class="s-num">03 / 05 · Funnel efficiency</div>
    <div class="s-title">The funnel before and after</div>
    <div class="s-sub">Stage-by-stage conversion improvement · Civica · Indexed, entry = 100 · All values confidentialised</div>
    <div class="s-badge">Civica · 2025–Present</div>
  </div>
  <div class="s-body">
    <div class="chart-panel">
      <div class="chart-lbl">Conversion index per funnel stage · Entry (grey) vs. Current (teal)</div>
      <div class="chart-canvas-wrap"><canvas id="c3"></canvas></div>
      <div class="legend-row">
        <div class="leg-item"><div class="leg-swatch" style="background:#C8C8C4"></div>At entry (baseline 100)</div>
        <div class="leg-item"><div class="leg-swatch" style="background:#4DB8A0"></div>Current</div>
        <div class="leg-item" style="font-style:italic">Largest gain = Attainment stage</div>
      </div>
    </div>
    <div class="ctx-panel">
      <div class="insight-box">
        <div class="insight-lbl">The insight</div>
        <div class="insight-txt">The biggest gain wasn't at the top of funnel — it was at <strong>Attainment</strong>, where sub-60% became 75%+ by fixing incentive structure and territory design.</div>
      </div>
      <div class="metrics-grid">
        <div class="metric-card"><div class="metric-val">112%</div><div class="metric-lbl">ARR growth from flat</div></div>
        <div class="metric-card"><div class="metric-val">21%</div><div class="metric-lbl">Bookings YoY</div></div>
        <div class="metric-card"><div class="metric-val">40pp</div><div class="metric-lbl">EBIT margin gain</div></div>
        <div class="metric-card"><div class="metric-val">75%+</div><div class="metric-lbl">Quota attainment</div></div>
      </div>
      <div class="bullets-box">
        <div class="bullets-lbl">What drove this</div>
        <ul class="bullets-list">
          <li>Territory redesign removed overlap — attainment improved within one quarter</li>
          <li>OpEx reduced 25% while bookings grew 21% — 40pp EBIT gain, no sacrifice to live revenue</li>
          <li>Funnel instrumented for the first time — decisions moved from instinct to data within 30 days</li>
        </ul>
      </div>
    </div>
  </div>
  <div class="s-ftr">
    <span>Scott Sampson</span><span class="ftr-role">Director of Growth · Voy</span><span>March 2025</span>
  </div>
</div>

<!-- ════════════════════════════════════════
     SLIDE 4 — The time the plan didn't work
═════════════════════════════════════════ -->
<div class="slide">
  <div class="s-hdr">
    <div class="s-num">04 / 05 · Setback &amp; recovery</div>
    <div class="s-title">The time the plan didn't work</div>
    <div class="s-sub">NRR index trajectory · Reward Gateway · Early expansion motion failed · What changed</div>
    <div class="s-badge">Reward Gateway · 2011–2016</div>
  </div>
  <div class="s-body">
    <div class="chart-panel">
      <div class="chart-lbl">NRR index · Entry = 100 (representing 65% NRR baseline) · Recovery trajectory</div>
      <div class="chart-canvas-wrap"><canvas id="c4"></canvas></div>
      <div class="ann-note ann-red">↓ Month 8 — First expansion motion launched. NRR deteriorated further. Wrong ICP, wrong trigger, wrong message. Rebuilt from scratch at month 14.</div>
    </div>
    <div class="ctx-panel">
      <div class="insight-box">
        <div class="insight-lbl">What I learned</div>
        <div class="insight-txt">The first expansion motion I designed <strong>made things worse</strong>. Too aggressive, too early, wrong segment. Rebuilding from that taught me more about retention economics than anything else in my career.</div>
      </div>
      <div class="metrics-grid">
        <div class="metric-card"><div class="metric-val">65%</div><div class="metric-lbl">NRR at entry</div></div>
        <div class="metric-card"><div class="metric-val">115%</div><div class="metric-lbl">NRR at exit</div></div>
        <div class="metric-card"><div class="metric-val">&lt;10%</div><div class="metric-lbl">Attrition at exit</div></div>
        <div class="metric-card"><div class="metric-val">£1.2m</div><div class="metric-lbl">LTV at exit (2×)</div></div>
      </div>
      <div class="bullets-box">
        <div class="bullets-lbl">The three things I changed</div>
        <ul class="bullets-list">
          <li>Killed volume-based expansion — rebuilt around value expansion only after the customer sees ROI</li>
          <li>Changed expansion trigger from contract renewal date to customer success milestone</li>
          <li>Fixed the activation problem, not the churn problem — if activation works, retention follows</li>
        </ul>
      </div>
    </div>
  </div>
  <div class="s-ftr">
    <span>Scott Sampson</span><span class="ftr-role">Director of Growth · Voy</span><span>March 2025</span>
  </div>
</div>

<!-- ════════════════════════════════════════
     SLIDE 5 — GTM Model Evolution
═════════════════════════════════════════ -->
<div class="slide">
  <div class="s-hdr">
    <div class="s-num">05 / 05 · Commercial model evolution</div>
    <div class="s-title">Redesigning the motion mid-flight</div>
    <div class="s-sub">Revenue index vs. cost:revenue ratio · Omnipresent · Growth and efficiency compounding together</div>
    <div class="s-badge">Omnipresent · 2021–2023</div>
  </div>
  <div class="s-body">
    <div class="chart-panel">
      <div class="chart-lbl">Revenue index (teal ↑) vs. Cost:revenue index (amber ↓ lower = better) · Omnipresent</div>
      <div class="chart-canvas-wrap"><canvas id="c5"></canvas></div>
      <div class="legend-row">
        <div class="leg-item"><div class="leg-swatch" style="background:#4DB8A0"></div>Revenue index ↑</div>
        <div class="leg-item"><div class="leg-swatch" style="background:#C8923A"></div>Cost:revenue index ↓ better</div>
        <div class="leg-item" style="font-style:italic">Crossover = commercial model matured</div>
      </div>
    </div>
    <div class="ctx-panel">
      <div class="insight-box">
        <div class="insight-lbl">The insight</div>
        <div class="insight-txt">Revenue tripled in 12 months while cost efficiency <strong>doubled</strong>. The model scaled because the growth engine was rebuilt, not just fuelled.</div>
      </div>
      <div class="metrics-grid">
        <div class="metric-card"><div class="metric-val">3×</div><div class="metric-lbl">Revenue in 12 months</div></div>
        <div class="metric-card"><div class="metric-val">2×</div><div class="metric-lbl">Cost efficiency gain</div></div>
        <div class="metric-card"><div class="metric-val">6×</div><div class="metric-lbl">Team scaled</div></div>
        <div class="metric-card"><div class="metric-val">107%</div><div class="metric-lbl">NRR at exit</div></div>
      </div>
      <div class="bullets-box">
        <div class="bullets-lbl">What drove this</div>
        <ul class="bullets-list">
          <li>Rebuilt ICP definition from broad to precise — same team, higher win rate, better-fit customers with lower churn</li>
          <li>Removed low-productivity channels and doubled down on the two that compounded</li>
          <li>NRR improvement 84%→107% reduced effective CAC burden — existing revenue compounded, new spend went further</li>
        </ul>
      </div>
    </div>
  </div>
  <div class="s-ftr">
    <span>Scott Sampson</span><span class="ftr-role">Director of Growth · Voy</span><span>March 2025</span>
  </div>
</div>

</div><!-- end track -->
</div><!-- end viewport -->

<!-- ARROW BUTTONS -->
<button class="arrow arrow-l" id="prev" onclick="go(-1)">&#8592;</button>
<button class="arrow arrow-r" id="next" onclick="go(1)">&#8594;</button>

<script>
// ── SLIDER ────────────────────────────────────────────────────────
let cur = 0;
const TOTAL = 5;
const track = document.getElementById('track');
const viewport = document.getElementById('viewport');

function setViewportHeight() {
  // Make viewport fill available height below topbar
  const topH = document.querySelector('.topbar').offsetHeight;
  viewport.style.height = (window.innerHeight - topH) + 'px';
}
setViewportHeight();
window.addEventListener('resize', () => { setViewportHeight(); renderAll(); });

function go(dir) {
  const next = cur + dir;
  if (next < 0 || next >= TOTAL) return;
  cur = next;
  track.style.transform = `translateX(-${cur * 100}vw)`;
  updateUI();
}

function goTo(n) {
  if (n === cur) return;
  cur = n;
  track.style.transform = `translateX(-${cur * 100}vw)`;
  updateUI();
}

function updateUI() {
  document.getElementById('prev').disabled = cur === 0;
  document.getElementById('next').disabled = cur === TOTAL - 1;
  document.getElementById('counter').textContent = (cur + 1) + ' / ' + TOTAL;
  document.querySelectorAll('.nav-pill').forEach((p, i) => p.classList.toggle('active', i === cur));
}

// Build nav dots
const dotWrap = document.getElementById('nav-dots');
for (let i = 0; i < TOTAL; i++) {
  const b = document.createElement('button');
  b.className = 'nav-pill' + (i === 0 ? ' active' : '');
  b.textContent = i + 1;
  b.onclick = () => goTo(i);
  dotWrap.appendChild(b);
}
updateUI();

// Keyboard navigation
document.addEventListener('keydown', e => {
  if (e.key === 'ArrowRight' || e.key === 'ArrowDown') go(1);
  if (e.key === 'ArrowLeft'  || e.key === 'ArrowUp')   go(-1);
});

// Touch/swipe support
let touchX = null;
viewport.addEventListener('touchstart', e => { touchX = e.touches[0].clientX; }, { passive: true });
viewport.addEventListener('touchend', e => {
  if (touchX === null) return;
  const dx = e.changedTouches[0].clientX - touchX;
  if (Math.abs(dx) > 50) go(dx < 0 ? 1 : -1);
  touchX = null;
}, { passive: true });

// ── CHART ENGINE (native Canvas API) ──────────────────────────────
const TEAL   = '#4DB8A0';
const TEAL_D = '#2E8B78';
const AMBER  = '#C8923A';
const RED    = '#C0392B';
const GREY   = '#C8C8C4';
const INK2   = '#4A4A46';
const INK3   = '#8A8A84';
const BG2    = '#ECEAE5';
const WHITE  = '#FFFFFF';
const FONT   = "-apple-system,'Helvetica Neue',Arial,sans-serif";

// Computed chart data
const DATA = {
  c1: {
    type: 'multiline',
    labels: ['Entry','M1','M2','M3','M4','M5','M6','M7','M8','M9','M10','M11','M12','M13','M14','M15','M16','M17','M18'],
    series: [
      { name:'Omnipresent', color:TEAL,   data:[100,108,118,130,145,162,182,205,230,260,285,308,320,null,null,null,null,null,null], dash:[] },
      { name:'Personio',    color:TEAL_D, data:[100,106,115,127,142,160,178,196,215,235,248,258,268,276,282,288,253,260,null], dash:[] },
      { name:'Civica',      color:'#8AC4B8', data:[100,100,101,105,112,122,134,148,163,null,null,null,null,null,null,null,null,null,null], dash:[4,3] }
    ],
    yMin:80, yLabel:'Indexed ARR',
    annotations:[{idx:3,label:'ICP\nredefined',color:TEAL},{idx:7,label:'Channel\nshift',color:TEAL_D}]
  },
  c2: {
    type: 'multiline',
    labels: ['Entry','Q1','Q2','Q3','Q4','Q5','Q6','Q7','Q8'],
    series: [
      { name:'Rev/FTE',   color:TEAL,  data:[100,112,128,148,173,210,268,340,420], dash:[] },
      { name:'Headcount', color:AMBER, data:[100,120,135,148,155,165,172,180,188], dash:[5,3] }
    ],
    yMin:80, yLabel:'Index (entry = 100)',
    annotations:[{idx:2,label:'Upmarket\nreposition',color:TEAL_D},{idx:5,label:'Motion\nsystemised',color:TEAL}]
  },
  c3: {
    type: 'grouped-bar',
    labels: ['Lead\nquality','Qualific-\nation','Demo','Proposal','Close\nrate','Attainment'],
    before: [100,100,100,100,100,100],
    after:  [118,126,135,148,138,165],
    yMin:80, yLabel:'Conversion index'
  },
  c4: {
    type: 'multiline',
    labels: ['Entry','M3','M6','M8','M10','M12','M14','M18','M24','M30','M36','M42','M48'],
    series: [
      { name:'NRR index', color:TEAL, data:[100,97,93,86,87,93,105,120,133,144,153,160,165], dash:[] }
    ],
    yMin:78, yLabel:'NRR index',
    dipRange:[2,4],
    annotations:[
      {idx:3,label:'Expansion\nfails',color:RED},
      {idx:6,label:'Redesigned\nactivation',color:TEAL}
    ]
  },
  c5: {
    type: 'multiline',
    labels: ['Entry','M1','M2','M3','M4','M5','M6','M7','M8','M9','M10','M11','M12'],
    series: [
      { name:'Revenue index',    color:TEAL,  data:[100,112,128,148,170,196,225,252,272,288,300,308,316], dash:[] },
      { name:'Cost:rev index ↓', color:AMBER, data:[100,102,100,96,92,86,80,73,67,62,58,55,52], dash:[5,3] }
    ],
    yMin:40, yLabel:'Index (entry = 100)',
    annotations:[{idx:2,label:'ICP\nprecision',color:TEAL_D},{idx:5,label:'Channel\nfocus',color:TEAL},{idx:9,label:'NRR\ninflects',color:AMBER}]
  }
};

function renderChart(canvasId, cfg) {
  const canvas = document.getElementById(canvasId);
  if (!canvas) return;
  const wrap = canvas.parentElement;
  const W = wrap.offsetWidth;
  const H = wrap.offsetHeight;
  if (!W || !H) return;

  const dpr = window.devicePixelRatio || 1;
  canvas.width  = W * dpr;
  canvas.height = H * dpr;
  const ctx = canvas.getContext('2d');
  ctx.scale(dpr, dpr);
  ctx.clearRect(0, 0, W, H);

  const PAD = { top:28, right:14, bottom:36, left:46 };
  const cW = W - PAD.left - PAD.right;
  const cH = H - PAD.top  - PAD.bottom;

  ctx.font = `10px ${FONT}`;

  if (cfg.type === 'multiline') {
    drawMultiLine(ctx, cfg, W, H, PAD, cW, cH);
  } else if (cfg.type === 'grouped-bar') {
    drawGroupedBar(ctx, cfg, W, H, PAD, cW, cH);
  }
}

function getY(val, yMin, yMax, cH, padTop) {
  return padTop + cH - ((val - yMin) / (yMax - yMin)) * cH;
}

function getX(idx, total, cW, padLeft) {
  return padLeft + (idx / (total - 1)) * cW;
}

function drawMultiLine(ctx, cfg, W, H, PAD, cW, cH) {
  const { labels, series, yMin: rawMin, yLabel, annotations, dipRange } = cfg;
  const allVals = series.flatMap(s => s.data.filter(v => v !== null));
  const yMax = Math.ceil(Math.max(...allVals) * 1.08 / 50) * 50;
  const yMin = rawMin;

  // Grid lines
  const ySteps = 5;
  for (let i = 0; i <= ySteps; i++) {
    const v = yMin + (yMax - yMin) * i / ySteps;
    const y = getY(v, yMin, yMax, cH, PAD.top);
    ctx.beginPath();
    ctx.strokeStyle = i === 0 ? 'rgba(0,0,0,.12)' : 'rgba(0,0,0,.05)';
    ctx.lineWidth = i === 0 ? 1 : 0.5;
    ctx.moveTo(PAD.left, y); ctx.lineTo(PAD.left + cW, y);
    ctx.stroke();
    // Y label
    ctx.fillStyle = INK3;
    ctx.font = `9px ${FONT}`;
    ctx.textAlign = 'right';
    ctx.fillText(Math.round(v), PAD.left - 5, y + 3);
  }

  // Dip shading (slide 4)
  if (dipRange) {
    const x0 = getX(dipRange[0], labels.length, cW, PAD.left);
    const x1 = getX(dipRange[1], labels.length, cW, PAD.left);
    ctx.fillStyle = 'rgba(192,57,43,.07)';
    ctx.fillRect(x0, PAD.top, x1 - x0, cH);
  }

  // X labels
  ctx.fillStyle = INK3; ctx.font = `9px ${FONT}`; ctx.textAlign = 'center';
  const step = Math.ceil(labels.length / 8);
  labels.forEach((l, i) => {
    if (i % step !== 0 && i !== labels.length - 1) return;
    const x = getX(i, labels.length, cW, PAD.left);
    ctx.fillText(l, x, H - 6);
  });

  // Annotations (dashed vertical lines)
  if (annotations) {
    annotations.forEach(a => {
      const x = getX(a.idx, labels.length, cW, PAD.left);
      ctx.save();
      ctx.setLineDash([3,3]);
      ctx.strokeStyle = a.color || TEAL_D;
      ctx.lineWidth = 1;
      ctx.globalAlpha = 0.55;
      ctx.beginPath(); ctx.moveTo(x, PAD.top); ctx.lineTo(x, PAD.top + cH); ctx.stroke();
      ctx.globalAlpha = 1;
      ctx.fillStyle = a.color || TEAL_D;
      ctx.font = `bold 7.5px ${FONT}`; ctx.textAlign = 'center';
      const lines = (a.label || '').split('\n');
      lines.forEach((l, li) => ctx.fillText(l, x, PAD.top + 8 + li * 10));
      ctx.restore();
    });
  }

  // Y axis label
  ctx.save();
  ctx.translate(11, PAD.top + cH / 2);
  ctx.rotate(-Math.PI / 2);
  ctx.fillStyle = INK3; ctx.font = `8px ${FONT}`; ctx.textAlign = 'center';
  ctx.fillText(yLabel, 0, 0);
  ctx.restore();

  // Lines
  series.forEach(s => {
    const pts = s.data.map((v, i) => ({ x: getX(i, labels.length, cW, PAD.left), y: v !== null ? getY(v, yMin, yMax, cH, PAD.top) : null }));
    ctx.beginPath();
    ctx.strokeStyle = s.color;
    ctx.lineWidth = 2.2;
    ctx.setLineDash(s.dash || []);
    let first = true;
    pts.forEach(p => {
      if (p.y === null) { first = true; return; }
      if (first) { ctx.moveTo(p.x, p.y); first = false; }
      else ctx.lineTo(p.x, p.y);
    });
    ctx.stroke();
    ctx.setLineDash([]);

    // Dots on data points
    pts.forEach(p => {
      if (p.y === null) return;
      ctx.beginPath();
      ctx.arc(p.x, p.y, 2.5, 0, Math.PI * 2);
      ctx.fillStyle = s.color; ctx.fill();
    });
  });
}

function drawGroupedBar(ctx, cfg, W, H, PAD, cW, cH) {
  const { labels, before, after, yMin: rawMin, yLabel } = cfg;
  const yMax = Math.ceil(Math.max(...after) * 1.12 / 20) * 20;
  const yMin = rawMin;
  const n = labels.length;
  const groupW = cW / n;
  const barW = groupW * 0.32;
  const gap = groupW * 0.06;

  // Grid
  for (let i = 0; i <= 5; i++) {
    const v = yMin + (yMax - yMin) * i / 5;
    const y = getY(v, yMin, yMax, cH, PAD.top);
    ctx.beginPath();
    ctx.strokeStyle = i === 0 ? 'rgba(0,0,0,.12)' : 'rgba(0,0,0,.05)';
    ctx.lineWidth = i === 0 ? 1 : 0.5;
    ctx.moveTo(PAD.left, y); ctx.lineTo(PAD.left + cW, y);
    ctx.stroke();
    ctx.fillStyle = INK3; ctx.font = `9px ${FONT}`; ctx.textAlign = 'right';
    ctx.fillText(Math.round(v), PAD.left - 5, y + 3);
  }

  // Y label
  ctx.save();
  ctx.translate(11, PAD.top + cH / 2);
  ctx.rotate(-Math.PI / 2);
  ctx.fillStyle = INK3; ctx.font = `8px ${FONT}`; ctx.textAlign = 'center';
  ctx.fillText(yLabel, 0, 0);
  ctx.restore();

  labels.forEach((lbl, i) => {
    const gx = PAD.left + i * groupW;
    const midX = gx + groupW / 2;

    // Before bar
    const bVal = before[i];
    const bY = getY(bVal, yMin, yMax, cH, PAD.top);
    const bH = getY(yMin, yMin, yMax, cH, PAD.top) - bY;
    ctx.fillStyle = 'rgba(200,200,196,.55)';
    ctx.fillRect(midX - barW - gap / 2, bY, barW, bH);

    // After bar — highlight last (attainment) in full teal
    const aVal = after[i];
    const aY = getY(aVal, yMin, yMax, cH, PAD.top);
    const aH = getY(yMin, yMin, yMax, cH, PAD.top) - aY;
    ctx.fillStyle = i === n - 1 ? TEAL : 'rgba(77,184,160,.6)';
    ctx.fillRect(midX + gap / 2, aY, barW, aH);

    // Value label on after bar
    ctx.fillStyle = i === n - 1 ? TEAL_D : INK2;
    ctx.font = `bold 8px ${FONT}`; ctx.textAlign = 'center';
    ctx.fillText(aVal, midX + gap / 2 + barW / 2, aY - 3);

    // X label (handle multi-line)
    ctx.fillStyle = INK3; ctx.font = `8px ${FONT}`; ctx.textAlign = 'center';
    const lines = lbl.split('\n');
    lines.forEach((l, li) => ctx.fillText(l, midX, H - 18 + li * 10));
  });
}

// ── RENDER ALL CHARTS ──────────────────────────────────────────────
function renderAll() {
  Object.entries(DATA).forEach(([id, cfg]) => renderChart(id, cfg));
}

// Render after DOM settles (fonts etc.)
window.addEventListener('load', () => setTimeout(renderAll, 80));
window.addEventListener('resize', () => setTimeout(renderAll, 80));
</script>
</body>
</html>
