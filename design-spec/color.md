# Color

> Neutral **paper & ink** with exactly **one accent**. The blue is for
> links, active navigation, and focus — nothing else. Everything else is
> background, surface, hairline, ink, or muted gray.

## Light palette (measured from the live site)

| Token | Value | Role |
|-------|-------|------|
| `--color-bg`         | `#fdfdfd` | Page background — near-white, very slightly warm neutral |
| `--color-surface`    | `#f4f4f3` | Cards, code blocks, hover fills on icon buttons |
| `--color-border`     | `#e4e3e1` | Hairline rules, dividers, card outlines (always 1px) |
| `--color-text`       | `#282728` | Primary ink — headings & body |
| `--color-text-muted` | `#6b6b6b` | Dates, breadcrumbs, captions, tag labels |
| `--color-accent`     | `#006cac` | Links, active nav item, focus ring |
| `--color-accent-hover` | `#00567f` | Link/button hover |

> These were sampled from screenshots, so they're close but may be ±a few
> values off the repo's real tokens. If the repo defines its own colors
> (Tailwind config, a `:root` block, an AstroPaper color scheme), treat
> **those** as canonical and just confirm they match the roles above.

## Dark palette — INFERRED, verify before shipping

Only light mode was captured. These are a sensible neutral-dark mapping;
**replace them with the repo's real dark values if they exist.**

| Token | Value | Notes |
|-------|-------|-------|
| `--color-bg`         | `#1c2030` | Dark neutral navy |
| `--color-surface`    | `#262b3d` | Raised surface |
| `--color-border`     | `#363c52` | Hairline on dark |
| `--color-text`       | `#e9ecf3` | Primary ink on dark |
| `--color-text-muted` | `#969eb2` | Muted on dark |
| `--color-accent`     | `#6cb6ff` | Blue lightened for contrast on dark bg |
| `--color-accent-hover` | `#93cbff` | |

Theme is toggled via `data-theme="dark"` on `<html>` (or a `.dark` class —
match whatever the repo already uses). The moon icon in the header flips it
and the choice persists in `localStorage`.

## Usage rules

- **Accent is sacred.** Use `--color-accent` only for: inline links, the
  active nav item (underline), focus rings, and primary-button fill. Do
  **not** tint headings, borders, backgrounds, or icons with it.
- **Icons & UI chrome** are `--color-text` (line icons, `stroke: currentColor`),
  never the accent.
- **Dividers** are always `--color-border` at 1px. No accent-colored or
  thick rules.
- **Muted gray** is for secondary information only (time, breadcrumb trail,
  captions). Body copy stays `--color-text`.
- **No gradients, no colored shadows, no tinted cards.** Surfaces differ
  from the background only by the subtle `--color-surface` step.

## Contrast

- `--color-text` on `--color-bg`: ~15:1 (AAA). Good.
- `--color-text-muted` on `--color-bg`: ~5:1 — fine for meta text at
  `--fs-sm`+, but never use muted gray for primary body copy.
- `--color-accent` on `--color-bg`: ~5.4:1 (AA). If you ever put link text
  on `--color-surface`, re-check it stays ≥4.5:1.
- Verify the dark accent (`#6cb6ff` on `#1c2030`) lands ≥4.5:1 once you
  confirm the real dark background.

## Focus state

```css
:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 2px;
  border-radius: var(--radius);
}
```
Never remove focus outlines — this blog is keyboard-friendly by default.
