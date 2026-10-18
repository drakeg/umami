# Coding Standards

These standards apply to fork-specific changes in this repository. Upstream Umami conventions should be preserved unless there is a clear security, compatibility, or maintainability reason to diverge.

## General

- Keep changes small and focused.
- Prefer maintained dependencies and supported runtimes.
- Remove obsolete compatibility code when the supported platform no longer requires it.
- Do not disable tests, security checks, or supply-chain controls to make a PR pass.
- Avoid unrelated formatting churn in functional PRs.
- Update tests and documentation with behavior changes.

## TypeScript and JavaScript

- Use TypeScript for new application code where the surrounding area uses TypeScript.
- Preserve strict typing; avoid `any` unless there is a documented interoperability reason.
- Prefer explicit return and domain types at API/package boundaries.
- Validate untrusted input with the repository's existing schema tooling.
- Keep server-only logic out of client bundles.
- Do not introduce deprecated Node.js APIs when a supported alternative exists.

## React and Next.js

- Follow the existing App Router and component conventions.
- Prefer server components by default; use client components only when browser state or APIs require them.
- Keep effects narrowly scoped and avoid derived state where a computed value is sufficient.
- Preserve accessibility semantics for interactive controls.
- Avoid unnecessary client-side data fetching when the server can provide the data directly.

## Data access

- Use Prisma and existing database abstractions consistently.
- Do not concatenate user-controlled values into SQL.
- Treat migrations as production artifacts: review them, test them, and keep schema/client generation synchronized.
- Keep PostgreSQL and optional ClickHouse behavior separated where backend-specific code is required.

## APIs and MCP

- Keep OpenAPI definitions and generated clients synchronized.
- Validate authentication and authorization before processing protected requests.
- Treat API keys, MCP credentials, tokens, and encryption keys as secrets.
- Never log secrets or include them in fixtures unless they are explicit non-production test values covered by secret-scanning allowlists.
- Any API intended for third-party consumption should have an explicit access model, rate/usage policy, and monetization/paywall decision before public launch.

## Dependencies

- Commit `pnpm-lock.yaml` with dependency changes.
- Use `pnpm install --frozen-lockfile` as the reproducibility check.
- Prefer upgrading or replacing vulnerable dependencies over pinning incompatible transitive overrides.
- Keep the minimum-release-age policy enabled.
- Do not merge a dependency PR with a red Snyk, Gitleaks, or Node CI check.
- Security updates may drop obsolete runtime compatibility when necessary.

## Formatting and linting

Biome is the source of truth.

Before submitting code changes, run:

```bash
pnpm lint
pnpm check
```

Use targeted formatting for small fixes where practical to avoid unrelated churn.

## Tests

Run the smallest relevant test set while developing, then the full required validation before merge.

Core validation:

```bash
pnpm install --frozen-lockfile
pnpm openapi:generate
pnpm openapi:check --explicit
pnpm check:api:client
pnpm build:packages
pnpm test
pnpm test:packages
pnpm build
```

For affected areas, also use:

```bash
pnpm test:e2e
pnpm test:api
```

Add regression tests for bug fixes whenever practical.

## Docker and configuration

- Runtime configuration must come from environment variables rather than source edits.
- User-facing container ports must be configurable.
- Provide safe development defaults where appropriate, but never ship production secrets.
- Keep example environment files synchronized with supported variables.
- A documented Compose deployment should be portable between development systems.

## Git and pull requests

- Use descriptive branch and commit names.
- One logical change per PR.
- Keep generated files and lockfiles in the same PR as the source change that requires them.
- Delete merged branches.
- Close superseded dependency PRs rather than stacking conflicting lockfile changes.
- Do not merge around failing required checks.

## Security

- Never commit real credentials, API keys, tokens, private keys, or production connection strings.
- Keep Gitleaks allowlists limited to known test fixtures.
- Favor least privilege for application and CI credentials.
- Use supported cryptography and secure random generation.
- Document any security-sensitive configuration change.

## Documentation

Update documentation when a change affects:

- installation or upgrades,
- environment variables,
- ports,
- Docker behavior,
- authentication,
- API/MCP behavior,
- database migrations,
- operator workflows,
- or compatibility requirements.
