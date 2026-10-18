# Project Plan

This fork tracks Umami 3.x with an emphasis on secure, reproducible self-hosting and low-friction maintenance.

## Current baseline

- Application: Umami 3.4.0
- Node.js: 22 in CI
- Package manager: pnpm 12.3.4
- Framework: Next.js 16.x / React 19.x
- Database tooling: Prisma 7.x
- Primary database: PostgreSQL
- Optional analytics backend: ClickHouse
- Formatting/linting: Biome
- Tests: Vitest and Playwright
- Dependency automation: Renovate and Dependabot
- Security gates: Snyk and Gitleaks

## Delivery principles

1. Keep `master` deployable and green.
2. Prefer current supported dependencies and remove obsolete packages rather than carrying insecure compatibility layers.
3. Do not weaken security controls to make dependency updates pass.
4. Keep Docker and local development portable between systems.
5. Require generated artifacts, lockfiles, tests, and documentation to stay synchronized with code changes.
6. Keep pull requests focused and easy to review.

## Sprint 1 — Baseline stabilization

Status: substantially complete.

Goals:

- Complete the Umami 3.4.0 modernization.
- Move to the current Next.js/React/Prisma toolchain.
- Replace obsolete dependencies such as `npm-run-all`.
- Restore reproducible pnpm installs.
- Ensure Node CI, Snyk, and Gitleaks are green.
- Normalize GitHub Actions to supported hosted runners.

Exit criteria:

- `pnpm install --frozen-lockfile` passes.
- Application and workspace package tests pass.
- Production build passes.
- No Snyk findings on the active PR head.
- Gitleaks passes.

## Sprint 2 — Developer experience and deployment

Goals:

- Review Docker Compose defaults for portable local deployment.
- Ensure all user-facing ports and environment-dependent settings can be configured through environment variables.
- Maintain a useful `.env.example` where applicable.
- Verify a clean deployment can be moved between development systems without manual database credential repair.
- Document local, Docker, and production validation paths.

Exit criteria:

- A new checkout can be configured without source edits.
- Docker Compose starts with documented defaults.
- Ports and credentials are environment-driven.
- Migration/startup behavior is documented and repeatable.

## Sprint 3 — Test and CI hardening

Goals:

- Add explicit lint/format validation to CI without modifying files in the runner.
- Expand API, MCP, and deployment-path tests where coverage is weak.
- Keep OpenAPI generation and generated-client checks mandatory.
- Prevent lockfile drift.
- Keep minimum-release-age supply-chain protection enabled.

Exit criteria:

- CI covers lint, generated artifacts, unit tests, package tests, and production build.
- Dependency PRs fail for actionable reasons only.
- Security automation does not require bypasses for routine updates.

## Sprint 4 — Operations and security

Goals:

- Review authentication, API-key, MCP, and 2FA configuration defaults.
- Document reverse-proxy and production environment requirements.
- Review public API exposure and determine whether rate limiting, quotas, or a developer-access/paywall layer is appropriate for this fork.
- Review container image/runtime hardening and dependency scanning.

Exit criteria:

- Production configuration is documented.
- Security-sensitive features have explicit enablement and operational guidance.
- Public API policy is documented before external consumption is enabled.

## Backlog

- Keep Renovate/Dependabot PRs current and remove superseded branches.
- Review upstream Umami releases periodically before planning version upgrades.
- Add release notes for fork-specific behavior.
- Improve self-hosting health checks and observability where useful.
- Review database backup/restore documentation.
- Review accessibility and browser test coverage.

## Definition of done

A change is done when:

- The implementation is complete and focused.
- Relevant tests are updated or added.
- `pnpm install --frozen-lockfile` succeeds.
- OpenAPI/client generated files are current when applicable.
- Unit/package tests pass.
- Production build passes.
- Biome checks pass for touched code.
- Snyk and Gitleaks are green.
- Documentation is updated for user-visible or operational changes.
