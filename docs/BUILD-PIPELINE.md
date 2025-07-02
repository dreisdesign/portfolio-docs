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

5. **File Formatting** (`04-format-files.sh`)
   - Formats CSS and JSON.
   - Minifies CSS.

6. **Portfolio Build** (`06-build-portfolio.mjs`)
   - Main build coordinator: processes portfolio pages, injects navigation, logos, tags, carousels, and generates index/tag pages.
   - Carousels and "Up Next" cards are now generated from modular HTML templates (`carousel-template.html`, `up-next-card-template.html`).

7. **Modular Head & Footer Injection** (`inject-head-upper.mjs`, `inject-head-lower.mjs`, `inject-footer.mjs`)
   - Injects upper and lower head content, and the footer into all HTML files in the build output.
   - Uses placeholders: `<!-- BUILD_INSERT id="head-upper" -->` and `<!-- BUILD_INSERT id="head-lower" -->` in templates/source files.
   - Head content is managed in separate template files for maintainability.
   - **Note:** The modular head injection system allows you to update meta tags, favicons, and scripts in a single place (`injected-head-upper.html` and `injected-head-lower.html`), ensuring consistency and maintainability across all pages.

8. **Responsive Image Transformation** (`05-transform-responsive-images.mjs`)
   - Updates image tags for responsive delivery.

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

## Documentation Sync Automation

A pre-push git hook automatically runs the docs sync script (`dev/scripts/deploy/deploy-support/utils/sync-public-docs.sh`) before every push. This ensures that all public documentation in the `DOCS/` and root-level `.md` files are always up to date and secure, without requiring manual steps.

- **Location:** `.git/hooks/pre-push`
- **Behavior:** Runs the sync script and blocks the push if the sync fails.
- **How it works:**
  1. You commit as usual.
  2. On `git push`, the sync script runs automatically.
  3. If the sync passes, the push proceeds. If not, the push is blocked and you see an error message.
- **To disable or customize:** Edit or remove `.git/hooks/pre-push`.

This workflow eliminates the need to remember to sync docs manually and ensures your public documentation is always current and safe.

## See Also
- [SCRIPTS.md](SCRIPTS.md) for details on each script
- [docs/simplified-workflow-guide.md](docs/simplified-workflow-guide.md) for a step-by-step workflow
