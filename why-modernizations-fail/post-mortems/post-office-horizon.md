# Post Office Horizon: When the Institution Defends the System

**Exec summary:** From 1999, the UK Post Office rolled out the Fujitsu-built Horizon accounting system to thousands of branches. When Horizon showed unexplained shortfalls, the Post Office treated its own subpostmasters as thieves: roughly 900 were wrongfully prosecuted over two decades, with imprisonments, bankruptcies, and suicides among the consequences [Computer Weekly](https://www.computerweekly.com/feature/Post-Office-Horizon-scandal-explained-everything-you-need-to-know). A statutory inquiry chaired by Sir Wyn Williams published Volume 1 of its final report on 8 July 2025, documenting the human impact and making 19 recommendations on redress [Post Office Horizon IT Inquiry, 2025](https://www.postofficehorizoninquiry.org.uk/reports-and-statements). This is not a migration failure; it is the definitive case of an organization trusting a system's output over evidence and people.

## By the numbers

| Metric | Value |
|---|---|
| Horizon rollout begins | 1999 |
| Wrongful prosecutions | ~900 |
| Years from rollout to full statutory inquiry report Volume 1 | 26 |
| Inquiry Volume 1 published | 8 July 2025 |
| Recommendations in Volume 1 | 19 |
| Illustrative human-impact case studies in Volume 1 | 17 |

## Timeline

| Year | Event |
|---|---|
| 1999 | Horizon rollout to Post Office branches begins (Fujitsu/ICL) [Computer Weekly](https://www.computerweekly.com/feature/Post-Office-Horizon-scandal-explained-everything-you-need-to-know) |
| 2000s | Subpostmasters report unexplained shortfalls; Post Office prosecutes based on Horizon data, roughly 900 in total [Computer Weekly](https://www.computerweekly.com/feature/Post-Office-Horizon-scandal-explained-everything-you-need-to-know) |
| 2009 | Computer Weekly first exposes subpostmasters' stories [Computer Weekly](https://www.computerweekly.com/feature/Post-Office-Horizon-scandal-explained-everything-you-need-to-know) |
| 2019 | High Court group litigation (Bates v Post Office) finds Horizon contained bugs, errors, and defects [Computer Weekly](https://www.computerweekly.com/feature/Post-Office-Horizon-scandal-explained-everything-you-need-to-know) |
| 2021 | Court of Appeal begins quashing convictions; statutory inquiry under Sir Wyn Williams gains full powers [Post Office Horizon IT Inquiry](https://www.postofficehorizoninquiry.org.uk/) |
| 2025 | Inquiry publishes Volume 1 of its final report on 8 July: human impact and redress, 19 recommendations, 17 illustrative case studies [Hansard, 2025](https://hansard.parliament.uk/Commons/2025-07-08/debates/25070846000011/PostOfficeHorizonInquiryReportVolume1) |

## What went wrong

- **System output treated as ground truth.** Horizon's balances were assumed correct; discrepancies were treated as postmaster theft or false accounting rather than as software defects to investigate [Computer Weekly](https://www.computerweekly.com/feature/Post-Office-Horizon-scandal-explained-everything-you-need-to-know).
- **Known defects, denied publicly.** Bugs that could corrupt branch accounts were known inside the Post Office and Fujitsu while prosecutions continued; the 2019 High Court judgment confirmed the system contained bugs, errors, and defects [Computer Weekly](https://www.computerweekly.com/feature/Post-Office-Horizon-scandal-explained-everything-you-need-to-know).
- **Prosecution instead of reconciliation.** The Post Office acted as investigator and prosecutor of its own staff, with no independent reconciliation of what the system reported against what actually happened in branches.
- **Single-supplier dependence.** Deep, decades-long dependence on one supplier for a mission-critical system weakened the Post Office's ability and willingness to challenge it (a core inquiry theme) [Post Office Horizon IT Inquiry](https://www.postofficehorizoninquiry.org.uk/).
- **The human cost.** Volume 1 of the inquiry's report documents wrongful prosecutions, ruined livelihoods, ill health, attempted suicides, and suicides among affected subpostmasters [Hansard, 2025](https://hansard.parliament.uk/Commons/2025-07-08/debates/25070846000011/PostOfficeHorizonInquiryReportVolume1).

## Root causes (taxonomy)

| Category | How it showed up |
|---|---|
| [8. Governance and accountability failure](../README.md#8-governance-politics-and-accountability-failure) | Institutional denial; the org prosecuted people rather than audit its system |
| [4. Testing and verification gaps](../README.md#4-testing-and-verification-gaps) | Account-corrupting defects shipped and persisted for years without independent verification |
| [9. Vendor and lock-in risk](../README.md#9-vendor-consultant-and-lock-in-risk) | Single-supplier dependence removed the incentive and capability to challenge system behavior |

## What would have prevented it

- **Independent reconciliation evidence.** A standing reconciliation process comparing system-reported balances against independent records, with every unexplained discrepancy logged as a system defect first and a people problem last. See [the parity pattern](../../patterns/06-parity.md) and the [parity report template](../../templates/parity-report.md), whose accepted-difference log exists precisely to force explanations.
- **A risk register that includes "the system is wrong."** Horizon-style failure requires that nobody with power ever asks the question. A [risk register](../../templates/risk-register.md) with an explicit "system integrity" risk, owned by someone independent of the vendor relationship, changes that.
- **Defect transparency across the org boundary.** Known-error databases shared between customer and supplier, with contractual disclosure duties. See [RACI template](../../templates/raci.md) for making that ownership explicit.

## Lessons checklist

- [ ] When our system and a human disagree, is our default to investigate the system or blame the human?
- [ ] Do we have reconciliation independent of the system being questioned?
- [ ] Can frontline staff report suspected system errors without personal risk?
- [ ] Does anyone outside the vendor relationship have authority to audit the vendor's defect list?
- [ ] Would we detect a bug that silently corrupts a small percentage of records? How?

## Sources

- [Computer Weekly, Post Office Horizon scandal explained](https://www.computerweekly.com/feature/Post-Office-Horizon-scandal-explained-everything-you-need-to-know)
- [Post Office Horizon IT Inquiry, reports and statements](https://www.postofficehorizoninquiry.org.uk/reports-and-statements)
- [Hansard, Post Office Horizon Inquiry Report Volume 1, 8 July 2025](https://hansard.parliament.uk/Commons/2025-07-08/debates/25070846000011/PostOfficeHorizonInquiryReportVolume1)
- [UK Government response to Inquiry Report Volume 1, 2025](https://www.gov.uk/government/publications/government-response-to-the-post-office-horizon-it-inquiry-report-volume-1)

**Next:** [The parity pattern](../../patterns/06-parity.md) | [Risk register template](../../templates/risk-register.md) | [Post-mortems index](README.md)
