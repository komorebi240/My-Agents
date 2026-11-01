---
name: api-convention
description: Design or review HTTP endpoint contracts, validation, safe errors and compatibility in this project.
---

# API convention

Read the [project API contract](../../../CLAUDE.md#api-contract), affected ApiResponse/ApiError,
frontend types and endpoint code. Do not introduce a fallback envelope.

- Preserve /api/v1, consumers and shared error/status mappings.
- Validate input and server-side authorization, ownership and tenant scope.
- Consider pagination, filtering and duplicate requests where relevant.
- Keep binary/stream responses and 204 distinct from JSON envelopes.
- Test affected success, invalid input, unauthorized and not-found behavior.
- Propose unapproved breaking/response changes before implementation.
