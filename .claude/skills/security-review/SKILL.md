---
name: security-review
description: Review application changes or code for exploitable security weaknesses, sensitive-data handling, and server-side trust boundaries.
---

# Security review

Use for auth, data access, endpoints, inputs, uploads, integrations, configuration, or explicit security review.

## Review

Inspect authentication, server-side authorization and ownership/tenant checks, IDOR and privilege escalation, injection (SQL, command, template), XSS, CSRF, SSRF, path traversal, file upload, CORS, session/token handling, passwords, rate limits, encryption, HTTPS, logging, errors, and secret exposure.

Validate untrusted input at the backend. Require parameterized queries and safe path/command handling. Ensure errors are safe for clients and logs omit sensitive data.

## Findings

For each issue report scanner severity separately from project impact, affected component, reachable attack scenario, remediation, and regression checks. Apply the [project acceptance rules](../../CLAUDE.md#project-specific-acceptance): record evidence, verification limits, reassessment triggers and a patch plan before deferring a non-applicable match. Check existing decisions when changing the affected feature/configuration/dependency. Pause the affected work for applicable serious risks or unknown exposure; a documented non-applicable match alone does not block progress.
