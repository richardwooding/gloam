# gloam components

Copy-paste markup for each component. Keep the `gl-*` classes; swap the content. All rely
on `gloam.css`; the interactive ones (`data-gl-*`) rely on `gloam.js`. Put `class="gl"` on
`<body>`.

## Page skeleton

```html
<body class="gl">
  <a class="gl-skip" href="#main">Skip to content</a>
  <header class="gl-nav"> … </header>
  <main id="main"> … </main>
  <footer class="gl-footer"> … </footer>
  <script src="gloam.js" defer></script>
</body>
```

## Nav (sticky, blurred, mobile toggle)

```html
<header class="gl-nav">
  <div class="gl-wrap">
    <span class="gl-brand">
      <svg width="26" height="26" viewBox="0 0 24 24" aria-hidden="true">
        <rect width="24" height="24" rx="6" fill="var(--gl-panel-2)"/>
        <rect x="5" y="12" width="3.5" height="7" rx="1" fill="var(--gl-accent)"/>
        <rect x="10.25" y="8" width="3.5" height="11" rx="1" fill="var(--gl-accent-2)"/>
        <rect x="15.5" y="4" width="3.5" height="15" rx="1" fill="#d2b3ff"/>
      </svg>
      yourbrand
    </span>
    <button class="gl-nav-toggle" aria-label="Toggle navigation" data-gl-nav-toggle="nav">☰</button>
    <nav id="nav">
      <a href="#features">Features</a>
      <a href="#pricing">Pricing</a>
      <a class="gl-btn ghost" href="#">GitHub ★</a>
    </nav>
  </div>
</header>
```

## Hero + faux-terminal

```html
<section class="gl-hero">
  <div class="gl-wrap gl-hero-grid">
    <div>
      <p class="gl-eyebrow">short · dot · separated · kicker</p>
      <h1>Your headline, <span class="gl-grad">accent half.</span></h1>
      <p class="sub">One or two sentences of value proposition — concrete, not fluffy.</p>
      <div class="gl-cta">
        <a class="gl-btn primary" href="#">Get started</a>
        <a class="gl-btn ghost" href="#">View on GitHub</a>
      </div>
    </div>
    <div class="gl-term">
      <div class="bar">
        <span class="dot" style="background:#ff5f56"></span>
        <span class="dot" style="background:#ffbd2e"></span>
        <span class="dot" style="background:#27c93f"></span>
        <span class="t">yourtool</span>
      </div>
<pre><span class="pr">$</span> yourtool run .
<span class="hd">STATUS   TARGET      NOTES</span>
<span class="n">ok</span>       parse       <span class="loc">142 files</span>
<span class="warn">warn</span>     3 findings  <span class="loc">see report</span></pre>
    </div>
  </div>
</section>
```

Terminal spans: `.pr` prompt, `.hd` header row, `.n` accent number/status, `.loc` muted
location, `.ok` green, `.warn` amber. Keep output realistic.

## Feature grid

```html
<section id="features">
  <div class="gl-wrap">
    <p class="gl-eyebrow">what you get</p>
    <h2>Section heading.</h2>
    <div class="gl-grid feat" style="margin-top:28px">
      <div class="gl-card">
        <h3>
          <span class="gl-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12l5 5L20 7"/></svg></span>
          Feature name
        </h3>
        <p>One sentence on the benefit.</p>
      </div>
      <!-- repeat cards; use .gl-grid.two for two-up -->
    </div>
  </div>
</section>
```

## Pill tabs (swap panels)

```html
<div class="gl-badges" role="tablist" aria-label="Choose" data-gl-tabs>
  <button class="gl-lang" role="tab" data-gl-tab="a" aria-selected="true">A</button>
  <button class="gl-lang" role="tab" data-gl-tab="b" aria-selected="false">B</button>
</div>
<div data-gl-panel="a">…panel A…</div>
<div data-gl-panel="b" hidden>…panel B…</div>
```

Non-tab pills (just badges) are the same `gl-lang` without `data-gl-tab`.

## Code block (with token colors) + side-by-side

```html
<div class="gl-split">
  <pre class="gl-code"><span class="c"># a comment</span>
<span class="k">command</span> --flag <span class="s">"value"</span></pre>
  <pre class="gl-code"> … </pre>
</div>
```

Spans: `.c` comment (faint), `.k` keyword (accent), `.s` string (green).

## Install snippets (copy button)

```html
<div class="gl-install">
  <div class="gl-snip">
    <span class="lbl">brew</span>
    <code id="i1">brew install yourtool</code>
    <button class="gl-copy" data-gl-copy="i1">Copy</button>
  </div>
</div>
```

Each `data-gl-copy` points at the `id` of the `<code>` to copy.

## Footer

```html
<footer class="gl-footer">
  <div class="gl-wrap">
    <span class="gl-brand" style="font-size:.98rem">yourbrand · MIT · <span data-gl-year></span></span>
    <nav class="gl-fnav">
      <a href="#">GitHub</a>
      <a href="#">Docs</a>
    </nav>
  </div>
</footer>
```

## Section helpers

- `gl-eyebrow` — small uppercase purple kicker above an `<h2>`.
- `gl-lede` — a muted intro paragraph (max ~60ch).
- `gl-hint` — tiny faint helper line.
- `gl-stat` — big monospace accent number for a stat/metric card.
