---
name: git-github
description: Manage repository changes safely, preserving user work and requiring explicit approval for commits, pushes, or protected-branch operations.
---

# Git and GitHub

Use for Git inspection, branching, commits, pushes, PR-related preparation, or history-sensitive changes.

## Workflow

Before changes inspect `git status`, current branch, and recent commits. Preserve uncommitted user work; never discard or overwrite it. Prefer `main`, `develop`, `feature/*`, `fix/*`, `refactor/*`, `chore/*`, and `security/*` naming when compatible with project practice. Use conventional commits such as `feat:`, `fix:`, `refactor:`, `test:`, `docs:`, `security:`, `chore:`, and `perf:`.

Follow the [Git approval procedure](../../CLAUDE.md#git-and-release). A direct commit/push request is authorization for that scope; do not ask twice. Review status/diff, run applicable checks, inspect secrets/excluded files, and report the verified result. Do not force-push protected branches or bypass checks.
