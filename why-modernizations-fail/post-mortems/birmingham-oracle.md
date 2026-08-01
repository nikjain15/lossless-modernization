# Birmingham City Council: The ERP Migration Behind a City's Bankruptcy

**Exec summary:** In April 2022, Birmingham City Council, Europe's largest local authority, switched from its 20-year-old SAP system to Oracle Cloud Fusion. The system did not work properly from day one: core financial controls including bank reconciliation broke, leaving the council unable to produce auditable accounts [The Register, 2023](https://www.theregister.com/2023/09/05/birmingham_city_council_oracle/). The £19M business case has grown to an estimated £144M [The Register, 2026](https://www.theregister.com/2026/01/29/birmingham_oracle_latest/), with total programme cost projected at £216.5M by April 2026 [Data Center Dynamics, 2024](https://www.datacenterdynamics.com/en/news/total-cost-of-birmingham-citys-oracle-system-failure-to-reach-2165m-by-2026-report/). In September 2023 the council issued a Section 114 notice, effective bankruptcy, driven primarily by a £760M equal pay liability with the Oracle failure as a contributing factor [The Register, 2023](https://www.theregister.com/2023/09/05/birmingham_city_council_oracle/).

## By the numbers

| Metric | Value |
|---|---|
| Business-case budget | £19M |
| Implementation cost estimate (2026) | £144M |
| Projected total programme cost by April 2026 | £216.5M |
| Go-live | April 2022 |
| Section 114 (effective bankruptcy) notice | September 2023 |
| Months of inadequate disclosure to councillors | ~13 |

## Timeline

| Date | Event |
|---|---|
| 2019-2021 | Council approves replacing its heavily customized 20-year-old SAP estate with Oracle Cloud Fusion; business case around £19M [The Register, 2023](https://www.theregister.com/2023/09/05/birmingham_city_council_oracle/) |
| Apr 2022 | Go-live. The system does not work properly on day one and has already cost roughly twice the business case [Audit Reform Lab, 2024](https://auditreformlab.group.shef.ac.uk/downloads/bcc-report-4-08-24.pdf) |
| 2022-2023 | Bank reconciliation and other core accounting functions fail; manual workarounds proliferate; the scale of the problem is not adequately disclosed to councillors for about 13 months [Audit Reform Lab, 2024](https://auditreformlab.group.shef.ac.uk/downloads/bcc-report-4-08-24.pdf) |
| 5 Sep 2023 | Section 114 notice issued: the council is effectively bankrupt, citing the £760M equal pay liability, with Oracle costs compounding the crisis [The Register, 2023](https://www.theregister.com/2023/09/05/birmingham_city_council_oracle/) |
| 2024-2026 | Council plans a reimplementation of Oracle closer to out-of-the-box; cost estimates reach £144M and beyond, with £216.5M projected total by April 2026 [The Register, 2026](https://www.theregister.com/2026/01/29/birmingham_oracle_latest/); [DCD, 2024](https://www.datacenterdynamics.com/en/news/total-cost-of-birmingham-citys-oracle-system-failure-to-reach-2165m-by-2026-report/) |

## What went wrong

- **A SaaS product bent to legacy processes.** The council heavily customized Oracle Fusion to reproduce how its old SAP system worked instead of adopting standard processes. The customizations undermined the integrity of a product designed to run standard [The Register, 2023](https://www.theregister.com/2023/09/05/birmingham_city_council_oracle/).
- **Core financial controls broke and stayed broken.** Bank reconciliation, the control that proves cash matches the ledger, failed after go-live, degrading the council's ability to produce auditable accounts and detect fraud [The Register, 2023](https://www.theregister.com/2023/09/05/birmingham_city_council_oracle/); [Audit Reform Lab, 2024](https://auditreformlab.group.shef.ac.uk/downloads/bcc-report-4-08-24.pdf).
- **Governance did not hear the truth.** Escalating failures and costs were not adequately disclosed to the council's cross-party democratic structures for around 13 months after go-live [Audit Reform Lab, 2024](https://auditreformlab.group.shef.ac.uk/downloads/bcc-report-4-08-24.pdf).
- **Costs compounding years after go-live.** From £19M planned to £144M and a projected £216.5M by April 2026, including remediation and a reimplementation on standard configuration [The Register, 2026](https://www.theregister.com/2026/01/29/birmingham_oracle_latest/); [DCD, 2024](https://www.datacenterdynamics.com/en/news/total-cost-of-birmingham-citys-oracle-system-failure-to-reach-2165m-by-2026-report/).

## Root causes (taxonomy)

| Category | How it showed up |
|---|---|
| [8. Governance failure](../README.md#8-governance-politics-and-accountability-failure) | 13 months of inadequate disclosure; go-live without working financial controls |
| [9. Vendor and lock-in risk](../README.md#9-vendor-consultant-and-lock-in-risk) | SaaS product economics punished the customize-everything approach |
| [3. Data migration and parity](../README.md#3-data-migration-and-parity) | Old-system processes and data assumptions did not map onto the new platform, and nobody proved they did before cutover |

## What would have prevented it

- **Adopt-vs-adapt decided at the top, in writing.** Like Lidl, Birmingham customized a standard product to match legacy behavior. That choice needs an [ADR](../../templates/adr.md) and a governance gate, not accretion. See [rewrite vs strangle vs wrap](../../decide/rewrite-vs-strangle-vs-wrap.md).
- **Financial-control parity as a go-live gate.** No cutover while bank reconciliation is unproven. A [parity report](../../templates/parity-report.md) reconciling cash, ledger, and payroll outputs between SAP and Oracle for parallel periods would have blocked the April 2022 go-live.
- **A risk register councillors actually see.** RAG-scored risks with defined escalation to elected oversight would have shortened the 13-month disclosure gap. See the [risk register template](../../templates/risk-register.md).
- **Independent readiness assessment.** Scoring the program against known failure categories before go-live surfaces "core controls untested" as an automatic red. See the [readiness scorecard](../../assessment/readiness-scorecard.md).

## Lessons checklist

- [ ] Are we customizing a SaaS product to preserve legacy processes? Who signed that decision?
- [ ] Which financial controls (reconciliation, audit trail, segregation of duties) are proven working before cutover?
- [ ] Does bad news reach oversight bodies on a defined schedule, with penalties for burying it?
- [ ] What is our maximum tolerable cost multiple before we stop and reassess the approach?
- [ ] If the new system degrades our ability to close the books, what is the rollback position?

## Sources

- [The Register, Birmingham City Council goes under after Oracle disaster, 2023](https://www.theregister.com/2023/09/05/birmingham_city_council_oracle/)
- [The Register, Birmingham Oracle latest, 2026](https://www.theregister.com/2026/01/29/birmingham_oracle_latest/)
- [Audit Reform Lab (University of Sheffield), report on the Birmingham City Council Section 114 bankruptcy, 2024](https://auditreformlab.group.shef.ac.uk/downloads/bcc-report-4-08-24.pdf)
- [Data Center Dynamics, total cost to reach £216.5M by 2026, 2024](https://www.datacenterdynamics.com/en/news/total-cost-of-birmingham-citys-oracle-system-failure-to-reach-2165m-by-2026-report/)
- [Birmingham City Council, commissioners' statement on Section 114, 2023](https://www.birmingham.gov.uk/news/article/1664/commissioners_statement_on_section_114_declaration)

**Next:** [Rewrite vs strangle vs wrap](../../decide/rewrite-vs-strangle-vs-wrap.md) | [Risk register template](../../templates/risk-register.md) | [Post-mortems index](README.md)
