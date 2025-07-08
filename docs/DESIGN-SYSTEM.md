# Portfolio Design System Documentation

*Last Updated: June 30, 2025*

> See `CHANGELOG.md` for full project update history. This document covers the current design system and workflow.

## Table of Contents

- [Overview](#overview)
- [Typography System](#typography-system)
- [Color System](#color-system)
- [Component System](#component-system)
- [Spacing System](#spacing-system)
- [Responsive Breakpoints](#responsive-breakpoints)
- [CSS Consolidation Results](#css-consolidation-results)
- [Content Guidelines](#content-guidelines)
  - [Section Naming & Structure Guidelines](#section-naming--structure-guidelines)
  - [Content & UI Text Capitalization Guidelines](#content--ui-text-capitalization-guidelines)
- [Developer Notes](#developer-notes)

---

## Overview

*This section has moved to [README.md](../README.md) for better discoverability and project onboarding. See the README for a high-level project summary and context.*

---

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

## Developer Notes

*This section has moved to [DEVELOPER-NOTES.md](DEVELOPER-NOTES.md) for clarity and maintainability. All browser-specific fixes, video optimization, and deep technical implementation notes are now documented there.*

---

*Recent system enhancements and release notes have moved to [CHANGELOG.md](../DOCS/CHANGELOG.md).*

## Content Guidelines

### Section Naming & Structure Guidelines

#### Universal Sections & Naming Conventions

1. **Overview Section**
   - Markup: `<!-- OVERVIEW SECTION: Project Summary -->`
   - Tag: `<section class="wrapper">`
   - Header: `<h2>Summary</h2>`
   - Use: Brief project summary and context.

2. **Challenges Section**
   - Markup: `<!-- SECTION: CHALLENGES -->`
   - Tag: `<section class="challenges">`
   - Header: `<h2>Business Problem & Challenge</h2>` (always plural, never just "Challenge")
   - Use: Key business problems, user pain points, and project constraints.

3. **Solution Section**
   - Markup: `<!-- SECTION: SOLUTION -->`
   - Tag: `<section class="solution">`
   - Header: `<h2>Research & Data-Driven Design</h2>` (or `<h2>Solution</h2>` if preferred for consistency)
   - Use: Approach, research, design process, and rationale.

4. **Case Study Content Cards**
   - Markup:
     - `<!-- CASE STUDY CONTENT CARD (Image) -->`
     - `<!-- CASE STUDY CONTENT CARD (Carousel) -->`
     - `<!-- CASE STUDY CONTENT CARD (Video) -->`
   - Tag: `<section class="content">`
   - Use: Visuals, prototypes, research artifacts, annotated screenshots, or carousels.
   - Caption: `<p class="content-caption">` (for images/videos) or `<div class="carousel-caption-source">` (for carousels)
   - **Labeling:** Always use `<strong>` (not `<b>`) for the label at the start of a caption or carousel caption for accessibility and consistency. Example:
     ```html
     <p class="content-caption"><strong>Label:</strong> Description text...</p>
     <div class="carousel-caption-source"><strong>Label:</strong> Description text...</div>
     ```

5. **Results Section**
   - Markup: `<!-- SECTION: RESULTS -->`
   - Tag: `<section class="results">`
   - Header: `<h2>Results & Business Outcomes</h2>`
   - Use: Measurable outcomes, business impact, and key metrics.

6. **Learnings/Next Steps Section**
   - Markup: `<!-- SECTION: LEARNINGS & NEXT STEPS -->`
   - Tag: (usually within `.results` or as a separate section)
   - Header: `<h2>Learnings & Next Steps</h2>`
   - Use: Key takeaways, process insights, and future roadmap.

7. **Optional/Other Patterns**
   - Carousel captions: `<div class="carousel-caption-source">` (always use `<strong>` for the label)
   - Card titles: `<div class="card-title">` (if used)
   - Tag categories: `<div class="header--descriptions">` (for role, industry, approach)

### Carousel Caption Markup
- Carousel captions should use a single <p class="carousel-caption-source"> with <strong> for the title and a <span class="spacer"> containing all summary bullets (manual bullets, <br> for line breaks).
- This matches the .content-caption pattern for spacing and visual consistency.
- Example:
  ```html
  <p class="carousel-caption-source">
    <strong>Title</strong>
    <span class="spacer">
      • Bullet 1<br>
      • Bullet 2
    </span>
  </p>
  ```
- Use this pattern for all carousel slides to ensure a unified look and maintainable markup.

#### Best Practices
- Use the above section names and order for all case studies unless a strong reason exists to deviate.
- Always use the same class and header structure for each section.
- Use HTML comments to clearly mark each section for maintainability.
- If a section is omitted, document the reason in the code or commit message.
- **Legacy pages:** Update any older case studies to match these conventions for strict consistency.

---

_See also: Content & UI Text Capitalization Guidelines for style and formatting rules._
