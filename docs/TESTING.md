# Tests and continuous integration

[Back to the project](../README.md) · [Setup](SETUP.md) · [Roadmap](ROADMAP.md)

## Existing test inventory

| Suite | Cases | What it exercises |
| --- | ---: | --- |
| `AuthControllerTests` | 16 | Signup/login controller calls and Zelle data/QR response paths |
| `GroupControllerTests` | 17 | Group creation, joining, listing, rename, leave, and delete controller paths |
| `ExpenseControllerTests` | 39 | Expense validation, edit/delete responses, receipt endpoints, settlement-plan and export responses |
| `FairShareBackendTests` | 26 | Service logic with mocked repositories, including splits, balances, groups, and account data |
| `GroupDetails.test.jsx` | 5 | Isolated payer-name, balance-color, currency, role, and invite-code examples |

Total: **98 backend unit tests and 5 frontend logic checks**. These counts reflect the source inventory and retained historical reports. Use the latest Actions run for current execution evidence.

The backend tests use JUnit 5 and Mockito. They are not full HTTP or database integration tests. The frontend file does not render the actual React components, so its five checks do not establish component or browser coverage.

## Run the checks

Backend, from `backend/fairshare-backend`:

```bash
mvn clean verify
```

Frontend, from `frontend/fairshare-frontend`:

```bash
npm ci
npm test
npm run build
```

The current unit tests use mocks and do not require a running MySQL server. Local application walkthroughs do require MySQL and both services as described in [SETUP.md](SETUP.md).

## Reports and coverage

| Report | Local output |
| --- | --- |
| Surefire results | `backend/fairshare-backend/target/surefire-reports/` |
| JaCoCo HTML | `backend/fairshare-backend/target/site/jacoco/index.html` |
| Vitest HTML | `frontend/fairshare-frontend/vitest-report.html` |

JaCoCo currently enforces a bundle-level **1% line coverage minimum** through Maven `verify`. The Sprint 3 presentation contains a historical coverage snapshot, but it is not a current coverage guarantee. The existing CI does not enforce frontend coverage.

Generated reports already committed to the repository are historical artifacts. Running a test may update them locally; do not include those generated changes in an unrelated pull request.

## What CI does

The existing [FairShare CI Build](../.github/workflows/ci.yml) runs on every push and pull request:

1. Checks out the repository and selects JDK 17.
2. Runs `mvn clean verify` in the backend.
3. Uploads JaCoCo and Surefire reports, including when an earlier step fails.
4. Selects Node 20, runs `npm ci`, and executes `npx vitest run`.

This workflow provides continuous integration. It has no application deployment, container publication, browser test, MySQL integration test, frontend production build, or dependency audit step. The documentation refresh leaves this workflow and all existing tests unchanged.

## Prioritized test expansion

Future work should target behavior that the current fast checks cannot prove:

- Server-side authentication and cross-group access boundaries.
- Expense/split persistence against MySQL and real HTTP request validation.
- Exact monetary reconciliation, percentage rounding, and opposing debts.
- Non-destructive settlements, duplicate-request handling, and history retention.
- Receipt and QR validation, authorized download, and failed uploads.
- Rendered React forms, loading/error states, and complete multi-user browser journeys.

See the [roadmap](ROADMAP.md) for planned work. A future coverage increase should follow meaningful tests rather than merely raising a badge number.
