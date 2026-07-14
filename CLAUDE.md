# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

This repo is a personal collection of draw.io / diagrams.net architecture and concept diagrams (currently focused on Apache ZooKeeper). There is no build, lint, or test tooling — it's just `.drawio.xml` files plus reference images.

## Structure

- `old_diagrams/` — prior diagrams to use as style references (colors, shapes, fonts) when creating new ones.
- `example/` — reference images (e.g. screenshots/exports of target diagrams) to match style/layout against.
- Top-level `*.drawio.xml` — the current diagrams.
- `.claude/skills/commit-push/` — repo-local skill for committing and pushing (see below).
- `.claude/skills/sync-remote/` — repo-local skill for syncing with `origin/main` before starting new diagram work (see below).

## Working with `.drawio.xml` files

- These are draw.io/diagrams.net native XML files (`<mxfile><diagram><mxGraphModel><root>...`). Edit them directly as XML — there is no separate build step to render them.
- After creating or editing a file, validate it's well-formed XML, e.g.:
  ```
  python3 -c "import xml.dom.minidom as m; m.parse('<file>.drawio.xml'); print('OK')"
  ```
- When asked to create a new diagram "in a similar style" to existing ones, read the relevant files in `old_diagrams/` (and any reference image in `example/`) first, and reuse their conventions: shape styles (`rounded=1`, `ellipse`, `shape=note2`), color palette (e.g. `gradientColor`/`fillColor` values already used), font sizes, and edge styles, rather than inventing a new visual language.
- Versioning a diagram: add each new version as a new `<diagram>` tab within the same `.drawio.xml` file rather than overwriting the existing one, so versions can be compared side by side in draw.io. Keep older tabs untouched. When reasoning about further edits or giving advice, only read/consider the latest (last) tab — older tabs are for visual comparison only, not input to current work.

## Committing changes

A repo-scoped skill `/commit-push` (`.claude/skills/commit-push/SKILL.md`) runs the full commit+push flow for this repo: `git add -A`, auto-generated commit message, `git commit`, `git push origin main`. Prefer invoking that skill over ad-hoc git commands when the user asks to commit and push.

Push after finishing every task in this repo, as a single commit (not several incremental ones), via the `/commit-push` skill.

## Syncing before new work

A repo-scoped skill `/sync-remote` (`.claude/skills/sync-remote/SKILL.md`) fetches and fast-forward pulls `origin/main`. Run it before starting a new diagram edit so local files reflect the latest remote state; it stops and asks rather than auto-resolving if there are uncommitted local changes or a diverged history.
