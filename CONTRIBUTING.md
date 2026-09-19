# Contributing to FairShare

FairShare is maintained by [Khushi Shah](https://github.com/KhushiShah-swe). Start with the [setup guide](docs/SETUP.md), [architecture](docs/ARCHITECTURE.md), and [roadmap](docs/ROADMAP.md).

## Propose a change

Search existing issues first. Use the bug report form for reproducible problems or the user story form for features. A useful story explains the user, benefit, business value, acceptance criteria, and test approach. Story points are relative estimates; the maintainer confirms scope and sprint placement.

For security reports, follow [SECURITY.md](SECURITY.md) instead of posting sensitive details publicly.

## Make a focused pull request

1. Create a branch from `main`, such as `docs/setup-guide`, `fix/receipt-preview`, or `feature/balance-export`.
2. Keep the change focused and link the issue it addresses.
3. Add or update tests when behavior changes. Documentation-only changes need link and accuracy checks.
4. Run the relevant [verification commands](docs/TESTING.md).
5. Use the pull request template to explain the problem, resulting behavior, evidence, and limitations.

Use descriptive commit messages, for example `docs: explain local MySQL setup` or `fix: validate percentage totals`. Preserve existing attribution and avoid unrelated formatting changes.

## Review expectations

- API and UI behavior agree, including loading, empty, and failure states.
- Expense totals, participant allocations, and balances remain consistent.
- Any change involving permissions includes negative access tests.
- Screenshots and examples contain synthetic data.
- No passwords, receipts, banking details, or local environment files are added.
- Generated build output and test reports stay out of new commits; current historical reports are not a substitute for a fresh CI run.
- Documentation distinguishes implemented behavior from planned work.

The existing CI workflow runs Maven verification and Vitest. A passing workflow is necessary for code changes, but does not establish production readiness. The repository currently has no LICENSE file; discuss reuse or licensing with the maintainer before relying on a permission grant.
