# 2025-06-27-colors-plan-readme

# Color System Consolidation & Organization Plan

## Goals
- Centralize all color definitions for maintainability and theme flexibility
- Eliminate hardcoded color values from CSS and HTML
- Use clear, consistent naming for all color variables
- Enable easy updates, theming, and documentation

## Current State
- Colors are managed using CSS custom properties (variables) in `main-base.css`
- Some colors may still be hardcoded or duplicated across files
- RGB channel variables are used for gradients and rgba()

## Opacity Variable Plan (Recommended)
To ensure all color/opacity combinations are tracked and maintainable, define variables for a concise, standardized set of opacity variants (best practice):

```css
:root {
  --color-black-05: rgba(0,0,0,0.05);
  --color-black-10: rgba(0,0,0,0.10);
  --color-black-20: rgba(0,0,0,0.20);
  --color-black-30: rgba(0,0,0,0.30);
  --color-black-40: rgba(0,0,0,0.40);
  --color-black-50: rgba(0,0,0,0.50);
  --color-black-60: rgba(0,0,0,0.60);
  --color-black-80: rgba(0,0,0,0.80);
  --color-black-90: rgba(0,0,0,0.90);
  --color-white-80: rgba(255,255,255,0.80);
  --color-white-90: rgba(255,255,255,0.90);
  /* Add more as needed based on audit */
}
```

- Use these variables in your CSS instead of inline `rgba()` or opacity values.
- Document all variables in your color system docs for easy reference.
- Update the audit and plan as new opacity needs arise.

## Consolidation Steps
- See color audit and opacity variable plan in this folder for details.

## Color Swap Reference Table

| Old Value / Pattern                        | New CSS Variable                | Notes / Usage Example                |
|--------------------------------------------|---------------------------------|--------------------------------------|
| `#202f48`                                 | `var(--color-primary)`          | Primary color                        |
| `#ffe1bb`                                 | `var(--color-secondary)`        | Secondary color                      |
| `#105cd7`                                 | `var(--color-link)`             | Link color                           |
| `#E0E6EE`                                 | `var(--color-border)`           | Border color                         |
| `#FAFAF9`                                 | `var(--color-background)`       | Background/surface                   |
| `#ff0000`                                 | `var(--color-error)`            | Error color                          |
| `#000000`                                 | `var(--color-black)`            | Black                                |
| `#ffffff`                                 | `var(--color-white)`            | White                                |
| `#ccc`                                    | `var(--color-black-20)`         | Use closest opacity for gray         |
| `#666`                                    | `var(--color-black-60)`         | Use closest opacity for dark gray    |
| `#0074D9`                                 | `var(--color-link)` or new var  | Consider adding if used often        |
| `rgb(160, 160, 244)`                      | —                               | Consider new variable if needed      |
| `rgba(var(--color-black-rgb), 0.05)`      | `var(--color-black-05)`         | Use new opacity variable             |
| `rgba(var(--color-black-rgb), 0.2)`       | `var(--color-black-20)`         | Use new opacity variable             |
| `rgba(var(--color-primary-rgb), 0.4)`     | `var(--color-primary-40)`       | Add if needed, or use closest step   |

This table should be referenced during refactoring and future maintenance to ensure consistency and clarity.

## Limitations: HTML Meta Theme Color
- The `<meta name="theme-color">` tag in HTML cannot use CSS variables directly. For consistency, set its value to match your `--color-background` or other primary background color variable.
- If you update your background color variable, remember to update the meta tag value in all HTML files for consistency across browser UI theming.

---

*This plan will ensure a scalable, maintainable, and designer-friendly color system for your portfolio project.*
