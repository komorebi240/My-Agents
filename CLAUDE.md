# Project engineering guidance

Read [.claude/CLAUDE.md](.claude/CLAUDE.md) for operating procedure and approvals.
This file defines technical constraints. Read only the skills relevant to the task;
their inventory and routing are in [.claude/skills.json](.claude/skills.json).

## Project map

- Product behavior, roles, limits and endpoints: [docs/SPECIFICATION.md](docs/SPECIFICATION.md).
- Backend: Java 17, Spring Boot 3.x, Maven, SQL Server, Flyway; see [backend/README.md](backend/README.md).
- Frontend: Next.js App Router, React, TypeScript, TanStack Query, Tailwind; see [frontend/README.md](frontend/README.md).
- This is one Git repository with self-contained backend and frontend folders.
- Deployment examples: deploy/; launchers: run-local.ps1, run-dev-parallel.ps1.
- Tool commands and limitations: [tools guide](docs/engineering/tools.md).
- Historical numbered references (sections 1–46) in code/notes refer to
  [legacy standards](docs/engineering/legacy-standards.md). Do not load that archive routinely;
  current guidance here and the operating procedure take precedence.

## Working scope

- Inspect the affected implementation and callers; expand only when dependencies require it.
- Prefer a root-cause fix in existing code. Avoid duplicate utilities, speculative abstractions and unrelated cleanup.
- Preserve behavior during refactors; identify consumers before changing shared contracts.
- Remove proven-unused code in the affected area after checking references.
- Reuse existing dependencies; justify new ones with a concrete need.
- Comments use English or Vietnamese without diacritics and explain non-obvious reasons.

## Backend structure

Feature packages live under com.company.project.modules.<feature>:
controller/, service/, service/impl/, repository/, domain/, dto/, mapper/.
Shared infrastructure lives in config/, common/, and security/.

- Controllers parse HTTP and validate request DTOs; business rules belong in services.
- Controllers depend on service interfaces, not repositories or another feature's internals.
- Return DTOs rather than JPA entities; follow existing mapping patterns.
- Use Bean Validation for request shape, service checks for business invariants.
- Enforce permissions and tenant/ownership boundaries server-side, including direct API requests.
- Use service transactions for writes that must succeed together; consider concurrency and retries.
- Use the shared exception handler and safe errors, not per-controller response formats.

## Frontend structure

- Routes/layouts: frontend/src/app/; features: src/features/<feature>/.
- Shared primitives: src/components/ui/; shared HTTP client: src/lib/api/client.ts.
- Feature API modules use the shared client; components do not introduce direct fetch/axios paths.
- Server state uses TanStack Query. Add client-state libraries only for a demonstrated need.
- Reuse components and Tailwind tokens; do not introduce a visual system for one page.
- Preserve theme and Vietnamese/English behavior when editing visible content.
- Check loading, empty, error, disabled and focus states; preserve keyboard navigation.
- Review actual desktop/mobile rendering for material UI changes, including overflow and touch targets.
- Components use PascalCase, hooks useXxx, other names follow nearby conventions and tooling.

## Database

- SQL Server is the target dialect; H2 is not a substitute for dialect/locking integration checks.
- Flyway owns schema changes in backend/src/main/resources/db/migration/V{n}__{description}.sql.
- Never edit a shipped migration; consider existing data and deployment order.
- Follow plural snake_case tables, snake_case columns and <entity>_id foreign keys.
- Enforce important invariants through constraints; declare indexes deliberately.
- Preserve applicable audit columns and soft-delete semantics, without adding them blindly.
- Parameterize queries. Check tenant scope, transactions and N+1 behavior for affected data access.

## API contract

- Base path: /api/v1/; preserve established consumers and download/stream responses.
- Envelope implementations: backend/src/main/java/com/company/project/common/ApiResponse.java
  and ApiError.java; frontend types: frontend/src/types/api-response.ts.
- JSON uses success, data, error, meta; null members are omitted.
- meta.timestamp is present; paginated results use meta.pagination with
  page, size, totalElements, totalPages. Errors use code, message, optional fieldErrors.
- 204 has no body; binary downloads/streams keep their declared content type.
- Use existing HTTP status/error mappings. Keep errors free of secrets, SQL and stack traces.
- Generated OpenAPI describes endpoints; [API notes](docs/api/README.md) cover versioning.

## Security and configuration

- Never commit or log credentials, tokens, private keys, OTPs or sensitive records.
- Keep local configuration in ignored files or environment variables; examples contain placeholders.
- Preserve password hashing, cookie/session protections, authorization and resource ownership checks.
- Validate inputs and uploads server-side; use safe filenames/paths, type and size checks.
- Keep production and development databases, credentials and processes separate.
- Do not expose extra Actuator/debug endpoints; health details remain restricted.
- Handle external-service failures with bounded timeouts and deliberate retry/idempotency behavior.
- Use security-review when the affected attack surface warrants it.

## Verification

- Run powershell -File .\project.ps1 doctor for toolchain and dependency availability.
- Run focused tests before broader checks. Report only checks actually executed and their results.
- Backend unit tests use JUnit/Mockito; Jest logic tests use Node and component tests opt into jsdom.
- Testcontainers dependencies exist; an integration command does not prove integrations exist or ran.
- Public Playwright smoke tests use a separate frontend and synthetic API responses; they do not verify backend authorization.
- CI configuration exists; distinguish configured checks from runs actually completed on GitHub.
- Prefer behavior/regression tests over implementation mirrors. Scale verification to risk.
- Security/tenant-sensitive changes need negative authorization cases.
- UI checks consider shared-component consumers and actual rendering when applicable.

## Documentation and completion

- Update the matching specification section/changelog for changed product behavior, data, roles, limits or endpoints.
- Tooling-only changes update tooling documentation; do not invent product changes.
- Record costly decisions using [ADRs](docs/architecture-decision-records/README.md).
- Finish with outcome, actual checks and unresolved limitations. Use a test matrix only when useful.
