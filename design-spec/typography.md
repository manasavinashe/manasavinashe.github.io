# Typography

> The single most important rule: **one typeface carries everything** —
> display headings, navigation, body, captions, code. Do not add a second
> family. Hierarchy comes from **weight** and **size**, never from a
> different font.

## Family

```
--font-mono: "IBM Plex Mono", ui-monospace, SFMono-Regular, Menlo,
             "Cascadia Mono", Consolas, monospace;
```

**IBM Plex Mono.** Load weights **400, 500, 700** plus **italic 400/500**.

Recommended self-host (preferred for a blog — no layout shift, no
third-party request):

```bash
npm i @fontsource/ibm-plex-mono
```
```js
// in the layout or global entry
import "@fontsource/ibm-plex-mono/400.css";
import "@fontsource/ibm-plex-mono/500.css";
import "@fontsource/ibm-plex-mono/700.css";
import "@fontsource/ibm-plex-mono/400-italic.css";
```

Google Fonts fallback:
```
https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:ital,wght@0,400;0,500;0,700;1,400&display=swap
```

## Weights

| Token | Value | Used for |
|-------|-------|----------|
| `--fw-regular` | 400 | body, descriptions, meta |
| `--fw-medium`  | 500 | nav links, button labels, emphasized meta |
| `--fw-bold`    | 700 | all headings, site title, post titles |

There is no light weight and no extra-bold. Bold = 700, full stop.

## The reduced type scale

Root is **15px** (`html { font-size: 93.75% }`, was 16px). All sizes are
`rem` so they scale from the root together. px values below assume 15px root.

| Token | rem | px | Weight | Line-height | Maps to |
|-------|-----|----|--------|-------------|---------|
| `--fs-2xl` | 2.30  | 34.5 | 700 | 1.18 | `h1` / home display ("Mingalaba") |
| `--fs-xl`  | 1.80  | 27   | 700 | 1.18 | `h2` / post & project titles |
| `--fs-lg`  | 1.40  | 21   | 700 | 1.40 | `h3` / section headings ("Overview", "Featured Projects") |
| `--fs-md`  | 1.133 | 17   | 700 | 1.40 | site title in header, lead/intro text |
| `--fs-base`| 1.00  | 15   | 400 | 1.70 | body copy, nav links |
| `--fs-sm`  | 0.867 | 13   | 400 | 1.60 | dates, breadcrumbs, captions |
| `--fs-xs`  | 0.80  | 12   | 400 | 1.50 | tags, fine print |

> **Before → after (the fix):** display heading ~56px → **34.5px**; post
> title ~40px → **27px**; section heading ~30px → **21px**; body ~16/17px
> → **15px**. If 15px still feels large to you, the cleanest next step is
> lowering the root to `91.6%` (14.7px) or `87.5%` (14px) — everything
> follows.

## Line-height & tracking

- `--lh-body: 1.70` — body copy (monospace needs generous leading).
- `--lh-snug: 1.40` — `h3`/`h4` and lead text.
- `--lh-tight: 1.18` — `h1`/`h2` display headings.
- `--tracking-tight: -0.01em` — apply to `--fs-lg` and larger only. Mono
  at display sizes looks tighter/cleaner with a hair of negative tracking;
  leave body at `0`.

## Element mapping

```css
h1 { font-size: var(--fs-2xl); font-weight: var(--fw-bold);
     line-height: var(--lh-tight); letter-spacing: var(--tracking-tight); }
h2 { font-size: var(--fs-xl);  font-weight: var(--fw-bold);
     line-height: var(--lh-tight); letter-spacing: var(--tracking-tight); }
h3 { font-size: var(--fs-lg);  font-weight: var(--fw-bold);
     line-height: var(--lh-snug);  letter-spacing: var(--tracking-tight); }
h4 { font-size: var(--fs-md);  font-weight: var(--fw-bold);
     line-height: var(--lh-snug); }
body, p, li { font-size: var(--fs-base); font-weight: var(--fw-regular);
     line-height: var(--lh-body); }
small, .meta, time { font-size: var(--fs-sm); color: var(--color-text-muted); }
```

## Prose / long-form rules

- **Measure:** cap body text at **~68ch** (`max-width: 68ch`) inside the
  48rem column for comfortable reading.
- **Paragraph rhythm:** `margin-block: 0 var(--space-6)` between paragraphs;
  no first-line indent.
- **Headings in prose:** `margin-top: var(--space-12)` above, `var(--space-4)`
  below — let sections breathe.
- **Lead / description paragraph** (the italic intro on post pages):
  `font-style: italic; color: var(--color-text);` at `--fs-md`.
- **Inline code:** same font (it already is mono); set on
  `--color-surface` with `padding: 0.1em 0.35em; border-radius: var(--radius)`.
- **Lists:** `padding-left: 1.2em; line-height: 1.8`.
- `text-wrap: pretty` on headings and `text-wrap: balance` on short
  display lines to avoid orphans.

## Don't

- Don't add a second typeface "for headings" or "for body".
- Don't use font-weight below 400 or a faux-bold above 700.
- Don't set body line-height below ~1.6 — monospace gets cramped.
- Don't size anything in `px` for type; use the `rem` tokens so the root
  knob keeps working.
