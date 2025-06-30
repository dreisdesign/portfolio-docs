# 2025-06-02-portfolio-tags-feature-readme

# Feature: Portfolio Item Tagging and Filtering from Roles

**Date:** June 2, 2025

## 1. Overview

This document outlines the plan to convert the current "Role" descriptions on portfolio item pages into clickable tags. These tags will allow users to filter and navigate portfolio pieces based on specific roles like "Research", "Product Design", etc. This feature aims to improve content discoverability and provide a more interactive way to explore portfolio projects.

## 2. User Stories

*   **As a user, I expect that when clicking on a role (e.g., "Research"), I will be taken to a view of all portfolio pieces that include that role/tag.**
*   **As a developer, I expect that when adding a new role to a portfolio page's HTML, the build process will automatically detect this role. If the role is new across the entire portfolio, the system will create any necessary structures (like a new tag filter page) for it.**
*   **As a developer, I expect the source HTML for portfolio items to remain as simple as possible, with the build process handling the generation of the tag list from the existing "Role:..." text.**

## 3. Proposed Solution

The implementation will involve parsing the existing HTML structure of portfolio pages and enhancements to the current Node.js-based build pipeline, primarily within the `/Users/danielreis/web/danrtzaq/dev/scripts/deploy/deploy-support/scripts/06-build-portfolio.mjs` script.
