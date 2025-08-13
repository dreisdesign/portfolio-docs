# Developer Notes

**Updated: August 13, 2025**

This document contains all technical implementation details for the portfolio system, including workflows, build pipeline, scripts reference, browser fixes, and advanced implementation notes. For design, content, and UI guidelines, see [DESIGN-SYSTEM.md](DESIGN-SYSTEM.md).
---

## Quick Workflows
- Edit your content or code in the private repo.
- Run `npm run menu` and select "Build" for a fast, smart build.
- Preview your changes locally with the preview server.
- Use the menu's "New Page" option or run `npm run create-new`.

## 2025-08-13: Theatre Mode Video Overlay System

### Overview
The Theatre Mode overlay system provides a focused, accessible video viewing experience for all portfolio videos. It is triggered by a dedicated Theatre Mode button (top-right of each video), which opens a modal overlay with a cloned video element. The overlay is always muted, has no native controls, and supports click-to-pause/play, click outside/ESC to close, and seamless resume of playback inline after closing.

### Technical Implementation
- **File:** `public_html/js/zoom-video.js`
- **Overlay Creation:**
  - Clicking the Theatre Mode button creates a modal overlay and clones the original video’s `<source>` elements for clean playback state.
  - Overlay video is always muted, no native controls, and auto-plays on open.
  - Overlay closes on click outside, ESC, or Theatre Mode button.
  - On close, playback state (currentTime, paused/playing) is synced back to the original inline video.
- **Button Fade-Out Logic:**
  - Theatre Mode button fades out after 2.5s of video playback.
  - Button reappears on mouse movement or when video is paused.
  - Always visible when paused.
- **SVG Icon Override:**
  - Uses a custom white SVG icon (`open_in_full.svg`).
  - Robust CSS override ensures icon is always white and has no unwanted margin/spacing, regardless of global SVG rules.
- **Dynamic Binding:**
  - Uses a MutationObserver and custom events (`protectedContentUnlocked`, `carouselsInitialized`) to bind Theatre Mode buttons to videos added after initial page load (e.g., carousels, password-protected pages).
  - Guards with `data-zoom-video-bound` to prevent duplicate bindings.
- **Robust Overlay Close:**
  - Overlay close logic is reliable on both public and password-protected pages, with no stray references or event handler issues.
- **Accessibility:**
  - Overlay is fully keyboard and mouse accessible (focus trap, ESC, scroll lock).
  - Button and overlay are navigable and usable via keyboard.

### Maintenance Notes
- All overlay/button logic is modular and robust to global CSS/JS changes.
- To update the Theatre Mode button/icon, edit the SVG in `assets/images/icons/open_in_full.svg` and the CSS override in `feature-zoom.css`.
- Overlay and button logic are self-contained in `zoom-video.js` and require no external dependencies.

---
- Add your content and assets as needed.

### 3. Tagging & Categorization
- Use standardized tag markup in your HTML (see README for details).
- The build system will automatically generate tag pages and indexes.

### 4. Syncing Docs to Public Repo
- Update or add docs in `DOCS/`.
- Run the sync utility to publish all docs to the public docs repo.
- Security checks will prevent accidental leaks of sensitive files.

### 5. Troubleshooting
- Check the build log for validation errors or skipped pages.
- Use the troubleshooting section in the README or this document for common issues.

---

## Build Pipeline Overview

This section provides a high-level overview of the portfolio build pipeline, including the order of operations, key scripts, and their responsibilities.

### Pipeline Steps

1. **HTML Validation** (`00-validate-html.mjs`)
   - Validates source HTML for structure, metadata, and accessibility.
   - Updates timestamps in HTML and CSS files.

2. **Image Processing** (`01-process-images.mjs`)
   - Optimizes, resizes, and converts images.
   - Applies automatic sharpening for clarity.

3. **Static Placeholders** (`02-create-static-placeholder.mjs`)
   - Generates static placeholder images for loading/fallback.

4. **Featured Images** (`03-preprocess-featured-images.mjs`)
   - Prepares all responsive sizes for featured images.

5. **File Formatting** (`04-format-files.sh`)
   - Formats CSS and JSON.
   - Minifies CSS.

6. **Portfolio Build** (`06-build-portfolio.mjs`)
   - Main build coordinator: processes portfolio pages, injects navigation, logos, tags, carousels, and generates index/tag pages.
   - Carousels and "Up Next" cards are now generated from modular HTML templates (`carousel-template.html`, `up-next-card-template.html`).
   - **Automated Version Replacement:** After all portfolio pages are generated, the build script automatically replaces all `{{VERSION}}` tokens in every HTML file in the build output directory with the current version from `package.json`. This ensures all asset URLs (CSS, JS, favicons, etc.) are cache-busted and versioned consistently.

7. **Modular Head & Footer Injection** (`inject-head-upper.mjs`, `inject-head-lower.mjs`, `inject-footer.mjs`)
   - Injects upper and lower head content, and the footer into all HTML files in the build output.
   - Uses placeholders: `<!-- BUILD_INSERT id="head-upper" -->` and `<!-- BUILD_INSERT id="head-lower" -->` in templates/source files.
   - Head content is managed in separate template files for maintainability.
   - **Note:** The modular head injection system allows you to update meta tags, favicons, and scripts in a single place (`injected-head-upper.html` and `injected-head-lower.html`), ensuring consistency and maintainability across all pages.

8. **Password Protection** (`inject-password-protection.mjs`)
   - Converts pages marked with `<!-- BUILD_INSERT id="password" data-password="access-code" -->` into password-protected versions
   - Base64 encodes original content and replaces with professional access form UI
   - Preserves HTML entities and complex JavaScript functionality (e.g., carousel components)
   - Integrates seamlessly with existing BUILD_INSERT pattern

9. **Responsive Image Transformation** (`05-transform-responsive-images.mjs`)
   - Updates image tags for responsive delivery.

10. **Pre-Deploy Checks** (`07-pre-deploy-check.sh`)
    - Runs final checks before deployment.

11. **Preview Server** (`08-preview-server.mjs`)
    - Optionally starts a local server for previewing the build.

### Build Pipeline Diagram

```
[Validate HTML] → [Process Images] → [Create Placeholders] → [Featured Images]
      ↓                 ↓                   ↓                    ↓
[Format & Inject Head] → [Responsive Images] → [Portfolio Build]
      ↓                 ↓                   ↓                    ↓
[Footer Inject] → [Password Protection] → [Pre-Deploy Checks] → [Preview Server]
```

### Documentation Sync Automation

A pre-push git hook automatically runs the docs sync script (`dev/scripts/deploy/deploy-support/utils/sync-public-docs.sh`) before every push. This ensures that all public documentation in the `DOCS/` and root-level `.md` files are always up to date and secure, without requiring manual steps.

- **Location:** `.git/hooks/pre-push`
- **Behavior:** Runs the sync script and blocks the push if the sync fails.
- **How it works:**
  1. You commit as usual.
  2. On `git push`, the sync script runs automatically.
  3. If the sync passes, the push proceeds. If not, the push is blocked and you see an error message.
- **To disable or customize:** Edit or remove `.git/hooks/pre-push`.

#### Automated "Updated:" Date in Docs

- During each sync, the script automatically updates the `Updated:` date in all Markdown docs (`.md`) to match the last git commit date for each file.
- This ensures every doc reflects its true last change, improving transparency and auditability.
- **How it works:**
  1. The sync script determines the correct source file path in the private repo for each `.md` file
  2. Uses `git log` to find the last commit date for that specific file
  3. Updates the `**Updated: August 13, 2025**` line in each file before syncing to the public repo
  4. Handles both root-level files (like `README.md`) and files in the `DOCS/` directory
- **Format:** Dates are automatically formatted as "Month Day, YYYY" (e.g., "July 9, 2025")
- **No manual intervention needed:** Just commit changes as usual and the sync handles date updates automatically
- **Verification:** Check the public repo after sync to confirm dates match the latest commit dates

This workflow eliminates the need to remember to sync docs manually and ensures your public documentation is always current and safe.

---

## Password Protection System

A secure global password protection system for portfolio pages with centralized management and session persistence.

### Architecture
- **Global Configuration**: Single password for all protected pages via `dev/env/password-config.mjs`
- **Session Management**: 24-hour localStorage persistence across all protected pages
- **Template-Driven UI**: Professional modal dialog via `password-protection-template.html`
- **BUILD_INSERT Integration**: Simple `<!-- BUILD_INSERT id="password" -->` markers

### Features
- **Modal Dialog**: Clean overlay with blurred preview content
- **Real Content Protection**: Content hidden from DOM until authentication
- **Auto-Unlock**: Valid sessions automatically unlock content without prompts
- **Global Password Management**: Single configuration file controls access to all protected pages
- **Audit Integration**: "Secure" metric in audit reports with detailed protected pages list

### Workflow
1. Add `<!-- BUILD_INSERT id="password" -->` to page top
2. Build pipeline converts to password-protected version
3. Users enter global password once per 24-hour session
4. All protected pages auto-unlock for valid sessions

### Configuration
- **Password**: Change `GLOBAL_PASSWORD` in `dev/env/password-config.mjs`
- **Session Duration**: Modify `SESSION_DURATION` constant (default: 24 hours)
- **Storage Key**: Customize `STORAGE_KEY` for localStorage

---

## Scripts Reference

This section describes the main scripts and utilities that power the portfolio build system. For most users, the interactive menu (`npm run menu`) is the easiest way to access these features.

### Core Scripts

- **00-validate-html.mjs**
  - Validates HTML structure, metadata, and accessibility.
  - Updates timestamps in HTML and CSS files.

- **01-process-images.mjs**
  - Optimizes, resizes, and sharpens images for web delivery.

- **02-create-static-placeholder.mjs**
  - Generates static placeholder images for loading/fallback.

- **03-preprocess-featured-images.mjs**
  - Prepares all responsive sizes for featured images.

- **04-format-files.sh**
  - Formats HTML, CSS, and JSON files.
  - Minifies CSS.

- **05-transform-responsive-images.mjs**
  - Transforms all images to include responsive `<picture>` elements.

- **06-build-portfolio.mjs**
  - Main script for generating portfolio structure, tags, and navigation.

- **08-preview-server.mjs**
  - Local development server for previewing builds.

### Password Protection System

- **inject-password-protection.mjs**
  - Location: `dev/scripts/deploy/deploy-support/password-protection/`
  - Applies password protection to pages marked with `BUILD_INSERT id="password"`
  - Uses template-driven architecture with `password-protection-template.html`
  - Integrates with build pipeline via `npm run password:protect`

- **add-password-protection.mjs**
  - Interactive utility for adding password protection to portfolio pages
  - Accessible via `npm run menu` → Utilities → Add Password Protection
  - Validates passwords and provides confirmation workflow

- **password-protection-template.html**
  - Location: `dev/scripts/deploy/deploy-support/build-portfolio-templates/`
  - HTML template with placeholders: `[[TITLE]]`, `[[DESCRIPTION]]`, `[[ENCODED_CONTENT]]`, `[[PASSWORD_HASH]]`
  - Professional UI with hiring manager instructions and security features
  - Updates image tags for responsive delivery (`srcset`, `sizes`).

- **06-build-portfolio.mjs**
  - Main build coordinator: processes portfolio pages, injects navigation, logos, tags, carousels, and generates index/tag pages.
  - **Tag index, tag pages, carousels, and "Up Next" cards are now 100% template-driven.**
    - Templates: `build-portfolio-templates/tag-index-template.html`, `build-portfolio-templates/tag-listing-template.html`, `build-portfolio-templates/carousel-template.html`, and `build-portfolio-templates/up-next-card-template.html`
    - No hardcoded HTML for these components in the script—if a template is missing, the build fails.
    - To change component layout or style, edit the template and rebuild.
    - The tag listing template is now fully aligned with the main portfolio index page in terms of stylesheet order, script placement, wrapper structure, and body class. This ensures visual and structural consistency across all portfolio pages.
  - **Automated Version Replacement:** At the end of the build, all `{{VERSION}}` tokens in HTML output are replaced with the version from `package.json`.

- **inject-head-upper.mjs**
  - Injects the upper portion of the HTML head (essential meta tags, charset, viewport, etc.) into all HTML files at the `<!-- BUILD_INSERT id="head-upper" -->` placeholder, using the `injected-head-upper.html` template.

- **inject-head-lower.mjs**
  - Injects the lower portion of the HTML head (fonts, favicons, CSS, versioning, and portfolio scripts) into all HTML files at the `<!-- BUILD_INSERT id="head-lower" -->` placeholder, using the `injected-head-lower.html` template.
  - Handles dynamic versioning and portfolio-specific script injection.

- **inject-password-protection.mjs**
  - Converts pages marked with `<!-- BUILD_INSERT id="password" data-password="access-code" -->` into password-protected versions
  - Base64 encodes original content and replaces with professional access form UI
  - Preserves HTML entities and complex JavaScript functionality (e.g., carousel components)
  - Integrates seamlessly with existing BUILD_INSERT pattern

- **inject-footer.mjs**
  - Ensures a single, correctly placed footer in every HTML file.

- **07-pre-deploy-check.sh**
  - Runs final checks before deployment.

- **08-preview-server.mjs**
  - Starts a local server for previewing the build.

### Utilities

- **audit.mjs**
  - Unified audit, comparison, and baseline update tool.
  - Usage: `node dev/scripts/deploy/deploy-support/utils/audit.mjs [options]`

- **insert-section.mjs & insert-section.sh**
  - Interactive utility for inserting prebuilt HTML sections (image, video, carousel) into any HTML file.

- **scrape-site-content.mjs**
  - Extracts text content from the live site for analysis or migration.

- **sync-public-docs.sh**
  - Syncs documentation from the private repo to the public docs repo, with security checks.

---

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

### Zoomable Image Safari Fixes
Safari also had issues with image zoom functionality where images would become aliased after zooming and centering was broken. This was resolved in `zoomable-image.js` by:
- Resetting transforms before applying new zoom transforms
- Using explicit centering calculations rather than relying on Safari's transform-origin
- Ensuring image quality is maintained during zoom operations
- **Using zoom-optimized image variants** for better performance and quality
- **Grayblue placeholder loading animation** that's comfortable and non-motion-based

### Zoom-Optimized Image Pipeline & Loading Experience
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

---

## Modular Media Zoom System (2025-08-12)

### Components
- `zoom-overlay-core.js` – Single overlay factory (focus trap, ESC, scroll lock, cleanup of prior instance)
- `zoomable-image.js` – Image zoom (progressive reveal, pan, zoom variant usage, placeholder fade)
- `zoom-video.js` – Video zoom (clone `<source>` nodes, skeleton placeholder, autoplay on reveal, preload escalation)

### Dynamic Binding
Late DOM insertions (carousels, password unlock) are handled via:
1. Custom events: `carouselsInitialized`, `protectedContentUnlocked`
2. A MutationObserver watching added nodes for `<img>` / `<video>`

Each candidate guarded with dataset flags (`data-zoom-bound`, `data-zoom-video-bound`) for idempotency.

### Password-Protected Pages
Template injects the same script bundle. After unlock it dispatches `protectedContentUnlocked`; no duplicate inline zoom code needed (removed redundant post-unlock tagging loop).

### Carousel Integration
Carousel emits `carouselsInitialized` once all instances mount, allowing zoom modules to bind media inside slides without tight coupling.

### SVG Navigation Icons
Prev/next buttons now inline SVG (currentColor). A global `.content svg` rule previously distorted sizing; scoped override in `feature-carousel.css` (`.carousel .carousel-button svg { width:24px; height:auto; }`) restores correct dimensions without weakening global styles.

### Debugging
Define `window.CAROUSEL_DEBUG = true` before interaction to re-enable verbose lifecycle logging routed through a `carouselDebug()` helper.

### Extensibility
Future media types can reuse the core by supplying a renderer that appends content to the overlay container and triggers a reveal transition.

---

## Video Performance Optimizations (2025-01-16)

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

## 2025-07-15: Password-Protected Page Feature Parity & Overlay Robustness

- Password-protected portfolio pages now preserve and re-initialize all feature CSS/JS (carousel, zoom, video, etc.)
- Zoom overlay and modal styles are inlined for reliability and mobile-friendliness
- No more CSS/JS duplication or missing features in protected pages
- Build pipeline improvements:
  - `inject-password-protection.mjs` extracts and preserves all relevant CSS/JS from original content
  - `inject-head-lower.mjs` ensures feature CSS is injected only when needed
  - Password-protection template only outputs preserved CSS/scripts, no hardcoded main.css
- Overlay and modal logic is robust to dev/prod differences and works identically on protected and public pages
- See also: `feature-zoom.css`, `password-protection-template.html`, and related build scripts

---
