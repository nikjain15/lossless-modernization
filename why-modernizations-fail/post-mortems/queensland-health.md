# Queensland Health Payroll: A $6.2M Contract That Cost $1.2B

**Exec summary:** In March 2010, Queensland Health replaced its aging LATTICE payroll system with an SAP and Workbrain solution delivered by IBM. The system went live on 14 March 2010 after ten aborted attempts, carrying 2,422 known defects, and promptly failed to pay tens of thousands of health workers correctly, generating around 35,000 payroll anomalies [Commission of Inquiry, 2013](https://cabinet.qld.gov.au/documents/2013/aug/health%20payroll%20response/Attachments/Report.pdf). The original AU$6.2M contract ballooned to AU$181M in project cost and an estimated AU$1.2B over eight years to repair and operate, roughly 200x [Commission of Inquiry, 2013](https://cabinet.qld.gov.au/documents/2013/aug/health%20payroll%20response/Attachments/Report.pdf). Commissioner Richard Chesterman called it possibly the worst failure of public administration in Australia.

## By the numbers

| Metric | Value |
|---|---|
| Original IBM contract | AU$6.2M |
| End-of-project cost | AU$181M |
| Estimated 8-year repair and operating cost | AU$1.2B+ |
| Cost multiple vs original contract | ~200x |
| Aborted go-live attempts before launch | 10 |
| Known defects at go-live | 2,422 |
| Payroll anomalies generated | ~35,000 |

## Timeline

| Date | Event |
|---|---|
| 2007 | IBM contracted (via CorpTech) to replace the LATTICE payroll system with SAP ECC and Workbrain rostering; initial contract AU$6.2M [Wikipedia](https://en.wikipedia.org/wiki/2010_Queensland_Health_payroll_system_implementation) |
| 2008-2010 | Ten aborted go-live attempts [Commission of Inquiry, 2013](https://cabinet.qld.gov.au/documents/2013/aug/health%20payroll%20response/Attachments/Report.pdf) |
| 14 Mar 2010 | Go-live with 2,422 known defects; pay runs immediately fail for thousands of staff [Commission of Inquiry, 2013](https://cabinet.qld.gov.au/documents/2013/aug/health%20payroll%20response/Attachments/Report.pdf) |
| 2010-2012 | Roughly 35,000 payroll anomalies; armies of manual workarounds to pay nurses and doctors [Commission of Inquiry, 2013](https://cabinet.qld.gov.au/documents/2013/aug/health%20payroll%20response/Attachments/Report.pdf) |
| 13 Dec 2012 | Richard Chesterman AO RFD QC appointed to lead a Commission of Inquiry; hearings open 1 Feb 2013 [QHPSCI](http://www.healthpayrollinquiry.qld.gov.au/) |
| 31 Jul 2013 | Inquiry report delivered; state bans IBM from new government contracts [QHPSCI](http://www.healthpayrollinquiry.qld.gov.au/); [Wikipedia](https://en.wikipedia.org/wiki/2010_Queensland_Health_payroll_system_implementation) |

## What went wrong

- **The most complex payroll in the state, treated as an interim project.** Queensland Health's award rules spanned thousands of pay combinations across nurses, doctors, and support staff. The replacement was scoped as an "interim" LATTICE replacement, and requirements were never adequately defined or agreed [Commission of Inquiry, 2013](https://cabinet.qld.gov.au/documents/2013/aug/health%20payroll%20response/Attachments/Report.pdf).
- **Go-live despite known defects.** The system was implemented with 2,422 known defects after ten aborted attempts; business sign-off happened under pressure to escape the dying LATTICE system rather than on evidence of readiness [Commission of Inquiry, 2013](https://cabinet.qld.gov.au/documents/2013/aug/health%20payroll%20response/Attachments/Report.pdf).
- **No parallel run against the old system.** Pay results were not verified at scale against LATTICE output before cutover, so wrong payments were discovered by unpaid nurses instead of by reconciliation.
- **Procurement and governance failure.** The inquiry examined how the tender was won and varied, and found the contract and its management deeply flawed; the state's response restructured its entire IT program governance [Queensland Government response, 2013](https://cabinet.qld.gov.au/documents/2013/aug/health%20payroll%20response/Attachments/Response.PDF).
- **The verdict.** Chesterman: the project "must take a place in the front rank of failures in public administration in this country. It may be the worst" [Commission of Inquiry, 2013](https://cabinet.qld.gov.au/documents/2013/aug/health%20payroll%20response/Attachments/Report.pdf).

## Root causes (taxonomy)

| Category | How it showed up |
|---|---|
| [8. Governance failure](../README.md#8-governance-politics-and-accountability-failure) | Flawed procurement, unclear accountability between IBM, CorpTech, and Queensland Health |
| [4. Testing and verification gaps](../README.md#4-testing-and-verification-gaps) | 2,422 known defects at go-live; no at-scale verification of pay outcomes |
| [7. Scope and requirements](../README.md#7-the-rewrite-trap) | Requirements for the most complex payroll in the state never stabilized |
| [5. Cutover risk](../README.md#5-cutover-and-big-bang-risk) | Forced cutover because the legacy system was end-of-life, with no fallback |

## What would have prevented it

- **Characterization of the legacy payroll first.** Capture LATTICE's actual pay outputs across representative pay cycles as executable expectations before building. See the [characterization test plan template](../../templates/characterization-test-plan.md).
- **A parallel pay run as the go-live gate.** Run both systems for multiple full pay cycles and reconcile every payslip; go live only when differences are explained and accepted. See [the parity pattern](../../patterns/01-parity.md) and [parity report template](../../templates/parity-report.md).
- **An honest deadline decision.** LATTICE's end-of-life created forced-march pressure. A [cutover strategy](../../decide/cutover-strategy.md) decision made early, with the option to extend legacy support priced against the risk of premature go-live, changes the calculus.
- **Single accountable owner.** The three-way split between agency, shared-services body, and vendor diffused responsibility. See the [RACI template](../../templates/raci.md).

## Lessons checklist

- [ ] For payroll-like domains: have we captured the legacy system's actual outputs as test expectations?
- [ ] Is a full parallel run (multiple cycles, full population) a hard gate before cutover?
- [ ] Are we going live because the system is ready, or because the old one is dying?
- [ ] Can one named person answer for the whole delivery chain, including subcontractors?
- [ ] Do we know our real requirement complexity (award rules, edge cases) in numbers, not adjectives?

## Sources

- [Queensland Health Payroll System Commission of Inquiry, final report, 31 July 2013](https://cabinet.qld.gov.au/documents/2013/aug/health%20payroll%20response/Attachments/Report.pdf)
- [Commission of Inquiry site](http://www.healthpayrollinquiry.qld.gov.au/)
- [Queensland Government response to the inquiry, 2013](https://cabinet.qld.gov.au/documents/2013/aug/health%20payroll%20response/Attachments/Response.PDF)
- [Wikipedia, 2010 Queensland Health payroll system implementation](https://en.wikipedia.org/wiki/2010_Queensland_Health_payroll_system_implementation)

**Next:** [Characterization test plan](../../templates/characterization-test-plan.md) | [Cutover strategy](../../decide/cutover-strategy.md) | [Post-mortems index](README.md)
