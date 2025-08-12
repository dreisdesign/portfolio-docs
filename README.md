# Portfolio System

**Updated: August 12, 2025**

A modern, maintainable UX portfolio system with automated build pipeline, responsive image processing, and comprehensive tagging system.

## ⚡ Quick Start

```bash
# Clone and setup
git clone https://github.com/dreisdesign/danrtzaq.git
cd danrtzaq
npm install

# Build and preview
npm run build

# Or use the interactive menu
npm run menu
```

## 🎯 What This Is

A complete portfolio build system featuring:
 - Automated build pipeline (validation, asset processing, audit)
 - Git-aware swift build (dirty + staged only, optional last commit)
 - Responsive & zoom image pipeline (Sharp variants + self-healing)
 - Portfolio tagging & tag index generation
 - Company logo injection & modular head templates
 - Password protection with global session & modal security layer
 - Automated documentation date + changelog archiving (WIP)
 - Menu-driven workflows & page/section scaffolding

## 🚀 Common Workflows

### Development
```bash
npm run build          # Build + preview server (most common)
npm start             # Start server on existing build
npm run menu          # Interactive menu system
```

### Creating Content
```bash
npm run menu          # → "New Page" to create portfolio projects
npm run menu          # → "Insert Section" to add content blocks
```

### Password Protection
```bash
npm run menu          # → "Utilities" → "Add Password Protection"
```

### Deployment
```bash
npm run deploy        # Deploy to production
npm run deploy:open   # Deploy + open site
```

## 📁 Project Structure

```
├── public_html/           # Source content
├── DOCS/                 # Documentation
├── dev/scripts/          # Build system
├── build/               # Build output
└── package.json         # Commands & dependencies
```

## 🎨 Key Features

### Swift Build System
Fast iterative builds driven by git state.

- Fast Development: ~18s builds processing only images that actually need work
- Default Scope: Unstaged working tree changes + staged/index changes + any images missing required variants (self-heal)
- Skips Last Commit By Default: Prevents reprocessing freshly committed large batches
- Opt-In Last Commit: Use `--include-last-commit` when you explicitly want the most recent commit's image edits re-validated
- Force Mode: `--force-all` regenerates every responsive + zoom variant (baseline refresh)
- Self-Healing: Missing or deleted variant/zoom files trigger automatic regeneration
- Transparent Logging: Logs clearly indicate which detection scopes were active

### Portfolio Tagging
Unified multi-category tagging (Role, Platform, Audience, Company) with:
- Automatic tag parsing & slug generation
- Individual tag pages with filtered cards
- Master tag index page grouped & categorized
- Consistent card template + +More spacer automation
- Configurable categories / counts at script top

### Password Protection
Global password + 24h session model:
- BUILD_INSERT marker detection => transformation
- Global password config (`dev/env/password-config.mjs`)
- LocalStorage session (timestamp validation) single entry per day
- Inline + modal based unlock flows (depending on page template)
- Audit visibility: protected page list + Secure metric

### Advanced Security Features
Protected pages ship only a placeholder & modal until authentication; real content injected post-verify, reducing scrape surface.


### Automated Systems
| System | Automation |
| ------ | ---------- |
| Image dimensions | Sharp metadata injection (removes 100s manual attrs) |
| Responsive variants | On-demand + regeneration for missing sizes |
| Zoom images | Compressed full-size `-zoom` variant generation |
| Version tokens | `{{VERSION}}` replacement post-build |
| Logo injection | Company detection via path structure |
| Tag pages | Generated from parsed metadata (cards + index) |
| Doc dates | Sync to last git commit date during public sync |
| Audit logs | Auto-archiving retaining baseline + last N |
| Changelog curation | (Planned) auto-archive beyond 10 releases |

## 📖 Documentation
Primary references (keep these updated):

- DEVELOPER-NOTES.md – Build pipeline internals, scripts, troubleshooting
- DESIGN-SYSTEM.md – Typography, spacing, components
- CHANGELOG.md – Last 10 releases (older in archive)


## 🛠️ Build Commands

```bash
# Development
npm run build             # Build + preview (most common)
npm run build:swift:fast  # 18-second fast build
npm run build:full        # Complete 3-minute build

# Content Creation
npm run create-new        # New portfolio project
npm run menu             # Interactive utilities & password protection

# Deployment
npm run deploy           # Deploy to production
npm run preview:deploy   # Build + deploy + open

# Image script direct flags (advanced):
# node dev/scripts/deploy/deploy-support/scripts/01-process-images-git.mjs --include-last-commit
# node dev/scripts/deploy/deploy-support/scripts/01-process-images-git.mjs --force-all
```

## 📋 Requirements
Minimal stack.

- Node.js 18+ (Sharp prebuilds benefit from newer versions)
- Git (required for change detection logic)
- macOS/Linux recommended (scripts use POSIX shell features)


## 🎯 Perfect For
Use cases:

- UX/Design portfolios needing fast iteration
- Case-study heavy sites with many large images
- Private/confidential work requiring gated access
- Designers wanting zero-CMS static workflow
- Sharing open-source build system patterns


## 🔗 Public Build System

This system is also available as a public repository for community use:

**Repository**: https://github.com/dreisdesign/portfolio-build

**Features**: Complete build pipeline, responsive image generation, tagging system, deployment scripts, and comprehensive documentation.


## 📝 Recent Highlights
Recent notable updates:

- 2.5.23: Image pipeline refinement (skip last commit by default, new `--include-last-commit` flag)
- Global password protection + session persistence
- Lock icon system for protected portfolio cards
- Modular head upper/lower injection
- Auto image dimension injection + responsive self-heal
- Swift Build v2.0 (git-based detection overhaul)


*See [CHANGELOG.md](DOCS/CHANGELOG.md) for complete version history.*

## 🆘 Need Help?

1. **Getting Started**: Run `npm run menu` for guided workflows
2. **Documentation**: Check the `DOCS/` folder for detailed guides
3. **Build Issues**: See [DEVELOPER-NOTES.md](DOCS/DEVELOPER-NOTES.md) troubleshooting section
4. **Design System**: Reference [DESIGN-SYSTEM.md](DOCS/DESIGN-SYSTEM.md) for UI patterns


*This portfolio system powers [danreis.design](https://danreis.design) - a fast, accessible, and maintainable UX portfolio.*
