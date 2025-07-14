# Changelog

All notable changes to this project will be documented in this file.

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
  - Updates `**Updated: July 14, 2025**` line before syncing to public repository
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

## [2.5.11] - 2025-07-01 - Card Styling Unification & Inline Style Removal

### Changed
- All inline `style` attributes have been removed from `.card` elements generated by the portfolio build system (portfolio index, tag pages, and "Up Next" cards).
- All card appearance and interactive styles (box-shadow, border, transitions, :hover/:active effects) are now handled exclusively by external CSS (`content-card.css`).
- Ensured consistent and maintainable card styling across all card types and pages.
- Updated documentation to reflect these changes.

## [2.5.10] - 2025-07-01 - Layout Padding Update

### Changed
- Updated `.wrapper` padding in `main-layout.css` to use left/right shorthand (`padding: 0 20px;`) for improved layout consistency and clarity.

## [2.5.9] - 2025-07-01 - Audit Log Auto-Archiving & Baseline Handling

### Added
- **Audit Log Auto-Archiving**: The audit script now automatically moves all but the 5 most recent audit files (plus the baseline) into the `_archive` folder within `dev/logs/audit/` after each run. This keeps the main audit folder clean and ensures the baseline is always retained.
- **Baseline Always Retained**: The baseline audit file is never archived, even if it is not among the 5 most recent.

### Changed
- **Audit Script**: Updated `audit.mjs` to include the new auto-archiving logic and improved baseline handling.
- **Documentation**: Updated README and workflow documentation to reflect the new audit log management system.

### Technical Details
- See `dev/scripts/deploy/deploy-support/utils/audit.mjs` for the archiving logic.
- Audit logs are now managed automatically; no manual cleanup required.

## [2.5.8] - 2025-06-30 - Portfolio Tag Display Refactor & Configurability

### Changed
- Refactored portfolio build system to show only "Industry & Platform" and "Approach & Deliverables" tags (TagCategory2 and TagCategory3) on all portfolio cards (Index, Up Next, Tag Pages), excluding "My Role" (TagCategory1).
- Tag display logic now uses a single configuration: `TAGS_PER_CARD` (number of tags per card) and `TAG_CATEGORIES_ON_CARDS` (which tag categories are shown).
- Tag display is now easily configurable from the top of the build script (`06-build-portfolio.mjs`).
- Updated documentation to describe new tag display rules and configuration options.
- All portfolio card types (main index, Up Next, tag pages) now use the same tag filtering and truncation logic for consistency.

### Technical Details
- See `dev/scripts/deploy/deploy-support/scripts/06-build-portfolio.mjs` for tag display configuration and logic.
- See `dev/docs/features/2025-06-30-portfolio-tag-spacer/2025-06-30-portfolio-tag-spacer-readme.md` for feature documentation.

## [2.5.7] - 2025-06-30 - Documentation Unification & Naming Cleanup

### Changed
- Unified all feature documentation to use the `date-topic-readme.md` naming convention for clarity and searchability.
- Merged all prompt instructions into a single canonical `.github/prompts/prompt.prompt.md` file; removed `.copilot/prompt.md`.
- Added redirect notices to legacy doc filenames and deleted obsolete files.
- Cleaned up and organized all feature folders, removing legacy and duplicate documentation.

### Technical Details
- See `dev/docs/features/` for new doc structure and naming.
- See `.github/prompts/prompt.prompt.md` for the unified prompt file.

## [2.5.6] - 2025-06-30 - Automated "+ More" Tag Spacer & Color System Finalization

### Added
- Automated insertion of `<span class="portfolio-tag-spacer"></span>` before the "+ More" tag in portfolio card HTML via the build script, ensuring consistent tag row layout across all cards.
- Finalized color system refactor: all color usage now centralized with CSS variables, legacy/duplicate color values and documentation removed.
- Emoji system and build/preview quick links documented in `.github/prompts/prompt.prompt.md`.

### Changed
- Refactored CSS/HTML/SVGs to use new color variables and opacity variants.
- Updated `.card--tags` CSS for 3-line support and improved "+ More" tag visibility and placement.
- Improved zoomable image overlay color and blur for better accessibility and visual consistency.

### Fixed
- UI/UX issues with tag row consistency and "+ More" tag placement.
- Removed unused assets and duplicate documentation.

### Technical Details
- See `dev/scripts/deploy/deploy-support/scripts/06-build-portfolio.mjs` for spacer automation logic.
- See `dev/docs/features/2025-06-27-color-system/` for color system documentation.

## [2.5.5] - 2025-06-25 - Tag Index & Portfolio Page Visual Consistency, Mobile-First, and Preview Automation

### Changed
- **Visual Consistency**: Tag index, tag pages, and portfolio index now share a unified, mobile-first design
  - Page backgrounds are offwhite (`--offwhite`), cards are white with subtle shadow
  - Tag index grid and tag/portfolio pages are visually consistent across all breakpoints
- **Mobile-First CSS**: Tag index and tag/portfolio pages use mobile-first grid and card layouts
- **Preview Automation**: Added one-liner and npm script for building and previewing any page with a single command
  - Example: `npm run build && PAGE=/portfolio/tags/your-tag-slug/ npm run preview:page`
- **Build System**: Updated build script to ensure all generated pages use the new styles

### Fixed
- **Body Background**: Forced offwhite background for `.portfolio-index` and `.portfolio-tag-page` to override global styles
- **Card Styling**: Ensured all `.card` elements are white with consistent border radius and shadow

### Technical Details
- Updated `page-portfolio.css` for backgrounds and card styles
- Updated build script to ensure generated tag index and tag pages use correct classes and structure
- Improved documentation in README for preview automation

## [2.5.4] - 2025-06-24 - Video Optimization Script Improvements

### Fixed
- **Video Optimization Script File Detection**: Fixed critical bug where "file not found" errors occurred for valid video files
  - Root cause: `while read` loop from `find` command was corrupted by `ffmpeg` execution in `optimize_video()` function
  - Solution: Changed to collect all file paths into array first, then process them separately
  - Eliminated spurious red "Error: [filename] (file not found)" messages for existing files
  - Script now processes all videos correctly without false errors

### Changed
- **Error Message Classification**: Updated "file not found" messages to display in red instead of yellow
  - File not found is now treated as an error that shouldn't be missed rather than a warning
  - Maintains yellow for informational skips (already small files)
  - Improved color coding: red for actual errors, yellow for informational messages

### Technical Details
- **Robust File Processing**: Replaced stream-based `while read` loop with array-based approach
- **Process Isolation**: Separated file discovery from video processing to prevent I/O corruption
- **Better Error Handling**: More reliable detection of actual missing files vs. processing artifacts

## [2.5.3] - 2025-06-24 - Video Performance Optimization Complete ✅

### Changed
- **Video loading performance**: Added intelligent preloading when videos enter viewport ✅
- **Progress indication**: Progress bar now shows real buffering progress instead of simulated ✅
- **Loading reliability**: Multiple fallback event listeners for better video loading detection ✅
- **Overlay preloading**: Changed from "metadata" to "auto" preload for faster overlay video startup ✅
- **User testing result**: Videos now load "really fast" ✅

### Added
- **Intersection Observer**: Videos preload metadata when entering viewport (-200px margin) ✅
- **Progressive loading**: Videos >70% visible preload full data after 1-second delay ✅
- **Video optimization script**: `/bin/optimize-videos.sh` for compressing existing videos ✅
- **Real-time progress**: Progress bar reflects actual video buffering state ✅

### Video Compression Results - IMPLEMENTED ✅
Successfully optimized portfolio videos with 50-84% file size reductions:
- **notion-asset-flex-process.mp4**: 4.1M → 696K (83% reduction)
- **component-database-demo.mp4**: 5.8M → 952K (84% reduction)
- **vip-prototype.mp4**: 4.1M → 2.0M (51% reduction)
- **mikmak-video-responsiveness-animation-mobile-figma.mp4**: 3.1M → 484K (84% reduction)
- **mikmak-responsiveness-breakpoint-documentation.mp4**: 12M → 3.0M (75% reduction)

### Performance Achievements
- **Loading speed**: Combined preloading + compression = videos now load "really fast"
- **File sizes**: Most videos now under 1MB (was 3-21MB)
- **Backup safety**: All originals preserved in backup-originals/ directory
- **Build integration**: Optimization script ready for future video processing

## [2.5.2] - 2025-06-24 - Improved Zoomable Image Loading Experience

### Added
- **Comfortable Loading Animation for Zoomable Images**: Replaced potentially dizzying blur effect with user-friendly grayblue placeholder
  - First zoom shows a solid grayblue (`--grayblue`) placeholder in the exact shape of the original image
  - Smooth fade-in transition (0.5s) from placeholder to high-resolution image
  - Subsequent zooms use simple "Loading..." text with faster fade-in (0.4s)
  - No motion effects or blur animations that could cause dizziness or discomfort
- **Enhanced Support for Transparent Images**: Added background fill for images with transparency
  - Offwhite (`--offwhite`) background with 4px border radius and subtle drop shadow
  - Ensures transparent PNGs (logos, icons, graphics) are clearly visible against dark overlay
  - Consistent styling with design system colors and placeholder appearance
- **Increased Zoom Padding**: Expanded padding around zoomed images from 40px to 80px for better visual breathing room

### Changed
- **Loading Animation Approach**: Moved from stepped blur reduction to solid color placeholder for better user experience
- **Design System Integration**: Loading states now use CSS variables (`--grayblue`, `--offwhite`) for consistency

## [2.5.1] - 2025-06-24 - Safari Layout and Image Rendering Fixes

### Added
- **Zoom-Optimized Image Variants**: Implemented Sharp-compressed zoom images for significantly better performance
  - Added creation of `{basename}-zoom.png` variants in image processing pipeline (`01-process-images-git.mjs`)
  - Zoom variants are full-size but compressed with Sharp (quality: 95, compressionLevel: 6)
  - Updated `zoomable-image.js` to use zoom-optimized variants instead of original uncompressed files
  - Implemented fallback chain: zoom variant → original PNG → current displayed image
  - Typical file size reduction of ~60-70% for zoom images while maintaining high visual quality
  - Missing zoom variant detection in build pipeline for self-healing builds

### Fixed
- **Safari "Up Next" Cards Layout Issue**: Fixed critical Safari-specific bug where portfolio cards in the "Up Next" section loaded too narrow on initial page load
  - Cards would only resize correctly after hover or page refresh, indicating layout timing issue
  - Implemented simple but effective fix in `safari-layout-fix.js` that forces complete layout recalculation
  - Solution waits for window load, then temporarily hides/shows the container to trigger Safari's layout engine
  - Safari-only targeting prevents unnecessary processing in other browsers
  - Thoroughly tested across multiple Safari versions and devices
- **Safari Zoomable Image Centering**: Resolved issues with image zoom functionality where centering was broken after zoom operations
  - Updated `zoomable-image.js` to reset transforms before applying new zoom transforms
  - Improved centering calculations to work reliably with Safari's WebKit engine
  - Fixed image aliasing issues that occurred after zooming in and out
  - Now uses zoom-optimized images for better performance and reduced bandwidth usage
- **Documentation Updates**: Added comprehensive Safari compatibility section to design system documentation
  - Documents browser-specific issues and solutions for future reference
  - Establishes testing requirements for Safari-specific fixes
  - Provides implementation details for maintenance and future improvements

### Development Process
- **Iterative Problem Solving**: Systematically tested multiple approaches to find robust, simple solution
- **Build Pipeline Integration**: Ensured all fixes are properly included in build output and preview server
- **Cross-Browser Compatibility**: Verified that Safari fixes don't negatively impact other browsers

## [2.5.0] - 2025-06-22 - Automatic Image Dimensions & Image System Improvements

### Added
- **Automatic Image Dimension Injection System**: Revolutionary improvement to developer experience and performance
  - Build system now automatically reads image metadata using Sharp and injects width/height attributes
  - Seamlessly integrated into existing responsive image transformation pipeline
  - Prevents cumulative layout shift (CLS) issues while eliminating manual measurement work
  - Smart injection logic only adds dimensions if not already present
  - Comprehensive error handling continues processing even if dimension reading fails
- **Source HTML Cleanup Automation**: Specialized scripts for comprehensive image attribute management
  - Created `remove-manual-dimensions.mjs` script to clean up existing source files (270 attributes removed from 18 files)
  - Created `standardize-image-attributes.mjs` script to remove redundant attributes (21 total: 16 crossorigin, 5 decoding)
  - Provides detailed reporting of files modified and attributes removed
  - Ensures clean, maintainable source HTML across entire portfolio
- **Image Attribute Standardization**: Build pipeline now handles all image attributes automatically
  - Featured images get `loading="eager"`, `fetchpriority="high"`, `decoding="async"`
  - Content images get `loading="lazy"`, `decoding="async"`
  - Removes unnecessary `crossorigin` attributes for local images
  - Centralizes attribute management in build system rather than source files

### Fixed
- **Zoomable Image Resolution**: Fixed critical bug where zoomable images loaded low-resolution variants instead of full-resolution originals
  - Root cause: Nested `<picture>` elements created by improper responsive transformation
  - Enhanced responsive transformation logic to properly handle existing picture elements
  - Updated `getLargestImage()` function in zoomable-image.js to correctly detect original vs variant images
  - Zoomable images now consistently load full-resolution versions for better user experience
- **Picture Element Structure**: Eliminated invalid HTML structure with nested picture elements
  - Fixed responsive transformation creating `<picture><picture>` nested structures
  - Enhanced logic detects existing picture wrapper and adds sources appropriately
  - Results in valid, semantic HTML structure
- **Build Script Error**: Fixed missing `compare-audits.mjs` error by updating build scripts to use the unified `audit.mjs` instead
  - Updated `build.mjs` and `swift-build.mjs` to call `audit.mjs --compare 3` instead of the deprecated `compare-audits.mjs --last=3`
  - Eliminates "Cannot find module" error that appeared in build logs
  - Maintains full audit comparison functionality through the unified audit system
- **Image Rendering**: Removed global `img` CSS rules from `feature-zoom.css` that were causing aliasing issues on regular (non-zoomable) images, especially on the portfolio index page. Image rendering improvements are now scoped only to zoomable images.
- **Zoomable Images**: Reverted zoom detection logic in favor of upscaling source images for better zoom quality and simpler code.

### Changed
- **Insert Section Template Updated**: Template system now generates clean HTML without redundant attributes
  - Removed hardcoded dimensions and manual attribute specifications
  - Templates now generate only essential attributes (`data-responsive="true"`, basic loading)
  - Build pipeline handles all additional attributes automatically
  - Improved developer workflow for adding new content sections
- **Developer Workflow Simplified**: Streamlined image addition and maintenance process
  - Images now require only `src`, `alt`, and `data-responsive="true"` attributes in source
  - Build system handles all dimension injection and attribute management automatically
  - No more manual measurement, dimension entry, or attribute duplication required
  - Consistent behavior across all portfolio pages and content types
  - Future-proof system that adapts as build pipeline capabilities expand

### Fixed
- **270 Manual Dimension Attributes Removed**: Cleaned up source HTML across entire portfolio
  - Removed redundant manual dimensions from 18 portfolio HTML files
  - Source files now use clean, semantic HTML without hardcoded dimensions
  - Automatic system ensures accurate dimensions without human error
  - Improved maintainability and reduced code complexity

### Technical Details
- **Build Pipeline Integration**: Dimension injection added to `05-transform-responsive-images.mjs`
  - Uses Sharp library to read image metadata during responsive transformation
  - Automatically injects dimensions for 144+ images across portfolio
  - Maintains existing responsive image generation and optimization
  - Provides clear logging of dimension injection for transparency

**Build Output Example:**
```
📐 Auto-injected dimensions: 1880x1000 for featured--cover.png
📐 Auto-injected dimensions: 4804x2486 for breakpoints.png
✅ Transformed 144 responsive images in 17 files
```

## [2.4.0] - 2025-01-07 - Layout Consistency & Cross-Browser Improvements

### Added
- **Semantic CSS Spacing System**: Converted spacing from `px` to `rem` units for better accessibility and scalability
  - Text elements (paragraphs, lists, headings) use rem-based margins for consistent, accessible spacing
  - Major sections maintain proper visual hierarchy with standardized spacing
  - Improved accessibility for users who adjust default font sizes
- **Safari-Specific Layout Fixes**: Added targeted CSS to resolve Safari rendering issues
  - Fixed "Up Next" project card sizing problems on initial page load
  - Added Safari-specific width constraints for proper card display
  - Improved cross-browser layout consistency
- **Enhanced Footer Responsiveness**: Improved footer behavior on small screens
  - Footer links break into two lines on mobile for better readability
  - Optimized spacing and layout for touch interfaces
  - Maintained accessibility and visual hierarchy

### Changed
- **Layout Container Architecture**: Refactored wrapper system for cleaner, more maintainable structure
  - `.wrapper--wide` and `.wrapper` now serve as full-width background containers only
  - Content constraints handled by inner containers for better separation of concerns
  - Removed redundant and conflicting width rules from child elements
  - Improved CSS organization and reduced specificity conflicts
- **Content Spacing Strategy**: Replaced grid-gap with semantic margin rules
  - Removed `grid-gap` from `.content-wrapper` for more precise control
  - Added specific margin rules for text elements, images, and major sections
  - Better visual rhythm and more predictable spacing behavior
  - Easier maintenance and customization of spacing patterns
- **Home Page Layout**: Specialized responsive behavior for homepage
  - Added responsive rules for `.wrapper--home` with different max-width at large breakpoints
  - Optimized homepage layout for better content presentation
  - Maintained consistency with portfolio page layouts

### Fixed
- **iOS Safari Footer Links**: Resolved persistent footer link color issues on iOS devices
  - Added `!important` declarations and `-webkit-text-fill-color` for proper color rendering
  - Forced iOS Safari to respect intended link colors
  - Improved consistency across all iOS browsers
- **Content Wrapper Spacing**: Eliminated inconsistent spacing between sections
  - Standardized spacing for images, headings, lists, and blockquotes within content areas
  - Replaced manual `<br />` tags with semantic CSS spacing
  - Better visual hierarchy and more maintainable code
- **Next Project Container**: Fixed layout and spacing issues in project navigation
  - Added proper margin and max-width constraints
  - Improved alignment with overall page layout
  - Better visual integration with content sections

## [2.3.0] - 2025-06-21 - Layout Width Consistency & Padding Fixes

### Fixed
- **Layout Width Consistency**: Fixed width inconsistency between Summary and Challenges sections across all breakpoints
  - Simplified container width strategy: only parent containers (`.wrapper`, `.wrapper--wide`) control width
  - Removed conflicting max-width constraints from child containers (`.piece--summary`, `.content-wrapper`)
  - Added consistent 20px padding to both wrapper containers at all screen sizes
  - Updated responsive rules to apply identical width constraints to both parent containers
  - Achieved perfect alignment between Summary and main content sections on mobile, tablet, and desktop
  - Eliminated fluid stretching behavior in favor of consistent, structured padding

## [Unreleased] - 2025-07-01
### Changed
- Updated `.wrapper` padding in `main-layout.css` to use left/right shorthand (`padding: 0 20px;`) for improved layout consistency and clarity.

### Added
- **Dynamic Company Logo Injection System**: Automated company logo injection for portfolio pages
  - `<!-- BUILD_INSERT id="company-logo" -->` placeholder replaces manual logo HTML
  - Automatic company detection from portfolio file paths (e.g., `/portfolio/mikmak/project/`)
  - Company name mapping with fallback capitalization for new companies
  - Logo file validation with graceful fallback if SVG doesn't exist
  - Generates proper company tag page links (`/portfolio/tags/{company}/`)
  - Integrated into build pipeline step #3 before tag injection
  - Comprehensive coverage: main headers, "Up Next" cards, tag pages, and portfolio index
  - Extensible design ready for new companies with minimal setup

### Changed
- **Portfolio Build Pipeline**: Added company logo injection as step #3 in build process
- **Company Detection**: Standardized company name mapping across all build functions
- **Create-New Script Template**: Updated to use `BUILD_INSERT id="company-logo"` placeholder
  - Removed obsolete manual logo HTML generation from template
  - Simplified company configuration (removed logoAlt property)
  - Template now leverages build-time logo injection system
- **Tag Display Logic**: Unified tag truncation logic across all card types
  - "Up Next" cards and tag page cards now use same 5-tag limit as main cards
  - Replaced character-based truncation with consistent tag count approach
  - CSS handles visual 2-line truncation with flexbox and overflow
  - Improved consistency and maintainability across portfolio display
- **CSS Optimization**: Cleaned up duplicate and conflicting styles
  - Removed duplicate `.content img[src$=".svg"]` styles from `main-layout.css`
  - Consolidated image styles in `main-components.css` for better organization
  - Improved CSS maintainability and reduced style conflicts
- **Image Display Refinement**: Enhanced content image behavior
  - Updated `.content img` to use full-width display with aspect-ratio preservation
  - Removed `max-width` constraints for better responsive behavior
  - Improved image presentation in content sections

### Fixed
- **Tag Page Category Headers**: Fixed bug where all tag pages showed "My Role" as category
  - Preserved original category field in tag map generation
  - Each tag page now displays correct category (Company, Platform, My Role, etc.)
- **Company Logo Links**: Added pointer cursor and hover effects for better UX
  - Company logos now properly indicate they are clickable
  - Enhanced visual feedback for logo link interactions

## [2.2.0] - 2025-06-20 - Unified Audit Workflow & Build System Streamlining

### Added
- **Unified Audit Script**: Single `audit.mjs` script handles all audit functionality with build integration
- **Smart Audit Workflow**: Automatically compares recent audits and provides intelligent recommendations
- **Build Integration**: Optional `--build` and `--build-full` flags to run builds before auditing
- **Enhanced Audit Output**: Improved comparison tables with better formatting and visual clarity
- **Baseline Management**: Comprehensive baseline update system with confirmation prompts

### Changed
- **Streamlined Menu System**: Updated interactive menu to use unified audit commands
- **Consolidated Scripts**: Merged all audit-related functionality into single script
- **Improved Output Format**:
  - Comparison table columns always in order: Baseline, Previous, Current
  - 12-hour time format with AM/PM
  - Images displayed as `Images 1710 (189)` (build count with source count in parentheses)
  - "Current" column highlighted in blue for better visibility
  - Increased column spacing for readability
  - Minimal final output: only "Build & Audit Complete!" for build+audit workflows
  - Suppressed empty "Recommendations" sections when no recommendations exist

### Removed
- **Legacy Audit Scripts**: Deleted redundant `quick-build-audit.mjs` and other duplicate audit scripts
- **Unnecessary Output**: Removed verbose "Everything looks good!" messages and empty recommendation headers
- **Menu Complexity**: Simplified utilities menu by removing redundant build+audit options

### Fixed
- **Menu Integration**: Fixed menu references to use new unified audit script commands
- **Build Workflow**: Ensured proper integration between build and audit phases
- **Error Handling**: Improved error messages and graceful failure handling

### Technical Details
- **Single Source of Truth**: `audit.mjs` now handles audit generation, comparison, baseline management, and optional building
- **Command Structure**:
  - `node audit.mjs` - Smart audit with recommendations
  - `node audit.mjs --build` - Build + smart audit (most common workflow)
  - `node audit.mjs --build-full` - Full build + smart audit
  - `node audit.mjs --compare [N]` - Compare last N audits
  - `node audit.mjs --update-baseline` - Update audit baseline
- **Enhanced CLI**: Comprehensive help system and flexible option parsing
- **Maintained Compatibility**: All existing npm scripts and workflows continue to work

### Impact
- **Simplified Daily Workflow**: Single command for most common build+audit use cases
- **Reduced Complexity**: Eliminated duplicate scripts and confusing menu options
- **Better User Experience**: Clear, minimal output with actionable recommendations
- **Maintainable Codebase**: Consolidated audit logic in single, well-documented script

## [2.1.4] - 2025-06-19 - Tag Categorization Logic Fix

### Fixed
- **Hardcoded Tag Categorization Removed**: Eliminated hardcoded tag arrays that were overriding natural HTML-based categorization
- **Company Tag Placement**: Fixed company names (Dataxu, Logmein, Mikmak) appearing in "My Role:" section instead of dedicated "Company:" section
- **Duplicate Company Section**: Removed duplicate "Company Tags" section in tag index page
- **Natural Tag Categorization Restored**: Tags now properly use their original category from HTML parsing (TagCategory1, TagCategory2, TagCategory3)

### Root Cause Analysis
- **Hardcoded Override Problem**: The `getTagCategory` function was using predefined arrays to re-categorize tags, overriding the correct categorization already parsed from HTML
- **Missing Company Category**: Company tags were being created without a proper `category` property, defaulting to TagCategory1
- **Template Duplication**: Tag index template had duplicate Company sections

### Technical Changes
- **Removed `getTagCategory` Function**: Eliminated hardcoded tag categorization logic
- **Preserved Natural Categories**: Tags now use their `category` property from HTML parsing
- **Added Company Category**: Company tags now properly assigned `category: 'Company'`
- **Fixed Template**: Removed duplicate Company section from tag index HTML template

### Impact
- **Maintainable System**: Tag categorization now based on HTML structure, not hardcoded lists
- **Flexible Architecture**: Easy to add new tags without modifying build scripts
- **Clean Organization**: Proper separation of roles, platforms, approaches, and companies
- **Source of Truth**: HTML files are now the single source of truth for tag categorization

## [2.1.3] - 2025-06-19 - Portfolio Tag Page Generation Fix

### Fixed
- **Critical Tag Page Generation Bug**: Resolved major issue where all 32 tag pages were generated empty without portfolio cards
- **Double Colon Header Fix**: Fixed tag page headers displaying "My Role::" instead of "My Role:"
- **Source Directory Data Collection**: Fixed build script to extract tag data from source files instead of processed build files
- **Path Processing Correction**: Corrected company name extraction and image path generation in portfolio metadata
- **Template Placeholder Matching**: Fixed regex pattern matching for card insertion in tag page templates

### Root Cause Analysis
- **Build vs Source Directory Confusion**: The build script was reading from processed build files instead of source HTML files for tag extraction
- **Lost Tag Information**: Processed build files had already been transformed and no longer contained the raw tag category markers (TagCategory1:, TagCategory2:, etc.)
- **Template Processing Issue**: When fixing the double colon bug, the card insertion logic wasn't properly replacing the placeholder comment
- **Path Resolution Errors**: Metadata extraction was getting confused between source and build directory paths

### Technical Changes
- **Build Script Enhancement**: Updated `collectPortfolioData()` function in `dev/scripts/deploy/deploy-support/scripts/06-build-portfolio.mjs`
- **Source Directory Reading**: Modified data collection to read from `PUBLIC_HTML_DIR` (source) instead of `BUILD_DIR` for tag extraction
- **Path Processing Fix**: Corrected path resolution to properly extract company names and image paths from source file paths
- **Template Placeholder Fix**: Ensured tag page template placeholder exactly matches the replacement regex pattern
- **Debug Logging Added**: Added comprehensive logging to track tag parsing and data collection process

### Testing & Validation
- **All Tag Pages Verified**: Confirmed all 32 tag pages now display relevant portfolio cards
- **Header Display Fixed**: Verified tag page headers show correct format ("My Role:", "Platform:", "Audience:")
- **Card Content Validation**: Checked that portfolio cards show proper company logos, tags, and "+more" indicators
- **Data Integrity Check**: Confirmed `portfolio-items.json` contains correct tag data for all projects

### Impact
- **Full Tag System Functionality**: Portfolio tag browsing system now works as designed
- **Enhanced User Experience**: Visitors can browse portfolio items by any tag category
- **Content Discoverability**: Portfolio projects are now properly categorized and accessible via tag navigation
- **Build System Reliability**: Fixed fundamental data collection issue that affected tag generation

### Files Modified
- **Primary Build Script**: `dev/scripts/deploy/deploy-support/scripts/06-build-portfolio.mjs` - Updated data collection and path processing logic
- **Tag Page Template**: Verified placeholder comment formatting for proper card insertion
- **Documentation**: Updated CHANGELOG.md and README.md to reflect system improvements

### Completion
This fix fully restores the portfolio tag system functionality, ensuring all tag pages display relevant portfolio cards and the browsing experience works as intended. The tag system is now complete and fully operational.

## [2.1.2] - 2025-06-19 - Portfolio Tag Consolidation System Fix

### Fixed
- **Critical Tag Consolidation Bug**: Resolved major issue where Platform and Audience tags would break/disappear when tag content exceeded character limits
- **Unlimited Tag Content Support**: All tag categories (Role, Platform, Audience) now support unlimited content length without layout issues
- **Robust Consolidation Logic**: Replaced fragile single regex with robust approach that handles any tag content length

### Root Cause Analysis
- **Restrictive Regex Pattern**: The consolidation regex in `06-build-portfolio.mjs` used `[^<]*` patterns that couldn't handle long tag content
- **Character Limit Failures**: Platform and Audience tags would fail consolidation when content exceeded internal regex limits
- **Role Category Exception**: Role tags worked because they were processed differently in the parsing pipeline

### Technical Changes
- **Build Script Enhancement**: Updated tag consolidation logic in `dev/scripts/deploy/deploy-support/scripts/06-build-portfolio.mjs`
- **Separate Pattern Matching**: Replaced single complex regex with individual pattern matching for each category:
  - `const rolePattern = /(<p[^>]*>\s*<strong>Role:<\/strong>[\s\S]*?<\/p>)/`
  - `const platformPattern = /(<p[^>]*>\s*<strong>Platform:<\/strong>[\s\S]*?<\/p>)/`
  - `const audiencePattern = /(<p[^>]*>\s*<strong>Audience:<\/strong>[\s\S]*?<\/p>)/`
- **Robust Processing**: New approach extracts content without HTML tags and creates consolidated paragraphs with line breaks
- **Universal Fix**: Solution works for any tag content length across all categories

### Testing & Validation
- **Extensive Testing**: Verified with very long Platform and Audience tag lists including complex content
- **Build System Integrity**: All portfolio pages, tag links, and index generation continue working correctly
- **Performance**: No impact on build performance - fix only affects tag consolidation step

### Impact
- **Content Flexibility**: Portfolio projects can now use extensive, detailed tag content without breaking
- **Enhanced Categorization**: New tag categorization plan can be fully implemented without technical limitations
- **Future-Proof**: Build system now handles any tag content length reliably
- **Developer Experience**: No more mysterious tag disappearances when content grows

### Files Modified
- **Primary Build Script**: `dev/scripts/deploy/deploy-support/scripts/06-build-portfolio.mjs` - Updated `injectTagsIntoHtml()` function with robust consolidation logic
- **Documentation**: Updated CHANGELOG.md and README.md to reflect technical improvements

### Completion
This fix enables Phase 2 of the portfolio tag restructuring plan, allowing safe implementation of tag category label changes (`Role:` → `Expertise:`, `Platform:` → `Channel:`, `Audience:` → `Industry:`) with confidence that the build system can handle any tag content length.

## [2.1.1] - 2025-06-17 - Added Public Repository Sync to Menu

### Added
- **Sync Public Repo**: Added automated sync option to utilities menu for updating public repository
- **Directory Handling**: Sync command properly changes directories and pushes to GitHub automatically

### Enhanced
- **Workflow Integration**: Public repository maintenance now accessible through main menu system
- **Automated Process**: One-click sync, sanitization, commit, and push to GitHub

## [2.1.0] - 2025-06-17 - Complete Menu System Overhaul

### Major Changes
- **Complete Menu Redesign**: Overhauled entire menu system for optimal daily workflow
- **Workflow Optimization**: Reordered menu items based on frequency of use and logical workflow
- **Performance Focus**: Primary build option now uses fastest Swift Build variant (~18 seconds)

### Enhanced
- **Streamlined Interface**: Removed redundant language, hyphens, and unnecessary parenthetical descriptions
- **Logical Organization**: Build → Insert Section → Start Server → New Page → Deploy → Utilities → Exit
- **Exit After Commands**: Menu now exits after running commands instead of forcing return to menu
- **Promoted Insert Section**: Moved from utilities to main menu for easier content editing access

### Added
- **Start Server Option**: Replaces redundant Preview with focused server-only functionality
- **Utilities Reorganization**: Advanced build options and tools moved to dedicated submenu
- **VS Code Workspace**: Added workspace configuration for automatic terminal directory setting

### Removed
- **Menu Redundancy**: Eliminated repetitive descriptions ("Deploy — Deploy...", "Preview — Preview...")
- **Unnecessary Build Options**: Consolidated multiple build variants into focused main option
- **Forced Menu Returns**: No longer loops back to menu after command execution

### Technical Details
- **Script Cleanup**: Archived legacy image processing scripts with documentation
- **Build Manager Update**: Updated to reference correct git-based image processing script
- **Menu Logic Simplification**: Removed complex subtext formatting in favor of clean names

### Menu Structure (Final)
**Main Menu**: Build, Insert Section, Start Server, New Page, Deploy, Utilities, Exit
**Utilities Menu**: Full Build, Swift Build with Audit, Scrape Site, Back to Main Menu

### Developer Experience
- **Faster Iteration**: Primary workflow (Build) completes in ~18 seconds with preview
- **Content Editing**: Insert Section readily available for quick HTML updates
- **Server Management**: Start Server option for viewing existing builds without processing
- **Clean Interface**: Minimal, focused menu options without visual clutter

## [2.0.4] - 2025-06-17 - Final Menu Optimization

### Changed
- **Replaced Preview with Start Server**: Removed redundant "Preview" option since "Build" already includes preview
- **Streamlined Workflow**: "Start Server" now serves existing builds without processing (faster iteration)
- **Eliminated Redundancy**: Build does full processing + preview, Start Server just serves existing build

### Menu Structure (Final)
- **Main Menu**: Build, Insert Section, Start Server, New Page, Deploy, Utilities, Exit
- **Utilities Menu**: Full Build, Swift Build (with audit), Scrape Site

## [2.0.3] - 2025-06-17 - Final Menu Polish and Reordering

### Changed
- **Menu Order Optimization**: Reordered menu for optimal workflow: Build → Insert Section → Preview → New Page → Deploy
- **Promoted Insert Section**: Moved from utilities to main menu for easier access
- **Renamed Menu Items**: "New Piece" → "New Page" for clarity
- **Visual Cleanup**: Removed hyphens, used parentheses for subtexts for cleaner appearance

### Enhanced
- **Workflow Priority**: Most common actions (Build, Insert Section) now at top of menu
- **Language Simplification**: Reduced verbose descriptions while maintaining clarity
- **Utilities Menu**: Streamlined to focus on advanced build options and tools

### Menu Structure
- **Main Menu**: Build, Insert Section, Preview, New Page, Deploy, Utilities, Exit
- **Utilities Menu**: Full Build, Swift Build (with audit), Scrape Site Content

## [2.0.2] - 2025-06-17 - Menu Cleanup and UX Improvements

### Changed
- **Streamlined Main Menu**: Simplified from 7 to 5 main options for better focus
- **Menu Behavior**: Menu now exits after running commands instead of returning to main menu
- **Language Cleanup**: Removed redundant descriptions and improved clarity

### Enhanced
- **Primary Build Option**: Main "Build" now uses the fastest Swift Build option (git-based, no audit)
- **Utilities Organization**: Moved Full Build and Swift Build (with audit) to utilities menu
- **Description Clarity**: Improved menu item descriptions to be more concise and informative

### Removed
- **Menu Redundancy**: Eliminated repetitive language in menu options
- **Unnecessary Menu Returns**: No longer forces user back to menu after command completion

### Menu Structure
- **Main Menu**: Utilities, New Piece, Build (Swift Fast), Preview, Deploy, Exit
- **Utilities Menu**: Full Build, Swift Build (with audit), Insert Section, Scrape Site Content

## [2.0.1] - 2025-06-17 - Script Cleanup and Archive Organization

### Changed
- **Script Organization**: Archived legacy image processing scripts to maintain clean active directory
- **Build Manager Update**: Updated build manager to reference the correct git-based image processing script

### Added
- **Archive Documentation**: Created comprehensive README.md documenting archived script versions and migration history
- **Version Naming**: Renamed archived scripts with descriptive version identifiers

### Removed
- **Legacy Scripts**: Moved `01-process-images.mjs` (v1.2.0 timestamp-based) and `01-process-images-simple.mjs` (v1.0.0 simple git) to archive
- **Script Redundancy**: Eliminated multiple image processing script versions in active directory

### Technical Details
- **Active Script**: Only `01-process-images-git.mjs` (v2.0.0) remains as the production image processing solution
- **Archive Location**: Legacy scripts stored in `_archive/scripts/image-processing-versions/` with documentation
- **Build System**: No disruption to current Swift Build functionality

## [2.0.0] - 2025-01-18 - Swift Build System with Git-Based Image Processing

### Major Changes
- **Git-Based Image Processing**: Completely rewritten image processing pipeline using git to detect changed images instead of unreliable timestamp/size comparisons
- **Smart Build System**: New "Swift Build" mode that only processes changed images, dramatically reducing build times
- **Self-Healing Pipeline**: Automatic detection and regeneration of missing image outputs without manual intervention

### Added
- **New Git-Based Image Detection**: Created `01-process-images-git.mjs` script that detects uncommitted, staged, and committed image changes
- **Fast Build Option**: Added `build:swift:fast` npm script that skips the site audit for maximum speed
- **Build Menu Updates**: Updated build menu with clear options for Full Build, Swift Build, and Swift Build (Fast)
- **Force Processing Mode**: Added `--force-all` flag to process all images regardless of git status

### Enhanced
- **Backup/Restore Safety**: Fixed backup logic to prevent overwriting current source images with old backups
- **Build Performance**: Swift builds now complete in ~18 seconds vs several minutes for full builds
- **Developer Experience**: Simplified build process with intelligent defaults and clear menu options
- **Documentation**: Comprehensive README updates explaining the new build system and workflow

### Fixed
- **Image Change Detection**: Eliminated false positives from timestamp-based detection
- **Missing Image Variants**: Self-healing logic ensures all responsive image variants are generated
- **Build Reliability**: Git-based detection provides deterministic, repeatable builds

### Technical Details
- **Git Integration**: Uses `git diff` and `git status` for reliable change detection
- **Process Optimization**: Only processes images that have actually changed since last commit
- **Output Validation**: Checks for missing processed images and regenerates them automatically
- **Menu Consistency**: Updated both main menu and utilities menu to reflect new options

## [1.4.8] - 2025-06-16 - Fixed "Up Next" Card Sequential Ordering

### Fixed
- **"Up Next" Card Ordering**: Fixed sequential ordering of "Up Next" cards to match portfolio index page order
- **Data Consistency**: Ensured "Up Next" navigation follows the same sort logic as portfolio index (MikMak → LogMeIn → DataXu, alphabetical within each company)
- **Build Script Synchronization**: Updated `createNextProjectMap` function in all three build script locations to use consistent sorting

### Technical Details
- **Sort Logic Applied**: Applied company-first (MikMak, LogMeIn, DataXu), then alphabetical sorting to next project mapping
- **Multiple Location Fix**: Updated sorting in `/dev/scripts/`, `/portfolio-build/build-system/scripts/`, and `/portfolio-build/build-system/deploy/` locations
- **Data Flow Consistency**: Ensured "Up Next" cards now progress sequentially through portfolio in intended order

## [1.4.7] - 2025-06-15 - Portfolio Tag Enhancements & "Up Next" Card Improvements

### Added
- **"Up Next" Card Tags**: Added portfolio tags to "Up Next" cards at the bottom of individual portfolio pages
- **Smart "+More" Indicator**: Added "+X more" indicator that specifically counts remaining Role tags when truncated
- **Extra Small Typography**: Added `0.75rem` font size for portfolio tags to fit more content in limited space

### Enhanced
- **Improved Tag Fitting**: Reduced portfolio tag font size from `0.875rem` to `0.75rem` for better space utilization
- **Intelligent Tag Truncation**: Updated character estimation from 25 to 30 characters per line due to smaller font
- **Context-Aware Spacing**: Fixed tag spacing to work correctly in both card containers (using gap) and inline contexts (using margin)

### Fixed
- **Next Project Data**: Fixed missing tag data in "Up Next" cards by including tags in the next project mapping
- **Tag Category Parsing**: Added proper category field to parsed tags for accurate Role tag filtering
- **Spacing Consistency**: Resolved spacing issues between tags in different contexts (cards vs inline)

### Technical Details
- **Build Script Enhancement**: Updated `createNextProjectMap` to include tag data for "Up Next" cards
- **Category-Specific Logic**: "+More" indicator only counts remaining Role tags, not Platform/Audience tags
- **CSS Optimization**: Separate margin handling for card-based vs inline portfolio tags
- **Design System Update**: Documented new extra small text size (0.75rem) in design system

## [1.4.6] - 2025-06-15 - Portfolio Card Layout & Safari Grid Fixes

### Fixed
- **Safari Grid Layout Issues**: Resolved text/image overlap on portfolio cards by switching from CSS Grid to Flexbox
- **2-Row Tag Rendering**: Fixed Safari-specific rendering issues when portfolio tags wrap to 2 lines
- **Card Height Consistency**: Ensured all portfolio cards maintain consistent heights with title truncation and tag limitation

### Enhanced
- **Card Layout Stability**: Replaced complex grid-based layout with predictable flexbox approach for portfolio cards
- **Tag Spacing**: Removed unnecessary left margin from portfolio tags to prevent indented appearance
- **Cross-Browser Compatibility**: Improved rendering consistency across Safari, Chrome, and Firefox

### Technical Details
- **Layout Approach**: Changed from `grid-template-rows: 1fr auto` to `flex-direction: column` with explicit ordering
- **Content Constraints**: Maintained 3-line title truncation and 2-row tag limitation for consistent card heights
- **CSS Simplification**: Removed complex min-height calculations in favor of natural content flow

## [1.4.5] - 2025-06-14 - Portfolio Tag Styling Unification & Safari Fixes

### Enhanced
- **Unified Portfolio Tag Styling**: Standardized tag appearance across all contexts (homepage cards, individual portfolio pages, tag listing pages)
- **Consistent Padding & Spacing**: Applied uniform `padding: 3px 6px` and `line-height` values across all portfolio tag locations
- **Improved Mobile Experience**: Fixed tag overlap issues on smaller screens with proper line-height adjustments

### Fixed
- **Safari Layout Bug**: Resolved text overlapping images on portfolio cards during initial page load
- **CSS Cascade Issues**: Fixed line-height conflicts where global styles were overriding portfolio tag styles
- **Responsive Consistency**: Ensured tags maintain proper spacing and sizing across all device sizes

### Technical Details
- **CSS Optimization**: Simplified portfolio tag selectors while maintaining visual consistency
- **Safari-Specific Fixes**: Added hardware acceleration and layout recalculation triggers for Safari
- **Line-Height Standardization**: Applied `line-height: 2` to portfolio page descriptions for better readability
- **Cross-Browser Compatibility**: Enhanced rendering across Safari, Chrome, and Firefox

## [1.4.4] - 2025-06-12 - Portfolio Animation and Spacing Enhancements

### Added
- **One-time Portfolio Animation**: Added session-based staggered animation control that plays only once per browser session
- **Performance Optimization**: Prevents the staggered animation from replaying when returning to portfolio page after viewing projects
- **Cross-browser Support**: Ensured animation compatibility with Safari and other browsers

### Fixed
- **Tag Space Consistency**: Added CSS margin to properly space category labels from portfolio tags
- **Layout Uniformity**: Ensured consistent spacing across all portfolio pages through CSS margin rules

### Technical Details
- **Implementation**: Uses sessionStorage to track if animation has played
- **Script Added**: Added portfolio-session.js to manage animation state
- **CSS Enhanced**: Updated main-components.css with improved label spacing rules
- **User Experience**: Maintains the hover effect on cards while preventing repetitive animations

## [1.4.3] - 2025-06-12 - CSS Design System Consolidation

### Added
- **Design System Documentation**: Created comprehensive `design-system.md` documenting typography scale, spacing, and component systems
- **Systematic Font-Size Scale**: Established consistent rem-based typography hierarchy from 0.875rem to 6rem
- **Enhanced About Page**: Added 2-column layout with icons for lab projects (Focus Timer, DailyNote, Tracker)
- **Contact Section Spacing**: Improved contact section layout with proper grouping and visual separation

### Changed
- **Font-Size Consolidation**: Reduced ~50 font-size instances to systematic scale
  - Standardized small text to single `0.875rem` value (was 0.75rem, 0.85rem, 0.87em, 14px)
  - Converted display text from `em` to `rem` units (3em→3rem, 3.7em→3.7rem, etc.)
  - Removed redundant `1rem` declarations leveraging inheritance from body
- **Line-Height Optimization**: Consolidated from 12+ instances to 3 meaningful values
  - Base `1.2` applied to body (inherited by most elements)
  - Tight `0.75` for impactful headlines
  - Spaced `2` for portfolio tags (better click targets)
- **Unit Standardization**:
  - Line-height values converted to unitless (CSS best practice)
  - Font-size primarily `rem` with strategic `px` for pixel-perfect needs
  - Mixed 24px/14px values converted to appropriate rem equivalents

### Improved
- **CSS Architecture**: More maintainable and consistent codebase
- **Performance**: Reduced CSS complexity and redundancy
- **Accessibility**: Consistent relative sizing allows better user control
- **Developer Experience**: Clear patterns established for future component additions

### Technical Details
- **Files Modified**: 8 CSS files updated with systematic consolidations
- **Lab Projects**: Added flex-based layout with SVG icons and proper spacing
- **Responsive Design**: Maintained all responsive scaling while improving consistency
- **Documentation**: Comprehensive design system documentation for future reference

## [1.4.2] - 2025-06-12 - Portfolio Tag Styling Unified

### Added
- **Consistent Font Sizing**: Individual portfolio page tags now use 0.875rem font-size to match homepage portfolio cards exactly
- **Improved Line Spacing**: Enhanced vertical spacing between tag categories (Role, Platform, Audience) for better readability
- **Clean Tag Presentation**: Removed comma separators between tags for cleaner, more modern appearance

### Changed
- **Build System Enhancement**: Modified tag injection logic to generate space-separated clickable tags instead of comma-separated format
- **CSS Architecture**: Consolidated portfolio tag styling in `main-components.css` for consistent application across all page types
- **Tag Spacing Logic**: Replaced ineffective line-height approach with block-level margin spacing for better cross-browser compatibility

### Fixed
- **Tag Overlap Issue**: Resolved overlapping tags caused by insufficient line spacing in individual portfolio pages
- **Font Size Inconsistency**: Eliminated discrepancy between portfolio card tags (0.875rem) and individual page tags (1rem)
- **Visual Coherence**: Achieved perfect styling match between homepage cards and individual project pages

### Technical Details
- **Modified Files**:
  - `public_html/styles/main-components.css` - Updated portfolio tag component styles with unified font sizing and spacing
  - `dev/scripts/deploy/deploy-support/scripts/06-build-portfolio.mjs` - Changed tag separator from `', '` to `' '` in `injectTagsIntoHtml()` function
- **CSS Improvements**:
  - Set `font-size: 0.875rem` and `line-height: 1.2` for all portfolio tags
  - Added `display: block` with `margin: 0.5rem 0` for proper `<br>` tag spacing
  - Enhanced specificity to ensure consistent styling across all contexts
- **Build Integration**: Portfolio tag changes automatically apply during swift builds, maintaining development efficiency

### Impact
- **User Experience**: Portfolio tags now have consistent, professional appearance across all pages
- **Visual Consistency**: Eliminated styling discrepancies between different portfolio page types
- **Readability**: Improved spacing and removed visual clutter from comma separators
- **Development Workflow**: Changes integrate seamlessly with existing swift build process

## [1.4.1] - 2025-06-11 - Portfolio Card Duplication Fix

### Fixed
- **Duplicate Portfolio Cards**: Resolved critical issue where 3 duplicate cards were appearing after the 16th card on the main portfolio index page
- **Incorrect Project Count**: Fixed portfolio build system incorrectly processing 19 projects instead of the expected 16 legitimate portfolio projects
- **Tag Page Interference**: Eliminated issue where company tag pages (`dataxu`, `logmein`, `mikmak`) from the `/tags/` directory were being treated as actual portfolio projects

### Root Cause Analysis
- **Metadata Collection Logic**: The portfolio build system was scanning ALL directories within the portfolio folder, including the `/tags/` subdirectory
- **Directory Processing Bug**: Build script's `fs.readdirSync()` loop processed every directory without filtering, causing tag pages to be included in project metadata
- **Cascading Effect**: Each incorrectly included tag page generated a duplicate portfolio card without proper project metadata or tags

### Technical Changes
- **Build Script Modification**: Updated portfolio data collection logic in both build script locations:
  - Primary: `/dev/scripts/deploy/deploy-support/scripts/06-build-portfolio.mjs`
  - Backup: `/portfolio-build/build-system/deploy/deploy-support/scripts/06-build-portfolio.mjs`
- **Directory Filter**: Changed condition from `if (dirent.isDirectory())` to `if (dirent.isDirectory() && dirent.name !== 'tags')`
- **Selective Processing**: Build system now explicitly excludes the `tags` directory from portfolio project collection while preserving all tag functionality

### Verification
- ✅ Portfolio build now correctly processes exactly 16 portfolio projects
- ✅ No duplicate cards appear on portfolio index page
- ✅ All tag pages continue to function properly (25 tag pages generated)
- ✅ Next-project navigation works correctly (16 sections generated)
- ✅ Build process runs cleanly without errors

### Impact
- **User Experience**: Portfolio page now displays clean, non-duplicated project cards
- **Build Performance**: Slightly improved build performance by processing fewer unnecessary directories
- **Data Integrity**: Portfolio metadata collection is now accurate and reliable
- **Maintainability**: Fix prevents similar issues if additional subdirectories are added to portfolio structure in the future

## [1.4.0] - 2025-06-06 - Portfolio Build System Migration to Public Repository

### Added
- **Public Repository Created**: Successfully migrated portfolio build system to public GitHub repository at `https://github.com/dreisdesign/portfolio-build`
- **Build System Isolation**: Created separate git repository (`build-system-repo/`) within private repo for clean migration management
- **Comprehensive Documentation**: Added detailed setup guides, technical documentation, and configuration examples for public use
- **Security Sanitization**: All sensitive information (credentials, domains, personal paths) replaced with configurable placeholder variables
- **Example Implementation**: Included sample portfolio structure demonstrating build system capabilities
- **Automated Sync Tools**: Created scripts for ongoing synchronization between private and public repositories

### Changed
- **Build System Structure**: Reorganized build pipeline for public distribution while maintaining private repo functionality
- **Configuration Management**: Converted hardcoded values to environment-based configuration system
- **Documentation Approach**: Split documentation between private (workflow-specific) and public (setup/technical) content

### Technical
- **Git Subtree Integration**: Used git subtree approach for seamless build system synchronization
- **Sanitization Pipeline**: Automated replacement of sensitive patterns across 31+ build system files
- **Repository Structure**: Created organized public repo with `/build-system/`, `/docs/`, `/config/`, `/example/`, and `/scripts/` directories
- **Migration Validation**: Verified no sensitive information exposed in public repository
- **Version Control**: Maintained clean git history and professional commit messaging for public release

### Security
- **Information Sanitization**: All deployment credentials, server paths, and personal identifiers safely anonymized
- **Environment Variables**: Converted sensitive configurations to `{{PLACEHOLDER}}` format for user customization
- **Safe Distribution**: Public build system ready for community use without security concerns

## [1.3.3] - 2025-06-06 - Portfolio Tag Index Categorization

### Added
- **Categorized Tag Index Page**: Completely reorganized the portfolio tag index page with logical category groupings
  - **Company First**: Company tags now appear first (MikMak, LogMeIn, DataXu) - most relevant for portfolio browsing
  - **Audience Second**: Target market tags (B2B SaaS, B2C, Internal Tool) for understanding project context
  - **Platform Third**: Technical platform tags (WebApp, Mobile, Desktop, Responsive) for filtering by implementation
  - **Role Last**: Professional role tags (18 total) including Design Systems, Research, Visual Design, etc.
  - **Descriptive Sections**: Each category includes helpful descriptions explaining what types of tags are included
  - **Improved Navigation**: Users can now quickly find tags by semantic meaning rather than alphabetical order
  - **Maintained Functionality**: All tag links, project counts, and existing styling preserved

### Changed
- **Tag Index Organization**: Reversed category order from Role → Platform → Audience → Company to Company → Audience → Platform → Role
- **Enhanced User Experience**: Portfolio browsing now starts with the most relevant organizational categories (company and audience)
- **Better Content Hierarchy**: Categories are ordered by user decision-making priority when exploring portfolio work

### Technical
- **Build Script Update**: Modified `generateTagIndexPage()` function in `06-build-portfolio.mjs`
- **Category Reordering**: Updated section generation order while maintaining all existing functionality
- **Template Structure**: Preserved existing HTML structure and CSS classes for consistent styling

## [1.3.2] - 2025-06-06 - Critical Bug Fixes & Source Cleanup

### Fixed
- **"All Tags" Link Hover Effect**: Fixed hover background to only apply to text width instead of full div width
  - Changed `.tag-index-link` from `display: block` to `display: inline-block` in `page-portfolio.css`
  - Resolved issue where hover effect extended across entire container width
- **Tag Categorization System**: Updated default tag category from "Other" to "Role"
  - Modified `getTagCategory()` function in `06-build-portfolio.mjs` to return `'Role'` as default
  - Ensures consistent tag categorization across portfolio projects
- **Major Source Contamination Cleanup**: Resolved critical build artifact contamination in source directory
  - **Removed 1,508+ Responsive Images**: Deleted all responsive image variants (`-320w`, `-640w`, `-960w`, `-1200w`, `-1800w` suffixes) from source
  - **Removed Generated WebP Files**: Cleaned up auto-generated WebP files from `/assets/images/` (kept legitimate video WebP files)
  - **Removed Inappropriate Directories**: Deleted `/portfolio/tags` directories from all asset types in source
  - **Removed Misplaced HTML File**: Deleted `/assets/images/portfolio/mikmak/vip-user-testing/community/index.html` with wrong content
  - **Source Directory Integrity**: Restored clean source/build separation - only 25 legitimate WebP video files remain

### Technical Notes
- Build artifacts should only exist in build directory, not source
- Responsive images and WebP conversions are generated during build process
- Source directory now contains only original, unprocessed assets
- This cleanup prevents future build conflicts and maintains proper version control

### To Be Verified
- **CSS Width Constraints**: Verify implementation of `.next-project-container .wrapper { max-width: none; }` CSS rule for proper next-project container layout

## [1.3.1] - 2025-06-05 - Portfolio Styling Fixes

### Fixed
- **Portfolio Tag Link Color Consistency**: Enhanced CSS specificity to ensure all portfolio tag links use consistent dark blue color
  - Added comprehensive selectors for all link states (`:link`, `:visited`, `:active`) with `!important` declarations
  - Fixed color persistence issues across different contexts (card details, tag pages, portfolio index)
- **"All Tags" Link Styling**: Updated `.tag-index-link` to display as block-level element with H2-equivalent styling
  - Added `display: block`, `font-weight: 700`, `font-size: 1rem`, `margin-top: 0.5rem` to match page hierarchy
- **Portfolio Header Layout**: Removed problematic `margin-bottom: -2rem` from portfolio page header styles
  - Fixed spacing issues that were affecting all portfolio pages inappropriately
- **CSS Version Management**: Bumped page-portfolio.css to version 2025-06-05-v6

### Changed
- **Documentation Updates**: Updated README.md and CHANGELOG.md to reflect completion of portfolio styling fixes

### Changed
- **Documentation Updates**: Updated README.md and CHANGELOG.md to reflect the completed state of the portfolio tagging system implementation
  - **README Current Status**: Updated status section to show all major components completed as of June 5, 2025
  - **CSS Layout Documentation**: Added comprehensive CSS Layout System section documenting wrapper system, responsive breakpoints, and next-project container behavior
  - **Project Completion**: Marked version 1.3.0 as complete with full portfolio tagging system implementation
  - **Verification Notes**: Added notes about CSS width constraint verification for next-project containers

## [1.3.0] - 2025-06-05 - Portfolio Tagging System Complete

### Added
- **Comprehensive Portfolio Tagging System Implementation**: Complete overhaul and standardization of the portfolio tagging system
  - **Three-Category Tag Structure**: Implemented standardized tag categories (Role, Platform, Audience) across all 16 portfolio projects
  - **Role Tags**: Define professional responsibilities and activities (e.g., "Design Systems", "Interaction Design & Prototyping", "Research", "Visual Design")
  - **Platform Tags**: Specify target platforms and device types (e.g., "WebApp", "Mobile", "Desktop", "Responsive")
  - **Audience Tags**: Identify target market and business model (e.g., "B2B SaaS", "B2C", "Enterprise", "Internal Tool")
  - **Company Tags**: Automatically extracted from project folder structure and added as clickable tags
  - **Enhanced Build System**: Updated `parseAllTagsFromHtml()` function to support multi-category tag parsing instead of role-only tags
  - **Advanced Tag Injection**: Enhanced `injectTagsIntoHtml()` to process all three tag categories with proper formatting and spacing
  - **Responsive Grid Layout**: Implemented portfolio tag page responsive grid system that applies only to tag pages
  - **Tag Page Template Updates**: Updated tag listing template with proper `portfolio-tag-page` body class for responsive grid targeting
  - **CSS Grid System**: Added responsive 2-column (900px+) and 3-column (1100px+) grid layouts specifically for portfolio tag pages
  - **Grid Layout Fix**: Added `main .cards .card { grid-column: auto; }` CSS rule at 768px breakpoint to resolve card layout issues
- **Portfolio Project Tag Standardization**: Updated all 16 portfolio projects with standardized three-category tagging
  - **DataXu Projects (7)**: Blog Subscription, Community, Contact, Marketing CMS, Product OneView, Rebrand, Summit Microsites
  - **LogMeIn Projects (3)**: Central Flow, New GoToMeeting, Responsive
  - **MikMak Projects (6)**: Acquisition Rebrand, Colgate Search UX Kit, Custom Report Builder, Platform Asset Flexibility, Responsive Commerce Template, VIP User Testing
  - **Consistent Tag Format**: All projects now use standardized `<strong>Category:</strong> Tag1, Tag2` format with line breaks between categories
  - **Reduced Tag Redundancy**: Eliminated duplicate and ambiguous tags (e.g., "UX/UI Design" vs. "UI and UX Design")
  - **Enhanced Discoverability**: Improved tag consistency makes portfolio projects more discoverable and organized
- **Documentation and Project Completion**: Comprehensive documentation updates and project archival
  - **CHANGELOG Updates**: Added detailed documentation of all tagging system implementation work
  - **README Updates**: Enhanced portfolio tagging documentation with responsive grid system details
  - **Project Archival**: Moved completed planning documents (`portfolio-tags-comprehensive-plan.md`, `portfolio-tag-mapping-2025-06-03.md`) to `_archive` directory
  - **Build System Verification**: Confirmed all 52 pages build successfully with 1,819 optimized images and 25 processed videos
  - **Tagging System Validation**: Verified tag parsing, clickable link generation, and responsive grid layouts function correctly across all portfolio pages

### Changed
- **CSS Version Update**: Updated all CSS file version numbers to 2025-06-04-v14 reflecting responsive grid system improvements
- **Build System Enhancement**: Enhanced portfolio build script to support comprehensive three-category tag parsing instead of role-only parsing
- **Master Tag Index Page**: Comprehensive directory page at `/portfolio/tags/` listing all available portfolio tags
  - **Complete Tag Directory**: Displays all portfolio tags alphabetically with project counts for each tag
  - **Project Count Display**: Shows how many projects use each tag (e.g., "Research (8 projects)", "Design (5 projects)")
  - **Clickable Navigation**: Each tag in the index links directly to its dedicated tag page
  - **Portfolio Template Integration**: Uses the same header, navigation, role formatting, and footer structure as other portfolio pages
  - **SEO Optimized**: Includes proper meta descriptions ("Browse Dan Reis's UX design portfolio by tags and skills...") and page titles
  - **Browse Integration**: Features the same "Browse by:" tag link format used throughout the portfolio section
  - **Build Pipeline Integration**: Tag index generation is fully integrated into the main build process as Step 7
- **Portfolio Tagging System**: Complete tagging and categorization system for portfolio projects
  - **Automatic Tag Parsing**: Portfolio pages can now include role tags using `<strong>Role:</strong> Tag1, Tag2, Tag3` format
  - **Clickable Tag Links**: Role tags are automatically converted to clickable links that navigate to dedicated tag pages
  - **Dynamic Tag Pages**: Individual tag pages are automatically generated for each unique tag, showing all portfolio items with that tag
  - **Consistent Card Layout**: Tag pages use the same responsive card layout as the main portfolio index page
  - **URL-Friendly Slugs**: Tags are converted to SEO-friendly URLs (e.g., "UX/UI Design" becomes `/portfolio/tags/uxui-design/`)
  - **Build Integration**: Tag parsing, link injection, and page generation are fully integrated into the main build pipeline
  - **Template Support**: Tag page template can be customized via `tag-listing-template.html` with automatic fallback generation
- **Enhanced Portfolio Build Process**: Extended `06-build-portfolio.mjs` with comprehensive tagging functionality
  - Tag parsing from portfolio HTML content with intelligent slug generation
  - Automatic injection of clickable tag links into existing portfolio pages
  - Dynamic generation of individual tag listing pages with full responsive design
  - Smart template handling with both external template support and inline fallback generation
  - Comprehensive error handling and logging for tag processing workflows
  - Master tag index page generation with alphabetical sorting and project count aggregation
