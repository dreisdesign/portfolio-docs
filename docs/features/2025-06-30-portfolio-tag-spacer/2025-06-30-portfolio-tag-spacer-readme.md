# 2025-06-30-portfolio-tag-spacer-readme

## Feature: Automated Portfolio Tag Spacer for "+ More" Consistency

**Date:** June 30, 2025

---

### Purpose
- Ensure the "+ More" tag indicator in portfolio cards always appears on a new line (third row) when tag content overflows.
- Maintain a visually consistent tag layout across all cards, regardless of tag count or length.
- Eliminate manual markup or guesswork for tag row breaks—handled automatically by the build system.

---

### How It Works
- The build script (`dev/scripts/deploy/deploy-support/scripts/06-build-portfolio.mjs`) automatically inserts a `<span class="portfolio-tag-spacer"></span>` before the "+ More" tag in the generated HTML for portfolio cards.
- The CSS rule for `.portfolio-tag-spacer` uses `flex-basis: 100%` and `order: 99` to force the "+ More" tag to the next row in the flex container (`.card--tags`).
- This prevents the "+ More" tag from appearing mid-row or breaking the tag layout, regardless of the number of tags or their lengths.

---

### Options Considered
- **No Spacer (Default Flex Wrap):**
  - "+ More" tag may appear mid-row, causing inconsistent layouts.
  - Not visually reliable, especially with variable tag lengths.
- **Manual Spacer Insertion:**
  - Requires hand-editing HTML for each card—error-prone and not scalable.
- **Automated Spacer (Current Solution):**
  - Build script detects when to insert the spacer, ensuring consistency and zero manual effort.
  - Works for all cards, all tag counts, and all breakpoints.

---

### Example Markup
```html
<div class="card--tags">
  <span class="portfolio-tag">Tag 1</span>
  <span class="portfolio-tag">Tag 2</span>
  <!-- ...more tags... -->
  <span class="portfolio-tag-spacer"></span>
  <span class="portfolio-tag portfolio-tag--more">+3 more</span>
</div>
```

---

### Key Files
- **Build Script:** `dev/scripts/deploy/deploy-support/scripts/06-build-portfolio.mjs`
- **CSS:** `public_html/styles/main-components.css` (see `.portfolio-tag-spacer` and `.card--tags`)

---

### Benefits
- Guarantees consistent tag row layout for all cards
- No manual markup required—handled automatically by the build system
- Works responsively and across all supported browsers
- Easy to maintain and extend

---

### See Also
- [Changelog 2.5.6](../../../CHANGELOG.md#256---2025-06-30---automated--more-tag-spacer--color-system-finalization)
- [Color System Documentation](../2025-06-27-color-system/2025-06-27-color-system-readme.md)

---

*This document describes the implementation, rationale, and options for the portfolio tag spacer feature. For tag system and categorization details, see related feature docs in this folder.*
