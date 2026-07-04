# gloam

A small, **dependency-free** design language: **dark-first, purple-accented,
terminal-flavored**. One CSS file, one optional JS file, and a Claude Code skill
that builds pages in the look for you.

**Live showcase:** https://richardwooding.github.io/gloam/

Extracted from the [codemetrics](https://github.com/richardwooding/codemetrics)
marketing site so the aesthetic can be reused anywhere.

## Quick start

Link the stylesheet (and the optional behaviors), put `class="gl"` on `<body>`:

```html
<link rel="stylesheet" href="gloam.css">
<script src="gloam.js" defer></script>
<body class="gl">…</body>
```

No build step, no framework, no external requests — inline the two files for a
fully self-contained page (great for GitHub Pages or Claude Artifacts).

## Build it with the skill

The repo ships a [Claude Code](https://claude.com/claude-code) skill under
[`skills/gloam/`](./skills/gloam). Drop it into a project (or your home config)
and ask for a page:

```sh
cp -r skills/gloam .claude/skills/gloam      # or ~/.claude/skills/gloam
```

> "build a landing page for my CLI in gloam"

The skill is self-contained — it bundles the tokens, a component catalog, and
copies of `gloam.css` / `gloam.js` under `references/`.

## Tokens

Every color is a `--gl-*` custom property. **Dark is the default**; light is
served via `prefers-color-scheme`, and either can be forced with
`:root[data-theme="light"|"dark"]`.

| Token | Role |
|-------|------|
| `--gl-bg`, `--gl-panel`, `--gl-panel-2` | page + elevated surfaces |
| `--gl-border` | hairline borders |
| `--gl-fg`, `--gl-muted`, `--gl-faint` | text: primary / secondary / tertiary |
| `--gl-accent`, `--gl-accent-2`, `--gl-accent-ink` | the purple + its ink |
| `--gl-green`, `--gl-amber` | status (ok / warn) |
| `--gl-radius`, `--gl-mono`, `--gl-sans`, `--gl-maxw` | radius, fonts, container |

## Components

Classes are prefixed `gl-`:

- **Layout:** `gl-wrap`, `gl-section`, `gl-eyebrow`, `gl-lede`, `gl-hint`, `gl-skip`
- **Nav:** `gl-nav`, `gl-brand`, `gl-nav-toggle`
- **Buttons:** `gl-btn` + `.primary` / `.ghost`
- **Theme toggle:** `gl-theme-toggle` (`.gl-sun` / `.gl-moon` SVGs swap via CSS)
- **Hero:** `gl-hero`, `gl-hero-grid`, `gl-grad`, `gl-cta`
- **Terminal:** `gl-term` (`.bar`, `.dot`, `pre` + `.pr/.hd/.n/.loc/.ok/.warn` spans)
- **Pills / tabs:** `gl-badges`, `gl-lang` (uses `aria-selected`)
- **Cards / grid:** `gl-grid` (`.two` / `.feat`), `gl-card`, `gl-icon`, `gl-stat`
- **Code:** `gl-code` (`.c` comment / `.k` keyword / `.s` string), `gl-split`
- **Install:** `gl-install`, `gl-snip`, `gl-copy`
- **Footer:** `gl-footer`, `gl-fnav`

## Behaviors (`gloam.js`, optional)

Data-attribute driven, no-ops when absent:

- `data-gl-copy="id"` — copy a snippet (Clipboard API + textarea fallback)
- `data-gl-tabs` / `data-gl-tab` / `data-gl-panel` — pill tabs
- `data-gl-nav-toggle="navId"` — mobile nav (closes on link tap)
- `data-gl-theme-toggle` — flip light/dark on `<html data-theme>`, persisted in
  localStorage (add `<script>try{var t=localStorage.getItem("gl-theme");if(t)document.documentElement.setAttribute("data-theme",t)}catch(e){}</script>` in `<head>` for flash-free restore)
- `data-gl-year` — current year

See [`index.html`](./index.html) for a full working example of every component.

## License

MIT — see [LICENSE](LICENSE).
