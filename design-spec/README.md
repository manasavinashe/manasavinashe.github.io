# Design Spec — manasavinashe.dev

A design specification for a **monospace, content-first** personal blog
(built with Astro). These files are written to be read by **Claude Code**
running locally against the repo: read them top-to-bottom, then apply the
tokens and component rules to the existing components.

## What this is

A minimalist, editorial blog where **a single typeface (IBM Plex Mono)**
carries the whole identity. Near-white paper, near-black ink, one blue
accent, hairline rules, a narrow centred column. No shadows, no gradients,
no decorative imagery.

## The active change

The monospace was **too large**. This spec reduces it:

- Root font-size set to **15px** (`html { font-size: 93.75% }`) — was 16px.
- Heading steps tightened (display drops from ~56px to **34.5px**).
- Everything is expressed in `rem`, so the whole system scales from the
  root. To rescale later, change one number.

## Files

| File | What's in it |
|------|--------------|
| `tokens.css`        | **Source of truth.** CSS variables: color, type scale, spacing, layout. Import this once. |
| `typography.md`     | Font, weights, the reduced type scale, element mapping, prose rules. |
| `color.md`          | Palette, light + dark, usage rules, contrast notes. |
| `spacing-layout.md` | Spacing scale, container width, header layout, breakpoints. |
| `components.md`     | Header/nav, links, post card, breadcrumb, buttons, tags, code, icons — with markup + CSS. |

## How to apply (suggested order)

1. Copy `tokens.css` into the project (e.g. `src/styles/`) and `@import`
   it at the top of the global stylesheet.
2. **Verify the dark-mode values** in `tokens.css` against whatever the
   repo already defines — only light mode was captured from screenshots.
   Keep the repo's real dark values if they exist.
3. Replace hard-coded fonts/sizes/colors with the variables.
4. Set the root size knob (`html { font-size: 93.75% }`) and confirm the
   smaller scale reads well, then fine-tune per `typography.md`.
5. Walk each component in `components.md` and align markup + classes.

## Non-negotiables (the things that make it *this* blog)

- **One typeface only.** Never introduce a second family.
- **One accent color.** Blue is for links/active/focus and nothing else.
- **Hairlines, not boxes.** 1px borders divide; avoid shadows entirely.
- **Hierarchy via weight + size**, not color or ornament.
- **Narrow column** (~48rem) — never full-bleed body text.
