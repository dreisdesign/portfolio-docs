# 2025-06-30-portfolio-build-migration-readme

# Portfolio Build System - Public Migration Plan

## Overview
Plan to extract and share the portfolio build system as an open-source project while protecting sensitive information.

## Phase 1: Repository Setup

### Create New Repository Structure
```bash
# 1. Create new directory for public repository
mkdir -p /Users/danielreis/web/portfolio-build

# 2. Initialize git repository
cd /Users/danielreis/web/portfolio-build
git init

# 3. Create base directory structure
mkdir -p {templates,dev/scripts/deploy,docs,example/public_html,config}
```

### Files to Copy (Sanitized)

#### Core Build System
- `dev/scripts/deploy/build.mjs` ✅
- `dev/scripts/deploy/deploy-support/scripts/` ✅ (all build scripts)
- `dev/scripts/deploy/deploy-support/head-templates/` ✅
- `dev/scripts/deploy/deploy-support/validation/` ✅
- `dev/scripts/deploy/deploy-support/utils/` ✅ (excluding sensitive utilities)

#### Development Tools
- `dev/server/` ✅ (development servers)
- `package.json` ✅ (sanitized dependencies only)
- `.eslintrc.cjs` ✅
- `.prettierrc` ✅
- `.editorconfig` ✅

#### Templates & Examples
- Create sanitized HTML templates
- Example portfolio structure
- Sample configuration files

## Phase 2: Content Sanitization

### Sensitive Information to Remove/Replace

#### Deployment Configurations
- Replace hardcoded server paths with environment variables
- Remove SSH keys and credentials
- Abstract deployment targets

#### Personal Content
- Remove actual portfolio projects
- Create generic example projects
- Replace personal branding with placeholders

#### Server-Specific Code
- Abstract hosting provider specifics
- Make deployment scripts generic
- Create configuration templates

### Sanitization Script
Create automated script to:
1. Copy files from private repository
2. Replace sensitive values with placeholders
3. Remove personal content
4. Update documentation

## Phase 3: Documentation Creation

### Public Documentation Structure

#### README.md (Main)
- Overview of the build system
- Key features and benefits
- Quick start guide
- Link to detailed documentation

#### SETUP.md
- System requirements
- Installation instructions
- Configuration setup
- Environment variables

#### BUILD-PIPELINE.md
- Detailed technical documentation
- Build step explanations
- Architecture overview
- Customization guide

#### PORTFOLIO-STRUCTURE.md
- HTML template requirements
- Tagging system documentation
- Asset organization
- Best practices

#### CONFIGURATION.md
- Environment variable reference
- Build script configuration
- Deployment options
- Advanced settings
