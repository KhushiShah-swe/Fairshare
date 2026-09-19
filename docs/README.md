# FairShare documentation

[Project home](../README.md) · [Final sprint demo](https://youtu.be/GIe5kEu0w4Q) · [GitHub issues](https://github.com/KhushiShah-swe/fairshare-app/issues)

## Start here

| Guide | What it answers |
| --- | --- |
| [Project case study](CASE_STUDY.md) | What problem does FairShare solve, and what engineering work does it demonstrate? |
| [Local setup](SETUP.md) | How do I run it on Windows, macOS, or Linux with MySQL? |
| [Architecture](ARCHITECTURE.md) | How are the application layers and data relationships organized? |
| [API reference](API.md) | Which routes, request fields, and behaviors exist? |
| [Testing and CI](TESTING.md) | What does the current suite verify, and how do I run it? |
| [Roadmap](ROADMAP.md) | What is the next prioritized engineering work? |
| [Contributing](../CONTRIBUTING.md) | How should an issue or pull request be prepared? |
| [Security policy](../SECURITY.md) | How should concerns be reported, and what is the evaluation scope? |

## Release planning and sprint evidence

The original presentations and recorded demonstrations are retained as historical project artifacts.

| Stage | Scope | Presentation | Recorded demonstration | GitHub tracking |
| --- | --- | --- | --- | --- |
| Release planning | Problem, personas, backlog, MVP, and sprint planning | [Release plan](FairShare%20-%20Release%20Planning.pdf) | — | [Historical stories](https://github.com/KhushiShah-swe/fairshare-app/issues?q=is%3Aissue%20is%3Aclosed) |
| Sprint 1 | Accounts, groups, expenses, equal splits, balances | [Sprint 1](Sprint%201.pdf) | [Watch demo](https://youtu.be/nV-iAE6gtnw) | [Milestone](https://github.com/KhushiShah-swe/fairshare-app/milestone/2) |
| Sprint 2 | Selected participants, percentages, receipts | [Sprint 2](Sprint%202%20.pdf) | [Watch demo](https://youtu.be/c3UXRfElc08) | [Milestone](https://github.com/KhushiShah-swe/fairshare-app/milestone/3) |
| Sprint 3 | Export, settlement instructions, reset workflow, payment references | [Sprint 3](SPRINT%203.pdf) | [Watch demo](https://youtu.be/GIe5kEu0w4Q) | [Milestone](https://github.com/KhushiShah-swe/fairshare-app/milestone/4) |

## Story traceability

| Sprint | Stories | Recorded points |
| --- | --- | ---: |
| Sprint 1 | [#1 Accounts](https://github.com/KhushiShah-swe/fairshare-app/issues/1), [#2 Create group](https://github.com/KhushiShah-swe/fairshare-app/issues/2), [#3 Join group](https://github.com/KhushiShah-swe/fairshare-app/issues/3), [#4 Add expense](https://github.com/KhushiShah-swe/fairshare-app/issues/4), [#5 Edit/delete](https://github.com/KhushiShah-swe/fairshare-app/issues/5), [#6 Equal split](https://github.com/KhushiShah-swe/fairshare-app/issues/6), [#7 Dashboard](https://github.com/KhushiShah-swe/fairshare-app/issues/7) | 37 |
| Sprint 2 | [#8 Selected participants](https://github.com/KhushiShah-swe/fairshare-app/issues/8), [#9 Percentages](https://github.com/KhushiShah-swe/fairshare-app/issues/9), [#10 Receipts](https://github.com/KhushiShah-swe/fairshare-app/issues/10) | 21 |
| Sprint 3 | [#11 Export](https://github.com/KhushiShah-swe/fairshare-app/issues/11), [#12 Settlement plan](https://github.com/KhushiShah-swe/fairshare-app/issues/12), [#13 Clear debts](https://github.com/KhushiShah-swe/fairshare-app/issues/13), [#14 Zelle references](https://github.com/KhushiShah-swe/fairshare-app/issues/14) | 26 |

The 14 historical issues record 84 estimated points. Earlier planning documents contain different intermediate scope totals; the table above follows the current issue estimates. It does not convert those estimates into measured productivity or independently verified delivery metrics.

## Reading the evidence accurately

Use the current Markdown guides and source code for implemented behavior. The original PDFs include plans, retrospective observations, concept visuals, and historical report snapshots. Their references to stronger authentication, PDF exports, optimized settlement, or preserved payment history should be read with the [current implementation boundaries](../README.md#current-boundaries).

The linked videos are the project's existing demonstration links; no live hosted application is configured in this repository. Current test evidence belongs in [GitHub Actions](https://github.com/KhushiShah-swe/fairshare-app/actions/workflows/ci.yml), rather than screenshots of earlier runs.

**Current maintainer:** [Khushi Shah · @KhushiShah-swe](https://github.com/KhushiShah-swe).
