# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
pnpm dev          # start dev server at localhost:4321
pnpm build        # type-check + build + run pagefind (search index) + copy to public/
pnpm preview      # preview the production build locally
pnpm lint         # ESLint
pnpm format       # Prettier (writes in place)
pnpm format:check # Prettier (check only, used in CI)
```

> `pnpm build` must be run before `pnpm preview` for search to work — pagefind indexes the `dist/` folder.

## Architecture

This is an **Astro 6** static site (AstroPaper theme) deployed to GitHub Pages via `.github/workflows/deploy.yml` on every push to `main`. The live URL is `https://manasavinashe.github.io/wretched-wavelength/`.

### Content collections

Defined in `src/content.config.ts`. Two collections, both using the `glob()` loader (supports subdirectories; files prefixed with `_` are excluded):

| Collection | Source path | URL pattern |
|---|---|---|
| `blog` | `src/data/blog/**/*.md` | `/posts/[slug]` |
| `projects` | `src/data/projects/**/*.md` | `/projects/[slug]` |

### Projects collection schema

```ts
title: string
description: string
category: "finance" | "computer-vision"   // controls which category page it appears on
pubDatetime: Date
github?: string
demo?: string
stack: string[]
featured?: boolean
ogImage?: image | string
```

- `category` must be exactly `"finance"` or `"computer-vision"` — these map 1:1 to `src/pages/finance.astro` and `src/pages/computer-vision.astro`.
- `featured: true` surfaces the project on the homepage (`src/pages/index.astro`), which picks one finance and one computer-vision project.
- The project detail page is `src/pages/projects/[slug].astro` — it renders the markdown body inside a `prose` container.

### Project images convention

Images for each project live in a project-specific subfolder to avoid filename collisions:

```
src/data/projects/
├── <slug>.md                        # references ./images/<slug>/filename.png
└── images/
    └── <slug>/
        └── *.png
```

Markdown image syntax: `![alt text](./images/<slug>/filename.png)`

### Site-wide configuration

All global settings (site URL, author, pagination, OG image, timezone) live in `src/config.ts` → `SITE`. Social links and share links are in `src/constants.ts` → `SOCIALS` / `SHARE_LINKS`.

### Key data flow

- `src/utils/getSortedPosts.ts` — sorts blog posts by date, filters drafts in production
- `src/utils/postFilter.ts` — draft/scheduled post logic
- `src/utils/slugify.ts` — used for tag URLs and view transition names
- `src/utils/generateOgImages.ts` — generates per-post OG images at build time using Satori + `@resvg/resvg-js`; templates are in `src/utils/og-templates/`

### Styling

Tailwind CSS v4 (via `@tailwindcss/vite` plugin — no `tailwind.config.*` file). Global styles in `src/styles/global.css`; prose/typography overrides in `src/styles/typography.css`.

### Search

Pagefind powers search. It runs as a post-build step (`pagefind --site dist`) and its output is copied into `public/pagefind/`. The search UI is at `src/pages/search.astro`.

## Adding a new project

See `ADD_PROJECT.md` at the repo root for the full Claude prompt and GitHub push protocol used to generate project writeups from external project directories.
