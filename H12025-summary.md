# 2025 Website Development & System Enhancements – Comprehensive Summary

**Author:** Dan Reis
**Scope:** All major features, fixes, and technical improvements to the website and build system in 2025

---

## Table of Contents
1. Tagging System & Portfolio Navigation
2. Build System & Automation
3. UI/UX & Design System
4. Security & Password Protection
5. Performance & Optimization
6. Documentation & Workflow
7. Notable Scripts & Technical Highlights

---

## 1. Tagging System & Portfolio Navigation
- **Three-Category Tagging:** Standardized all portfolio items with Role, Industry & Platform, and Approach tags. Tags are clickable and enable filtering across the portfolio.
- **Tag Index & Pages:** Auto-generated tag index and individual tag pages for every unique tag. Tag pages use a responsive grid and show all related projects.
- **Dynamic Company Logo Injection:** Company logos are injected automatically into cards and headers based on project metadata.
- **Tag Normalization:** All tags are canonicalized, alphabetized, and consistently categorized. No non-canonical tags remain.
- **Enhanced Tag Categorization:** Improved semantic accuracy and granularity for all tags, with clear documentation and audit.
- **Automated '+ More' Tag Spacer:** Build system inserts a spacer before the '+ More' tag for consistent tag row layout.

## 2. Build System & Automation
- **Swift Build System v2.0:** Git-based image and asset change detection, self-healing for missing outputs, and 17x faster builds (18s typical).
- **Unified Audit Workflow:** All audit functionality consolidated into a single script (`audit.mjs`). Menu and CLI are streamlined.
- **Automated Version Token Replacement:** All `{{VERSION}}` tokens in HTML are replaced with the current version for cache-busting.
- **Menu System Overhaul:** Interactive menu is simplified, with clear build, preview, deploy, and utility options. All audit and build commands are non-blocking.
- **Automated Doc Sync & Git Hooks:** Documentation is auto-synced to the public repo with pre-push hooks and last commit date updates.
- **Modular Head Injection:** HTML head is now template-driven, split into upper/lower parts for maintainability.
- **Template-Driven Carousel & Cards:** Carousel and "Up Next" cards are now generated from HTML templates, not JS strings.

## 3. UI/UX & Design System
- **Unified Card Styling:** All card appearance is handled by external CSS; inline styles are eliminated.
- **Mobile-First & Responsive:** Tag index, tag pages, and portfolio index use a unified, mobile-first grid and card layout.
- **Color System Finalization:** All color usage is centralized with CSS variables; legacy/duplicate color values removed.
- **Portfolio Tag Styling:** Tags have consistent font size, spacing, and appearance across all contexts.
- **Theatre Mode Overlay for Video:** Videos feature a dedicated Theatre Mode button with fade-out UX and robust overlay logic.
- **Zoomable Image & Video Overlays:** Unified overlay core for images and videos, with focus trap, ESC handling, and scroll lock.
- **Safari & iOS Compatibility:** All browser-specific layout and rendering issues resolved.

## 4. Security & Password Protection
- **Global Password Protection:** Centralized password config for all protected pages, with 24-hour session persistence and localStorage.
- **Password Modal & Anti-Scraping:** Protected pages use a secure modal dialog and blurred preview; content is only loaded after authentication.
- **Comprehensive Lock Icon System:** Password-protected cards display lock icons in all portfolio contexts, with proper color inheritance and responsive design.
- **Menu Utilities:** CLI utilities for updating the global password and printing the access code on demand.

## 5. Performance & Optimization
- **Automatic Image Dimension Injection:** Build system reads image metadata and injects width/height, eliminating manual work and preventing CLS.
- **Video Optimization:** Portfolio videos are compressed (50-84% reduction), with intelligent preloading and real buffering progress.
- **Self-Healing Image Pipeline:** Missing responsive/zoom image variants are auto-regenerated.
- **CSS Minification & Smart Build Logic:** Only minifies/optimizes assets if changes are detected.

## 6. Documentation & Workflow
- **Documentation Consolidation:** All technical docs merged into three files: `README.md`, `DEVELOPER-NOTES.md`, `DESIGN-SYSTEM.md`.
- **Automated Doc Date Updates:** All markdown docs have their `Updated:` date set to the last git commit date during sync.
- **Feature Docs:** Each major feature/change is documented in a dated folder with a summary readme.
- **Changelog Management:** Only the 10 most recent releases are in `CHANGELOG.md`; older entries are auto-archived.

## 7. Notable Scripts & Technical Highlights
- **audit.mjs:** Unified audit script for all build, compare, and baseline management.
- **01-process-images-git.mjs:** Git-based image processing with self-healing and force/commit flags.
- **06-build-portfolio.mjs:** Main build script for portfolio, tags, cards, and company logo injection.
- **optimize-videos.sh:** Shell script for compressing and optimizing all portfolio videos.
- **password-protection utilities:** Scripts for adding, updating, and printing password/access code.
- **sync-public-docs.sh:** Syncs and sanitizes documentation to the public repo, with auto date update.

---

## Highlights by Month

### June 2025
- Portfolio tag system overhaul: clickable tags, tag index, and tag pages
- Enhanced tag categorization and company logo automation
- Automatic image dimension injection and optimization
- Unified audit workflow and menu simplification
- CSS/JS consolidation and design system documentation

### July 2025
- Global password protection system and modal
- Lock icon system for protected cards
- Modular head injection and carousel/card templates
- Documentation system consolidation and automation
- Theatre Mode overlay for video

### August 2025
- Tag normalization and technical documentation tag expansion
- Refined image change detection and build performance
- Modular media zoom system and carousel icon integration

---

**This file summarizes all major 2025 work on the website and build system. For full details, see the changelog and feature docs.**
