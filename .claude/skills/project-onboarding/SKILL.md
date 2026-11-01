---
name: project-onboarding
description: Inspect an unfamiliar project or subsystem before making changes, identifying its stack, workflows, boundaries, and operational constraints.
---

# Project onboarding

Use before coding in an unfamiliar project or when the affected subsystem is unclear.

## Workflow

1. Start with affected paths, their manifests and nearby tests; use project.ps1 doctor for tool availability.
2. Identify commands and constraints needed for this task. Explore deployment, migrations or integrations only when affected.
3. Trace callers and data flow until the relevant boundary is understood; do not survey unrelated modules.
4. Check repository status and existing `.claude/` guidance before modifying anything.
5. State what was verified, what is absent, and what remains unknown. Do not infer missing details.

## Checklist

- Project structure and ownership boundaries understood.
- Relevant data, API, security and operational dependencies identified; unrelated areas need not be surveyed.
- Actual build/test commands sourced from project files.
- Existing local changes and configuration preserved.
