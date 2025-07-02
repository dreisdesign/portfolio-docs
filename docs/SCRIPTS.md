# Portfolio Build System Scripts

This document describes the main scripts and utilities that power the portfolio build system. For most users, the interactive menu (`npm run menu`) is the easiest way to access these features.

## Core Scripts

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
  - Updates image tags for responsive delivery (`srcset`, `sizes`).

- **06-build-portfolio.mjs**
  - Main build coordinator: processes portfolio pages, injects navigation, logos, tags, carousels, and generates index/tag pages.
  - **Tag index, tag pages, carousels, and "Up Next" cards are now 100% template-driven.**
    - Templates: `build-portfolio-templates/tag-index-template.html`, `build-portfolio-templates/tag-listing-template.html`, `build-portfolio-templates/carousel-template.html`, and `build-portfolio-templates/up-next-card-template.html`
    - No hardcoded HTML for these components in the script—if a template is missing, the build fails.
    - To change component layout or style, edit the template and rebuild.
    - The tag listing template is now fully aligned with the main portfolio index page in terms of stylesheet order, script placement, wrapper structure, and body class. This ensures visual and structural consistency across all portfolio pages.

- **inject-head-upper.mjs**
  - Injects the upper portion of the HTML head (essential meta tags, charset, viewport, etc.) into all HTML files at the `<!-- BUILD_INSERT id="head-upper" -->` placeholder, using the `injected-head-upper.html` template.

- **inject-head-lower.mjs**
  - Injects the lower portion of the HTML head (fonts, favicons, CSS, versioning, and portfolio scripts) into all HTML files at the `<!-- BUILD_INSERT id="head-lower" -->` placeholder, using the `injected-head-lower.html` template.
  - Handles dynamic versioning and portfolio-specific script injection.

- **inject-footer.mjs**
  - Ensures a single, correctly placed footer in every HTML file.

- **07-pre-deploy-check.sh**
  - Runs final checks before deployment.

- **08-preview-server.mjs**
  - Starts a local server for previewing the build.

## Utilities

- **audit.mjs**
  - Unified audit, comparison, and baseline update tool.
  - Usage: `node dev/scripts/deploy/deploy-support/utils/audit.mjs [options]`

- **insert-section.mjs & insert-section.sh**
  - Interactive utility for inserting prebuilt HTML sections (image, video, carousel) into any HTML file.

- **scrape-site-content.mjs**
  - Extracts text content from the live site for analysis or migration.

- **sync-public-docs.sh**
  - Syncs documentation from the private repo to the public docs repo, with security checks.

## See Also
- [BUILD-PIPELINE.md](BUILD-PIPELINE.md) for the build process overview
- [docs/](docs/) for in-depth guides and feature documentation
