---
name: sync-remote
description: Fetch and pull the latest changes from origin main before making diagram edits in this repo. Use when the user asks to "sync", "pull latest", "update from remote", or before starting new diagram work.
---

# Sync with remote

Run this before starting new work on a diagram, to make sure local files are up to date with `origin/main`:

1. `git status` — check for uncommitted or untracked changes first.
   - If there are uncommitted changes, stop and tell the user. Do not stash, discard, or commit on their behalf — ask whether they want to commit (e.g. via `/commit-push`) or stash before syncing.
2. `git fetch origin`
3. `git pull --ff-only origin main`
   - If the fast-forward fails (local has diverged), stop and report it — do not force, rebase, or merge automatically. Explain the situation and ask the user how to proceed.
4. Report a short summary: whether new commits were pulled, and what changed (e.g. `git log --oneline HEAD@{1}..HEAD` if a pull happened).
