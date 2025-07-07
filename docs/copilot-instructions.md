---
applyTo: '**'
---
Coding standards, domain knowledge, and preferences that AI should follow.

Please start every response with an emoji

# Prompt Style Guidelines

## Emoji System for AI Responses

Use these at the start of each AI response for clarity:

- ✅ = complete/success
- ⚠️ = issue/warning
- 💬 = options/clarification
- 🚧 = in progress
- 🔍 = searching/auditing
- 📝 = doc/note
- 🟢 = ready/green-light

## Response Style
- Use plain, simple language
- Be concise (e.g., say “Agreed.” instead of “You're absolutely right…”)
- Skip blame or filler — just provide the fix
- Ask for clarification if the request is ambiguous
- Use consistent terminology and formatting
- Prefer bulleted lists for clarity
- Provide examples or analogies when useful
- Explain reasoning briefly when needed

## Solution Guidelines
- Favor reliable, well-known methods
- Offer step-by-step instructions when applicable
- Suggest tools or approaches I may not have considered
- Avoid over-engineering or unnecessary files
- Prioritize maintainability and clarity
- Follow existing patterns and conventions where possible
- Document decisions and rationale clearly
- Simplify especially if something has failed multiple times

## Context
- **Environment**: macOS in VS Code
- **Project Focus**: Personal portfolio static site (HTML, CSS, vanilla JS/ESM)
- **Workflow**: Custom Node.js build system, npm scripts, shell commands, Git for build-time change detection
- **Style**: Structured, maintainable code; deep build pipeline knowledge
- **Role**: Senior Product Designer with strong front-end skills

## Tone + Depth
- **Technical Level**: Mid-to-senior front-end/build tools; skip beginner explanations
- **Clarity**: Focus on how/why solutions work in this setup
- **Code**: Examples relevant to structure/conventions (e.g., `dev/scripts/...`, 2-space Prettier)

## Experimental Suggestions
- **Creativity**: Open to clever/unconventional ideas, especially for automation/workflow
- **Constraints**: Stick to Node.js, shell scripts, vanilla JS
- **Risk Framing**: Pitch experiments as low-risk, easy to test; include benefits/trade-offs

---

# Build System Quick Commands

- **Build site and start preview:** `npm run build`
  Main build pipeline + preview server (most common workflow)
- **Start preview server only:** `npm start`
  Local server to preview existing build
- **Interactive menu:** `npm run menu`
  Interactive menu with Build & Preview, Start Server, Deploy, etc.
- **Preview a specific page:** `PAGE=/portfolio/tags/ npm run preview:page`
  Build/preview just one page (replace path as needed)
- **Watch for changes (auto-rebuild):** `npm run dev`
  Dev server with file watching
- **Lint all JS files:** `npm run lint`
  Run ESLint on the codebase
- **Format codebase:** `npm run format`
  Apply Prettier to all source files
- **Run a specific build script:** `node build-system/scripts/06-build-portfolio.mjs`
  (Or any script in your scripts/ folder)
- **Check for build errors:** `cat build_output.log | tail -20`
  See last 20 lines of the build log
- **Sync from private repo:** `sh scripts/sync-from-private.sh`
  Sync content/config from private sources
- **Validate HTML output:** `node build-system/scripts/00-validate-html.mjs`
  Run output validation

---

## Semantic Search & Troubleshooting Tips

- Confirm you’re in the correct working directory before running scripts (e.g., `danrtzaq/` vs. `portfolio-build/`).
- Prefer absolute or project-root-relative paths in scripts and commands.
- If a script fails, check for:
  - Typos in script names or paths
  - Missing dependencies (`npm install`)
  - File permissions (e.g., `chmod +x script.sh` for shell scripts)
  - Required environment variables (e.g., `PAGE=...`)
- Use `ls` or `tree` to confirm file locations before running custom scripts.
- For ambiguous commands, refer to `package.json` scripts and `README.md` for canonical usage.
- If a command is not found, try `npm run <script>` or `node <path>` explicitly.
- When in doubt, search for the script/function name in the workspace to find its definition and usage.
- Use `cat build_output.log | tail -20` to quickly diagnose build failures.
- For new scripts, add a comment at the top describing usage and required context.

---

## Important Safety Note

- Avoid running build scripts that overwrite or modify files in your source directories (e.g., `_source-content/`, `dev/`, or `build-system/`).
- Always confirm the output path and script intent before running new or experimental build scripts.
- Prefer running builds that output to a dedicated `build/`, `public_html/`, or similar directory.
- If unsure, review the script or run it on a test branch to prevent accidental data loss.

- **Do not search or operate in the `postsforpause.com/` directory.** This folder is not part of the main portfolio build and should be excluded from all automation, search, and build steps.

---

## Workspace & Repo Structure

- **danrtzaq/**  (Private main repo)
  - Your primary, private workspace for all source, content, and build scripts
  - Contains: custom build system, content, automation, and experimental scripts
- **portfolio-build/**  (Public portfolio-build repo)
  - Public-facing, minimal repo for the static portfolio site
  - Contains: only the files needed to build and deploy the public site
- **build-system-repo/**
  - (If present) Used for modularizing or versioning the build system separately
  - Useful for sharing build logic across projects or as a submodule

### Git & Workflow Tips

- Keep private and public repos clearly separated to avoid accidental leaks
- Use `.gitignore` in both repos to prevent build artifacts, logs, and secrets from being committed
- For cross-repo sync, use scripts (e.g., `sync-from-private.sh`) and always review diffs before pushing
- Use branches for experimental features or major changes; merge to main only after validation
- Tag releases in the public repo for clear versioning
- Use `git status` and `git diff` before every commit to catch accidental changes
- For submodules (if using `build-system-repo` as a submodule), remember to update and commit submodule refs

---

For more details, see:
- `README.md` (project overview, setup, usage)
- `CHANGELOG.md` (recent changes/updates)
- `docs/BUILD-PIPELINE.md` (detailed build pipeline steps)
