# template.html

The kiss page template. Copy everything inside the html block below.

```html
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>How a Thing Travels</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:opsz,wght@12..96,500;12..96,700;12..96,800&family=Atkinson+Hyperlegible:wght@400;700&family=JetBrains+Mono:wght@400;600&display=swap">
<style>
/* Layout: a story told top to bottom, one stamped step per stop, picture left, few words right */
:root {
  --bg: #F0EEE6;
  --surface: #FFFFFF;
  --ink: #141413;
  --muted: #5F5D57;
  --line: #D6D2C6;
  --accent: #D97757;
  --accent-ink: #1F0C04;
  --yes: #4E6B38;
  --no: #A8323E;
  --font-display: "Bricolage Grotesque", "Avenir Next", system-ui, sans-serif;
  --font-body: "Atkinson Hyperlegible", "Segoe UI", system-ui, sans-serif;
  --font-mono: "JetBrains Mono", ui-monospace, "SF Mono", Menlo, monospace;
  color-scheme: light;
}
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --bg: #141413; --surface: #1F1E1C; --ink: #F0EEE6; --muted: #A6A398; --line: #3B3934;
    --accent: #DE8463; --accent-ink: #1F0C04; --yes: #93B57C; --no: #E8848A;
    color-scheme: dark;
  }
}
:root[data-theme="dark"] {
  --bg: #141413; --surface: #1F1E1C; --ink: #F0EEE6; --muted: #A6A398; --line: #3B3934;
  --accent: #DE8463; --accent-ink: #1F0C04; --yes: #93B57C; --no: #E8848A;
  color-scheme: dark;
}

body { margin: 0; background: var(--bg); color: var(--ink); font-family: var(--font-body); font-size: 17px; line-height: 1.55; }
.page { max-width: 1060px; margin: 0 auto; padding-inline: 20px; padding-block: 40px 72px; display: grid; gap: 56px; }

/* hero */
.hero { display: grid; gap: 14px; max-width: 760px; }
.eyebrow { font-family: var(--font-mono); font-size: 13px; letter-spacing: .08em; text-transform: uppercase; color: var(--muted); }
h1 { font-family: var(--font-display); font-weight: 800; font-size: clamp(38px, 6vw, 64px); line-height: 1.02; margin: 0; text-wrap: balance; letter-spacing: -.01em; }
.hero p { margin: 0; font-size: 20px; color: var(--muted); max-width: 60ch; }
.hero b { color: var(--ink); }

/* route strip */
.route { display: flex; flex-wrap: wrap; gap: 8px; align-items: center; font-family: var(--font-mono); font-size: 13px; }
.route span.stop { background: var(--surface); border: 1px solid var(--line); border-radius: 999px; padding: 6px 12px; }
.route span.arrow { color: var(--muted); }

/* steps */
.step { display: grid; grid-template-columns: minmax(0, 360px) minmax(0, 1fr); gap: 36px; align-items: center; }
.step + .step { border-top: 1px dashed var(--line); padding-top: 48px; }
.pic { background: var(--surface); border: 1px solid var(--line); border-radius: 18px; padding: 14px; }
.pic svg { display: block; width: 100%; height: auto; }
.words { display: grid; gap: 12px; min-width: 0; }
.head { display: flex; gap: 14px; align-items: center; }
.stamp { flex: none; width: 52px; height: 52px; display: grid; place-items: center; border: 2px dashed var(--accent); border-radius: 6px; font-family: var(--font-display); font-weight: 800; font-size: 24px; color: var(--ink); background: color-mix(in srgb, var(--accent) 16%, transparent); }
.stamp.why { font-size: 15px; letter-spacing: .04em; text-transform: uppercase; }
.small { margin: 0; font-size: 14px; color: var(--muted); }
.reasons { margin: 0; padding-left: 22px; display: grid; gap: 10px; max-width: 62ch; }
.reasons li::marker { font-family: var(--font-display); font-weight: 800; color: var(--muted); }
h2 { font-family: var(--font-display); font-weight: 700; font-size: clamp(24px, 3.2vw, 32px); line-height: 1.12; margin: 0; text-wrap: balance; }
.words p { margin: 0; max-width: 62ch; }
.big-idea { font-family: var(--font-display); font-weight: 700; font-size: 21px; line-height: 1.3; border-left: 4px solid var(--accent); padding-left: 14px; }

code, .tag { font-family: var(--font-mono); font-size: .82em; }
code { background: color-mix(in srgb, var(--ink) 8%, transparent); padding: 1px 6px; border-radius: 5px; overflow-wrap: anywhere; }
.tags { display: flex; flex-wrap: wrap; gap: 6px; }
.tag { border: 1px solid var(--line); background: var(--surface); border-radius: 6px; padding: 3px 8px; color: var(--muted); }

/* small tables */
.scroll { overflow-x: auto; }
table { border-collapse: collapse; width: 100%; font-size: 15px; font-variant-numeric: tabular-nums; }
th, td { text-align: left; padding: 8px 10px; border-bottom: 1px solid var(--line); vertical-align: top; }
td code { overflow-wrap: break-word; }
th { font-family: var(--font-mono); font-size: 12px; letter-spacing: .06em; text-transform: uppercase; color: var(--muted); font-weight: 600; }
.pill { display: inline-block; font-family: var(--font-mono); font-size: 12px; font-weight: 600; border-radius: 999px; padding: 2px 9px; white-space: nowrap; }
.pill.yes { background: color-mix(in srgb, var(--yes) 16%, transparent); color: var(--yes); }
.pill.no { background: color-mix(in srgb, var(--no) 14%, transparent); color: var(--no); }
.pill.new { background: color-mix(in srgb, var(--accent) 26%, transparent); color: var(--ink); }

/* before / after */
.ba { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 12px; }
.ba > div { border: 1px solid var(--line); border-radius: 12px; padding: 12px 14px; background: var(--surface); display: grid; gap: 6px; }
.ba h3 { margin: 0; font-family: var(--font-mono); font-size: 12px; letter-spacing: .08em; text-transform: uppercase; color: var(--muted); font-weight: 600; }
.ba ul { margin: 0; padding-left: 18px; display: grid; gap: 4px; font-size: 15px; }

/* doors */
.doors { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 12px; }
.door { border: 1px solid var(--line); border-radius: 12px; padding: 14px; background: var(--surface); display: grid; gap: 8px; align-content: start; min-width: 0; }
.door h3 { margin: 0; font-family: var(--font-display); font-size: 19px; }
.door p { margin: 0; font-size: 15px; color: var(--muted); }
pre { margin: 0; font-family: var(--font-mono); font-size: 12.5px; line-height: 1.5; background: var(--bg); border: 1px solid var(--line); border-radius: 8px; padding: 10px 12px; overflow-x: auto; }

/* status */
.status { border: 2px solid var(--ink); border-radius: 18px; padding: 22px; display: grid; gap: 14px; background: var(--surface); }
.status h2 { font-size: 26px; }
.status ul { list-style: none; margin: 0; padding: 0; display: grid; gap: 10px; }
.status li { display: grid; grid-template-columns: 112px minmax(0, 1fr); gap: 12px; align-items: baseline; }
a { color: inherit; text-decoration-color: var(--accent); text-decoration-thickness: 2px; text-underline-offset: 3px; }

/* svg paint */
.s-ink { stroke: var(--ink); }
.s-muted { stroke: var(--muted); }
.s-line { stroke: var(--line); }
.s-accent { stroke: var(--accent); }
.f-surface { fill: var(--surface); }
.f-bg { fill: var(--bg); }
.f-ink { fill: var(--ink); }
.f-muted { fill: var(--muted); }
.f-accent { fill: var(--accent); }
.f-yes { fill: var(--yes); }
.f-no { fill: var(--no); }
.f-line { fill: var(--line); }
.svg-t { font-family: var(--font-mono); font-size: 12px; fill: var(--ink); }
.svg-tm { font-family: var(--font-mono); font-size: 11px; fill: var(--muted); }
.svg-tb { font-family: var(--font-display); font-weight: 700; font-size: 15px; fill: var(--ink); }
.svg-ta { font-family: var(--font-display); font-weight: 700; font-size: 14px; fill: var(--accent-ink); }

a:focus-visible { outline: 3px solid var(--accent); outline-offset: 2px; }

@media (max-width: 760px) {
  body { font-size: 16px; }
  .step { grid-template-columns: minmax(0, 1fr); gap: 20px; }
  .ba, .doors { grid-template-columns: minmax(0, 1fr); }
  .status li { grid-template-columns: minmax(0, 1fr); gap: 2px; }
}
</style>
</head>
<body>
<main class="page">

  <header class="hero">
    <div class="eyebrow">Topic · explained simply</div>
    <h1>How a thing travels</h1>
    <p>Someone does <b>the first thing</b>. Here is every stop it makes, from <b>where it starts</b> to <b>where the answer comes from</b>.</p>
    <div class="route" aria-label="The route in short">
      <span class="stop">first stop</span><span class="arrow">→</span>
      <span class="stop">real_name</span><span class="arrow">→</span>
      <span class="stop">third stop</span><span class="arrow">→</span>
      <span class="stop">real_name</span>
    </div>
  </header>

  <!-- 1 -->
  <section class="step">
    <div class="pic">
      <svg viewBox="0 0 340 220" role="img" aria-label="A phone sends two letters">
        <rect x="34" y="14" width="118" height="192" rx="20" class="f-surface s-ink" stroke-width="3"/>
        <rect x="46" y="36" width="94" height="146" rx="8" class="f-bg"/>
        <rect x="56" y="52" width="74" height="8" rx="4" class="f-line"/>
        <rect x="56" y="68" width="56" height="8" rx="4" class="f-line"/>
        <rect x="56" y="84" width="66" height="8" rx="4" class="f-line"/>
        <rect x="56" y="140" width="74" height="28" rx="14" class="f-accent"/>
        <text x="93" y="159" text-anchor="middle" class="svg-ta">Continue</text>
        <path d="M152 120 C190 100, 200 70, 236 60" fill="none" class="s-muted" stroke-width="2" stroke-dasharray="5 5"/>
        <path d="M152 140 C196 150, 206 160, 236 152" fill="none" class="s-muted" stroke-width="2" stroke-dasharray="5 5"/>
        <g transform="translate(238 38)">
          <rect width="78" height="48" rx="6" class="f-surface s-ink" stroke-width="2.5"/>
          <path d="M3 4 L39 28 L75 4" fill="none" class="s-ink" stroke-width="2.5"/>
          <text x="39" y="66" text-anchor="middle" class="svg-tm">real_name</text>
        </g>
        <g transform="translate(238 128)">
          <rect width="78" height="48" rx="6" class="f-surface s-ink" stroke-width="2.5"/>
          <path d="M3 4 L39 28 L75 4" fill="none" class="s-ink" stroke-width="2.5"/>
          <text x="39" y="66" text-anchor="middle" class="svg-tm">real_name</text>
        </g>
      </svg>
    </div>
    <div class="words">
      <div class="head"><div class="stamp">1</div><h2>One claim, in plain words</h2></div>
      <p>What happens, in short sentences. The plain word comes first, then the real name: <b>a letter</b> (<code>real_name</code>).</p>
      <p>Under the hood, with the real names and numbers the drawing shows.</p>
      <div class="tags">
        <span class="tag">letter = real_name</span>
        <span class="tag">button = real_name</span>
      </div>
    </div>
  </section>

  <!-- 2 -->
  <section class="step">
    <div class="pic">
      <svg viewBox="0 0 340 220" role="img" aria-label="Three places to look, in order; the first one found wins">
        <g transform="translate(18 30)">
          <rect width="96" height="128" rx="12" class="f-surface s-ink" stroke-width="2.5"/>
          <text x="48" y="34" text-anchor="middle" class="svg-tb">1</text>
          <rect x="18" y="48" width="60" height="38" rx="5" class="f-accent"/>
          <path d="M20 50 L48 70 L76 50" fill="none" class="s-ink" stroke-width="2"/>
          <text x="48" y="110" text-anchor="middle" class="svg-tm">first place</text>
        </g>
        <g transform="translate(122 30)">
          <rect width="96" height="128" rx="12" class="f-surface s-line" stroke-width="2"/>
          <text x="48" y="34" text-anchor="middle" class="svg-tb">2</text>
          <circle cx="48" cy="60" r="13" class="f-line"/>
          <rect x="28" y="76" width="40" height="14" rx="7" class="f-line"/>
          <text x="48" y="110" text-anchor="middle" class="svg-tm">second place</text>
        </g>
        <g transform="translate(226 30)">
          <rect width="96" height="128" rx="12" class="f-surface s-line" stroke-width="2"/>
          <text x="48" y="34" text-anchor="middle" class="svg-tb">3</text>
          <circle cx="44" cy="64" r="16" fill="none" class="s-muted" stroke-width="3"/>
          <path d="M56 76 L68 88" class="s-muted" stroke-width="4"/>
          <text x="48" y="110" text-anchor="middle" class="svg-tm">third place</text>
        </g>
        <text x="170" y="196" text-anchor="middle" class="svg-t">first one found wins</text>
      </svg>
    </div>
    <div class="words">
      <div class="head"><div class="stamp">2</div><h2>A rule that decides</h2></div>
      <p>A table when the reader must compare a few cases.</p>
      <div class="scroll">
        <table>
          <thead><tr><th>Case</th><th>What happens</th></tr></thead>
          <tbody>
            <tr><td><code>real_name</code></td><td><span class="pill yes">yes</span> and why</td></tr>
            <tr><td><code>real_name</code></td><td><span class="pill no">no</span> and why</td></tr>
            <tr><td><code>real_name</code></td><td><span class="pill new">new</span> what changed</td></tr>
          </tbody>
        </table>
      </div>
      <p class="big-idea">The one sentence a reader repeats to a colleague.</p>
    </div>
  </section>

  <!-- 3 -->
  <section class="step">
    <div class="pic">
      <svg viewBox="0 0 340 220" role="img" aria-label="Two doors in: one with a ticket, one with a signed-in person">
        <g transform="translate(24 20)">
          <rect width="128" height="176" rx="12" class="f-surface s-ink" stroke-width="2.5"/>
          <rect x="18" y="20" width="92" height="120" rx="46" class="f-bg s-ink" stroke-width="2"/>
          <circle cx="92" cy="84" r="5" class="f-ink"/>
          <rect x="30" y="58" width="52" height="30" rx="4" class="f-accent"/>
          <text x="56" y="78" text-anchor="middle" class="svg-ta">ticket</text>
          <text x="64" y="162" text-anchor="middle" class="svg-tm">door one</text>
        </g>
        <g transform="translate(188 20)">
          <rect width="128" height="176" rx="12" class="f-surface s-ink" stroke-width="2.5"/>
          <rect x="18" y="20" width="92" height="120" rx="46" class="f-bg s-ink" stroke-width="2"/>
          <circle cx="92" cy="84" r="5" class="f-ink"/>
          <circle cx="56" cy="66" r="12" class="f-ink"/>
          <rect x="40" y="80" width="32" height="18" rx="8" class="f-ink"/>
          <text x="64" y="162" text-anchor="middle" class="svg-tm">door two</text>
        </g>
      </svg>
    </div>
    <div class="words">
      <div class="head"><div class="stamp">3</div><h2>Two ways in</h2></div>
      <p>Doors when there are two real paths, each with its own code.</p>
      <div class="doors">
        <div class="door">
          <h3>Door 1 · who uses it</h3>
          <p>When this path applies, in one sentence.</p>
<pre>GET /real/path?key=…

{ "answer": true }</pre>
        </div>
        <div class="door">
          <h3>Door 2 · who uses it</h3>
          <p>When this path applies, in one sentence.</p>
<pre>GET /real/path

{ "answer": true }</pre>
        </div>
      </div>
    </div>
  </section>

  <!-- 4 -->
  <section class="step">
    <div class="pic">
      <svg viewBox="0 0 340 220" role="img" aria-label="Before: the letter went to the bin. After: it fills two drawers.">
        <text x="85" y="28" text-anchor="middle" class="svg-tb">before</text>
        <text x="255" y="28" text-anchor="middle" class="svg-tb">after</text>
        <line x1="170" y1="16" x2="170" y2="206" class="s-line" stroke-width="2" stroke-dasharray="6 6"/>
        <g transform="translate(46 44)">
          <rect width="78" height="48" rx="6" class="f-surface s-ink" stroke-width="2.5"/>
          <path d="M3 4 L39 28 L75 4" fill="none" class="s-ink" stroke-width="2.5"/>
        </g>
        <path d="M85 98 L85 126" class="s-muted" stroke-width="2.5"/>
        <path d="M58 132 L112 132 L104 192 L66 192 Z" class="f-line"/>
        <rect x="52" y="126" width="66" height="8" rx="3" class="f-muted"/>
        <text x="85" y="210" text-anchor="middle" class="svg-tm">ignored</text>
        <g transform="translate(216 44)">
          <rect width="78" height="48" rx="6" class="f-surface s-ink" stroke-width="2.5"/>
          <path d="M3 4 L39 28 L75 4" fill="none" class="s-ink" stroke-width="2.5"/>
        </g>
        <path d="M240 98 L210 126 M270 98 L300 126" class="s-ink" stroke-width="2.5"/>
        <rect x="178" y="130" width="72" height="40" rx="6" class="f-yes" opacity=".2"/>
        <text x="214" y="148" text-anchor="middle" class="svg-t">drawer</text>
        <text x="214" y="162" text-anchor="middle" class="svg-tm">real_name</text>
        <rect x="262" y="130" width="72" height="40" rx="6" class="f-yes" opacity=".2"/>
        <text x="298" y="148" text-anchor="middle" class="svg-t">drawer</text>
        <text x="298" y="162" text-anchor="middle" class="svg-tm">real_name</text>
        <text x="255" y="196" text-anchor="middle" class="svg-tm">saved</text>
      </svg>
    </div>
    <div class="words">
      <div class="head"><div class="stamp">4</div><h2>What changes</h2></div>
      <div class="ba">
        <div>
          <h3>Before</h3>
          <ul>
            <li>One short fact.</li>
            <li>One short fact.</li>
          </ul>
        </div>
        <div>
          <h3>After</h3>
          <ul>
            <li>One short fact.</li>
            <li>One short fact.</li>
          </ul>
        </div>
      </div>
    </div>
  </section>

  <!-- why -->
  <section class="step">
    <div class="pic">
      <svg viewBox="0 0 340 220" role="img" aria-label="The naive way sees one box; the real way sees all three">
        <rect x="30" y="34" width="84" height="64" rx="10" class="f-bg s-ink" stroke-width="2"/>
        <rect x="128" y="34" width="84" height="64" rx="10" class="f-bg s-line" stroke-width="2"/>
        <rect x="226" y="34" width="84" height="64" rx="10" class="f-bg s-line" stroke-width="2"/>
        <text x="72" y="71" text-anchor="middle" class="svg-t">one</text>
        <text x="170" y="71" text-anchor="middle" class="svg-t">two</text>
        <text x="268" y="71" text-anchor="middle" class="svg-t">three</text>
        <rect x="22" y="26" width="100" height="80" rx="14" fill="none" class="s-muted" stroke-width="3"/>
        <rect x="14" y="14" width="312" height="104" rx="18" fill="none" class="s-accent" stroke-width="3" stroke-dasharray="8 6"/>
        <rect x="30" y="148" width="16" height="16" rx="4" fill="none" class="s-muted" stroke-width="3"/>
        <text x="54" y="161" class="svg-t">naive way: sees one</text>
        <rect x="30" y="176" width="16" height="16" rx="4" fill="none" class="s-accent" stroke-width="3" stroke-dasharray="4 3"/>
        <text x="54" y="189" class="svg-t">real way: sees all three</text>
      </svg>
    </div>
    <div class="words">
      <div class="head"><div class="stamp why">why</div><h2>Why it works this way</h2></div>
      <ol class="reasons">
        <li><b>A reason in bold.</b> One or two sentences with the real name.</li>
        <li><b>A reason in bold.</b> One or two sentences with the real name.</li>
      </ol>
    </div>
  </section>

  <section class="status" aria-labelledby="end">
    <h2 id="end">Before you rely on it</h2>
    <ul>
      <li><span class="pill no">catch</span><span>The one thing that bites people, and what to do instead.</span></li>
      <li><span class="pill new">ask next</span><span><b>A question a sharp reader asks next?</b> A short answer.</span></li>
      <li><span class="pill new">simplified</span><span>What this page leaves out on purpose, in one line.</span></li>
      <li><span class="pill yes">sources</span><span><a href="https://example.com/spec">The spec</a>, <a href="https://example.com/docs">the official docs</a> or <code>src/the/file.ts</code>.</span></li>
      <li><span class="pill no">not verified</span><span>A claim you could not check.</span></li>
    </ul>
  </section>

</main>
</body>
</html>
```
