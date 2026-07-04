---
name: gloam
description: Build web pages in the "gloam" design language — a dark-first, purple-accented, terminal-flavored aesthetic (tokens + components: sticky nav, hero with a faux-terminal, feature-card grids, code blocks, install snippets with copy buttons, pill tabs, footer). Use when building a landing/marketing page, product hero, feature grid, pricing, or docs/site that should look like gloam; when the user says "gloam", "the gloam look", "like the codemetrics site", or asks for a dark purple terminal-style page; or when styling an HTML Artifact or GitHub Pages site in this aesthetic. Produces a self-contained, responsive, accessible, dark/light-aware page.
---

# gloam design language

gloam is a small, dependency-free web design language: **dark-first, purple-accented,
terminal-flavored**. This skill lets you build pages in that look — either by linking the
`gloam.css` / `gloam.js` files, or by inlining everything into one self-contained file.

Everything you need is in this skill folder:

- `references/tokens.md` — the color/type/spacing tokens (dark + light).
- `references/components.md` — copy-paste HTML for every component.
- `references/gloam.css` — the full stylesheet (link it, or inline its contents).
- `references/gloam.js` — the optional behaviors (copy buttons, pill tabs, mobile nav,
  theme toggle).
- `scripts/sync-gloam.sh` + `scripts/gloam-sync.yml` — keep a linked consumer's copy of
  the assets in sync with the gloam repo (see "Keeping a consumer in sync").

## When to use this

Building a landing page, hero, feature grid, pricing section, docs site, or any page/
component that should carry the gloam aesthetic — or when the user names gloam or asks for
a "dark purple terminal-style" page. Also appropriate for an HTML **Artifact** (inline
mode) or a **GitHub Pages** site — either inlined, or **linked** with the sync workflow so
the published page tracks gloam upstream (both modes below).

## The look, in one paragraph

Near-black background with elevated panels and hairline borders; a single **purple** accent
(`--gl-accent`) for buttons, links, selected states, and emphasis numbers; monospace for
code and terminal chrome, system sans for prose; generous section padding; rounded 14px
corners. The signature element is a **faux-terminal** card in the hero. It is calm and
technical, not flashy — restraint is the point. Light mode is a first-class inversion, not
an afterthought.

## Two ways to ship it

**A — Linked (multi-file site / repo).** Copy `references/gloam.css` and
`references/gloam.js` next to your page and:

```html
<link rel="stylesheet" href="gloam.css">
<script src="gloam.js" defer></script>
<body class="gl"> … </body>
```

**B — Inlined (single self-contained file — Artifacts, GitHub Pages, email-safe).** Paste
the entire contents of `references/gloam.css` into a `<style>` in `<head>`, and
`references/gloam.js` into a `<script>` before `</body>`. No external requests. This is the
required mode for Claude Artifacts (a strict CSP blocks external hosts). For a **GitHub
Pages** site either mode works: inline for a truly single-file drop, or **linked** (below)
so the sync workflow keeps the page current with gloam.

Either way, put `class="gl"` on `<body>` so the base typography/reset applies.

## Keeping a consumer in sync

A linked consumer holds a *copy* of `gloam.css`/`gloam.js`, so it can drift as
gloam evolves. This skill ships a sync step in `scripts/`:

- `scripts/sync-gloam.sh [dir] [ref]` — refetch both files from
  `github.com/richardwooding/gloam` (default `main`) into `dir` and record the
  source commit in `dir/.gloam-version`. Drop it next to the vendored files
  (e.g. `site/sync-gloam.sh`) and run `sh site/sync-gloam.sh site`.
- `scripts/gloam-sync.yml` — a GitHub Actions workflow template that runs the
  script weekly and opens a PR when the copy drifts. Copy it into the
  consumer's `.github/workflows/` and set `GLOAM_DIR`.

A **GitHub Pages** site is the natural linked consumer: vendor `gloam.css`/`gloam.js`
into `docs/`, drop `sync-gloam.sh` beside them, link them from the page, and add
`gloam-sync.yml` with `GLOAM_DIR: docs` — a weekly PR then keeps the published page in
step with gloam.

Inlined pages have no separate files to sync — re-run the skill (or re-paste
`references/gloam.css`/`gloam.js`) to update them.

## How to build a page

1. **Start from the structure**, not the pixels: nav → hero (headline + faux-terminal) →
   a feature-card grid → a code/install section → footer. Pull the exact markup from
   `references/components.md` and swap in real content.
2. **Use tokens, never hardcode colors.** If you need a new shade, derive it with
   `color-mix(in srgb, var(--gl-accent) 18%, transparent)` rather than inventing a hex.
   Read `references/tokens.md` for the full set.
3. **One accent.** Purple is the only brand color — don't add competing hues. Status green
   (`--gl-green`) and amber (`--gl-amber`) are for ok/warn signals only.
4. **The hero should feel like a terminal.** Use the `gl-term` component with a realistic
   command and a few output rows (`.pr` prompt, `.hd` header, `.n` accent number, `.loc`
   muted location, `.ok`/`.warn` status). Make the content real, not lorem ipsum.
5. **Wire behaviors with data-attributes** (`data-gl-copy`, `data-gl-tabs`/`data-gl-tab`/
   `data-gl-panel`, `data-gl-nav-toggle`, `data-gl-theme-toggle`, `data-gl-year`,
   `data-gl-carousel`) — `gloam.js` activates them.

## Rules that keep it "gloam"

- **Dark-first, but theme-aware.** Ship both: the tokens already handle
  `prefers-color-scheme: light` and `data-theme` overrides — don't hardcode a single theme.
- **Self-contained & fast.** No web fonts, no CDNs, no frameworks. Inline SVG for icons/logo
  (a small bar-chart mark is the house motif). Use the system font stacks in the tokens.
- **Responsive with no sideways scroll.** Grids collapse at the provided breakpoints; wide
  code/terminal blocks get their own `overflow-x:auto` — the page body must never scroll
  horizontally.
- **Accessible.** One `<h1>`; a `.gl-skip` skip-link first in `<body>`; real `<button>`s for
  interactive pills (with `aria-selected`); visible `:focus-visible` rings; sufficient
  contrast in both themes (the tokens are tuned for it).
- **Restraint over decoration.** Whitespace, one accent, crisp type. Avoid gradients beyond
  the primary button and the hero headline `gl-grad`. Motion is subtle and optional: the
  only animated component is the carousel, and it must honor `prefers-reduced-motion`.

## Quick reference

- Layout: `gl-wrap` (centered max-width), `gl-section`, `gl-eyebrow`, `gl-lede`, `gl-hint`.
- Nav: `gl-nav` > `gl-wrap` > `gl-brand` + `<nav>`; mobile via `gl-nav-toggle` +
  `data-gl-nav-toggle`.
- Buttons: `gl-btn` + `.primary` / `.ghost`.
- Theme toggle: `gl-theme-toggle[data-gl-theme-toggle]` with `.gl-sun` + `.gl-moon` SVGs;
  persists `data-theme` in localStorage (add the `<head>` restore snippet for no flash).
- Hero: `gl-hero` > `gl-wrap.gl-hero-grid`; headline accent = `gl-grad`.
- Terminal: `gl-term` > `.bar` (three `.dot`s + `.t` title) + `<pre>`.
- Pills/tabs: `gl-badges[data-gl-tabs]` of `gl-lang[data-gl-tab]`, panels `[data-gl-panel]`.
  Interactive styling is scoped to `[data-gl-tab]`; a bare `gl-lang` is a **static badge** —
  use a semantic `<ul class="gl-badges">` of `<li class="gl-lang">` for a list of them.
- Cards: `gl-grid.feat`/`.two` > `gl-card` (`gl-icon` chip, `gl-stat` big number).
- Carousel: `gl-carousel[data-gl-carousel]` > `gl-carousel-viewport[data-gl-carousel-viewport]`
  of `gl-card` slides + `gl-carousel-ctrls` (prev/next `gl-carousel-btn` + empty
  `gl-carousel-dots`). `gloam.js` builds the dots and auto-advances (motion-safe).
- Code: `pre.gl-code` with `.c`/`.k`/`.s` spans; side-by-side via `gl-split`.
- Install: `gl-install` > `gl-snip` (`.lbl` + `<code id>` + `gl-copy[data-gl-copy]`).
- Footer: `gl-footer` > `gl-wrap` > `gl-brand` + `gl-fnav`.

Full, correct markup for each is in `references/components.md` — prefer copying from there.
