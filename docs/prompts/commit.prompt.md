# Prompt: Commit and Push Docs or Code to Remote

- Review all recent changes in the codebase (diff, staged, or unstaged).
- Propose specific edits to all relevant `.md` documentation files:
  - `.github/copilot-instructions.md`
  - `README.md`
  - `CHANGELOG.md`
  - `docs/BUILD-PIPELINE.md`
  - Any other affected docs
- Show the proposed doc changes and ask:
  **"Apply these documentation changes and make them remote? (Y/N)"**
- If approved (Y):
  - Save the doc changes and push them to the remote repository (handle all Git steps: stage, commit, push).
  - Use a commit message like:
    `docs: update [doc name(s)] — [short summary of change]`
- Then ask:
  **"Save and push any other code or content changes to remote? (Y/N)"**
  - If yes, prompt for a commit message and proceed.
- Double-check for consistency across all docs.
- If onboarding or workflow is affected, update `.github/copilot-instructions.md` as well.
- Use concise, emoji-driven responses and maintain a clear, stepwise flow.
- Explain that "make remote" means all Git steps (stage, commit, push) are handled for the user.
