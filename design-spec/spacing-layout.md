# Spacing & Layout

## Spacing scale (4px base)

Use these tokens for all margins, padding, and gaps. Don't invent
in-between values.

| Token | rem | px | Typical use |
|-------|-----|----|-------------|
| `--space-1`  | 0.25 | 4  | icon-to-label gaps, tight insets |
| `--space-2`  | 0.5  | 8  | meta row gaps, pill padding |
| `--space-3`  | 0.75 | 12 | small stacks, tag spacing |
| `--space-4`  | 1.0  | 16 | default element gap, card inset (sm) |
| `--space-6`  | 1.5  | 24 | nav gaps, paragraph spacing, between cards |
| `--space-8`  | 2.0  | 32 | card inset, between groups |
| `--space-12` | 3.0  | 48 | section padding, heading top margin |
| `--space-16` | 4.0  | 64 | page top/bottom rhythm |

**Prefer flex/grid with `gap`** over per-element margins for any row or
group (nav, meta row, tag row, button row, icon cluster). It survives
edits and keeps spacing explicit.

## Layout

| Token | Value | Meaning |
|-------|-------|---------|
| `--container` | `48rem` | Max-width of the main reading column |
| `--container-pad` | `1.25rem` | Horizontal gutter (left/right) |
| `--radius` | `4px` | The only corner rounding — buttons, cards, code, hover fills |

```css
.wrap {            /* the page column — header inner + main both use it */
  max-width: var(--container);
  margin-inline: auto;
  padding-inline: var(--container-pad);
}
```

- Everything lives in one **centred ~48rem column** — header, content,
  footer. Never let body text run full-bleed.
- Long-form prose is capped tighter still (~68ch, see `typography.md`).
- Vertical rhythm between major sections: `--space-12` padding, separated
  by a 1px `--color-border` rule.

## Header layout

```
[ Site title ]  [ nav: Finance CV Blog Tags About ]      [ icons: archive search theme ]
─────────────────────────────────────────────────────────────────────────── (1px rule)
```

- Single flex row inside `.wrap`: `display:flex; align-items:center;
  gap: var(--space-6)`.
- Site title (`--fs-md`, weight 700) sits first; nav links follow.
- Icon cluster is pushed right with `margin-left:auto`.
- Bottom border: `1px solid var(--color-border)`. Header is **not** sticky.
- On narrow screens the row wraps (`flex-wrap: wrap`); see breakpoints.

## Breakpoints

Mobile-first; only two real breakpoints needed.

| Name | Min-width | Changes |
|------|-----------|---------|
| base | —     | single column, header may wrap, display heading can step down to `--fs-xl` |
| `sm` | 640px | header sits on one row, full type scale |
| `md` | 768px | column hits its 48rem cap and centres with gutters |

```css
/* Optional: ease the display heading down on small screens */
@media (max-width: 480px) {
  h1 { font-size: var(--fs-xl); }
}
```

## Rules / dividers

- Section dividers and the header underline are the **only** structural
  lines: `border-top: 1px solid var(--color-border)` (or `<hr>` styled the
  same). No thick rules, no accent color, no shadows anywhere.
