# Portfolio Design System Documentation

*Last Updated: June 30, 2025*

> See `CHANGELOG.md` for full project update history. This document covers the current design system and workflow.

## Recent System Enhancements (2025-06)

### Tag Display Logic & Configurability
- Portfolio card tag display is now fully configurable via `TAGS_PER_CARD` and `TAG_CATEGORIES_ON_CARDS` in the build script (`06-build-portfolio.mjs`).
- Only "Industry & Platform" and "Approach & Deliverables" tags are shown on cards by default; "My Role" tags are excluded for clarity and focus.
- All card types (main index, Up Next, tag pages) use the same tag filtering and truncation logic for visual consistency.
- The "+ More" tag spacer is now automated in the build, ensuring consistent tag row layout and clear overflow indication.

### Color System Finalization
- All color usage is now centralized with CSS variables defined in `main-base.css`.
- Opacity variants (e.g., `--color-black-05`, `--color-black-20`) are used for overlays, borders, and subtle backgrounds, supporting accessible contrast and visual hierarchy.
- Legacy/duplicate color values and documentation have been removed for maintainability.

### Card & Tag Visual Consistency
- `.card--tags` CSS supports up to 3 lines for tags, with improved "+ More" tag placement and visibility.
- Tag index, tag pages, and portfolio index now share a unified, mobile-first design with consistent backgrounds and card styles.

### Feature Documentation Structure
- All feature documentation now uses the `date-topic-readme.md` naming convention for clarity and searchability.
- See `dev/docs/features/` for detailed feature documentation and technical notes.

## Overview

This document outlines the systematic design approach for the portfolio website, including the CSS consolidation work completed to create a more maintainable and consistent codebase.

## Typography System

### Font-Size Scale

The font-size system uses a consistent `rem`-based scale with systematic progression:

#### Base Configuration
- **HTML base:** `24px` (creates 1.5rem = 24px conversion)
- **Body base:** `1rem` (16px equivalent)

#### Size Scale
- **Extra Small Text:** `0.75rem` *(12px equivalent)*
  - Portfolio tags (compact display)
  - Secondary metadata
  - Fine print

- **Small Text:** `0.875rem` *(standardized)*
  - Mobile responsive text
  - Sidebar content
  - Carousel descriptions
  - Contact section titles
  - Navigation links
  - Error messages

- **Base Text:** `1rem` *(inherited from body)*
  - Default paragraph text
  - List items
  - H2 base size

- **Medium Text:**
  - `1.25rem` - Responsive H2 (medium+ screens), card titles (mobile)
  - `1.35rem` - Card titles (extra large screens)
  - `1.5rem` - H1 base, home subheadline, interactive buttons, responsive H2 (large)
  - `1.75rem` - Responsive H2 (x-large screens)
  - `1.8rem` - Home subheadline (responsive)

- **Large Text:**
  - `2.25rem` - Responsive H1 (medium screens)
  - `3rem` - Responsive H1 (large), home headline base
  - `3.25rem` - Responsive H1 (x-large)

- **Display Text:**
  - `3.7rem` - Home headline (medium screens)
  - `4.5rem` - Home headline (large screens)
  - `5rem` - Home headline (x-large screens)
  - `6rem` - Home headline (xx-large screens)

#### Special Values
- `0` - Text hiding (portfolio tag commas)
- `inherit` - Carousel text elements

### Line-Height System

Consolidated line-height values for optimal reading and visual hierarchy:

- **Base:** `1.2` *(applied to body, inherited by most elements)*
- **Tight Headlines:** `0.75` *(H1 elements for impact)*
- **Spaced Elements:** `2` *(portfolio tags for better click targets)*

### Font Weights & Variations

- **Light:** `350` (body text)
- **Medium:** `500` (portfolio tags)
- **Semibold:** `600` (buttons, strong emphasis)
- **Bold:** `700` (H2, strong elements)
- **Heavy:** `800` (H1-H6 headings)
- **Black:** `900` (H1, maximum impact)

## Color System

All colors are now managed using CSS custom properties for consistency and maintainability. The legacy variables (e.g., `--darkblue`, `--linkblue`, `--highlight-1`) have been replaced by a systematic naming convention:

### Variable Naming
- **Primary:** `--color-primary` / `--color-primary-rgb`
- **Link:** `--color-link` / `--color-link-rgb`
- **Highlight:** `--color-highlight` / `--color-highlight-rgb`
- **Accent:** `--color-accent` / `--color-accent-rgb`
- **Background:** `--color-bg` / `--color-bg-rgb`
- **Component:** `--color-component` / `--color-component-rgb`
- **Interactive:** `--color-interactive` / `--color-interactive-rgb`

### Example Variable Definitions (from `main-base.css`)
```css
:root {
  --color-primary: #202f48;
  --color-secondary: #ffe1bb;
  --color-link: #105cd7;
  --color-accent: var(--color-link);
  --color-border: var(--color-black-20);
  --color-border-dark: var(--color-black-30);
  --color-background: #FAFAF9;
  --color-surface: #FAFAF9;
  --color-text: #202f48;
  --color-error: #ff0000;
  --color-white: #ffffff;
  --color-black: #000000;

  /* Opacity Color Variables (2025-06-27 color system, simplified) */
  --color-black-05: rgba(0, 0, 0, 0.05);
  --color-black-10: rgba(0, 0, 0, 0.10);
  --color-black-20: rgba(0, 0, 0, 0.20);
  --color-black-30: rgba(0, 0, 0, 0.30);
  --color-black-40: rgba(0, 0, 0, 0.40);
  --color-black-50: rgba(0, 0, 0, 0.50);
  --color-black-60: rgba(0, 0, 0, 0.60);
  --color-black-80: rgba(0, 0, 0, 0.80);
  --color-black-90: rgba(0, 0, 0, 0.90);
  --color-white-20: rgba(255, 255, 255, 0.20);
  --color-white-80: rgba(255, 255, 255, 0.80);
  --color-white-90: rgba(255, 255, 255, 0.90);
  --color-white-95: rgba(255, 255, 255, 0.95);
  --color-accent-05: rgba(16, 92, 215, 0.05); /* Used for tag hover backgrounds */
}
```

### Usage
- **Solid:** `background: var(--color-primary);`
- **RGBA:** `background: rgba(var(--color-primary-rgb), 0.08);`
- **Accent Example:** `background: rgba(var(--color-accent-rgb), 0.1);`
- **Gradient:** `background: linear-gradient(90deg, var(--color-primary), var(--color-link));`

### Best Practices
- Define all color variables in `:root` in `main-base.css`.
- Use `-rgb` variables for any `rgba()` or gradient.
- Never use hardcoded color values in CSS or templates—always use variables.
- Set opacity directly in `rgba()` as needed.

### Migration Summary
- All CSS and build scripts now use this variable system.
- Enables easy theming and ensures color consistency across all components.

## Component System

### Buttons
- **Base:** `0.875rem` font-size, `1.2` line-height
- **Padding:** `10px 20px` (standard), `10px 15px` (home variant)
- **Border-radius:** `30px`
- **Transition:** `all 0.1s ease-in`

### Cards
- **Background:** Always white (`#fff`) for maximum contrast and clarity, regardless of page background (offwhite backgrounds are set at the page level for `.portfolio-index` and `.portfolio-tag-page`).
- **Border-radius:** `10px` for all cards, ensuring a consistent, modern look across the site.
- **Shadow:** Subtle shadow for depth and separation from the background, supporting accessibility and visual hierarchy.
- **Padding:** Consistent internal padding for all cards, supporting both mobile and desktop layouts.
- **Responsive Headlines:**
  - Mobile: `1.25rem`
  - Tablet: `1rem`
  - Large: `1rem`
  - Extra Large: `1.35rem`
- **Aspect Ratio:** `1880 / 1000` for images
- **Grid Gap:** `30px`
- **Layout:** All card layouts are mobile-first, with grid and spacing unified across tag index, tag pages, and portfolio index for visual consistency.

### Portfolio Tags
- **Font-size:** `0.875rem`
- **Line-height:** `2` (converted from `1.75rem`)
- **Padding:** `3px 6px`
- **Border-radius:** `4px` (6px on hover)

## Spacing System

### Base Units
- **Small:** `0.25rem`, `0.5rem`
- **Medium:** `1rem`, `1.5rem`
- **Large:** `2rem`, `3rem`

### Component Spacing
- **Lab Projects:** `1rem` gap, `1.5rem` between projects
- **Contact Sections:** `0.25rem` within groups, `1rem` between groups
- **Cards:** `30px` grid gap, consistent internal padding, and unified spacing across all card types
- **Content:** `20px` standard padding

### Layout & Background Standards
- All tag index, tag pages, and portfolio index pages use a unified, mobile-first grid layout.
- Page backgrounds are offwhite (`#FAFAF9`), while cards are always white for contrast and clarity.
- Spacing and padding are standardized for a consistent, accessible, and visually balanced experience across all breakpoints.

## Responsive Breakpoints

- **Tiny Mobile:** `280px+`
- **Small:** `350px+`
- **Medium:** `530px+`
- **Large:** `768px+`
- **X-Large:** `1244px+`
- **XX-Large:** `1200px+` (with min-height: `800px`)

## CSS Consolidation Results

### Completed Optimizations

#### Line-Height Consolidation
- **Reduced from:** 12+ instances to 2 meaningful values
- **Standardized to:** `1.2` (base), `0.75` (headlines), `2` (tags)
- **Removed redundant declarations** from h2, p, li, ol, ul selectors

#### Font-Size Consolidation
- **Reduced from:** ~50 scattered declarations to systematic scale
- **Standardized small text** to single `0.875rem` value
- **Converted units** from mixed px/em to consistent `rem`
- **Eliminated redundancy** by leveraging inheritance

#### Unit Standardization
- **Line-height:** All unitless (CSS best practice)
- **Font-size:** Primarily `rem` with strategic `px` for pixel-perfect needs
- **Spacing:** Consistent `rem`-based scale

### Impact & Benefits

1. **Maintainability:** Easier to understand and modify typography
2. **Consistency:** Unified approach across all components
3. **Performance:** Reduced CSS complexity and redundancy
4. **Scalability:** Clear patterns for adding new components
5. **Accessibility:** Consistent relative sizing for better user control

## File Structure

### Core CSS Files
- `main-base.css` - Base typography, colors, foundational styles
- `main-components.css` - Reusable components (buttons, tags, etc.)
- `main-responsiveness.css` - Responsive breakpoints and adaptations
- `content-card.css` - Card component system
- `feature-carousel.css` - Carousel component
- `feature-zoom.css` - Image zoom functionality

### Page-Specific Files
- `page-home.css` - Homepage-specific styles
- `page-about.css` - About page layout and lab projects
- `page-portfolio.css` - Portfolio-specific components

## Future Considerations

### Potential Next Steps
1. **Spacing System:** Consolidate margin/padding values
2. **Border Radius:** Standardize corner radius values
3. **Shadows:** Create consistent shadow scale
4. **Animation:** Standardize transition timing and easing
5. **Grid Systems:** Document grid patterns and breakpoints

### Best Practices Established
- Use inheritance over explicit declarations
- Prefer `rem` units for scalability
- Maintain responsive design integrity during consolidation
- Document systematic approaches for future reference
- Test across breakpoints after major changes

## Browser-Specific Fixes

### Safari Layout Compatibility

#### Issue: "Up Next" Cards Loading Narrow
Safari's layout engine sometimes incorrectly calculates grid/flexbox dimensions on initial page load, causing the "Up Next" project cards to render too narrow. The cards would resize correctly on hover or page refresh, indicating a layout calculation timing issue.

#### Solution: Force Layout Recalculation
Implemented `safari-layout-fix.js` with a simple but effective approach:

```javascript
// Wait for complete page load
window.addEventListener('load', () => {
  setTimeout(() => {
    const container = document.querySelector('.next-project-container');
    if (container) {
      // Force complete layout recalculation by hiding/showing container
      const display = container.style.display;
      container.style.display = 'none';
      container.offsetHeight; // Force reflow
      container.style.display = display;
    }
  }, 100);
});
```

**Key principles:**
- **Safari-only targeting:** Uses user agent detection to avoid unnecessary processing in other browsers
- **Complete page load:** Waits for `window.load` event to ensure all assets are loaded
- **Simple force reflow:** Temporarily hides container to force Safari to recalculate entire layout
- **Minimal timeout:** 100ms delay ensures timing is right for Safari's layout engine

#### Zoomable Image Safari Fixes
Safari also had issues with image zoom functionality where images would become aliased after zooming and centering was broken. This was resolved in `zoomable-image.js` by:
- Resetting transforms before applying new zoom transforms
- Using explicit centering calculations rather than relying on Safari's transform-origin
- Ensuring image quality is maintained during zoom operations
- **Using zoom-optimized image variants** for better performance and quality
- **Grayblue placeholder loading animation** that's comfortable and non-motion-based

#### Zoom-Optimized Image Pipeline & Loading Experience
The build system now creates compressed zoom variants and provides a comfortable loading experience:
- **Source:** Original high-resolution images (typically large, upscaled files)
- **Zoom Variants:** `{basename}-zoom.png` files created by Sharp with quality: 95, compressionLevel: 6
- **File Size Reduction:** Typically 60-70% smaller than originals while maintaining zoom quality
- **Fallback Chain:** Zoom variant → Original PNG → Currently displayed image
- **Build Integration:** Missing zoom variants are auto-detected and regenerated during builds

**Loading Animation:**
- **First zoom:** Shows a grayblue (`--grayblue`) placeholder in the exact shape of the original image
- **High-res fade-in:** Smooth opacity transition from placeholder to final image (0.5s)
- **Subsequent zooms:** Simple "Loading..." text indicator with faster fade-in (0.4s)
- **Transparent image support:** Offwhite (`--offwhite`) background with subtle shadow and rounded corners
- **Comfortable UX:** No blur or motion effects that could cause dizziness

The zoom-optimized approach significantly reduces bandwidth usage for zoomable images while maintaining the high quality needed for detailed examination of portfolio work.

### Testing Requirements
All Safari-specific fixes must be tested in actual Safari browsers, as Safari's WebKit engine behaves differently from Chrome's WebKit implementation, and these differences cannot be reliably simulated in other browsers.

## Video Performance Optimizations (2025-01-16) ✅

### Immediate Code Improvements - IMPLEMENTED & TESTED
- **Intelligent preloading**: Videos now preload metadata when they come into viewport (-200px margin)
- **Progressive loading**: Videos in prominent view (70%+ visible) preload full data after 1 second delay
- **Real progress indication**: Progress bar shows actual buffering progress instead of simulated loading
- **Better loading detection**: Multiple fallback event listeners (`loadeddata`, `canplay`, `progress`) for more reliable loading
- **Increased timeout**: Extended fallback timeout to 8 seconds for large files
- **Result**: Significantly faster video loading experience - videos now load "really fast" per user testing

### Performance Issues Identified
- Video files are 1MB-21MB (most 3-8MB) - too large for web
- High resolution (1080p+) and bitrate (2.1-2.3 Mbps) for short demos
- No web optimization in current workflow

### Video Optimization Script - OPTIONAL FURTHER IMPROVEMENT
Created `/bin/optimize-videos.sh` to compress existing videos for even better performance:
- Reduces bitrate to 1.2 Mbps (web-optimized)
- Limits max width to 1280px
- Uses efficient H.264 encoding with faststart
- Creates backups before optimization
- Targets 50-80% file size reduction

To run: `./bin/optimize-videos.sh`

*Note: Current loading performance is already fast due to preloading optimizations. Video compression would provide additional bandwidth savings and faster initial page loads.*

### Recommended Workflow Changes
1. Export videos at 720p-1080p max with 1-1.5 Mbps bitrate
2. Use H.264 codec with "fast start" enabled
3. Consider WebM format for additional compression
4. Implement responsive video sources for different screen sizes

---

*This design system reflects the systematic approach taken to create a more maintainable, consistent, and scalable CSS architecture while preserving the original design intent and responsive behavior.*
