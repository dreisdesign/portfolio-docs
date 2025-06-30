# 2025-06-27-color-audit-readme

# Color Usage Audit – public_html (2025-06-27)

## Purpose
- Document all color usage in `public_html/` (CSS, HTML)
- Identify hardcoded, duplicate, or legacy color values
- Prepare for full migration to standardized CSS variables

## Audit Steps
- Searched for all hex codes (`#`), rgb/rgba, and CSS variable usage
- Focused only on `public_html/` (main portfolio source)
- Excluded `postsforpause.com/` and other non-core folders

## Findings

### Hardcoded Color Values

| Color Value                | Type   | Example Location(s)                                   |
|---------------------------|--------|------------------------------------------------------|
| `#202f48`                 | hex    | main-base.css (primary), index.html (SVG stroke)      |
| `#ffe1bb`                 | hex    | main-base.css (secondary), index.html (SVG fill)      |
| `#105cd7`                 | hex    | main-base.css (link), page-about.css, etc.            |
| `#E0E6EE`                 | hex    | main-base.css (border), feature-carousel.css          |
| `#FAFAF9`                 | hex    | main-base.css (background/surface), page-portfolio.css|
| `#ff0000`                 | hex    | main-base.css (error)                                 |
| `#000000`                 | hex    | main-base.css (black), feature-video.css              |
| `#ffffff`                 | hex    | main-base.css (white), meta theme-color, etc.         |
| `#ccc`                    | hex    | feature-carousel.css (background)                     |
| `#666`                    | hex    | page-portfolio.css (text)                             |
| `#0074D9`                 | hex    | feature-video-wrapper.css (outline)                   |
| `rgb(160, 160, 244)`      | rgb    | page-home.css (gradient)                              |
| `rgba(var(--color-black-rgb), 0.05)` | rgba(var) | content-card.css (box-shadow)             |
| `rgba(var(--color-black-rgb), 0.2)`  | rgba(var) | feature-video.css, feature-video-wrapper.css          |
| `rgba(var(--color-primary-rgb), 0.4)`| rgba(var) | main-components.css (border)                          |

### CSS Variable Usage

| CSS Variable                | Example Location(s)                        |
|-----------------------------|--------------------------------------------|
| `var(--color-primary)`      | main-components.css, etc.                  |
| `var(--color-secondary)`    | content-card.css, page-about.css, etc.     |
| `var(--color-link)`         | page-about.css, etc.                       |
| `var(--color-background)`   | body, page-portfolio.css                   |
| `var(--color-surface)`      | main-base.css                              |
| `var(--color-text)`         | html, content-card.css, etc.               |
| `var(--color-white)`        | content-card.css, feature-zoom.css, etc.   |
| `var(--color-black)`        | main-base.css                              |
| `var(--color-accent-rgb)`   | main-base.css, main-components.css         |
| ...                         | ...                                        |

*Note: See codebase for full details and additional values.*

## Next Steps
- Replace hardcoded colors with variables
- Refactor to use only standardized variables
- Remove duplicates and legacy values
- Update documentation and code comments

---

*This audit supports the color system consolidation plan and maintainable design system.*
