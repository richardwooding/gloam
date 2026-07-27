# gloam for Marp

The gloam design language as a [Marp](https://marp.app/) theme — dark-first,
purple-accented, terminal-flavored slides that match the gloam web look.

- **`gloam.marp.css`** — the theme (declares `/* @theme gloam */`).
- **`example.md`** — a starter deck exercising every slide type.

## Use it

**One-off (explicit theme file):**

```sh
marp example.md --theme gloam.marp.css -o deck.html   # or .pdf / .pptx
marp example.md --theme gloam.marp.css --images png   # one PNG per slide
```

**By name (register the theme once), then `theme: gloam` in front-matter:**

```sh
marp --theme-set path/to/gloam.marp.css deck.md
```

**VS Code (Marp for VS Code):** add the file to the theme set in settings —

```jsonc
// .vscode/settings.json
{ "markdown.marp.themes": ["marp/gloam.marp.css"] }
```

Then a deck opts in via front-matter:

```yaml
---
marp: true
theme: gloam
paginate: true
footer: your deck · footer
---
```

## Slide classes & spans

Dark is the default. Set a class on one slide with `<!-- _class: … -->` or the
rest of the deck with `<!-- class: … -->`.

| Class | Effect |
|-------|--------|
| `lead` | Centered title slide; gradient headline, muted subtitle. |
| `terminal` | Faux macOS terminal window (traffic-light dots, mono). |
| `end` | Centered closing slide. |
| `light` | Light palette (deliberate opt-in; exports stay stable). |

Inline spans (write them as HTML in Markdown): `<span class="n">42</span>` for an
accent number, plus `.muted`, `.ok`, `.warn` for secondary/status text.

Everything else is plain Markdown: `#`/`##` headings get the gloam accent bar,
fenced code blocks become elevated panels with palette-matched syntax tints,
tables get mono accent headers, and blockquotes sit behind an accent rule.

## Keep it gloam

Same rules as the web language: **one accent** (purple), monospace for
code/terminal and system sans for prose, status colors for signals only, and
restraint over decoration. See the repo [`README`](../README.md) and the
[`skill`](../skills/gloam) for the full design language.
