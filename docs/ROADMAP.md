# Engineering roadmap

[Back to the project](../README.md) · [Open issues](https://github.com/KhushiShah-swe/fairshare-app/issues?q=is%3Aissue%20is%3Aopen)

FairShare's three historical sprints remain recorded in issues #1–#14 and their original milestones. The work below is a follow-up backlog based on the current implementation. It is not part of the completed sprint estimates, and it has no promised release date.

## Prioritized follow-up work

| Priority | Work | Proposed points | Why it matters |
| --- | --- | ---: | --- |
| High | [#15: Account protection and group authorization](https://github.com/KhushiShah-swe/fairshare-app/issues/15) | 8 | Establish authenticated identity, safe account responses, and consistent record access |
| High | [#16: Exact currency allocation](https://github.com/KhushiShah-swe/fairshare-app/issues/16) | 8 | Ensure shares and balances reconcile to the original amount |
| High | [#17: Settlement ledger and completed payment-recording flow](https://github.com/KhushiShah-swe/fairshare-app/issues/17) | 8 | Preserve expenses and receipts, handle retries, and complete the dashboard API contract |
| Medium | [#18: API, database, and browser testing](https://github.com/KhushiShah-swe/fairshare-app/issues/18) | 5 | Verify real integration behavior and strengthen CI evidence |
| Medium | [#19: Reproducible demo and release process](https://github.com/KhushiShah-swe/fairshare-app/issues/19) | 5 | Simplify setup and prepare a credible deployment path after hardening |

Suggested order: begin account and monetary work, build the settlement ledger on those boundaries, expand integration coverage alongside each change, and then prepare hosting. Estimates require maintainer review before sprint commitment.

## Additional product opportunities

- Exact-amount participant splits.
- PDF balance exports with safe and accessible formatting.
- Export hardening, including spreadsheet formula handling and snapshot consistency.
- Stronger upload content validation and attachment access controls.
- Accessibility, keyboard navigation, and small-screen usability checks.
- A public demo containing only synthetic records, with a clearly documented reset process.

These items are opportunities, not implemented features. A cloud provider, budget, licensing choice, and public deployment should be selected explicitly when that work is scheduled.

## Historical records and evidence

Issues #1–#14 retain their original states, labels, milestones, and story-point estimates. Updated descriptions distinguish acceptance criteria from current verification evidence. Existing closed status should not be interpreted as a guarantee that all historical requirements are covered or production-ready.

The [architecture](ARCHITECTURE.md), [API reference](API.md), and [testing guide](TESTING.md) describe the current source. Original PDFs preserve the planning and review record; some include intended features that exceed the implemented scope.

## Definition of done for future changes

- Observable acceptance criteria and a linked issue.
- Verified behavior through appropriate unit, integration, or browser checks.
- Current CI passes, with any remaining verification limits stated.
- Documentation describes the resulting behavior and operational consequences.
- Financial records, access rules, and error paths are considered when relevant.
- Screenshots and demos use synthetic data; no secrets or generated build output enter the change.

These are review expectations for future development. Repository rules and branch protection must be configured separately to enforce review gates.
