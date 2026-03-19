# Feature: 3D Models Page — Masonry Grid Layout & Dynamic Pipeline

**Date:** 2026-03-18
**Completed:** 2026-03-19

---

## Overview

A dedicated page at `/3d/` showcasing Printables.com iframe embeds for 3D print models. The page uses a fluid CSS Grid masonry layout to handle embeds of varying sizes, with a Phase 2 build pipeline planned to automate model injection from a JSON data file.

---

## Architecture

### Naming Conventions
- Generic, reusable CSS component: `.masonry-grid`, `.masonry-card`, `.masonry-card--{size}`
- Page-specific overrides: `.wrapper--3d`, `.content--3d`
- Follows existing `feature-*.css` pattern for reusable components

### CSS Files
- **`public_html/styles/feature-masonry.css`** — Generic masonry grid. Reusable on any page.
- **`public_html/styles/page-3d.css`** — 3D page layout overrides only. References `.masonry-grid`.

### Source folder
- `public_html/3d/` — lowercase. The build canonicalizes to lowercase anyway; keeping it lowercase in source prevents a macOS case-insensitive FS bug where the canonicalization step would delete the folder.

---

## Phase 1 — Layout ✅

### Approach: CSS Grid with auto-fill
Pure CSS, zero JS. Uses `repeat(auto-fill, minmax(360px, 1fr))` with `align-items: start`.

### Aspect ratio scaling
iframes have **no `height` attribute** — CSS owns sizing entirely. Each size class sets `aspect-ratio` matching the Printables embed's native dimensions, so height scales proportionally with column width. No clipping at any breakpoint.

### Size modifier classes
Maps directly to Printables embed size variants:

| Class | Printables size | Dimensions | Columns | Aspect ratio |
|---|---|---|---|---|
| `masonry-card--sm` | Small | 300×340 | 1 | 300/340 |
| `masonry-card--card` | Card | 400×445 | 1 | 400/445 |
| `masonry-card--lg` | Large | 640×640 | 2 (at ≥640px) | 1/1 |
| `masonry-card--wide` | Wide | 640×190 | 2 (at ≥640px) | 640/190 |

`lg` and `wide` use `grid-column: span 2` at ≥640px, matching Printables' own large embed breakpoint.

### Key decisions
- Sidebar removed — Printables logo appears in every embed card
- No `height` attribute on iframes — `aspect-ratio` in CSS handles it
- `loading="lazy"` on all iframes
- No JS required
- Source folder is `public_html/3d/` (lowercase) — prevents macOS case-insensitive FS bug where build canonicalization would delete the folder

### Files
- `public_html/3d/index.html` — Page with 36 iframe embeds (sorted newest first)
- `public_html/styles/feature-masonry.css` — Reusable masonry grid component
- `public_html/styles/page-3d.css` — 3D page overrides
- `dev/scripts/deploy/deploy-support/head-templates/inject-nav.mjs` — "3D" link added between AI and About

---

## Utility Script — Auto-sync from Printables ✅

`dev/scripts/utilities/update-3d-models.mjs`

- Fetches all public models from the Printables GraphQL API (no auth required)
- Rebuilds the entire `.masonry-grid` in API order (newest first) on every run
- Preserves any manually set size class overrides per card
- New models default to `masonry-card--card`
- Idempotent — safe to run repeatedly

**Usage:**
```bash
npm run update:3d-models
# or via: npm run menu → Utilities → Update 3D Models
```

**Adding a new model after publishing on Printables:**
1. Run `npm run update:3d-models`
2. Rebuild (`echo "1" | npm run menu`)
3. Optionally change the size class on the new card if not `card`

---

## Phase 2 — Dynamic Build Pipeline _(Under Consideration)_

Originally planned as a `BUILD_INSERT` injection approach. Reconsidered — the utility script approach is simpler and keeps `index.html` as the single source of truth with no extra build pipeline step. Revisit only if the page needs to be fully generated at build time (e.g., for SSG or multi-site use).

---

## Notes
- `.masonry-grid` is intentionally generic — reusable in portfolio, labs, or any future page
- Aesthetic card styling (borders, shadows, labels) deferred to a future pass

