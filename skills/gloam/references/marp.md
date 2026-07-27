# gloam for Marp (slide decks)

gloam also ships a **Marp** theme so presentations carry the same dark-first,
purple-accented, terminal-flavored look. Use it when the user wants a slide deck,
talk, or presentation "in gloam" (Marp / Markdown slides).

- The theme file is `gloam.marp.css` in this folder — it declares `/* @theme gloam */`.
- Author the deck as a Marp Markdown file; render with `marp`.

## Build a deck

1. **Front-matter opts in** and names the theme:
   ```yaml
   ---
   marp: true
   theme: gloam
   paginate: true
   footer: talk title · author
   ---
   ```
2. **Title slide** — `<!-- _class: lead -->` then `#` headline (renders as a
   purple gradient), `##` subtitle (muted), and a line of context. Add
   `<!-- _paginate: false -->` to hide its page number.
3. **Content slides** — a `#` or `##` title (gets the gloam accent bar) plus
   Markdown: bullet lists (accent markers), `**bold**`, blockquotes (accent rule).
4. **A terminal slide** — `<!-- _class: terminal -->` for the signature gloam
   element: the slide becomes a faux macOS window (traffic-light dots, mono).
   Put a realistic command + output in a ```console fence.
5. **Code slides** — fenced blocks become elevated panels; syntax is tinted
   within the palette (purple keywords, green strings, amber numbers, faint
   comments). Keep snippets real, not lorem ipsum.
6. **Closing** — `<!-- _class: end -->` centered, with a link.

## Render

```sh
marp deck.md --theme gloam.marp.css -o deck.html     # or .pdf / .pptx
marp deck.md --theme gloam.marp.css --images png     # preview PNGs
```

## Rules that keep it gloam

- **Dark by default.** Light is a deliberate opt-in via `<!-- class: light -->` —
  don't rely on `prefers-color-scheme` for a deck (exports must be stable).
- **One accent.** Purple only; green/amber are for ok/warn signals. Accent
  numbers use `<span class="n">…</span>`; secondary text `<span class="muted">`.
- **Monospace for code/terminal, sans for prose.** Same fonts as the web tokens.
- **Restraint.** One idea per slide, generous space, no competing colors or
  gratuitous gradients (the gradient is reserved for the `lead` headline).

See `../marp/README.md` (repo) for the full class/span reference and VS Code
setup, and `example.md` for a complete deck.
