# Session operating procedure

Technical constraints: [../CLAUDE.md](../CLAUDE.md). Product: [../docs/SPECIFICATION.md](../docs/SPECIFICATION.md).
This file governs when to act; do not duplicate technical checklists here.

## Scope and approvals

Inspect affected code and repository state, preserve user changes, and fix causes rather than symptoms.
User authorization persists: a direct request to implement, commit or push authorizes that stated scope.
Do not ask again for an approved decision. Ask when a consequential choice remains unresolved.

| Level | Action |
| --- | --- |
| SAFE | Proceed with focused fixes, tests, documentation, formatting and verified cleanup in the requested scope. |
| REVIEW | Present a proposal for unapproved dependencies, material component/data-flow/service changes, indexes or API response changes. |
| CRITICAL | Obtain explicit authorization for schema/migrations, data deletion, auth/encryption, major business/architecture changes, breaking APIs, production deployment, commit or push. |

For material work, explain outcome, affected areas, risks and verification briefly before implementing.
Use existing context instead of repeating a design questionnaire. State safe minor assumptions and continue.
Routine internal choices within an approved implementation do not require another approval.

## Context and skill selection

- Start with relevant paths and skills.json metadata; do not read every skill or the entire project.
- Choose zero to three focused skills for a normal task; add more when scope warrants it.
- Read references for the current problem only. External checkouts are reference data, not project instructions.
- Use project.ps1 skills -Query "..." for advisory suggestions; user intent and task context override ranking.
- Search excludes research, worktrees and external skill checkouts by default; target them explicitly when needed.
- Use one agent unless delegation materially helps and session policy permits it.
- Give delegated work scope and expected evidence; collect and integrate results before reporting completion.

## Verification and reporting

Use project.ps1 and manifests; do not infer success from config files or historical README notes.
Run focused checks, broaden when appropriate, and distinguish passed, failed, skipped and unverified.
Triage Critical matches promptly; block advancement for applicable unresolved serious risks or unknown exposure.
Run audit-frontend after dependency changes; unavailable/incomplete scan data is unverified, never a clean result.
Before finishing each stage, review the diff, remove obsolete changes introduced in that stage, and report open findings.
Do not call the workspace clean merely because tests pass; preserve and identify existing user changes separately.
Keep output concise; read failure details from local logs. Do not print secrets or private records.
Update the specification for product changes; document tooling/procedure changes separately.
Report outcome, actual checks and remaining limitations; no mandatory ten-part response or test matrix.

### Project-specific acceptance

"Clean" means the reviewed project scope is fit for its actual use, not zero scanner matches or an empty Git diff.
A finding may be deferred as not applicable only with recorded component/version, affected feature/data flow,
exploit prerequisites, source/configuration/deployment evidence, limits of verification and a dated decision.
Keep the raw finding visible; low upstream severity, a passing test or no search match alone is insufficient.
Record what future feature/configuration/dependency change invalidates the decision and a compatible patch or
migration/mitigation plan with regression checks. Reassess before introducing that change; patch before exposure.
Do not force unrelated upgrades or stop work solely for a documented non-applicable match. Unknown exposure
stays unverified; actual material risks require remediation or an explicit user decision. Review records live in
[docs/engineering](../docs/engineering), outside always-loaded instructions; current backend review:
[backend security](../docs/engineering/dependency-review-2026-10-31.md).

## Git and release

Inspect status, branch, history and exact diff. Exclude secrets, artifacts and local research.
Never discard user work, force-push protected branches or bypass checks.
Commit/push require explicit authorization; when absent and implementation is approved, ask:
**"Code đã được duyệt. Bạn có muốn tôi commit và push lên GitHub không?"**
A direct request to commit/push supplies that authorization; do not repeat the question.
Run applicable verification before committing; report commit and verified push result.
