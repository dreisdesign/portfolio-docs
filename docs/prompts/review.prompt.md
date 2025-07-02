# Build Review Checklist Prompt

After each build, review the following page types (using the build output temp URLs) to ensure all templates are rendering correctly and all build-time features (timestamps, navigation, footers, etc.) are present:

- **Home page:** `build/temp/public_html/index.html`
- **About page:** `build/temp/public_html/about/index.html`
- **Portfolio home page:** `build/temp/public_html/portfolio/index.html`
- **Portfolio project page:** e.g., `build/temp/public_html/portfolio/mikmak/custom-report-builder/index.html`
- **Tag listing page:** e.g., `build/temp/public_html/portfolio/tags/ab-testing/index.html`
- **Tag index page:** `build/temp/public_html/portfolio/tags/index.html`
- **Legal page:** `build/temp/public_html/legal/terms.html`
- **404 page:** `build/temp/public_html/404.html`

For each, check:
- Timestamp comment is present and correct (first line)
- Navigation and footer are injected
- Responsive images and assets load
- Version tokens are replaced
- No duplicate or malformed comments/whitespace
- **All documented placeholders are replaced:**
  - `<!-- BUILD_INSERT id="head-upper" -->` (all pages)
  - `<!-- BUILD_INSERT id="head-lower" -->` (all pages)
  - `<!-- BUILD_INSERT id="company-logo" -->` (portfolio project pages)
  - `<!-- BUILD_INSERT id="nav" -->` (all pages with navigation)
  - `<!-- BUILD_INSERT id="footer" -->` (all pages)
  - Any others referenced in your pipeline docs

| Placeholder                        | Appears On                        |
|------------------------------------|-----------------------------------|
| `head-upper`                       | All pages                         |
| `head-lower`                       | All pages                         |
| `company-logo`                     | Portfolio project pages           |
| `nav`                              | All pages with navigation         |
| `footer`                           | All pages                         |

_This prompt ensures every template type and all build-time injections/placeholders are covered in post-build QA._
