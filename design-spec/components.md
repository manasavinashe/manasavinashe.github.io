# Components

Each component below: when to use it, markup shape, key CSS (using the
tokens), and states. Match the repo's existing component files — these are
the target styles, not a demand to rewrite the framework.

---

## Header / Nav

Single flex row in the page column, 1px bottom rule. Not sticky.

```html
<header class="site">
  <div class="wrap nav-row">
    <a href="/" class="brand">Manas Avinashe</a>
    <nav class="primary">
      <a href="/finance">Finance</a>
      <a href="/cv">CV</a>
      <a href="/blog" class="active">Blog</a>
      <a href="/tags">Tags</a>
      <a href="/about">About</a>
    </nav>
    <div class="nav-icons">
      <button class="icon-btn" aria-label="Archive">…</button>
      <button class="icon-btn" aria-label="Search">…</button>
      <button class="icon-btn" aria-label="Toggle theme">…</button>
    </div>
  </div>
</header>
```

```css
.site { border-bottom: 1px solid var(--color-border); }
.nav-row { display:flex; align-items:center; gap:var(--space-6);
           padding-block:var(--space-6); flex-wrap:wrap; }
.brand { font-size:var(--fs-md); font-weight:var(--fw-bold);
         color:var(--color-text); letter-spacing:var(--tracking-tight); }
.primary { display:flex; align-items:center; gap:var(--space-6);
           font-size:var(--fs-base); }
.primary a { color:var(--color-text); font-weight:var(--fw-medium); }
.primary a:hover { text-decoration:underline; text-underline-offset:4px; }
.primary a.active { text-decoration:underline; text-underline-offset:4px; }
.nav-icons { margin-left:auto; display:flex; align-items:center; gap:var(--space-2); }
```

- **Active page:** the current nav item is underlined (offset 4px), not
  colored.
- Nav links are `--color-text` (not accent) — only inline content links
  are blue.

---

## Icon button

40×40 hit target, 20px line icon, subtle surface fill on hover.

```css
.icon-btn { width:40px; height:40px; display:inline-flex;
  align-items:center; justify-content:center; border:none; background:none;
  cursor:pointer; color:var(--color-text); border-radius:var(--radius); }
.icon-btn:hover { background:var(--color-surface); }
.icon-btn svg { width:20px; height:20px; stroke:currentColor; fill:none;
  stroke-width:1.6; stroke-linecap:round; stroke-linejoin:round; }
```

Icons are **Tabler-style line icons** (1.6 stroke, round caps): archive,
search, moon/sun (theme), calendar (dates), chevron-left ("Go back"),
plus social marks (GitHub, LinkedIn, mail). Keep them monochrome
`currentColor`. If the repo already uses an icon set, keep it — just
match weight (~1.6–2) and 20px size in the header, 15px inline.

---

## Links

```css
a { color: var(--color-accent); text-decoration: none; }
a:hover { text-decoration: underline; text-underline-offset: 3px; }
```

- **Content links** → accent blue, underline on hover.
- **"View on GitHub"-style action links** → dotted underline always on:
  ```css
  .link-dotted { color:var(--color-accent); text-decoration:underline;
    text-decoration-style:dotted; text-underline-offset:4px; }
  ```
- **Nav links** → ink color, underline on hover/active (see Header).

---

## Post / Project card

Used in "Featured Projects" and blog/tag listings. No box — separated by
whitespace; optionally a 1px top rule between items.

```html
<article class="card">
  <h3 class="post-title"><a href="/p/alpha">Alpha Research Portfolio</a></h3>
  <div class="meta-row">
    <svg class="cal">…calendar…</svg><time>1 Mar, 2026</time>
  </div>
  <p class="post-desc">Systematic daily trading strategies on US equities.</p>
  <div class="tag-row"><span>Python</span><span>LightGBM</span></div>
  <a class="link-dotted" href="…">View on GitHub</a>
</article>
```

```css
.post-title { font-size:var(--fs-lg); font-weight:var(--fw-bold);
  line-height:1.25; margin:0 0 var(--space-2); }
.post-title a { color:var(--color-accent); }
.meta-row { display:flex; align-items:center; gap:var(--space-2);
  color:var(--color-text-muted); font-size:var(--fs-sm);
  margin-bottom:var(--space-3); }
.meta-row svg { width:15px; height:15px; stroke:currentColor; fill:none;
  stroke-width:1.6; }
.post-desc { margin:0 0 var(--space-3); }              /* --fs-base */
.tag-row { display:flex; gap:var(--space-4); font-size:var(--fs-sm);
  color:var(--color-text-muted); margin-bottom:var(--space-3); }
```

- Title is the **only** accent-blue element in the card.
- Date sits in a meta row with a calendar icon, in muted gray.
- Cards separated by `--space-12`; optional `border-top:1px solid var(--color-border)`.

---

## Breadcrumb

Muted trail with `»` separators; current page is muted (not linked).

```html
<nav class="crumb">
  <a href="/">Home</a><span class="sep">»</span>
  <a href="/projects">Projects</a><span class="sep">»</span>
  <span>geospatial-map-reconstruction-vqa</span>
</nav>
```

```css
.crumb { display:flex; flex-wrap:wrap; gap:var(--space-2);
  color:var(--color-text-muted); font-size:var(--fs-sm); }
.crumb a { color:var(--color-accent); }
.crumb .sep { opacity:.6; }
```

---

## "Go back" link

Chevron + label, ink colored.

```css
.go-back { display:inline-flex; align-items:center; gap:var(--space-2);
  color:var(--color-text); font-size:var(--fs-base); }
.go-back svg { width:16px; height:16px; stroke:currentColor; fill:none;
  stroke-width:1.8; }
.go-back:hover { text-decoration:underline; text-underline-offset:3px; }
```

---

## Buttons

Square-ish (4px radius), monospace label, medium weight.

```css
.btn { font-family:var(--font-mono); font-size:var(--fs-sm);
  font-weight:var(--fw-medium); padding:var(--space-2) var(--space-4);
  border:1px solid var(--color-border); border-radius:var(--radius);
  background:var(--color-bg); color:var(--color-text); cursor:pointer; }
.btn:hover { background:var(--color-surface); }
.btn.primary { background:var(--color-accent); border-color:var(--color-accent);
  color:#fff; }
.btn.primary:hover { background:var(--color-accent-hover); }
```

Use sparingly — this is a reading site. Most actions are plain links.

---

## Tags / pills

Two forms: plain inline labels (in cards) and outlined pills (on tag pages).

```css
.pill { font-size:var(--fs-xs); color:var(--color-text-muted);
  border:1px solid var(--color-border); border-radius:999px;
  padding:2px 10px; }
```

Lowercase tag text. Muted gray, never accent-filled.

---

## Code blocks

```css
pre.code { background:var(--color-surface); border:1px solid var(--color-border);
  border-radius:var(--radius); padding:var(--space-4); overflow:auto;
  font-size:var(--fs-sm); line-height:1.6; }
code { font-family:var(--font-mono); }       /* inline */
:not(pre) > code { background:var(--color-surface); padding:0.1em 0.35em;
  border-radius:var(--radius); }
```

Since the body is already monospace, code blocks differ from prose only by
the surface fill + hairline border, not by font.

---

## Dividers

The only structural lines on the page.

```css
hr, .section + .section { border:none; border-top:1px solid var(--color-border); }
```

Section padding `--space-12`. No shadows, no thick or colored rules.
