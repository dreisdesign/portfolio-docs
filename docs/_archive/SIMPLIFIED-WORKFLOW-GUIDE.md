# Simplified Workflow Guide

This guide walks you through the most common workflows for building, previewing, and deploying your portfolio using the interactive menu and build scripts.

## 1. Daily Development
- Edit your content or code in the private repo.
- Run `npm run menu` and select "Build" for a fast, smart build.
- Preview your changes locally with the preview server.

## 2. Adding a New Portfolio Page
- Use the menu's "New Page" option or run `npm run create-new`.
- Follow prompts to generate a new project folder and starter files.
- Add your content and assets as needed.

## 3. Tagging & Categorization
- Use standardized tag markup in your HTML (see README for details).
- The build system will automatically generate tag pages and indexes.

## 4. Syncing Docs to Public Repo
- Update or add docs in `dev/docs/`.
- Run the sync utility to publish all docs to the public docs repo.
- Security checks will prevent accidental leaks of sensitive files.

## 5. Troubleshooting
- Check the build log for validation errors or skipped pages.
- Use the troubleshooting section in the README or docs for common issues.

## See Also
- [README.md](../README.md)
- [BUILD-PIPELINE.md](../BUILD-PIPELINE.md)
- [SCRIPTS.md](../SCRIPTS.md)
