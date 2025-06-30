# Build Pipeline Overview

This document provides a high-level overview of the portfolio build pipeline, including the order of operations, key scripts, and their responsibilities.

## Pipeline Steps

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

5. **Formatting & Head Injection** (`04-format-files.sh`, `head-templates/inject-head.mjs`)
   - Formats HTML, CSS, and JSON.
   - Minifies CSS and injects head elements.

6. **Responsive Image Transformation** (`05-transform-responsive-images.mjs`)
   - Updates image tags for responsive delivery.

7. **Portfolio Build** (`06-build-portfolio.mjs`)
   - Main build coordinator: processes portfolio pages, injects navigation, logos, tags, carousels, and generates index/tag pages.

8. **Footer Injection** (`inject-footer.mjs`)
   - Ensures a single, correctly placed footer in every HTML file.

9. **Pre-Deploy Checks** (`07-pre-deploy-check.sh`)
   - Runs final checks before deployment.

10. **Preview Server** (`08-preview-server.mjs`)
    - Optionally starts a local server for previewing the build.

## Diagram

```
[Validate HTML] → [Process Images] → [Create Placeholders] → [Featured Images]
      ↓                 ↓                   ↓                    ↓
[Format & Inject Head] → [Responsive Images] → [Portfolio Build]
      ↓                 ↓                   ↓                    ↓
[Footer Inject] → [Pre-Deploy Checks] → [Preview Server]
```

## See Also
- [SCRIPTS.md](SCRIPTS.md) for details on each script
- [docs/simplified-workflow-guide.md](docs/simplified-workflow-guide.md) for a step-by-step workflow
