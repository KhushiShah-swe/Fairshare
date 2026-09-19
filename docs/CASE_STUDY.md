# FairShare: from shared-expense friction to a full-stack prototype

[Watch the final sprint demo](https://youtu.be/GIe5kEu0w4Q) · [Source code](../README.md) · [Sprint evidence](README.md)

**Maintainer:** [Khushi Shah](https://github.com/KhushiShah-swe)
**Project context:** Agile software engineering project developed across three sprints.
**Stack:** Java 17, Spring Boot, React, MySQL, JUnit/Mockito, Vitest, GitHub Actions.

## The problem

Shared expenses are easy to record incompletely. One person pays, only some group members participate, and the receipt may live in a separate conversation. When repayment time comes, the group has to reconstruct both the spending and the agreement behind it.

FairShare models those decisions explicitly: a group, the payer, selected participants, an allocation method, and supporting receipt information. The dashboard and CSV export make the resulting balances easier to inspect.

## Product decisions

| Decision | Reason | Evidence |
| --- | --- | --- |
| Start with a small complete journey | Account → group → expense → balance provides usable value early | Sprint 1 stories #1–#7 |
| Store participant allocations | Different expenses can involve different subsets of the same group | `ExpenseSplit` model and Sprint 2 stories |
| Add percentages and receipts together | Flexible allocation needs supporting context and transparency | Stories #9 and #10 |
| Put settlement instructions next to exports and payment details | Help users review obligations and coordinate repayment | Sprint 3 demo and stories #11–#14 |
| Keep planning artifacts beside source | Reviewers can trace intent, implementation, and retrospective lessons | Release plan, sprint PDFs, issues, milestones |

## Engineering evidence

- **Full-stack integration:** React pages call a Spring Boot REST API backed by MySQL.
- **Domain modeling:** users, memberships, groups, expenses, and participant splits represent the shared-expense workflow.
- **Business logic:** equal and percentage allocation, expense editing, derived balances, and consolidated direct debts are implemented in services.
- **Automated feedback:** 98 backend unit tests, five frontend logic checks, JaCoCo reports, and GitHub Actions provide an existing verification foundation.
- **Delivery process:** the 14 historical stories record 37, 21, and 26 estimated points across three sprints, with recorded demos and retrospectives.

These are repository artifacts, not claims about production users, revenue, measured performance, or complete security coverage. The [testing guide](TESTING.md) explains what the existing checks establish.

## Lessons and next iteration

The prototype makes the core workflows visible and reviewable. The next iteration should strengthen the boundaries around them: authenticated identity, group authorization, exact monetary arithmetic, and settlement records that retain history.

Testing should then expand from mocked unit behavior to real HTTP/database interactions and browser journeys. This sequence makes the planned improvements assessable: each item has a user story, business value, acceptance criteria, and a verification approach in the [roadmap](ROADMAP.md).

## Suggested review route

1. Watch the [Sprint 3 demo](https://youtu.be/GIe5kEu0w4Q) for the product flow.
2. Read the [architecture](ARCHITECTURE.md) and inspect the expense service and split model.
3. Open the [latest CI run](https://github.com/KhushiShah-swe/fairshare-app/actions/workflows/ci.yml) and its reports.
4. Compare a historical story with its implementation and the documented follow-up work.
5. Run the [local demo](SETUP.md) with synthetic accounts to explore the behavior directly.
