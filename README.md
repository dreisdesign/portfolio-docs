# Portfolio System

**Updated: July 14, 2025**

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

- **Automated Build Pipeline** - Git-based change detection, image optimization, HTML validation
- **Smart Image Processing** - Automatic dimension injection, responsive variants, format conversion
- **Portfolio Tagging System** - Auto-generated tag pages and categorized navigation
- **Swift Build** - 18-second builds vs 3+ minute full builds (17x faster)
- **Company Logo Injection** - Automatic logo detection and linking
- **Responsive Design** - Mobile-first, accessible, performance-optimized

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
- **Fast Development**: 18-second builds with git-based change detection
- **Smart Image Processing**: Only processes changed images
- **Self-Healing**: Auto-regenerates missing responsive variants

### Portfolio Tagging
- **Auto-Generated Tags**: Role, Platform, Audience, Company categories
- **Tag Pages**: Individual pages for each tag with relevant projects
- **Tag Index**: Organized, searchable tag directory

### Password Protection
- **Confidential Work Protection**: BUILD_INSERT-based password protection for sensitive portfolio pages
- **Interactive Menu Utility**: User-friendly password addition through utilities menu
- **Professional UI**: Clean access forms with hiring manager instructions
- **Security Features**: Client-side hashing, content encoding, anti-scraping measures
- **Build Integration**: Seamless integration with existing build pipeline

### Advanced Security Features

- **Password Protection Modal:** Protected pages show a blurred, placeholder preview with a modal password prompt. Real content is only loaded after authentication, preventing unauthorized access via source inspection. Modal disables background scrolling and matches the site's design system.

### Automated Systems
- **Image Dimensions**: Automatic injection using Sharp metadata
- **Company Logos**: Auto-detection based on folder structure
- **Responsive Images**: WebP/AVIF conversion with fallbacks
- **Version Management**: Cache-busting for all assets

## 📖 Documentation

- **[DEVELOPER-NOTES.md](DOCS/DEVELOPER-NOTES.md)** - Technical implementation, build pipeline, and workflows
- **[DESIGN-SYSTEM.md](DOCS/DESIGN-SYSTEM.md)** - UI guidelines and patterns
- **[CHANGELOG.md](DOCS/CHANGELOG.md)** - Detailed version history

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
```

## 📋 Requirements

- **Node.js** 16+
- **Sharp** (auto-installed) for image processing
- **Git** for change detection

## 🎯 Perfect For

- **UX/UI Portfolios** with case studies and project showcases
- **Design Systems** requiring consistent, maintainable components
- **Performance-Critical Sites** with optimized images and fast builds
- **Teams** needing automated, reliable build processes

## 🔗 Public Build System

This system is also available as a public repository for community use:

**Repository**: https://github.com/dreisdesign/portfolio-build

**Features**: Complete build pipeline, responsive image generation, tagging system, deployment scripts, and comprehensive documentation.

---

## 📝 Recent Highlights

- ✅ **Automated Doc Date Updates** - Documentation dates sync automatically with git history
- ✅ **Swift Build V2.0** - 17x faster builds with intelligent change detection
- ✅ **Modular Head Injection** - Template-driven HTML head management
- ✅ **Image Dimension Automation** - 270+ manual attributes removed, auto-injected
- ✅ **Mobile-First Design** - Unified responsive layout across all pages

*See [CHANGELOG.md](DOCS/CHANGELOG.md) for complete version history.*

## 🆘 Need Help?

1. **Getting Started**: Run `npm run menu` for guided workflows
2. **Documentation**: Check the `DOCS/` folder for detailed guides
3. **Build Issues**: See [DEVELOPER-NOTES.md](DOCS/DEVELOPER-NOTES.md) troubleshooting section
4. **Design System**: Reference [DESIGN-SYSTEM.md](DOCS/DESIGN-SYSTEM.md) for UI patterns

---

*This portfolio system powers [danreis.design](https://danreis.design) - a fast, accessible, and maintainable UX portfolio.*
