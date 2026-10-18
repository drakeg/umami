# Contributing to Umami

Thanks for your interest in contributing to Umami! This document outlines the process for contributing code.

## Branching

This fork uses `master` as the active integration and deployable branch.

- Create feature, fix, documentation, and dependency branches from `master`.
- Open pull requests against `master`.
- Keep `master` green and deployable; do not bypass required CI or security checks.

If upstream Umami uses a different branching model, preserve upstream compatibility when syncing changes, but follow this fork's `master` workflow for local development.

## Submitting a Pull Request

1. Create your branch from the latest `master`:
   ```bash
   git checkout master
   git pull origin master
   git checkout -b my-feature
   ```
2. Make your changes. Keep PRs focused — one logical change per PR.
3. Ensure the project builds and lints cleanly:
   ```bash
   pnpm install
   pnpm build
   pnpm lint
   ```
4. Push your branch and open a pull request **against `master`**.
5. Fill in the PR description with what changed and why. Link any related issues.

See [docs/CODING_STANDARDS.md](./docs/CODING_STANDARDS.md) for fork-specific engineering requirements and [docs/PROJECT_PLAN.md](./docs/PROJECT_PLAN.md) for the current roadmap.

## Reporting Issues

- Search [existing issues](https://github.com/umami-software/umami/issues) before opening a new one.
- For bugs, include reproduction steps, expected vs. actual behavior, and your environment (Umami version, database, browser).
- For feature requests, describe the use case before the proposed solution.

## Development Setup

See the [README](./README.md) for instructions on installing dependencies, configuring the database, and running Umami locally.

## License

By contributing, you agree that your contributions will be licensed under the [MIT License](./LICENSE).
