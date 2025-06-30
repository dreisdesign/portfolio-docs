# Portfolio System: Table of Contents & Authoring Guide

**Updated: June 30, 2025**

## Overview
This project is a modern, maintainable UX portfolio system for Dan Reis. It features a robust build pipeline with git-based change detection, comprehensive portfolio tagging system, automated navigation and head injection, dynamic company logo injection, automatic image dimension injection, pixel-perfect zoomable image functionality, a simplified authoring workflow for carousels and content, and a fully automated tag row layout (including '+ More' tag spacer logic).

### Current Status (June 30, 2025)
- ✅ **Color System Finalized**: All color usage is now centralized and modernized with CSS variables. Legacy/duplicate color values and documentation removed.
- ✅ **Automated '+ More' Tag Placement**: '+ More' tag placement is now fully automated in the build system for consistent tag row layout.
- ✅ **Emoji System & Quick Links**: Emoji system and build/preview quick links are documented for contributors in `.github/prompts/prompt.prompt.md`.
- ✅ **Feature Docs Organized**: All feature, audit, and idea docs are organized in a dated feature folder structure.
- ✅ **UI/UX Improvements**: Zoomable image overlays and tag/card layout improvements are complete

### Latest (June 30, 2025)
- ✅ **Automatic Image Dimension Injection**: Revolutionary improvement to developer experience and performance
  - Build system automatically reads image metadata using Sharp and injects width/height attributes
  - 270 manual dimension attributes removed from source HTML files for cleaner, more maintainable code
  - Prevents cumulative layout shift (CLS) issues while eliminating manual measurement work
  - Integrated seamlessly into existing responsive image transformation pipeline
  - Updated insert-section template to generate clean HTML without manual dimensions
  - Source HTML now requires only `data-responsive="true"` - dimensions handled automatically
- ✅ **Source HTML Cleanup**: Completely automated dimension removal across entire portfolio
  - Created specialized script to remove all manual width/height attributes from source files
  - 144 images now processed automatically during build with proper dimension injection
  - Developer workflow simplified: just add images with alt text and data-responsive attribute
  - Build pipeline validates successful dimension injection and continues processing
  - Template system updated to generate clean, dimension-free HTML
- ✅ **Tag Index & Portfolio Visual Consistency**: Tag index, tag pages, and portfolio index now share a unified, mobile-first design
  - Offwhite page backgrounds, white cards with subtle shadow, and consistent grid/card layout
  - Tag index grid and tag/portfolio pages are visually consistent across all breakpoints
- ✅ **Mobile-First CSS**: Tag index and tag/portfolio pages use mobile-first grid and card layouts
- ✅ **Preview Automation**: One-liner and npm script for building and previewing any page
  - Example: `npm run build && PAGE=/portfolio/tags/your-tag-slug/ npm run preview:page`
- ✅ **Body Background Fix**: Forced offwhite background for `.portfolio-index` and `.portfolio-tag-page` to override global styles
- ✅ **Card Styling**: All `.card` elements are white with consistent border radius and shadow
- ✅ **Color Variable System**: All colors in the portfolio system are now managed using CSS custom properties (variables) for maximum maintainability and theme flexibility
  - Centralized color definitions in `public_html/styles/_variables.css`
  - Example usage: `background: var(--color-primary);`

### Previous Updates (January 7, 2025)
- ✅ **Complete Layout & Spacing Overhaul**: Achieved perfect consistency across all portfolio pages
  - Refactored wrapper container architecture for cleaner, more maintainable CSS structure
  - Implemented semantic spacing system using rem units for better accessibility
  - Standardized content spacing with margin-based approach replacing grid-gap
  - Added proper spacing rules for images, headings, lists, blockquotes, and section breaks
- ✅ **Safari & iOS Compatibility**: Fixed all browser-specific layout and rendering issues
  - Resolved Safari "Up Next" card sizing problems on initial page load
  - Fixed persistent iOS Safari footer link color issues with forced rendering
  - Added Safari-specific CSS for consistent cross-browser behavior
- ✅ **Enhanced Responsive Design**: Improved layout behavior across all screen sizes
  - Specialized homepage responsive rules for optimal content presentation
  - Enhanced footer responsiveness with improved mobile layout
  - Better touch interface optimization for small screens
- ✅ **Code Quality & Maintainability**: Cleaned up CSS architecture and removed redundancies
  - Eliminated conflicting width rules and simplified container responsibilities
  - Converted manual spacing breaks to semantic CSS for better code maintenance
  - Improved CSS organization with better separation of concerns

### Previous Updates (June 21, 2025)
- ✅ **Layout Width Consistency Fixed**: Resolved width inconsistency between Summary and Challenges sections
  - Simplified container width strategy for cleaner, more maintainable CSS
  - Consistent 20px padding across all screen sizes for structured, professional appearance
  - Perfect alignment achieved across mobile, tablet, and desktop breakpoints
  - Eliminated conflicting nested container width rules
- ✅ **Dynamic Company Logo Injection**: Automated company logo system replaces manual HTML
  - `<!-- BUILD_INSERT id="company-logo" -->` placeholder automatically detects company from file path
  - Works across all areas: main headers, "Up Next" cards, tag pages, portfolio index
  - Extensible design ready for new companies with minimal setup (just add SVG logo file)
  - Integrated into build pipeline with logo validation and graceful fallbacks
- ✅ **Tag Categorization Fixed**: Resolved issue where tags were miscategorized due to hardcoded categorization overriding HTML-based parsing
- ✅ **Company Tags Organized**: Company names now properly appear in dedicated "Company:" section instead of "My Role:"
- ✅ **Build System Simplified**: Removed hardcoded tag arrays in favor of natural HTML-based categorization for better maintainability
- ✅ **Tag System Complete**: Full implementation of 3-category portfolio tagging (Role, Platform, Audience) + Company
- ✅ **Tag Index Categorization**: Portfolio tag index organized by logical categories (Company → Audience → Platform → Role)
- ✅ **Merged to Main**: Tag system successfully integrated and deployed
- ✅ **Portfolio Styling Complete**: All tag link colors, "All Tags" styling, and header layout issues resolved and deployed
- ✅ **Critical Bug Fixes Complete**: "All Tags" hover effect and tag categorization fixes deployed (v1.3.2)
- ✅ **Source Contamination Resolved**: Removed 1,500+ build artifacts from source directory - clean source/build separation restored
- ✅ **Public Build System Released**: Portfolio build system successfully migrated to public GitHub repository (v1.4.0)
- ✅ **Swift Build V2.0**: Ultra-fast git-based change detection with self-healing image processing
- ✅ **Portfolio Tag Styling Unified**: Individual portfolio pages now match homepage card styling exactly - consistent font size (0.875rem), spacing, and transparent background with subtle borders. Removed commas between tags for cleaner presentation.
- ✅ **"Up Next" Sequential Ordering**: Fixed "Up Next" card ordering to follow portfolio index sequence (MikMak → LogMeIn → DataXu, alphabetical within companies)
- ✅ **Build Performance Optimized**: ~18 second fast builds vs previous 3+ minute builds (17x faster)
- ✅ **Development Workflow Enhanced**: Edit images → immediate detection without committing changes
- ✅ **Tag Consolidation System Robust**: Fixed critical issue where Platform/Audience tags would break with long content - all categories now support unlimited tag content length
- ✅ **Tag Page Generation Fixed**: Resolved critical issue where tag pages were empty - all 32 tag pages now display relevant portfolio cards correctly

### Public Build System
The portfolio build system has been successfully migrated to a public GitHub repository for community use and contribution:

**🔗 Repository**: https://github.com/dreisdesign/portfolio-build

**Features Available Publicly**:
- Complete build pipeline with HTML validation and image processing
- Responsive image generation (WebP/AVIF support)
- Portfolio tagging and categorization system
- Development servers (BrowserSync, static file server)
- Automated deployment scripts with retry logic
- ESLint, Prettier, and EditorConfig integration
- Comprehensive documentation and examples

**Security**: All sensitive information has been sanitized and replaced with configurable placeholders. The public repository is safe for community use and contains no private credentials or personal data.

## Streamlined Audit Workflow (June 20, 2025)

**🎉 All audit functionality consolidated into a single, powerful script!**

The audit system is now dramatically simpler and more user-friendly:

- **Single Source of Truth:** All audit, comparison, and baseline update tasks are handled by `audit.mjs` (`dev/scripts/deploy/deploy-support/utils/audit.mjs`).
- **Legacy scripts removed:** All previous audit scripts (`audit-site.mjs`, `compare-audits.mjs`, `update-audit-baseline.mjs`, `smart-audit.mjs`, `quick-build-audit.mjs`) have been removed or replaced.
- **Unified menu and npm scripts:** The interactive menu and all npm scripts now use only the new unified audit system.
- **Minimal, clear output:** Audit output is concise, visually clear, and only shows recommendations if needed. Comparison tables always show Baseline → Previous → Current, with blue highlighting for the current column.
- **Easy daily use:** The most common workflow is now just:
  ```bash
  node dev/scripts/deploy/deploy-support/utils/audit.mjs --build
  # or via menu: npm run menu → Build
  ```
- **Other tasks:**
  ```bash
  node dev/scripts/deploy/deploy-support/utils/audit.mjs           # Audit only
  node dev/scripts/deploy/deploy-support/utils/audit.mjs --compare # Compare audits
  node dev/scripts/deploy/deploy-support/utils/audit.mjs --update-baseline # Update baseline
  node dev/scripts/deploy/deploy-support/utils/audit.mjs --build-full      # Full build + audit
  ```

See [dev/docs/simplified-workflow-guide.md](dev/docs/simplified-workflow-guide.md) for full documentation and migration notes.

## Table of Contents
- [Getting Started](#getting-started)
- [Streamlined Audit Workflow](#streamlined-audit-workflow-june-20-2025)
- [Public Build System](#public-build-system-structure)
- [Using the Interactive Menu](#using-the-interactive-menu)
- [Swift Build Feature](#swift-build-feature)
- [Content-Only Workflow](#content-only-workflow)
- [Adding a New Portfolio Page](#adding-a-new-portfolio-page)
- [Using the Create-New Script](#using-the-create-new-script)
- [Portfolio Tagging System](#portfolio-tagging-system)
- [CSS Layout System](#css-layout-system)
- [Content Cards](#content-cards)
- [Adding Images](#adding-images)
- [Adding Video](#adding-video)
- [Image Sharpening](#image-sharpening)
- [Using Carousels](#using-carousels)
- [Navigation & Head Injection](#navigation--head-injection)
- [Footer Injection](#footer-injection)
- [Build & Deploy](#build--deploy)
- [Technical Implementation & Build Pipeline](#technical-implementation--build-pipeline)
- [Authoring Requirements](#authoring-requirements)
- [Carousel & Video Implementation](#carousel--video-implementation)
- [Advanced Configuration](#advanced-configuration)
- [Troubleshooting](#troubleshooting)
- [Migration Notes](#migration-notes)
- [Code Formatting](#code-formatting)
- [HTML Timestamps](#html-timestamps)
- [Utilities: Insert Section Script](#utilities-insert-section-script)
- [Color Variable System](#color-variable-system-2025-06-26)

## Getting Started
- Clone the repo: `git clone https://github.com/dreisdesign/danrtzaq.git`
- Run `npm install` at the project root to install dependencies
- Run `npm run menu` to access the interactive menu system for common tasks
- See the [CHANGELOG.md](CHANGELOG.md) for detailed version history and updates
- **Note:** This project uses a `.copilot/prompt.md` file for Copilot customization. See `.copilot/prompt.md` for project-specific prompt instructions and workflow tips.

## Public Build System Structure

The build system has been separated into its own repository structure for public distribution:

### Private Repository (`/Users/danielreis/web/danrtzaq/`)
- **Source Files**: Contains all portfolio content, assets, and private configuration
- **Build System Repo**: `build-system-repo/` - Isolated copy of build system for sync purposes
- **Development Environment**: Full development setup with private deployment configuration

### Public Repository (`https://github.com/dreisdesign/portfolio-build`)
- **`/build-system/`** - Core build pipeline and deployment scripts (sanitized)
- **`/docs/`** - Setup guides, technical documentation, and tutorials
- **`/config/`** - Configuration templates and examples with placeholder variables
- **`/example/`** - Sample portfolio implementation demonstrating system capabilities
- **`/scripts/`** - Maintenance and synchronization utilities
- **`/templates/`** - Reusable templates for new projects

### Synchronization Workflow
1. **Development**: Work in private repository with full access to build system
2. **Updates**: Use `sync-from-private.sh` script to update public repository
3. **Sanitization**: Automated replacement of sensitive information with placeholders
4. **Distribution**: Public repository provides clean, secure build system for community use

### Key Benefits
- **Security**: No sensitive credentials or personal data in public repository
- **Maintenance**: Easy synchronization between private development and public distribution
- **Community**: Open source build system available for portfolio developers
- **Documentation**: Comprehensive guides for setup and customization

## Using the Interactive Menu
The easiest way to interact with this project is through the interactive menu system:

1. From any directory within the project, run:
   ```bash
   npm run menu
   ```

2. The menu provides quick access to commonly used commands with a clean, optimized interface:

   **Main Menu:**
   - **Build** - Smart build with git-based change detection (~18 seconds)
   - **Insert Section** - Add content sections to HTML files
   - **Start Server** - Launch preview server on existing build
   - **New Page** - Create a new portfolio project
   - **Deploy** - Deploy to production
   - **Utilities** - Advanced build options and tools
   - **Exit** - Exit the menu

   **Utilities Menu:**
   - **Full Build** - Complete build with full validation
   - **Swift Build with Audit** - Swift build including site audit
   - **Sync Public Repo** - Update public repository with latest changes
   - **Scrape Site** - Extract text content from live site

3. **Streamlined Workflow**: The menu exits after running commands (no forced returns to menu)

4. **Automatic Directory Handling**: Commands execute from the correct project directory regardless of where you run the menu

5. **Performance Optimized**: Primary "Build" option uses the fastest Swift Build variant for daily development

## Swift Build Feature
The Swift Build feature provides ultra-fast development iteration with intelligent git-based change detection and self-healing image processing. This dramatically reduces build times while maintaining full build pipeline functionality.

### How It Works
1. **Asset Preservation**: Backs up existing processed responsive images from previous complete build
2. **Fresh Source Copy**: Copies latest source files to build directory
3. **Asset Restoration**: Restores processed assets (replacing source assets)
4. **Smart Image Processing**: Git-based detection processes only changed images (uncommitted + committed changes)
5. **Self-Healing**: Automatically regenerates missing responsive variants if detected
6. **Full Pipeline**: Runs complete build pipeline (HTML processing, portfolio generation, etc.)
7. **Optional Audit Skip**: Fast mode skips site audit for maximum speed

### Build Options
**Swift Build (Fast) - Development:**
```bash
npm run build:swift:fast  # ~18 seconds (skips audit)
```

**Swift Build (Full) - Production:**
```bash
npm run build:swift      # ~45 seconds (includes audit)
```

**Complete Build - First Time:**
```bash
npm run build:full       # ~3 minutes (generates all assets)
```

### Git-Based Image Detection
- **Detects uncommitted changes**: Edit an image → immediate detection (no commit needed)
- **Detects staged changes**: `git add` tracked files
- **Detects committed changes**: Between HEAD~1 and HEAD
- **Force all images**: `npm run process:images:all` when needed

### Usage
**Via Interactive Menu:**
```bash
npm run menu
# Select "Swift Build (Fast)" for development
# Select "Swift Build" for production builds
```

### Prerequisites
- Requires a complete `npm run build:full` first to generate processed assets
- Subsequent swift builds reuse those assets while processing everything else fresh

### Perfect For
- **Development workflow**: Edit → Build → Preview in seconds
- Testing content changes
- Iterating on layout modifications
- Portfolio structure updates
- Any work where only some images change

### Performance Comparison
- **Swift Build (Fast)**: ~18 seconds (git-based image detection + skip audit)
- **Swift Build (Full)**: ~45 seconds (git-based image detection + audit)
- **Complete Build**: ~3 minutes (processes all 1,800+ responsive image variants)
- **Image Detection**: <1 second when no images changed
- **Self-Healing**: Automatically fixes missing responsive variants

## Content-Only Workflow
If you're only updating content (not modifying build scripts):

1. Make your content changes directly in this repository (`public_html` directory)
2. Build and preview your changes:
   ```bash
   npm run build
   npm run preview
   ```
3. Once satisfied, deploy directly from this repository:
   ```bash
   npm run deploy
   ```

## Adding a New Portfolio Page
1. **Option 1 (Recommended):** Use the automated `create-new.mjs` script to generate a new project (see [Using the Create-New Script](#using-the-create-new-script)).
2. **Option 2 (Manual):** Create a new folder under `public_html/portfolio/[company]/[project]/` and add an `index.html` file.
   - Use `<!-- BUILD_INSERT id="head" -->`, `<!-- BUILD_INSERT id="nav" -->`, and `<!-- BUILD_INSERT id="company-logo" -->` in your HTML for automated injection.
   - Add a `<h1>`, `<meta name="description">` , and a featured image (named `featured--cover.png`).
   - Company logos are automatically injected based on the folder path (e.g., `/portfolio/mikmak/project/` uses `company-logo--mikmak.svg`).
   - To prevent a template or example page from being processed or deployed, add the comment `<!-- TEMPLATE: DO NOT PROCESS -->` anywhere in the file.

## Using the Create-New Script
The `create-new.mjs` script automates the creation of new portfolio projects:

1. The easiest way to run the script is through the menu:
   ```bash
   npm run menu
   ```
   Then select "Create New Project" from the options.

2. Alternatively, you can run it directly:
   ```bash
   npm run create-new
   ```

3. Follow the interactive prompts:
   - Select a company (MikMak, LogMeIn, DataXu)
   - Enter a project name (will be converted to a URL-friendly slug)
   - Confirm the generated URL slug

4. The script will create:
   - A project directory at `/public_html/portfolio/[company]/[project-slug]/`
   - An `index.html` file with placeholder content and all required structural elements
   - Asset directories at:
     - `/public_html/assets/images/portfolio/[company]/[project-slug]/`
     - `/public_html/assets/videos/portfolio/[company]/[project-slug]/`
     - `/public_html/assets/documents/portfolio/[company]/[project-slug]/`
   - Placeholder files for images and videos

5. After creation, edit the generated files to add your actual project content.

6. Template and placeholder files are stored in:
   ```
   dev/scripts/deploy/deploy-support/create-new-page/templates/
   dev/scripts/deploy/deploy-support/create-new-page/placeholders/
   ```

## Company Landing Pages & Logo Navigation

- Each company in the portfolio (e.g., MikMak, LogMeIn, DataXu) now has its own landing page at `/portfolio/[company]/`.
- **Clicking the company logo** on any project page will take you to that company's landing page, showing all related projects.
- Company landing pages are generated automatically from the folder structure—no manual setup required.

## Portfolio Tagging System

The portfolio system features a comprehensive three-category tagging system that automatically generates clickable tag links and dedicated tag pages for enhanced discoverability and navigation.

### Tag Categories

The system supports four types of tags, each serving a specific organizational purpose:

#### 1. Role Tags
Define your professional responsibilities and activities on the project:
```html
<strong>Role:</strong> UX Design, Prototyping, User Research, Information Architecture
```

**Common Role Tags:**
- UX Design, UI Design, Visual Design
- Prototyping, Wireframing
- User Research, Usability Testing
- Information Architecture
- Design Systems, Component Design
- Product Strategy, Design Strategy

#### 2. Platform Tags
Specify the technical platforms and device types:
```html
<strong>Platform:</strong> WebApp, Mobile, Desktop
```

**Available Platform Tags:**
- **WebApp** - Web-based applications
- **Mobile** - Mobile applications (iOS/Android)
- **Desktop** - Desktop applications and software
- **Responsive** - Responsive web design projects

#### 3. Audience Tags
Identify the target market and business model:
```html
<strong>Audience:</strong> B2B SaaS, Enterprise
```

**Available Audience Tags:**
- **B2C** - Business-to-Consumer products
- **B2B** - Business-to-Business products
- **B2B SaaS** - Software-as-a-Service for businesses
- **Enterprise** - Large enterprise solutions
- **Consumer** - Direct consumer products
- **Internal** - Internal company tools and systems

#### 4. Company Tags (Automatic)
Company names are automatically extracted and converted to clickable tags based on the project's folder structure. No manual tagging required.

### Tag Implementation

1. **Add tags to your project's HTML** using the standardized format above
2. **Use consistent spacing** - tags are separated by line breaks (not paragraph breaks) for clean visual presentation
3. **Multiple categories** - you can include any combination of Role, Platform, and Audience tags
4. **Automatic processing** - the build system automatically:
   - Converts all tags to clickable links
   - Generates individual tag pages showing all projects with that tag
   - Creates a comprehensive tag index page
   - Extracts company names as clickable tags

### Example Implementation
```html
<div class="project-meta">
  <strong>Role:</strong> UX Design, Prototyping, User Research<br>
  <strong>Platform:</strong> WebApp, Mobile<br>
  <strong>Audience:</strong> B2B SaaS
</div>
```

### Generated Pages
The system automatically creates:
- **Individual tag pages** (e.g., `/portfolio/tags/ux-design/`) showing all projects with that tag
- **Tag index page** (`/portfolio/tags/`) listing all available tags across all categories
- **Company pages** showing all projects for each company

### Categorized Tag Index
The main tag index page (`/portfolio/tags/`) organizes all portfolio tags into logical categories for improved navigation:

1. **Company Tags** (First) - Projects organized by company (MikMak, LogMeIn, DataXu)
   - Most relevant for portfolio browsing and career timeline understanding
   - Automatically extracted from project folder structure

2. **Audience Tags** (Second) - Target market and business model categories
   - B2B SaaS, B2C, Internal Tool
   - Helps visitors understand project context and business impact

3. **Platform Tags** (Third) - Technical platforms and device types
   - WebApp, Mobile, Desktop, Responsive
   - Useful for filtering by technical implementation interests

4. **Role Tags** (Fourth) - Professional responsibilities and activities
   - 18 comprehensive role tags including Design Systems, Research, Visual Design
   - Detailed breakdown of skills and contributions across projects

Each category includes:
- **Descriptive Headers**: Clear explanations of what each category represents
- **Project Counts**: Shows how many projects use each tag (e.g., "Design Systems (6 projects)")
- **Clickable Navigation**: Direct links to individual tag pages
- **Consistent Styling**: Maintains portfolio page design system and responsive behavior

### Best Practices
- Use consistent tag names across projects for better organization
- Choose the most specific and accurate tags for each project
- Include tags from multiple categories when relevant
- Company tags are handled automatically - no manual setup needed

**Automated '+ More' Tag Spacer:**
The build system now automatically inserts `<span class="portfolio-tag-spacer"></span>` before the '+ More' tag in each portfolio card, ensuring it always appears on the third row for consistent layout. No manual editing is required—this is handled entirely by the build pipeline.

## CSS Layout System

The portfolio system uses a sophisticated CSS layout system with responsive width constraints to ensure optimal readability and visual hierarchy across all devices.

### Wrapper System
The site uses a centralized wrapper system for content width management:

- **Base Max-Width**: Content is constrained to `max-width: 650px` for optimal readability on smaller screens
- **Responsive Expansion**: At 1244px+ screen width, content expands to `max-width: 960px` for better use of available space
- **Universal Application**: The `.wrapper` class applies these constraints consistently across all pages

### Next-Project Containers
Portfolio pages feature "next project" navigation sections that may require special width handling:

- **Standard Behavior**: Next-project containers inherit the wrapper width constraints by default
- **Full-Width Option**: If needed, next-project containers can be styled with `max-width: none` to break out of the wrapper constraints
- **Build Integration**: Next-project sections are automatically generated by the build system as static HTML

### CSS Files Structure
The layout system is organized across multiple CSS files:

- **`main-layout.css`**: Contains base wrapper styles and fundamental layout rules
- **`main-responsiveness.css`**: Handles responsive breakpoints and width adjustments
- **`page-portfolio.css`**: Portfolio-specific layout overrides and enhancements
- **`main.css`**: Central import file that coordinates all CSS modules

### Verification Notes
As of June 5, 2025, the CSS width constraint system should be verified to ensure next-project containers display properly across all screen sizes. The rule `.next-project-container .wrapper { max-width: none; }` may need to be implemented if next-project sections appear too narrow on larger screens.

## Content Cards
- Content cards are used to highlight key information, images, or videos in a visually distinct way.
- Use the following structure for a content card:

```html
<section class="content">
  <picture>
    <img src="/assets/images/portfolio/[company]/[project]/[image].png" alt="Descriptive alt text" width="1200" height="648" loading="lazy" data-responsive="true" />
  </picture>
  <p class="content-caption">
    <b>Card Title:</b> Brief description or context for the card content.
  </p>
</section>
```
- You can also use `.video-wrapper` inside a content card for video highlights.

## Adding Images
- Place images in `/assets/images/portfolio/[company]/[project]/`.
- Use descriptive `alt` text for accessibility.
- Use the `data-responsive="true"` attribute for images that should be responsive.
- For featured images, use the filename `featured--cover.png` and provide all required responsive sizes (see technical guide).

## Adding Video
- To add a video to a carousel or content section, always use the `.video-wrapper` structure for overlays and poster support:

```html
<div class="video-wrapper">
  <div class="overlay"></div>
  <video class="standard-video mobile-preview" playsinline webkit-playsinline muted loop preload="none" width="100%" height="auto">
    <source src="/path/to/video.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
</div>
```
- For carousels, place the `.video-wrapper` inside a `.carousel-slide-source`.
- Posters and overlays are handled automatically by the build and JS.
- The `mobile-preview` class can be added to the `video` tag to apply specific mobile styling, which is defined in `public_html/styles/feature-video.css`.

## Image Sharpening
- All images are automatically sharpened during the build process using conservative settings.
- Sharpening is applied after resizing to ensure optimal image quality and minimize artifacts.
- Original images are also sharpened to enhance the zoom view experience.
- To manually sharpen individual images, use the standalone utility:
  ```bash
  npm run sharpen public_html/assets/images/portfolio/[company]/[project]/image.png
  ```
- Customize sharpening parameters for specific images:
  ```bash
  npm run sharpen public_html/assets/images/portfolio/[company]/[project]/image.png --sigma=1.0 --flat=1.2 --jagged=1.5
  ```
- Available parameters:
  - `--sigma`: Controls the size of the Gaussian mask (default: 0.8, range: 0.3-3.0)
  - `--flat`: Controls enhancement in flat areas (default: 1.0, range: 0.3-1.5)
  - `--jagged`: Controls enhancement along edges (default: 1.2, range: 0.7-2.0)
  - `--suffix`: Custom suffix for output filename (default: 'sharp')
  - `--overwrite`: Overwrite the original file instead of creating a new one

## Using Carousels
- Use the simplified `.carousel-source` and `.carousel-slide-source` markup in your source HTML.
- The build process will transform this into the full, production-ready carousel HTML automatically.
- **For carousel captions with bulleted lists**: Use `<div class="carousel-caption-source">` instead of `<p class="carousel-caption-source">` to ensure proper HTML nesting (HTML doesn't allow `<ul>` elements inside `<p>` tags).
- For videos, use the `.video-wrapper` structure as described above.

## Navigation & Head Injection
- Always use `<!-- BUILD_INSERT id="nav" -->` and `<!-- BUILD_INSERT id="head" -->` in your source HTML for consistent, automated injection.
- Navigation is injected before validation, so your pages will always pass validation and be included in the portfolio index.

## Footer Injection
- The standard site footer is automatically injected into every HTML file during the build process.
- You do not need to add the footer manually in your source files.
- The build script ensures only one footer is present per page, always placed immediately before </body>.

## Build & Deploy
- Run `npm run build` to build the site.
- Run `npm run deploy` to deploy to production.
- Run `npm run deploy:open` to deploy and automatically open the site in a browser.
- The build process validates, injects, transforms, and generates all required files.

### Available Build & Deploy Commands
```bash
# Full build with all optimizations
npm run build

# Build with skipping image processing (faster)
npm run build:dev

# Deploy to production
npm run deploy

# Deploy with dry run (no actual changes)
npm run deploy:dry

# Deploy and open the site in browser
npm run deploy:open

# Preview local build in browser
npm run preview

# Build + Deploy in one step
npm run preview:deploy

# Build + Deploy + Open browser in one step
npm run preview:deploy:open

# Test browser opening functionality
npm run test:browser-open
```

## Build & Preview Commands

To build and preview any page instantly:
```bash
npm run build && PAGE=/your-page-path/ npm run preview:page
```

Examples:
- Homepage: `npm run build && PAGE=/ npm run preview:page`
- Portfolio index: `npm run build && PAGE=/portfolio/ npm run preview:page`
- Specific portfolio project: `npm run build && PAGE=/portfolio/mikmak/vip-user-testing/ npm run preview:page`
- Tag page: `npm run build && PAGE=/portfolio/tags/user-research/ npm run preview:page`

The preview server will start automatically and open your page at `http://localhost:3000`.

## Recent Updates

### Visual Consistency (v1.7.0)
- **Mobile-First Design**: All portfolio pages now use consistent offwhite backgrounds with white cards
- **Unified Tag System**: Tag index, tag pages, and portfolio index share the same visual style
- **Responsive Layout**: Optimized for mobile devices with consistent spacing and typography

### Animation Fixes (v1.7.1)
- **Homepage SVG**: Fixed waving hand animation visibility issue - SVG now displays correctly from page load
- **Smooth Interactions**: Enhanced animation performance with proper CSS properties

## Technical Implementation & Build Pipeline

The build process is orchestrated by a series of scripts in `dev/scripts/deploy/deploy-support/scripts/`, run in this order:

- **00-validate-html.mjs**: Validates source HTML for required structure, metadata, and accessibility. Updates timestamps in HTML and CSS files. Should be run both before and after transformation steps.
- **01-process-images.mjs**: Processes and optimizes all images (resizing, compression, format conversion). Applies automatic sharpening with conservative parameters for enhanced clarity. Ensures images are web-optimized and responsive-ready.
- **02-create-static-placeholder.mjs**: Generates static placeholder images for use during loading or as fallbacks. Improves perceived performance and user experience.
- **03-preprocess-featured-images.mjs**: Prepares and generates all required responsive sizes for featured images (e.g., `featured--cover.png`). Ensures every portfolio project has the correct image assets for all breakpoints.
- **04-format-files.sh**: Formats HTML, CSS, and JSON files in the build directory. Minifies CSS files and injects common head elements (using `head-templates/inject-head.mjs`). Handles placeholder replacement for `<!-- BUILD_INSERT id="head" -->`.
- **05-transform-responsive-images.mjs**: Scans HTML for image tags and updates them to use responsive `srcset` and `sizes` attributes. Ensures all images are delivered in the optimal format and size for each device.
- **06-build-portfolio.mjs**: Main build coordinator for portfolio content. Processes and validates portfolio pages, transforms carousel markup, injects company logos and tags, generates portfolio index page and tag pages, and creates next-project sections. Includes comprehensive tagging system with automatic tag parsing, clickable link generation, dynamic company logo injection, and dynamic tag page creation.
- **head-templates/inject-head.mjs**: Injects common HTML head elements and portfolio-specific scripts. Handles versioning and cache-busting for assets. Called by 04-format-files.sh.

### Build Steps
1. **HTML Validation:** Validates all source HTML and updates timestamps (`00-validate-html.mjs`).
2. **Image Processing:** Optimizes and generates all required images (`01-process-images.mjs`, `02-create-static-placeholder.mjs`, `03-preprocess-featured-images.mjs`).
3. **Copy Assets:** Copies all files to the build directory (handled by your npm scripts or shell commands).
4. **Formatting & Head Injection:** Formats files, minifies CSS, and injects head elements (`04-format-files.sh`, `head-templates/inject-head.mjs`).
5. **Responsive Image Transformation:** Updates image tags for responsive delivery (`05-transform-responsive-images.mjs`).
6. **Portfolio Build:** Injects navigation, validates portfolio pages, injects company logos, parses and injects clickable tags, transforms carousels, generates portfolio index page, creates individual tag pages, and generates next-project sections (`06-build-portfolio.mjs`).
7. **Footer Injection:** Injects the standard footer before </body> if not already present (`inject-footer.mjs`).
8. **Pre-Deploy Checks:** Runs final checks before deployment (`07-pre-deploy-check.sh`).
9. **Preview Server:** Optionally start a local server to preview the build (`08-preview-server.mjs`).

## Authoring Requirements
- Use `<!-- BUILD_INSERT id="nav" -->`, `<!-- BUILD_INSERT id="head" -->`, and `<!-- BUILD_INSERT id="company-logo" -->` in all source HTML.
- Each portfolio page must have:
  - `<h1>` (project title)
  - `<meta name="description">` (project description)
  - Company logo placeholder: `<!-- BUILD_INSERT id="company-logo" -->` (replaces manual `.card--company-logo` HTML)
  - Featured image named `featured--cover.png`
  - `.next-project-container` div

### BUILD_INSERT System
The BUILD_INSERT system automatically injects content during the build process:

- **`<!-- BUILD_INSERT id="head" -->`**: Injects common head elements, CSS links, and scripts
- **`<!-- BUILD_INSERT id="nav" -->`**: Injects navigation menu with active page highlighting
- **`<!-- BUILD_INSERT id="company-logo" -->`**: Automatically injects company logo with proper links based on portfolio path
  - Detects company from file path (e.g., `/portfolio/mikmak/project/` → `mikmak`)
  - Uses logo file: `company-logo--{company}.svg`
  - Links to company tag page: `/portfolio/tags/{company}/`
  - Gracefully handles missing logos (removes placeholder)
  - Works across all areas: main headers, "Up Next" cards, tag pages, portfolio index

### Adding New Companies
To add a new company (e.g., "spotify"):

1. **Add logo file**: `/public_html/assets/images/portfolio/company-logo--spotify.svg`
2. **Optional - Add name mapping** in `06-build-portfolio.mjs`:
   ```javascript
   const COMPANY_NAME_MAP = {
     // ...existing mappings...
     'spotify': 'Spotify'
   };
   ```
3. **Update create-new script** (optional): Add to `COMPANIES` array in `create-new.mjs`

The system automatically handles the rest!
- For portfolio tagging, include tags using the three-category system: `<strong>Role:</strong> Tag1, Tag2`, `<strong>Platform:</strong> Tag1, Tag2`, and `<strong>Audience:</strong> Tag1, Tag2` formats

## Carousel & Video Implementation
- Use `.carousel-source` and `.carousel-slide-source` for carousels.
- For videos, use the `.video-wrapper` structure for overlays and poster support.

## Advanced Configuration
- To change validation rules, edit `validateHtml` and `validatePortfolioPage` in `06-build-portfolio.mjs`.
- To add new build steps, update the main build function in the same script.

## Troubleshooting
- If a page is skipped, check the build log for validation errors or missing metadata.
- Ensure navigation is injected before validation.
- **Tags Not Being Processed**: If role tags aren't being converted to clickable links:
  - Ensure tags are in the format: `<strong>Role:</strong> Tag1, Tag2, Tag3`
  - Check that the portfolio page is being processed by the build system (not skipped due to validation errors)
  - Verify the page is located in the correct portfolio directory structure
- **Tag Pages Not Generated**: If individual tag pages aren't being created:
  - Check the build log for tag page generation messages
  - Ensure at least one portfolio page has properly formatted role tags
  - Verify the build process completed the portfolio build step (`06-build-portfolio.mjs`)
- **Carousel Lists Not Showing**: If bulleted lists in carousel captions are missing from the build output:
  - Ensure carousel captions use `<div class="carousel-caption-source">` instead of `<p class="carousel-caption-source">`
  - HTML nesting rules don't allow `<ul>` elements inside `<p>` tags
  - The build script automatically processes these correctly when using `<div>` wrappers

## Migration Notes
- Legacy carousels and videos should be updated to the new markup for full compatibility.

## Code Formatting
- All HTML, CSS, and JS files are automatically formatted using [Prettier](https://prettier.io/) as part of the build process.
- The project enforces 2-space indentation for all files. This is configured in the `.prettierrc` file at the project root:

```json
{
  "tabWidth": 2,
  "useTabs": false
}
```
- You do not need to manually format files—just run the build and Prettier will handle it.

## HTML Timestamps
- All HTML files automatically receive a "Last updated" timestamp as an HTML comment at the top of the file.
- The timestamp is added during the build process by the `00-validate-html.mjs` script.
- For files with existing timestamps, the comment is updated with the current date and time.
- For files without timestamps, a new timestamp comment is automatically added:
  ```html
  <!-- Last updated: June 4, 2024, 3:45:12 PM -->
  ```
- Timestamps are placed before the DOCTYPE declaration for proper documentation.
- This feature ensures all files have accurate modification dates for maintenance purposes.
- The build process reports statistics on both updated timestamps and newly added timestamps.

## Utilities: Insert Section Script

### insert-section.mjs & insert-section.sh

This utility consists of two files that work together to provide intelligent, project-aware HTML section insertion:

- **insert-section.mjs**: The main script with project-aware functionality. Automatically detects project paths, manages assets, and generates sections with project-specific asset paths.
- **insert-section.sh**: A shell wrapper that finds the most recently modified HTML file, sets up the environment, and ensures the script runs from the correct project root.

**You should keep and use both files for the best experience.**
- Run the shell script (`insert-section.sh`) from the menu or terminal for convenience and correct environment setup.
- The shell script will always call the JS script (`insert-section.mjs`) to do the actual work.

#### Key Features
- **🎯 Project Path Detection**: Automatically extracts project path from HTML file location (e.g., `mikmak/acquisition-rebrand`)
- **📁 Smart Asset Management**: Creates project-specific directories and copies placeholder assets as needed
- **🔗 Dynamic Asset Paths**: Generated HTML uses project-specific paths like `/assets/images/portfolio/mikmak/acquisition-rebrand/placeholder-image.png`
- **💾 VS Code Integration**: Auto-save functionality and clear guidance for handling file changes
- **🚫 Duplicate Prevention**: Only creates placeholder assets if they don't already exist
- **✅ Enhanced UX**: Better error handling, confirmation prompts, and success feedback

#### How it works
- Run the script via the Utilities menu or directly.
- The script detects your project path and ensures proper asset structure exists.
- Select the target HTML file and the line number after which to insert.
- Choose one of the following section types:
  - **Image**: A content card with project-specific image path and caption.
  - **Video**: A content card with project-specific video path and caption.
  - **Carousel**: A multi-slide carousel with project-specific placeholder assets.
- The script inserts the HTML snippet with proper asset paths and handles VS Code synchronization.

#### Example usage
1. Run the menu: `npm run menu` (or use the utility script directly)
2. Choose "Insert Section (HTML)"
3. Follow the prompts to select file, line, and section type
4. Edit the inserted placeholder text as needed

---

# Changelog

## [Unreleased]
- Added `insert-section.mjs` utility: insert prebuilt Image, Video, or Carousel HTML sections into any HTML file at a specified line via an interactive menu.
- Utility supports quick prototyping and content block insertion for portfolio/case study pages.

# Batch upscaling and PNG compression utilities added to /dev/scripts/utilities/:
- `batch-upscayl.sh`: Safe batch upscaling workflow for UpScayl, with duplicate filename handling and robust restore.
- `compress-pngs.js`: Sharp-based PNG compression utility for batch testing.

All image build, upscaling, and compression scripts are now organized in the utilities directory. See script comments for usage details.

Recent improvements:
- Automatic image dimension injection in build pipeline (Sharp)
- Removal of manual width/height attributes from all source HTML
- Standardized image attributes (loading, fetchpriority, decoding)
- Improved zoomable image logic and JS for sharpness and cross-browser consistency
- Updated insert-section template for new image standards
- All image sharpening removed from build scripts
- Full build validated for correct transformation and attribute injection

## Color Variable System (2025-06-26)

All colors in the portfolio system are now managed using CSS custom properties (variables) for maximum maintainability and theme flexibility.

### Defining Colors
- **Hex Variables:**
  - Example: `--color-primary: #202f48;`
- **RGB Channel Variables:**
  - Example: `--color-primary-rgb: 32, 47, 72;`
  - Used for `rgba()` and gradients.
- **Accent Color:**
  - Example: `--color-accent-rgb: 16, 92, 215;`
  - Used for tag hover backgrounds and other accent elements.

### Usage Examples
```css
background: var(--color-primary);
background: rgba(var(--color-primary-rgb), 0.08);
background: linear-gradient(90deg, var(--color-primary), var(--color-link));
background: rgba(var(--color-accent-rgb), 0.1); /* Tag hover */
```

### Best Practices
- Always use variables for all color values (no hardcoded hex or rgb).
- Use `-rgb` variables for any `rgba()` or gradient that requires channel separation.
- Define all variables in `:root` in `main-base.css` for global access.
- Opacity should be set directly in `rgba()`, not as a variable.

### Migration Notes
- All previous hardcoded color values have been replaced with variables.
- Build scripts and templates have been updated to output CSS using these variables.
- This system enables easy theming and consistent color usage across all components.
