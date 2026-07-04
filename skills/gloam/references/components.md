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
    <button class="gl-nav-toggle" aria-label="Toggle navigation" data-gl-nav-toggle="nav" aria-expanded="false">☰</button>
    <nav id="nav">
      <a href="#features">Features</a>
      <a href="#pricing">Pricing</a>
      <a class="gl-btn ghost" href="#">GitHub ★</a>
    </nav>
  </div>
</header>
```

## Theme toggle

A `data-gl-theme-toggle` button flips `<html data-theme>` between light and dark and
persists the choice in `localStorage`. `gloam.js` wires it up, keeps `aria-pressed` in
sync, and restores the saved theme on load. The sun/moon icons swap via CSS — no JS. Drop
it in the nav (before the GitHub button):

```html
<button class="gl-theme-toggle" data-gl-theme-toggle aria-label="Toggle color theme" aria-pressed="true">
  <svg class="gl-moon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M21 12.8A9 9 0 1 1 11.2 3a7 7 0 0 0 9.8 9.8z"/></svg>
  <svg class="gl-sun" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><circle cx="12" cy="12" r="4"/><path d="M12 2v2M12 20v2M2 12h2M20 12h2M4.9 4.9l1.4 1.4M17.7 17.7l1.4 1.4M19.1 4.9l-1.4 1.4M6.3 17.7l-1.4 1.4"/></svg>
</button>
```

For **flash-free** restore, also add this one-liner in `<head>` (it runs before first
paint, so the page never flickers from dark to the saved light theme):

```html
<script>try{var t=localStorage.getItem("gl-theme");if(t)document.documentElement.setAttribute("data-theme",t)}catch(e){}</script>
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

## Carousel (feature cards)

A scroll-snap track of `gl-card`s. `gloam.js` (via `data-gl-carousel`) generates the
dot indicators, wires prev/next, and auto-advances every 6s — pausing on hover/focus and
disabling autoplay entirely under `prefers-reduced-motion`. Without JS it degrades to a
plain scrollable row, and the viewport is the only thing that scrolls sideways.

```html
<div class="gl-carousel" data-gl-carousel role="group" aria-roledescription="carousel" aria-label="Projects">
  <div class="gl-carousel-viewport" data-gl-carousel-viewport>
    <article class="gl-card">
      <h3>Project one</h3>
      <p>One sentence on what it is.</p>
    </article>
    <!-- repeat gl-card slides -->
  </div>
  <div class="gl-carousel-ctrls">
    <button class="gl-carousel-btn" data-gl-carousel-prev aria-label="Previous">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M15 18l-6-6 6-6"/></svg>
    </button>
    <div class="gl-carousel-dots" data-gl-carousel-dots></div>
    <button class="gl-carousel-btn" data-gl-carousel-next aria-label="Next">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M9 18l6-6-6-6"/></svg>
    </button>
  </div>
</div>
```

Shows 3 cards at a time (2 ≤820px, 1 ≤560px). The `.gl-carousel-dots` container is
filled by `gloam.js`; leave it empty. Slides are ordinary `gl-card`s.

## Pill tabs (swap panels)

```html
<div class="gl-badges" role="tablist" aria-label="Choose" data-gl-tabs>
  <button class="gl-lang" role="tab" data-gl-tab="a" aria-selected="true">A</button>
  <button class="gl-lang" role="tab" data-gl-tab="b" aria-selected="false">B</button>
</div>
<div data-gl-panel="a">…panel A…</div>
<div data-gl-panel="b" hidden>…panel B…</div>
```

Non-tab pills (just badges) are the same `gl-lang` without `data-gl-tab` — they
render static (no pointer/hover/focus). For a **static list** of badges, use a
semantic list so screen readers announce the count:

```html
<ul class="gl-badges" aria-label="Supported types">
  <li class="gl-lang">go</li>
  <li class="gl-lang">rust</li>
</ul>
```

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
