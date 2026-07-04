# gloam tokens

All design decisions live in CSS custom properties, prefixed `--gl-*`. Reference them;
don't hardcode hex values. The full definitions are in `gloam.css` (this folder) — this
file is the human-readable map.

## Colors

| Token | Dark (default) | Light | Role |
|-------|---------------|-------|------|
| `--gl-bg` | `#0d1117` | `#ffffff` | page background |
| `--gl-panel` | `#161b22` | `#f6f8fa` | cards, nav, terminal, code |
| `--gl-panel-2` | `#1c2230` | `#eef1f5` | inset chrome (terminal bar, copy button) |
| `--gl-border` | `#2a3038` | `#d8dee4` | hairline borders |
| `--gl-fg` | `#e6edf3` | `#1f2328` | primary text |
| `--gl-muted` | `#9aa7b4` | `#59636e` | secondary text |
| `--gl-faint` | `#6b7684` | `#818b98` | tertiary / comments |
| `--gl-accent` | `#a371f7` | `#7c3aed` | **the purple** — buttons, selected, emphasis |
| `--gl-accent-2` | `#bd93ff` | `#6d28d9` | links, gradient partner, accent numbers |
| `--gl-accent-ink` | `#f5efff` | `#ffffff` | text on the accent |
| `--gl-green` | `#3fb950` | `#1a7f37` | ok status only |
| `--gl-amber` | `#d29922` | `#9a6700` | warn status only |

## Scale & type

| Token | Value | Role |
|-------|-------|------|
| `--gl-radius` | `14px` | card/panel corner radius |
| `--gl-mono` | `ui-monospace, SFMono-Regular, Menlo, …` | code, terminal, pills, stats |
| `--gl-sans` | `-apple-system, "Segoe UI", Roboto, …` | prose |
| `--gl-maxw` | `1080px` | centered content width (`gl-wrap`) |

Spacing is not tokenized — use multiples of 4px; sections use `72px` vertical padding
(`gl-section`), the hero `84px 0 64px`.

## Theming

Dark is the default `:root`. Light ships two ways, both already in `gloam.css`:

- **Automatic:** `@media (prefers-color-scheme: light)` remaps the tokens.
- **Forced:** `:root[data-theme="light"]` or `:root[data-theme="dark"]` overrides the
  system preference (set `data-theme` on `<html>` from a toggle).

Because everything derives from these tokens, a theme switch needs no per-component work.

## Deriving shades

Need a tint (e.g. an icon chip background)? Mix from a token instead of inventing a color:

```css
background: color-mix(in srgb, var(--gl-accent) 18%, transparent);
```

New components reuse these tokens — nothing new is needed. The carousel, for instance,
adds no tokens; it styles its track, buttons, and dots entirely from the set above.
