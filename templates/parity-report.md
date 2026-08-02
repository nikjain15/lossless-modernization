# Parity Report Template

**Exec summary.** The parity report is the artifact that earns the right to cut over. It is execution evidence that the new system produces the same outputs as the old one on the same inputs, at a defined grain, with every discrepancy explained and every accepted difference signed by a named business approver. This is the industry's converging practice under different names: UK GDS dark-launch comparisons [UK GDS, moving away from legacy systems](https://www.gov.uk/service-manual/technology/moving-away-from-legacy-systems), Google Cloud Dual Run's side-by-side parity certification [Google Cloud, Dual Run](https://cloud.google.com/blog/products/infrastructure-modernization/dual-run-by-google-cloud-helps-mitigate-mainframe-migration-risks), and Mechanical Orchard's transaction-by-transaction behavioral parity [Mechanical Orchard platform](https://www.mechanical-orchard.com/platform). AI can translate code; only execution-based parity evidence certifies it. No signed parity report, no cutover.

**Produced in:** the Build Parity Evidence phase of the [artifact lifecycle](../playbook/README.md), refreshed until the final pre-cutover run.
**Owner:** parity or QA lead. **Signs off:** business, architecture, and engineering. All three, by name.

## The template

```markdown
# Parity Report: <app / slice name>

Version: <x.y> | Reporting period: <YYYY-MM-DD> to <YYYY-MM-DD> | Owner: <name, role>
Verdict this period: <On track / At risk / Ready for cutover>

## 1. Scope

| Item | Value |
|---|---|
| Outputs compared | Daily fee statements, GL postings, advisor performance reports |
| Outputs explicitly out of scope | <output, and why, and where it is covered instead> |
| Grain of comparison | Per transaction and per account-day roll-up |
| Input population | 100% of production trade flow, <n> accounts, <date range> |
| Environments | Legacy prod vs new system on mirrored prod feed |

State the grain honestly. "Matches at month-end total" and "matches per transaction" are different claims; a total can match while every line is wrong twice.

## 2. Comparison method

| Item | Value |
|---|---|
| Method | <side-by-side batch diff / dark launch (new system shadow-serves, outputs compared, not returned) / full parallel run in production> |
| Duration to date | <n> weeks continuous (target: <n> weeks clean) |
| Comparison tooling | <harness name / repo link>, automated diff, tolerance rules versioned at <link> |
| Tolerance rules | Exact match except: rounding <n> decimal places on <fields>, timestamps ignored on <fields>. Every tolerance is listed; none are silent. |
| Run cadence | <every batch cycle / continuous> |

## 3. Match rate by output class

| Output class | Records compared | Match rate | Target | Trend vs last period | Status |
|---|---|---|---|---|---|
| Fee statements (per transaction) | 4,182,304 | 99.97% | 99.99% | +0.12 pts | Amber |
| <output class> | <n> | <%> | <%> | <+/- pts> | <G/A/R> |

## 4. Discrepancy log

Every mismatch gets a row. There are exactly three legitimate resolutions.

| ID | Description | Root cause | Resolution | Approver + date (if accepted difference) | Status |
|---|---|---|---|---|---|
| D-041 | Fee rounds down on legacy, half-up on new, for <edge case> | Legacy COBOL ROUNDED clause behavior | fix-new: match legacy rounding | n/a | Closed <YYYY-MM-DD> |
| D-042 | Legacy double-charges accounts closed mid-cycle | Confirmed legacy defect | fix-old-bug-with-signoff: new system keeps correct behavior; legacy defect formally acknowledged | R. Chen, Head of Fees, <YYYY-MM-DD> | Closed |
| <D-nnn> | <what differed, at what grain> | <root cause, not symptom> | <fix-new / fix-old-bug-with-signoff / accepted-difference> | <name, role, date or n/a> | <Open / Closed> |

Resolution definitions:
- fix-new: the new system is wrong; change it to match legacy.
- fix-old-bug-with-signoff: legacy is wrong; the new system is deliberately different, and the business signs that the legacy behavior was a defect.
- accepted-difference: both are defensible; the business chooses the new behavior and signs it.
Anything else ("known issue," "minor," "timing") is an open discrepancy wearing a costume.

## 5. Accepted-difference register

The permanent record of every intentional behavior change, carried into operations after cutover.

| ID | Behavior change | Business justification | Approver, role | Date | Communicated to |
|---|---|---|---|---|---|
| AD-007 | Statements now order line items by trade date, not entry date | Matches client expectation; entry-date order was an artifact of batch sequence | R. Chen, Head of Fees | <YYYY-MM-DD> | Client services, <ticket link> |
| <AD-nnn> | <difference> | <why it is right> | <name, role> | <date> | <who was told> |

## 6. Intermediate vs final parity

| Layer | What is compared | Match rate | Note |
|---|---|---|---|
| Final outputs (statements, postings, files) | <what> | <%> | The number that gates cutover |
| Intermediate results (calc steps, staging tables) | <what> | <%> | Diagnostic only; intermediate divergence with final parity is acceptable if explained |

Final-output parity is the contract. Intermediate parity is the debugging aid that tells you where final parity will break next.

## 7. Sign-off

Cutover eligibility requires all three signatures against a specific report version.

| Role | Name | Statement | Date |
|---|---|---|---|
| Business owner | <name, role> | Match rates and every accepted difference reviewed and approved | <YYYY-MM-DD> |
| Architecture | <name, role> | Comparison method and tolerances are sound and complete | <YYYY-MM-DD> |
| Engineering | <name, role> | Harness results reproducible from tagged build <sha> | <YYYY-MM-DD> |
```

## Why this template is strict

The failure mode it prevents is specific: teams declare "testing complete" on sampled checks and green dashboards, then discover in production that legacy had undocumented behavior the business depended on. A parity report forces the uncomfortable list of everything that does not match, and makes someone with business authority own each difference in writing. Twelve-plus weeks of clean production parallel running across 5,000+ business scenarios is what this looked like on a $1.6T platform; the report format scales down to a single service.

## Quality bar

- [ ] Scope names the grain of comparison, and the grain matches the business's actual exposure
- [ ] Every tolerance rule is written down; zero silent tolerances in the diff tooling
- [ ] Match rates reported per output class, never one blended number
- [ ] Every discrepancy carries one of the three resolutions; no fourth category exists
- [ ] Every accepted difference has a named business approver and a date
- [ ] Sign-off block has all three roles, with names, against a specific version and build
- [ ] The harness run is reproducible: tagged code, versioned rules, archived inputs

Next: [characterization test plan](characterization-test-plan.md) | [cutover runbook](cutover-runbook.md) | [parity pattern deep-dive](../patterns/06-parity.md)
