# California EDD: The Price of Never Modernizing

**Exec summary:** When pandemic lockdowns hit in March 2020, unemployment claims flooded California's Employment Development Department. Its decades-old COBOL-era claims systems and manual processes buckled: by September 2020 the backlog reached 1.6M claims, the call center answered only a fraction of calls, and fraud controls failed at catastrophic scale, with an estimated $20B paid to fraudsters [CalMatters, 2023](https://calmatters.org/economy/2023/11/california-unemployment-covid/); [CA State Auditor, 2021](https://information.auditor.ca.gov/reports/2020-128and628.1/responses.html). The state auditor found EDD had failed for years to prepare despite prior recession backlogs. Unlike the other cases in this series, the failure here was not a modernization attempt gone wrong. It was the bill for postponing one.

## By the numbers

| Metric | Value |
|---|---|
| Claim backlog at September 2020 | 1.6M |
| Estimated fraud losses | ~$20B |
| Months into the surge before substantive fraud-detection changes | ~4 (July 2020) |
| State auditor reports issued January 2021 | 2 (2020-128/628.1 and 2020-628.2) |
| Modernization program completed before the crisis | None |

## Timeline

| Date | Event |
|---|---|
| 2010s | EDD experiences backlogs in the prior recession; auditor later finds it failed for years to prepare for the next spike [CA State Auditor, 2021](https://information.auditor.ca.gov/reports/2020-128and628.1/responses.html) |
| Mar 2020 | Pandemic shutdown triggers an unprecedented claim surge; legacy systems and manual identity checks bottleneck immediately [CalMatters, 2023](https://calmatters.org/economy/2023/11/california-unemployment-covid/) |
| Jul 2020 | Governor appoints a strike team to assess EDD; auditor later notes EDD made no substantive fraud-detection changes until July 2020 [CalMatters, 2023](https://calmatters.org/economy/2023/11/california-unemployment-covid/) |
| Sep 2020 | Strike team assessment lands; claim backlog measured at 1.6M using the strike team's methodology [CalMatters, 2023](https://calmatters.org/economy/2023/11/california-unemployment-covid/) |
| Jan 2021 | State Auditor publishes reports 2020-128/628.1 and 2020-628.2 documenting systemic failures in preparation, claim processing, and fraud prevention [CA State Auditor, 2021](https://information.auditor.ca.gov/reports/2020-628.2/index.html) |
| 2021-2023 | Estimated fraud losses settle around $20B, mostly in the federally funded Pandemic Unemployment Assistance program [CalMatters, 2023](https://calmatters.org/economy/2023/11/california-unemployment-covid/) |

## What went wrong

- **A known-fragile system met a foreseeable shock.** Unemployment systems exist for recessions; surge is their core requirement. EDD's aging claims processing and workload systems could not scale, and the auditor found the agency had failed for years to prepare despite earlier backlog crises [CA State Auditor, 2021](https://information.auditor.ca.gov/reports/2020-128and628.1/responses.html).
- **Manual processes as the real bottleneck.** Claims that fell out of automation required manual identity verification and adjudication by a workforce that could not scale, producing the 1.6M-claim backlog [CalMatters, 2023](https://calmatters.org/economy/2023/11/california-unemployment-covid/).
- **Fraud controls sacrificed for throughput.** Under pressure to pay quickly, EDD relaxed and delayed fraud detection; the auditor found no substantive changes to fraud practices until July 2020, months into the surge. Estimated losses: around $20B [CalMatters, 2023](https://calmatters.org/economy/2023/11/california-unemployment-covid/); [CA State Auditor, 2021](https://information.auditor.ca.gov/reports/2020-128and628.1/responses.html).
- **The public paid twice.** Legitimate claimants waited months without income while fraudulent claims were paid at scale, the worst of both worlds and a direct consequence of having neither modern automation nor modern controls.

## Root causes (taxonomy)

| Category | How it showed up |
|---|---|
| [12. Cost of NOT modernizing](../README.md#12-the-cost-of-not-modernizing) | Deferred modernization converted a demand spike into a $20B loss and a humanitarian backlog |
| [1. Knowledge loss and undocumented logic](../README.md#1-knowledge-loss-and-undocumented-logic) | Decades-old COBOL-era systems with scarce staff who understood them limited emergency response options |
| [8. Governance failure](../README.md#8-governance-politics-and-accountability-failure) | Years of audit warnings without funded action |

## What would have prevented it

- **A business case that prices inaction.** The strongest argument for modernization funding is the quantified cost of the status quo under stress: surge scenarios, fraud exposure, staffing cliffs. See the [business case template](../../templates/business-case.md), which includes a cost-of-doing-nothing section for exactly this reason.
- **A readiness scorecard reviewed annually.** Scoring the estate against the [12 failure categories](../README.md), including surge capacity and knowledge concentration, turns "we know it's old" into a tracked risk with owners. See the [readiness scorecard](../../assessment/readiness-scorecard.md).
- **Incremental modernization of the choke points.** The bottlenecks (identity verification, claim intake) could have been strangled out of the legacy core years earlier without a full rewrite. See the [strangler fig pattern](../../patterns/02-strangler-fig.md) and [choose your strategy](../../decide/choose-your-strategy.md).
- **A knowledge map before the crisis.** Knowing exactly who understands which COBOL modules, and contracting that risk down, is cheap insurance. See the [legacy knowledge map template](../../templates/legacy-knowledge-map.md).

## Lessons checklist

- [ ] Have we quantified what a 10x demand spike does to our legacy estate, in money and hours?
- [ ] Which manual processes sit behind our automated front door, and what is their scaling limit?
- [ ] Do our fraud or integrity controls survive an emergency throughput mode, or get switched off?
- [ ] What did the last three audits warn about, and which warnings are still unfunded?
- [ ] If the modernization budget is denied this year, what risk did we just accept in writing?

## Sources

- [CalMatters, Internal documents reveal the story behind California's unemployment crash, 2023](https://calmatters.org/economy/2023/11/california-unemployment-covid/)
- [California State Auditor, Report 2020-128/628.1, EDD's poor planning and ineffective management, 2021](https://information.auditor.ca.gov/reports/2020-128and628.1/responses.html)
- [California State Auditor, Report 2020-628.2, EDD's fraud prevention failures, 2021](https://information.auditor.ca.gov/reports/2020-628.2/index.html)
- [Ways and Means Committee letter on EDD fraud, 2021](https://waysandmeans.house.gov/wp-content/uploads/2021/02/SFR-Nunes-CA-Delegation-Letter-to-CA-EDD.pdf)

**Next:** [Business case template](../../templates/business-case.md) | [Readiness scorecard](../../assessment/readiness-scorecard.md) | [Post-mortems index](README.md)
