# example.html

A finished kiss page at `normal` depth: how an email reaches an inbox. Copy its drawing style, not its topic. Everything inside the html block below is the page.

```html
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>How an Email Travels</title>
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
    <div class="eyebrow">Email · explained simply</div>
    <h1>How an email travels</h1>
    <p>You press <b>Send</b> on a note from alice@example.com to bob@example.net. It makes <b>two hand-offs</b> and passes <b>three checks</b> before it lands in Bob's inbox.</p>
    <div class="route" aria-label="The route in short">
      <span class="stop">Send</span><span class="arrow">→</span>
      <span class="stop">:587</span><span class="arrow">→</span>
      <span class="stop">MX lookup</span><span class="arrow">→</span>
      <span class="stop">:25</span><span class="arrow">→</span>
      <span class="stop">SPF · DKIM · DMARC</span><span class="arrow">→</span>
      <span class="stop">INBOX</span>
    </div>
  </header>

  <!-- 1 -->
  <section class="step">
    <div class="pic">
      <svg viewBox="0 0 340 220" role="img" aria-label="A laptop sends the letter to its own post box, which opens only with a key">
        <rect x="24" y="44" width="122" height="88" rx="10" class="f-surface s-ink" stroke-width="3"/>
        <rect x="34" y="54" width="102" height="68" rx="4" class="f-bg"/>
        <rect x="44" y="64" width="70" height="7" rx="3.5" class="f-line"/>
        <rect x="44" y="78" width="54" height="7" rx="3.5" class="f-line"/>
        <rect x="44" y="96" width="44" height="18" rx="9" class="f-surface s-ink" stroke-width="2"/>
        <text x="66" y="109" text-anchor="middle" class="svg-t">Send</text>
        <path d="M16 134 H154 L162 148 H12 Z" class="f-line s-ink" stroke-width="2.5" stroke-linejoin="round"/>
        <text x="85" y="172" text-anchor="middle" class="svg-tm">your app</text>
        <path d="M148 80 C162 80, 170 92, 182 96" fill="none" class="s-muted" stroke-width="2" stroke-dasharray="5 5"/>
        <text x="269" y="44" text-anchor="middle" class="svg-tm">your post office</text>
        <text x="269" y="61" text-anchor="middle" class="svg-t">:587</text>
        <rect x="226" y="70" width="86" height="100" rx="14" class="f-ink"/>
        <rect x="240" y="92" width="58" height="10" rx="5" class="f-bg"/>
        <rect x="263" y="170" width="12" height="36" class="f-ink"/>
        <circle cx="198" cy="97" r="13" class="f-accent"/>
        <circle cx="194" cy="97" r="4.5" class="f-surface"/>
        <rect x="208" y="93" width="46" height="8" rx="2" class="f-accent"/>
        <rect x="230" y="100" width="6" height="9" class="f-accent"/>
        <rect x="242" y="100" width="6" height="9" class="f-accent"/>
        <text x="184" y="130" text-anchor="middle" class="svg-tm">SMTP AUTH</text>
      </svg>
    </div>
    <div class="words">
      <div class="head"><div class="stamp">1</div><h2>Your app posts it at your own post office</h2></div>
      <p>Your app never talks to Bob's server. It drops the letter in <b>your own post box</b>, and the box opens only with your login.</p>
      <p>The app (the <code>MUA</code>) connects to your server's submission port, <code>587</code>, and logs in with <code>SMTP AUTH</code>. By default, the submission server must refuse mail from a session that has not logged in.</p>
      <div class="tags">
        <span class="tag">your app = MUA</span>
        <span class="tag">post box = port 587</span>
        <span class="tag">key = SMTP AUTH</span>
      </div>
    </div>
  </section>

  <!-- 2 -->
  <section class="step">
    <div class="pic">
      <svg viewBox="0 0 340 220" role="img" aria-label="A card for example.net lists two mail servers; the MX 10 row is tried first">
        <rect x="36" y="12" width="96" height="24" rx="5" class="f-surface s-ink" stroke-width="2.5"/>
        <text x="84" y="29" text-anchor="middle" class="svg-tm">DNS card</text>
        <rect x="24" y="34" width="214" height="152" rx="10" class="f-surface s-ink" stroke-width="2.5"/>
        <text x="40" y="62" class="svg-tb">example.net</text>
        <rect x="36" y="76" width="190" height="28" rx="6" class="f-accent"/>
        <text x="46" y="95" class="svg-ta">MX 10  mx1.example.net</text>
        <rect x="36" y="112" width="190" height="28" rx="6" class="f-bg"/>
        <text x="46" y="131" class="svg-t">MX 20  mx2.example.net</text>
        <rect x="36" y="148" width="190" height="26" rx="6" class="f-bg"/>
        <text x="46" y="166" class="svg-tm">TXT  v=spf1 …</text>
        <circle cx="276" cy="104" r="26" fill="none" class="s-ink" stroke-width="4"/>
        <path d="M295 123 L318 146" class="s-ink" stroke-width="8" stroke-linecap="round"/>
        <text x="282" y="184" text-anchor="middle" class="svg-tm">your server</text>
        <text x="282" y="198" text-anchor="middle" class="svg-tm">asks</text>
      </svg>
    </div>
    <div class="words">
      <div class="head"><div class="stamp">2</div><h2>Your post office looks up Bob's in DNS</h2></div>
      <p>Your server reads the part after the @ and asks DNS who takes mail for <code>example.net</code>. The answer is a short list, best first.</p>
      <p>Each <code>MX</code> record names a host and a preference. Lower numbers go first, so <code>mx2</code> gets the letter only when <code>mx1</code> does not answer. With no MX record at all, the domain itself is the target.</p>
<pre>$ dig +short MX example.net
10 mx1.example.net.   # example values
20 mx2.example.net.</pre>
      <div class="tags">
        <span class="tag">card = DNS record</span>
        <span class="tag">row = MX record</span>
      </div>
    </div>
  </section>

  <!-- 3 -->
  <section class="step">
    <div class="pic">
      <svg viewBox="0 0 340 220" role="img" aria-label="Your post office hands the letter to Bob's post office, which sends back a 250 OK receipt">
        <path d="M20 88 L76 52 L132 88 Z" class="f-surface s-line" stroke-width="2" stroke-linejoin="round"/>
        <rect x="28" y="88" width="96" height="78" class="f-surface s-line" stroke-width="2"/>
        <rect x="62" y="126" width="28" height="40" rx="3" class="f-bg s-line" stroke-width="2"/>
        <text x="76" y="186" text-anchor="middle" class="svg-tm">yours</text>
        <path d="M208 88 L264 52 L320 88 Z" class="f-surface s-ink" stroke-width="2.5" stroke-linejoin="round"/>
        <rect x="216" y="88" width="96" height="78" class="f-surface s-ink" stroke-width="2.5"/>
        <rect x="250" y="126" width="28" height="40" rx="3" class="f-bg s-ink" stroke-width="2"/>
        <text x="264" y="186" text-anchor="middle" class="svg-tm">Bob's</text>
        <text x="264" y="200" text-anchor="middle" class="svg-t">:25</text>
        <rect x="142" y="104" width="50" height="32" rx="4" class="f-surface s-ink" stroke-width="2.5"/>
        <path d="M144 106 L167 122 L190 106" fill="none" class="s-ink" stroke-width="2.5"/>
        <path d="M104 150 C134 172, 196 172, 246 152" fill="none" class="s-muted" stroke-width="2" stroke-dasharray="5 5"/>
        <rect x="136" y="36" width="62" height="32" rx="4" class="f-accent"/>
        <text x="167" y="57" text-anchor="middle" class="svg-ta">250 OK</text>
        <path d="M212 70 C206 60, 204 56, 200 54" fill="none" class="s-muted" stroke-width="2" stroke-dasharray="5 5"/>
      </svg>
    </div>
    <div class="words">
      <div class="head"><div class="stamp">3</div><h2>After one receipt, the letter is Bob's server's job</h2></div>
      <p>The two servers talk in short commands on port <code>25</code>. The envelope goes first, then the letter, then a receipt comes back.</p>
      <p><code>MAIL FROM</code> and <code>RCPT TO</code> are the envelope. The <code>From:</code> line Bob sees is inside the letter, sent after <code>DATA</code>.</p>
      <div class="scroll">
        <table>
          <thead><tr><th>Reply</th><th>What happens</th></tr></thead>
          <tbody>
            <tr><td><code>250</code></td><td><span class="pill yes">taken</span> Bob's server now owns the letter.</td></tr>
            <tr><td><code>4xx</code></td><td><span class="pill new">try later</span> Wait at least 30 minutes. Keep trying for 4–5 days.</td></tr>
            <tr><td><code>5xx</code></td><td><span class="pill no">refused</span> Alice gets a bounce.</td></tr>
          </tbody>
        </table>
      </div>
      <div class="tags">
        <span class="tag">envelope = MAIL FROM + RCPT TO</span>
        <span class="tag">receipt = 250 reply</span>
      </div>
    </div>
  </section>

  <!-- 4 -->
  <section class="step">
    <div class="pic">
      <svg viewBox="0 0 340 220" role="img" aria-label="The envelope carries a postmark and a wax seal; a rule book from example.com says what to do with a fake">
        <rect x="20" y="50" width="184" height="120" rx="8" class="f-surface s-ink" stroke-width="3"/>
        <path d="M23 54 L112 114 L201 54" fill="none" class="s-ink" stroke-width="3"/>
        <circle cx="58" cy="132" r="22" fill="none" class="s-muted" stroke-width="2.5" stroke-dasharray="4 3"/>
        <text x="58" y="136" text-anchor="middle" class="svg-t">SPF</text>
        <circle cx="112" cy="114" r="15" class="f-ink"/>
        <text x="112" y="150" text-anchor="middle" class="svg-t">DKIM</text>
        <path d="M204 104 C214 102, 220 100, 228 98" fill="none" class="s-muted" stroke-width="2" stroke-dasharray="5 5"/>
        <rect x="232" y="44" width="82" height="112" rx="6" class="f-accent"/>
        <path d="M244 44 V156" class="s-ink" stroke-width="2" opacity=".35"/>
        <text x="279" y="92" text-anchor="middle" class="svg-ta">DMARC</text>
        <text x="279" y="112" text-anchor="middle" class="svg-ta">p=reject</text>
        <rect x="236" y="156" width="78" height="10" rx="2" class="f-surface s-ink" stroke-width="2"/>
        <text x="275" y="190" text-anchor="middle" class="svg-tm">rule book</text>
      </svg>
    </div>
    <div class="words">
      <div class="head"><div class="stamp">4</div><h2>Bob's server checks the postmark and the seal</h2></div>
      <p>The postmark shows which post office posted it. The wax seal shows nobody changed it. The rule book, written by <code>example.com</code>, says what to do with a fake.</p>
      <div class="scroll">
        <table>
          <thead><tr><th>Check</th><th>Reads</th><th>Proves</th></tr></thead>
          <tbody>
            <tr><td><code>SPF</code></td><td>a <code>v=spf1</code> TXT record of the envelope's domain</td><td>this server may send for it</td></tr>
            <tr><td><code>DKIM</code></td><td>the <code>DKIM-Signature</code> header and a key at <code>&lt;selector&gt;._domainkey</code></td><td>nobody changed the signed parts</td></tr>
            <tr><td><code>DMARC</code></td><td><code>_dmarc.example.com</code>: <code>p=none</code>, <code>quarantine</code> or <code>reject</code></td><td>SPF or DKIM passed for the <code>From:</code> domain</td></tr>
          </tbody>
        </table>
      </div>
      <div class="tags">
        <span class="tag">postmark = SPF</span>
        <span class="tag">wax seal = DKIM signature</span>
        <span class="tag">rule book = DMARC policy</span>
      </div>
      <p class="big-idea">SPF and DKIM prove some domain. DMARC asks if it is the one in From.</p>
    </div>
  </section>

  <!-- 5 -->
  <section class="step">
    <div class="pic">
      <svg viewBox="0 0 340 220" role="img" aria-label="A filing cabinet keeps the letter in the INBOX drawer, and Bob's phone reads it there over IMAP">
        <rect x="20" y="24" width="180" height="180" rx="10" class="f-surface s-ink" stroke-width="3"/>
        <rect x="32" y="36" width="156" height="48" rx="6" class="f-accent"/>
        <text x="46" y="65" class="svg-ta">INBOX</text>
        <rect x="150" y="56" width="26" height="8" rx="4" class="f-surface"/>
        <rect x="32" y="92" width="156" height="48" rx="6" class="f-bg s-line" stroke-width="2"/>
        <text x="46" y="121" class="svg-t">Junk</text>
        <rect x="150" y="112" width="26" height="8" rx="4" class="f-line"/>
        <rect x="32" y="148" width="156" height="48" rx="6" class="f-bg s-line" stroke-width="2"/>
        <text x="46" y="177" class="svg-t">Sent</text>
        <rect x="150" y="168" width="26" height="8" rx="4" class="f-line"/>
        <path d="M190 60 C214 58, 226 74, 244 84" fill="none" class="s-muted" stroke-width="2" stroke-dasharray="5 5"/>
        <text x="283" y="48" text-anchor="middle" class="svg-tm">Bob's app</text>
        <rect x="246" y="60" width="74" height="128" rx="14" class="f-surface s-ink" stroke-width="2.5"/>
        <rect x="254" y="74" width="58" height="96" rx="5" class="f-bg"/>
        <rect x="262" y="86" width="42" height="7" rx="3.5" class="f-line"/>
        <rect x="262" y="100" width="32" height="7" rx="3.5" class="f-line"/>
        <rect x="262" y="114" width="38" height="7" rx="3.5" class="f-line"/>
        <text x="283" y="206" text-anchor="middle" class="svg-t">IMAP :993</text>
      </svg>
    </div>
    <div class="words">
      <div class="head"><div class="stamp">5</div><h2>The letter waits in a drawer, and Bob's app reads it there</h2></div>
      <p>A spam filter reads the letter and picks a drawer: Inbox or Junk. The letter stays in the cabinet, so Bob's phone and laptop both see it.</p>
      <p>Bob's app opens the drawer with <code>IMAP</code> on port <code>993</code> (TLS). <code>INBOX</code> is the main mailbox, and flags such as <code>\Seen</code> live on the server. With <code>IDLE</code>, the server tells the app the moment a letter lands.</p>
      <div class="tags">
        <span class="tag">cabinet = mailbox store</span>
        <span class="tag">drawer = IMAP mailbox</span>
      </div>
    </div>
  </section>

  <!-- why -->
  <section class="step">
    <div class="pic">
      <svg viewBox="0 0 340 220" role="img" aria-label="SPF checks the envelope's sender, but Bob sees the From line inside the letter">
        <text x="90" y="28" text-anchor="middle" class="svg-tb">SPF checks</text>
        <text x="252" y="28" text-anchor="middle" class="svg-tb">Bob sees</text>
        <line x1="170" y1="16" x2="170" y2="196" class="s-line" stroke-width="2" stroke-dasharray="6 6"/>
        <rect x="26" y="48" width="128" height="84" rx="8" class="f-surface s-muted" stroke-width="2.5"/>
        <path d="M29 52 L90 96 L151 52" fill="none" class="s-muted" stroke-width="2.5"/>
        <text x="90" y="156" text-anchor="middle" class="svg-t">MAIL FROM:</text>
        <text x="90" y="172" text-anchor="middle" class="svg-tm">x@spam.example</text>
        <rect x="184" y="44" width="136" height="150" rx="6" class="f-surface s-ink" stroke-width="2.5"/>
        <rect x="192" y="54" width="120" height="26" rx="4" fill="none" class="s-accent" stroke-width="3" stroke-dasharray="5 3"/>
        <text x="200" y="71" class="svg-t">From: you@bank</text>
        <rect x="196" y="94" width="100" height="7" rx="3.5" class="f-line"/>
        <rect x="196" y="110" width="80" height="7" rx="3.5" class="f-line"/>
        <rect x="196" y="126" width="110" height="7" rx="3.5" class="f-line"/>
        <rect x="196" y="142" width="60" height="7" rx="3.5" class="f-line"/>
      </svg>
    </div>
    <div class="words">
      <div class="head"><div class="stamp why">why</div><h2>Why one check is not enough</h2></div>
      <ol class="reasons">
        <li><b>SPF checks the envelope, not the letter.</b> A spammer passes SPF with their own domain in <code>MAIL FROM</code> and writes <code>From: you@bank.example</code> inside.</li>
        <li><b>Forwarding breaks SPF.</b> The forwarder posts the letter again from its own server, which your SPF record does not list. The DKIM seal rides inside the letter and survives.</li>
        <li><b>Only DMARC ties the checks to the visible From.</b> It also tells Bob's server what to do with a fail: deliver, send to Junk or refuse.</li>
      </ol>
    </div>
  </section>

  <section class="status" aria-labelledby="end">
    <h2 id="end">Before you rely on it</h2>
    <ul>
      <li><span class="pill no">catch</span><span>Your mail can pass SPF and still fail DMARC. This happens when your mail provider's bounce domain is not your <code>From:</code> domain. Sign with DKIM as your own domain (<code>d=example.com</code>), or set a custom bounce domain.</span></li>
      <li><span class="pill new">ask next</span><span><b>Why did my mail arrive an hour late?</b> Bob's server answered <code>4xx</code>, so your server waited at least 30 minutes before the next try.</span></li>
      <li><span class="pill new">ask next</span><span><b>How do I see which checks passed?</b> Open the raw message and find <code>Authentication-Results</code>. Bob's server writes the <code>spf=</code>, <code>dkim=</code> and <code>dmarc=</code> results there.</span></li>
      <li><span class="pill new">simplified</span><span>One hop each way. Real mail can pass more relays, and TLS between servers is left out.</span></li>
      <li><span class="pill yes">sources</span><span>RFCs <a href="https://www.rfc-editor.org/rfc/rfc5321">5321</a> (SMTP), <a href="https://www.rfc-editor.org/rfc/rfc6409">6409</a> (submission), <a href="https://www.rfc-editor.org/rfc/rfc7208">7208</a> (SPF), <a href="https://www.rfc-editor.org/rfc/rfc6376">6376</a> (DKIM), <a href="https://www.rfc-editor.org/rfc/rfc7489">7489</a> (DMARC), <a href="https://www.rfc-editor.org/rfc/rfc9051">9051</a> (IMAP) and <a href="https://www.rfc-editor.org/rfc/rfc8601">8601</a>.</span></li>
      <li><span class="pill no">not verified</span><span>How a spam filter picks Inbox or Junk. No RFC defines it.</span></li>
    </ul>
  </section>

</main>
</body>
</html>
```
