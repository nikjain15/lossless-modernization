# Modernization Post-Mortems

**Exec summary:** Eight of the most instructive modernization and legacy-system failures of the last 25 years, written as engineering post-mortems: what was planned, what happened, what it cost, and which pattern in this playbook would have changed the outcome. Combined damage across these eight cases exceeds $5B in direct costs, plus one national miscarriage of justice and one municipal bankruptcy. Every fact is sourced; every root cause maps to the [12-category taxonomy](../README.md).

## The index

| Case | Org / Country | Year | Planned cost | Actual cost | What happened | Root-cause category | The pattern that would have helped |
|---|---|---|---|---|---|---|---|
| [TSB Bank](tsb-bank.md) | UK bank | 2018 | n/a (migration program) | ~£1B total damage | One-weekend big-bang migration of 5.2M customers locked customers out for weeks | 5. Cutover and big-bang risk | [Cutover strategy](../../decide/cutover-strategy.md), [parallel run with parity evidence](../../patterns/06-parity.md) |
| [Post Office Horizon](post-office-horizon.md) | UK Post Office | 1999-2025 | N/A (rollout) | £1B+ redress, ~900 wrongful prosecutions | Institution prosecuted its own staff rather than admit system defects | 8. Governance and accountability | [Parity and reconciliation evidence](../../patterns/06-parity.md), [risk register](../../templates/risk-register.md) |
| [Queensland Health](queensland-health.md) | AU state government | 2010 | AU$6.2M contract | AU$1.2B+ over 8 years | Payroll go-live with 2,422 known defects; 35,000 pay anomalies | 8. Governance; 4. Testing gaps | [Characterization test plan](../../templates/characterization-test-plan.md), [cutover strategy](../../decide/cutover-strategy.md) |
| [HealthCare.gov](healthcare-gov.md) | US federal | 2013 | $464M | $824M+ | Site crashed at launch; 6 enrollments on day one | 8. Governance (no integrator); 4. Testing gaps | [RACI with an empowered integrator](../../templates/raci.md), [cutover strategy](../../decide/cutover-strategy.md) |
| [Lidl SAP (eLWIS)](lidl-sap.md) | German retailer | 2011-2018 | N/A | ~€500M written off | Data-model mismatch (purchase vs retail prices) drove endless customization | 3. Data migration and parity; 7. Scope | [Parity thinking before build](../../patterns/06-parity.md), [rewrite vs strangle vs wrap](../../decide/rewrite-vs-strangle-vs-wrap.md) |
| [FBI Virtual Case File](fbi-virtual-case-file.md) | US federal | 2000-2005 | $170M component | $170M scrapped ($105M unusable code) | Big-bang rewrite with churning requirements, never deployed | 7. The rewrite trap | [Strangler fig](../../patterns/02-strangler-fig.md), [rewrite vs strangle vs wrap](../../decide/rewrite-vs-strangle-vs-wrap.md) |
| [Birmingham City Council](birmingham-oracle.md) | UK local government | 2022- | £19M | £144M+ (est. £216.5M by 2026) | Over-customized cloud ERP broke core accounting; contributed to effective bankruptcy | 8. Governance; 9. Vendor risk | [Rewrite vs strangle vs wrap](../../decide/rewrite-vs-strangle-vs-wrap.md), [risk register](../../templates/risk-register.md) |
| [California EDD](california-edd.md) | US state government | 2020 | N/A (deferred modernization) | ~$20B fraud + claim backlog crisis | Deferred COBOL-era modernization collapsed under pandemic load | 12. Cost of NOT modernizing | [Business case for acting](../../templates/business-case.md), [readiness scorecard](../../assessment/readiness-scorecard.md) |

## How to read these

Each post-mortem follows the same skeleton: exec summary, timeline, what went wrong (sourced), root causes mapped to the [taxonomy](../README.md), what would have prevented it (specific artifacts from this playbook), and lessons as a checklist you can apply to your own program this week.

Three themes repeat across all eight:

1. **Nobody had parity evidence.** No case had record-level reconciliation or behavior-equivalence proof before go-live. See [the parity pattern](../../patterns/06-parity.md).
2. **The go-live decision ignored the data.** Open defect counts, failed tests, and written warnings were all visible; governance overrode them. See [cutover strategy](../../decide/cutover-strategy.md).
3. **Rollback was an afterthought or impossible.** Big-bang designs removed the exit. See the [rollback plan template](../../templates/rollback-plan.md).

**Next:** [Why modernizations fail](../README.md) | [Cutover strategy](../../decide/cutover-strategy.md) | [The playbook lifecycle](../../playbook/README.md)
