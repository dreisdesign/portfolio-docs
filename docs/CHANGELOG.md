# Changelog

**Note:** This changelog only shows the 10 most recent releases. For older entries, see the [Changelog Archive](./archive/CHANGELOG-archive.md).

All notable changes to this project will be documented in this file.

## [2.5.24] - 2025-08-12 - Modular Media Zoom System & Carousel Icon Integration

### Added
- **Modular Overlay Core**: Introduced `zoom-overlay-core.js` as a unified accessible overlay foundation (focus trap, ESC handling, scroll lock) consumed by both image and video zoom modules.
- **Video Zoom Parity**: New `zoom-video.js` delivers feature parity with image zoom (enlarged playback, placeholder fade-in, auto-play) by cloning `<source>` elements for clean playback state.
- **Dynamic Lifecycle Binding**: MutationObserver + custom events (`protectedContentUnlocked`, `carouselsInitialized`) ensure images/videos added after initial load (carousel initialization, password unlock) are seamlessly bound without duplicates (dataset guard flags).

### Changed
- **Image Zoom Refactor**: `zoomable-image.js` updated to consume overlay core; removed legacy inline overlay logic from password-protection template.
- **Password-Protected Page Parity**: Forced script injection guarantees zoom + carousel scripts load inside protected builds; event dispatch after unlock triggers re-binding.
- **Carousel Navigation**: Replaced textual prev/next controls with inline currentColor SVG arrow icons; vertically centered buttons and standardized sizing.
- **Scoped SVG Override**: Added `.carousel .carousel-button svg { width:24px; height:auto; }` in `feature-carousel.css` to neutralize broad global `.content svg` rule that previously distorted navigation icons.
- **Logging Reduction**: Carousel verbose logs routed through a `carouselDebug` helper gated by `window.CAROUSEL_DEBUG`.

### Removed
- **Redundant Post-Unlock Zoom Tagging**: Eliminated duplicate video tagging loop in password template (single tagging + event now sufficient).

### Fixed
- **Missed Video Zoom on Protected Pages**: Videos now reliably open in overlay after unlock (binding no longer races original DOM insert).
- **Icon Mis-Sizing**: Carousel arrows no longer inherit unintended width/height from global SVG rule.

### Technical Implementation
- Shared overlay factory returns overlay root & close logic reused by both modules.
- Video zoom uses optimistic reveal with timeout safety net and progressive preload via IntersectionObserver.
- Dataset idempotency flags prevent re-binding during rapid DOM mutations.
- Event-driven architecture avoids brittle polling and keeps feature JS lean.

### Impact
- **Consistency**: Images and videos present a unified zoom experience (public + protected pages, inside carousels).
- **Maintainability**: Overlay behavior centralized; future media types can adopt same core.
- **Performance**: Lazy binding & conditional preload minimize network use while keeping interactions instant.
- **DX**: Cleaner template and quieter console.

### Migration Notes
No action required. Existing pages gain video zoom automatically after rebuild. Enable debug with `window.CAROUSEL_DEBUG = true`.

## [2.5.23] - 2025-08-12 - Refined Git Image Change Detection (Script v2.0.1)

### Changed
- **Image Processing Default Behavior**: Git-based image pipeline now ignores the previous commit diff (`HEAD~1..HEAD`) by default, preventing recently committed images from being repeatedly reprocessed on every subsequent build.
- **Detection Scope**: Now only processes images that are (a) unstaged working tree changes, (b) staged/index changes, (c) missing any responsive/zoom outputs (self‑healing), or (d) explicitly forced.
- **Logging Clarity**: Updated logging to clearly show whether last commit changes are included.

### Added
- **`--include-last-commit` Flag**: Opt-in flag to restore prior behavior of also processing images changed in the most recent commit.
- **Documentation**: README updated to reflect new flags and refined detection model.

### Unchanged
- **Force Mode**: `--force-all` still processes every image (e.g., for baseline regeneration).
- **Self-Healing**: Missing variant or zoom files still trigger regeneration automatically.

### Impact
- **Faster Repeat Builds**: Avoids unnecessary reprocessing after committing large image batches.
- **Deterministic Behavior**: Builds are stable across runs until new modifications occur or variants go missing.

### Migration Notes
No action required. Existing workflows continue to work. Use `--include-last-commit` if you depended on the old behavior for post-commit verification builds.

## [2.5.22] - 2025-08-11 - Comprehensive Lock Icon System for Password-Protected Portfolio Cards

### Added
- **Visual Lock Icon System**: Complete implementation of lock icons for password-protected portfolio cards across all portfolio locations
  - **Portfolio Index Page**: Lock icons appear on password-protected cards with white color on dark background overlay
  - **Up Next Cards**: Lock icons displayed on password-protected projects in "Up Next" sections at bottom of portfolio pages
  - **Tag Pages**: Lock icons shown on password-protected cards within all tag listing pages
  - **SVG Lock Icon**: Custom lock icon asset at `/assets/images/icons/lock.svg` with proper currentColor inheritance
- **Comprehensive Password Detection**: Enhanced portfolio build system with intelligent password protection detection
  - **BUILD_INSERT Marker Detection**: Automatic detection of `<!-- BUILD_INSERT id="password" -->` markers in source HTML
  - **Portfolio Data Integration**: Password protection status included in portfolio metadata JSON for all card generation
  - **Next Project Mapping Fix**: Corrected "Up Next" card generation to include password protection status from portfolio data

### Enhanced
- **Build Pipeline Integration**: Lock icon generation fully integrated into portfolio build process
  - **Step Integration**: Lock icon injection added to portfolio build pipeline after tag processing
  - **Conditional Generation**: Lock icons only generated for cards where `isPasswordProtected: true`
  - **Template System**: Lock icon HTML generation via `generateLockIcon()` function with proper CSS class structure
- **CSS Design System**: Professional lock icon styling with design system integration
  - **Color Inheritance**: Lock icons use `fill="currentColor"` for proper CSS color inheritance
  - **Dark Background Overlay**: Lock icons display on dark semi-transparent background for visibility
  - **Responsive Design**: Lock icons scale appropriately across all device sizes and card layouts

### Fixed
- **SVG Color Inheritance**: Resolved lock icon color issues by changing from explicit CSS custom property references to `currentColor` values
  - **Previous Issue**: SVG fill attributes using `fill="var(--color-black-80)"` were overriding CSS color inheritance
  - **Solution Applied**: Updated `generateLockIcon()` function to use `fill="currentColor"` for both path and circle elements
  - **Result**: Lock icons now properly inherit white color from parent `.card--lock-icon` CSS styling
- **Up Next Card Data Flow**: Fixed missing password protection data in "Up Next" card generation
  - **Root Cause**: `createNextProjectMap()` function was not including `isPasswordProtected` property from portfolio metadata
  - **Fix Applied**: Enhanced next project mapping to include all portfolio metadata including password protection status
  - **Impact**: "Up Next" cards now correctly display lock icons for password-protected projects

### Technical Implementation
- **generateLockIcon() Function**: Centralized lock icon HTML generation with proper CSS class structure and currentColor inheritance
- **Portfolio Build Script**: Enhanced `06-build-portfolio.mjs` with comprehensive password detection and lock icon injection
- **CSS Integration**: Lock icon styling integrated into existing design system with `.card--lock-icon` class
- **Asset Management**: Lock icon SVG properly versioned and included in build asset pipeline

### Impact
- **User Experience**: Clear visual indication of password-protected content across all portfolio browsing contexts
- **Consistent Design**: Lock icons maintain design system consistency with proper color inheritance and responsive behavior
- **Build System Reliability**: Automated lock icon generation ensures consistent application across all password-protected content
- **Maintainable Architecture**: Centralized lock icon generation function enables easy updates and modifications

## [2.5.21] - 2025-07-15 - Password-Protected Page Feature Parity & Overlay Robustness

### Changed
- Password-protected portfolio pages now fully preserve and re-initialize all feature CSS/JS (carousel, zoom, video, etc.)
- Zoom overlay and modal styles are robust, inlined, and mobile-friendly
- Eliminated CSS/JS duplication and missing features in protected pages
- Improved build pipeline for password protection and head injection (see `inject-password-protection.mjs` and `inject-head-lower.mjs`)
- All protected pages now visually and functionally match public portfolio pages

## [2.5.20] - 2025-07-14 - Global Password Protection System

### Added
- **Global Password Configuration**: Centralized password management via `dev/env/password-config.mjs`
  - **Single Password for All Protected Pages**: Simplified from individual passwords to global portfolio password (`dr2025`)
  - **Session Persistence**: 24-hour localStorage session across all protected pages - users only enter password once per day
  - **Automatic Session Validation**: Smart session checking with timestamp validation and cleanup
  - **Configurable Session Duration**: Easy adjustment of session length via configuration constant
- **Enhanced Audit System**: Password protection tracking and reporting
  - **"Secure" Metric**: Added security status to audit comparison tables showing count of protected pages
  - **Protected Pages Display**: Detailed list of protected pages shown below audit comparison table
  - **Source Directory Scanning**: Tracks password markers in source files (since they're processed out of build)
  - **Global Password Documentation**: Clear instructions on where to change the global password
- **Simplified Menu Workflow**: Streamlined password protection addition process
  - **Removed Password Input Prompts**: No longer asks users to input passwords during protection process
  - **Global Password Usage**: All protected pages automatically use the centralized global password
  - **Clear Status Reporting**: Shows count of available vs. already protected pages
  - **Simplified BUILD_INSERT Markers**: Reduced from `id="password" data-password="pass"` to just `id="password"`

### Changed
- **Password Protection Template**: Enhanced with localStorage session management
  - **Auto-Unlock Functionality**: Protected pages automatically unlock for users with valid sessions
  - **Session Storage Integration**: Seamless integration with existing password verification system
  - **Improved UX**: Users no longer need to re-enter passwords on each page visit within 24-hour window
- **Password Protection Scripts**: Updated to use global password configuration
  - **Centralized Configuration Import**: All scripts now import from `dev/env/password-config.mjs`
  - **Removed Individual Password Handling**: Scripts no longer process `data-password` attributes
  - **Simplified Marker Detection**: Standardized detection of password protection markers
- **Existing Protected Pages**: Updated markup to remove individual password attributes
  - **Cleaned BUILD_INSERT Markers**: Removed `data-password` attributes from existing protected pages
  - **Backwards Compatibility**: All existing protections continue to work with global password system

### Enhanced
- **Audit Reporting**: Comprehensive password protection visibility
  - **Integration with Comparison Tables**: "Secure" column shows protected page counts across audit history
  - **Detailed Protected Pages List**: Shows specific paths of all password-protected pages
  - **Global Password Management Info**: Clear documentation on where to update the global password
  - **Visual Formatting**: Professional formatting with emojis and clear section headers

### Benefits
- **Simplified User Experience**: Single password provides access to all protected portfolio content
- **Persistent Sessions**: 24-hour login sessions eliminate repeated password entry
- **Centralized Management**: Easy password updates via single configuration file
- **Better Audit Visibility**: Clear tracking and reporting of protection status across all pages
- **Streamlined Workflow**: Menu-driven protection addition without password input complexity

## [2.5.19] - 2025-07-14 - Advanced Password Protection Modal

### Added
- **Password Protection Modal:** Implemented a secure modal dialog for portfolio pages, overlaying a blurred, non-disclosing placeholder preview. Real content is only loaded after successful authentication, preventing scraping or source inspection. Modal disables background scrolling and uses the site's design system for a seamless experience.

## [2.5.18] - 2025-07-14 - Password Protection System Refactoring

### Enhanced
- **Template-Driven Password Protection**: Refactored password protection system to use template-based architecture
  - **Template Separation**: Extracted HTML/CSS/JS to `build-portfolio-templates/password-protection-template.html`
  - **Placeholder System**: Implemented `[[TITLE]]`, `[[DESCRIPTION]]`, `[[ENCODED_CONTENT]]`, `[[PASSWORD_HASH]]` placeholders
  - **Improved Maintainability**: Separated presentation logic from script logic for better code organization
  - **Path Reorganization**: Moved password protection scripts to `dev/scripts/deploy/deploy-support/password-protection/`
  - **Build Integration**: Updated npm script paths to match new organized structure

### Fixed
- **Build Pipeline Integration**: Corrected password protection script path in package.json for proper build execution

## [2.5.17] - 2025-07-14 - Password Protection System & Interactive Menu Enhancement

### Added
- **Password Protection System**: Implemented BUILD_INSERT-based password protection for confidential portfolio pages
  - **Integration with Build Pipeline**: Added `password:protect` npm script and build step after all BUILD_INSERT processing
  - **HTML Entity Preservation**: Enhanced Base64 encoding/decoding to properly handle HTML entities (e.g., carousel arrow icons)
  - **Professional UI**: Clean access form with hiring manager instructions and error handling
  - **Security Features**: Client-side password hashing, content encoding, and anti-scraping protections
  - **Carousel Compatibility**: Fixed HTML entity handling to ensure carousel navigation works properly after unlocking
- **Interactive Password Protection Utility**: Added user-friendly menu option for adding password protection to portfolio pages
  - **File Discovery**: Automatically finds all portfolio pages and filters out already-protected ones
  - **Password Validation**: Enforces minimum length requirements and prevents problematic characters
  - **Confirmation Workflow**: Shows file path and masked password before applying protection
  - **Top-Level Placement**: Correctly places password marker at very top of HTML files
  - **Menu Integration**: Added "Add Password Protection" option to utilities submenu

### Fixed
- **Password Marker Placement**: Fixed utility script to place password protection marker at top of file instead of after `<body>` tag

## [2.5.16] - 2025-07-09 - Documentation System Consolidation & Automation

### Added
- **Git-Aware Build Pipeline Optimizations**: Enhanced build performance with intelligent change detection
  - **Featured Image Processing**: Only processes featured images if git changes detected (matches main image pipeline)
  - **CSS Minification**: Only minifies CSS files if changes detected in styles directory
  - **Build Timing Tracking**: Build times now saved to `latest-build-timing.json` and displayed in audit reports
  - **Smart Build Logic**: Eliminates unnecessary processing when no relevant changes detected
- **Audit Workflow Improvements**: Enhanced audit system with better integration and timing
  - **Build Timing in Audit Reports**: Shows build duration in audit output (e.g., "Last Build: 4.22s")
  - **Build Timing in Comparison Tables**: Added "Build Time" row between Date and Pages in audit comparisons
  - **Server Shutdown Audit**: Audit now runs when stopping server (Ctrl+C or "q" quit) instead of during build
  - **Clean Build Logs**: Removed duplicate audit results and cleaned up legacy swift-build logs
- **Automated Doc Date Updates**: All Markdown documentation files (`.md`) now have their `Updated:` date automatically set to the last git commit date for each file during the sync-to-public process
  - Sync script automatically detects last commit date using `git log`
  - Updates `**Updated: August 12, 2025**` line before syncing to public repository
  - Handles both root-level files and files in `DOCS/` directory
  - Formats dates consistently as "Month Day, YYYY"
  - Fully functional and tested end-to-end
- **Git Hook Automation**: Pre-push git hook automatically syncs documentation to public repository
  - Hook location: `.git/hooks/pre-push` (executable and functional)
  - Runs `sync-public-docs.sh` automatically before every push
  - Blocks push if sync fails (safety feature)
  - Eliminates need to manually remember documentation sync
  - Ensures public documentation is always current and secure
- **Documentation Consolidation**: Merged all technical documentation into streamlined 3-file structure
  - Consolidated `BUILD-PIPELINE.md`, `SCRIPTS.md`, and `SIMPLIFIED-WORKFLOW-GUIDE.md` into `DEVELOPER-NOTES.md`
  - Created single source of truth for all technical implementation details
  - Archived old documentation files to `DOCS/_archive/` for reference
  - Updated all cross-references in README.md and copilot instructions
- **Public Docs Repository .gitignore**: Added `.gitignore` to portfolio-docs repo with `_archive/` exclusions
  - Prevents archive folders from being committed to public repository
  - Includes common patterns for system files, editor files, and backups
  - Maintains clean, focused public documentation

### Changed
- **Documentation Structure**: Reduced from 6+ docs to focused 3-document system
  - **README.md**: User-focused project overview (unchanged)
  - **DOCS/DEVELOPER-NOTES.md**: All technical implementation, workflows, build pipeline, and scripts reference
  - **DOCS/DESIGN-SYSTEM.md**: UI/content guidelines (unchanged)
  - **DOCS/CHANGELOG.md**: Version history (unchanged)
- **DEVELOPER-NOTES.md Organization**: Structured with clear sections for discoverability
  - Quick Workflows (from SIMPLIFIED-WORKFLOW-GUIDE.md)
  - Build Pipeline Overview (from BUILD-PIPELINE.md)
  - Scripts Reference (from SCRIPTS.md)
  - Browser-Specific Fixes (existing technical content)
  - Video Performance Optimizations (existing technical content)

### Benefits
- **Optimized Build Performance**: Intelligent pipeline reduces unnecessary processing
  - Git-aware change detection prevents redundant image and CSS processing
  - Build timing tracking provides insights into build performance
  - Audit workflow improvements reduce build interruptions and provide better feedback
  - Smart build logic significantly reduces build times when no relevant changes detected
- **Fully Automated Documentation Pipeline**: Complete end-to-end automation from commit to public sync
  - Git hook ensures documentation is always synced without manual intervention
  - Automatic date updates provide transparent, accurate documentation history
  - Public repository stays current and secure automatically
- **Single Source of Truth**: All technical information consolidated in one location
- **Easier Maintenance**: One file to update instead of multiple scattered docs
- **Better Developer Experience**: Everything technical in one place for reference
- **Cleaner Repository**: Follows documentation best practices (user README + consolidated technical docs)
- **Build Pipeline Integration**: Documentation sync integrated into development workflow
  - No additional steps required - just commit and push as usual
  - Automatic validation and error handling
  - Maintains security and prevents accidental sensitive file exposure

## [Recent Updates] - Portfolio System Evolution

### Current Status (July 2025)
- ✅ **Modular Head Injection**: Template-driven HTML head management with upper/lower parts
- ✅ **Audit Log Auto-Archiving**: Keeps 5 most recent audit logs, archives older ones automatically
- ✅ **Color System Finalized**: Centralized CSS variables for all colors
- ✅ **Automated '+ More' Tag Placement**: Fully automated tag row layout
- ✅ **Feature Docs Organized**: Dated feature folder structure
- ✅ **UI/UX Improvements**: Zoomable image overlays and tag/card layout

### Latest Features (July 2025)
- ✅ **Automatic Image Dimension Injection**: Revolutionary developer experience improvement
  - Build system automatically reads image metadata using Sharp
  - 270 manual dimension attributes removed from source HTML
  - Prevents cumulative layout shift (CLS) issues
  - Source HTML now requires only `data-responsive="true"`
- ✅ **Source HTML Cleanup**: Completely automated dimension removal
  - 144 images now processed automatically during build
  - Developer workflow simplified: just add images with alt text
  - Template system updated to generate clean HTML
- ✅ **Tag Index & Portfolio Visual Consistency**: Unified, mobile-first design
  - Offwhite page backgrounds, white cards with subtle shadow
  - Consistent grid/card layout across all breakpoints
- ✅ **Mobile-First CSS**: Responsive grid and card layouts
- ✅ **Preview Automation**: One-liner page building and preview
- ✅ **Card Styling Unified**: External CSS-only styling, no inline styles
- ✅ **Color Variable System**: CSS custom properties for maximum maintainability
- ✅ **Automated Version Token Replacement**: Cache-busting for all assets

### Performance & Build System (2025)
- ✅ **Swift Build V2.0**: Ultra-fast git-based change detection with self-healing
  - 18-second builds vs 3+ minute full builds (17x faster)
  - Smart image processing: only changed images
  - Self-healing: auto-regenerates missing responsive variants
- ✅ **Build Performance Optimized**: Development workflow enhanced
  - Edit images → immediate detection without committing
  - Git-based change detection for all asset types
- ✅ **Tag Consolidation System**: Robust handling of unlimited tag content
- ✅ **Tag Page Generation**: All 32 tag pages display correctly

### Layout & Design System (2025)
- ✅ **Complete Layout & Spacing Overhaul**: Perfect consistency across all pages
  - Refactored wrapper container architecture
  - Semantic spacing system using rem units
  - Margin-based approach replacing grid-gap
- ✅ **Safari & iOS Compatibility**: All browser-specific issues resolved
  - "Up Next" card sizing fixed on Safari
  - iOS footer link color issues resolved
- ✅ **Enhanced Responsive Design**: Improved layout behavior
  - Homepage responsive rules optimized
  - Better touch interface optimization

### Portfolio System Features (2025)
- ✅ **Dynamic Company Logo Injection**: Automated logo system
  - `<!-- BUILD_INSERT id="company-logo" -->` auto-detects company
  - Works across headers, cards, tag pages, portfolio index
  - Extensible design for new companies
- ✅ **Tag System Complete**: 3-category portfolio tagging
  - Role, Platform, Audience + Company categories
  - Tag index organized by logical categories
  - Auto-generated tag pages and navigation
- ✅ **Portfolio Tag Styling Unified**: Consistent styling across all pages
  - Font size (0.875rem), spacing, transparent backgrounds
  - Removed commas between tags for cleaner presentation
- ✅ **"Up Next" Sequential Ordering**: Follows portfolio index sequence

### Public Build System & Community
- ✅ **Public Build System Released**: GitHub repository for community use
  - Repository: https://github.com/dreisdesign/portfolio-build
  - Complete build pipeline with documentation
  - Security: All sensitive information sanitized
- ✅ **Source Contamination Resolved**: Clean source/build separation
  - Removed 1,500+ build artifacts from source directory

### Audit & Quality Systems
- ✅ **Streamlined Audit Workflow**: Single, powerful audit script
  - All audit functionality consolidated into `audit.mjs`
  - Legacy scripts removed or replaced
  - Minimal, clear output with recommendations
  - Easy daily use workflow

## [2.5.15] - 2025-07-07 - NPM Script & Interactive Menu Restructuring

### Changed
- **NPM Script Renaming**: Restructured npm scripts for better workflow clarity
  - Renamed `build` → `build:only` (build without server)
  - Renamed `preview` → `build` (build + preview server - most common workflow)
  - `npm start` now only starts preview server on existing build
- **Interactive Menu Updates**: Updated menu commands to match new npm script structure
  - "Build" → "Build & Preview" (runs `npm run build`)
  - "Preview" → "Start Server" (runs `npm start`)
  - Moved advanced audit build to "Swift Build + Audit" in Utilities submenu
- **Documentation Updates**: Updated `.github/copilot-instructions.md` and `README.md` to reflect new command structure

### Benefits
- Clearer separation between build-only and build-with-preview workflows
- More intuitive menu naming that matches actual functionality
- Consistent command patterns across the project

## [2.5.14] - 2025-07-02 - Automated Version Token Replacement

### Added
- **Automated `{{VERSION}}` Replacement**: The build script now automatically replaces all `{{VERSION}}` tokens in HTML output with the version from `package.json` after all other build steps. This ensures correct cache-busting and versioning for all assets, including the homepage.

## [2.5.13] - 2025-07-02 - Modular Carousel & "Up Next" Card Refactor

### Changed
- **Carousel Generation**: Refactored carousel generation in `06-build-portfolio.mjs` to be 100% template-driven, using the new `carousel-template.html`. All hardcoded carousel HTML has been removed from the script.
- **"Up Next" Card Generation**: Refactored the "Up Next" card generation to use the `up-next-card-template.html`. The script now injects data into the template, rather than building the HTML from strings.
- **Maintainability**: This change makes both the carousel and "Up Next" card components easier to maintain and update, as their structure is now defined in clean HTML templates instead of being embedded in JavaScript.

## [2.5.12] - 2025-07-02 - Modular Head Injection Refactor

### Changed
- Refactored the build pipeline to use a modular, template-driven head injection system.
- The HTML head is now split into upper and lower parts, managed in `injected-head-upper.html` and `injected-head-lower.html`.
- New scripts `inject-head-upper.mjs` and `inject-head-lower.mjs` inject these templates at the `<!-- BUILD_INSERT id="head-upper" -->` and `<!-- BUILD_INSERT id="head-lower" -->` placeholders in all HTML files in the build output.
- Dynamic versioning, CSS suffix, and portfolio-specific scripts are handled in the lower head injection.
- Documentation and build scripts updated to reflect the new modular approach.
- Fixed build path issues in injection scripts to ensure correct operation.
