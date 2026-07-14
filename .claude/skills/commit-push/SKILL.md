---
name: commit-push
description: Stage all changes, commit with an auto-generated message, and push to origin main for this repo. Use when the user asks to "commit and push", "save and push", or similar in this repository.
---

# Commit and Push

Run this exact sequence for this repository:

1. `git add -A`
2. Look at `git diff --staged` and recent `git log` (for style) to write a concise
   commit message summarizing the *why* of the change, ending with:

   ```
   Co-Authored-By: Claude Sonnet 5 <noreply@anthropic.com>
   ```

3. `git commit -m "<message>"` (use a HEREDOC to preserve formatting)
4. `git push origin main`

Notes:
- If there is nothing staged after `git add -A`, stop and tell the user there's nothing to commit — do not create an empty commit.
- If the commit fails due to a pre-commit hook, fix the issue, re-stage, and create a new commit (never `--amend`, never `--no-verify`).
- If `git push` fails (e.g. remote has new commits), stop and report the error instead of force-pushing.
