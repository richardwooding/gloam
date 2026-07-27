---
marp: true
theme: gloam
paginate: true
footer: gloam · dark-first · purple-accented
---

<!-- _class: lead -->
<!-- _paginate: false -->

# gloam for slides

## A dark, purple, terminal-flavored Marp theme

richardwooding/gloam

---

# One accent, lots of restraint

Every slide title gets the gloam accent bar. Body copy stays calm and readable.

- Purple (`--gl-accent`) is the **only** brand color
- Monospace for anything code-shaped, system sans for prose
- Status colors are for signals only — <span class="ok">ok</span> and <span class="warn">warn</span>
- Emphasis numbers read as accents: <span class="n">99.9%</span> uptime

> Pull quotes sit behind an accent rule and muted text — used sparingly.

---

<!-- _class: terminal -->

# ~/gloam $ marp deck.md

```console
$ marp example.md --theme gloam.marp.css -o deck.html
[  INFO ] Converting 1 markdown...
[  INFO ] example.md => deck.html
✔ rendered 6 slides   theme=gloam   ok
```

The `terminal` class turns a slide into a faux terminal window — the signature
gloam element, now on a slide.

---

# Code reads in the palette

```go
// A tiny handler, gloam-tinted.
func handler(w http.ResponseWriter, r *http.Request) {
    name := r.URL.Query().Get("name") // strings are green
    if name == "" {
        name = "world"                // keywords are purple
    }
    fmt.Fprintf(w, "hello, %s", name) // numbers amber: 200
}
```

Fenced blocks become elevated panels with a hairline border and soft shadow.

---

# Tables stay tidy

| Token | Role | Dark |
|-------|------|------|
| `--gl-accent` | the purple | `#a371f7` |
| `--gl-fg` | primary text | `#e6edf3` |
| `--gl-panel` | elevated surface | `#161b22` |
| `--gl-green` | ok status only | `#3fb950` |

Headers are mono, uppercase, accent-colored; rows separated by hairlines.

---

<!-- _class: end -->

# Thanks

Build your deck in gloam — `theme: gloam`, then write Markdown.

[github.com/richardwooding/gloam](https://github.com/richardwooding/gloam)
