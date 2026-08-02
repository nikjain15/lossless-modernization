# Lidl SAP (eLWIS): The €500M Data-Model Mismatch

**Exec summary:** In 2011, Lidl launched eLWIS ("electronic Lidl merchandise management and information system") to replace its homegrown inventory system with SAP for Retail, deploying thousands of staff and hundreds of consultants [Consultancy.uk, 2018](https://www.consultancy.uk/news/18243/lidl-cancels-sap-introduction-having-sunk-500-million-into-it). Seven years later, in July 2018, Lidl cancelled the program and wrote off roughly €500M [Computer Weekly, 2018](https://www.computerweekly.com/news/252446965/Lidl-dumps-500m-SAP-project). The fatal flaw was semantic: Lidl's entire operation keyed inventory on purchase prices, SAP for Retail assumed retail prices, and Lidl chose to customize the product rather than change its process. The customization spiral consumed the program.

## By the numbers

| Metric | Value |
|---|---|
| Program start | 2011 |
| Program cancelled | July 2018 |
| Duration | 7 years |
| Amount written off | ~€500M |
| Working system delivered | None (reverted to its own legacy system) |
| Months between SAP "best customer" award and cancellation | ~15 |

## Timeline

| Date | Event |
|---|---|
| 2011 | eLWIS kicks off to replace Lidl's homegrown merchandise management system with SAP for Retail [Consultancy.uk, 2018](https://www.consultancy.uk/news/18243/lidl-cancels-sap-introduction-having-sunk-500-million-into-it) |
| 2011-2017 | Hundreds of external consultants work the program; costs climb as customizations multiply [RetailDetail, 2018](https://www.retaildetail.eu/news/food/lidls-failed-it-project-cost-half-billion/) |
| Apr 2017 | SAP names Lidl one of its best customers, awarding the project a prize [Consultancy.uk, 2018](https://www.consultancy.uk/news/18243/lidl-cancels-sap-introduction-having-sunk-500-million-into-it) |
| Jul 2018 | Lidl cancels eLWIS, writes off ~€500M, and reverts to its own system [Computer Weekly, 2018](https://www.computerweekly.com/news/252446965/Lidl-dumps-500m-SAP-project) |

## What went wrong

- **One semantic mismatch, discovered too late to be cheap.** Lidl's stock management is based on purchase prices; SAP for Retail is built around retail prices. Adapting the software to Lidl's model proved brutally difficult, with costs increasing as several hundred consultants worked on it while efficiency decreased [Computer Weekly, 2018](https://www.computerweekly.com/news/252446965/Lidl-dumps-500m-SAP-project).
- **Customize-the-product instead of change-the-process.** Lidl declined to adapt its established processes to the standard software, so every process difference became bespoke code, and every bespoke change made upgrades and integration harder [RetailDetail, 2018](https://www.retaildetail.eu/news/food/lidls-failed-it-project-cost-half-billion/).
- **Sunk-cost momentum for seven years.** The program ran from 2011 to 2018 before leadership accepted the model mismatch was structural, not a solvable backlog item [Consultancy.uk, 2018](https://www.consultancy.uk/news/18243/lidl-cancels-sap-introduction-having-sunk-500-million-into-it).
- **External validation masked internal failure.** A year before cancellation, the project was receiving vendor awards, a reminder that vendor recognition is not delivery evidence [Consultancy.uk, 2018](https://www.consultancy.uk/news/18243/lidl-cancels-sap-introduction-having-sunk-500-million-into-it).
- **The ending.** Lidl walked away, wrote off around €500M, and continued developing its existing homegrown system instead [Computer Weekly, 2018](https://www.computerweekly.com/news/252446965/Lidl-dumps-500m-SAP-project).

## Root causes (taxonomy)

| Category | How it showed up |
|---|---|
| [3. Data migration and parity](../README.md#3-data-migration-and-parity) | Purchase-price vs retail-price semantics: the two systems disagreed about what "inventory value" means |
| [7. Scope and requirements](../README.md#7-the-rewrite-trap) | Refusal to adapt processes turned a product implementation into an unbounded custom build |
| [8. Governance failure](../README.md#8-governance-politics-and-accountability-failure) | Seven years of escalating spend before anyone stopped the program |

## What would have prevented it

- **A semantic parity check before contract signature.** Map the legacy system's core entities and their meaning (what a price is, when inventory is valued, how returns post) against the target product's data model. The mismatch here was discoverable in week one with a [legacy knowledge map](../../templates/legacy-knowledge-map.md) and an [application inventory](../../templates/application-inventory.md) that records semantics, not just system names.
- **An explicit adopt-vs-adapt decision.** "Change our process to fit the product" versus "change the product to fit us" is a strategy decision with known failure statistics, and it belongs in a written [ADR](../../templates/adr.md) reviewed by the board, not in a thousand individual customization tickets. See [rewrite vs strangle vs wrap](../../decide/rewrite-vs-strangle-vs-wrap.md).
- **Kill criteria in the business case.** A [business case](../../templates/business-case.md) with pre-agreed thresholds ("if customization exceeds X% of spend or the core model requires modification, stop and reassess") converts sunk-cost drift into a decision point.
- **Incremental proof.** Piloting one country or category end-to-end before scaling would have surfaced the price-model collision at a fraction of the cost. See the [wave plan template](../../templates/wave-plan.md).

## Lessons checklist

- [ ] Have we compared the legacy and target data models entity-by-entity for meaning, not just field mappings?
- [ ] Have we made an explicit, board-visible decision: adapt our processes or customize the product?
- [ ] Does the business case contain written kill criteria and customization budgets?
- [ ] Is there an end-to-end pilot slice that proves the model fits before we scale?
- [ ] Are we measuring delivery evidence (working reconciled slices) rather than activity or vendor praise?

## Sources

- [Computer Weekly, Lidl dumps €500M SAP project, 2018](https://www.computerweekly.com/news/252446965/Lidl-dumps-500m-SAP-project)
- [Consultancy.uk, Lidl cancels SAP introduction having sunk €500M into it, 2018](https://www.consultancy.uk/news/18243/lidl-cancels-sap-introduction-having-sunk-500-million-into-it)
- [RetailDetail, Lidl's failed IT project cost half a billion, 2018](https://www.retaildetail.eu/news/food/lidls-failed-it-project-cost-half-billion/)
- [Henrico Dolfing, Case study: Lidl's €500 million SAP debacle](https://www.henricodolfing.ch/en/case-study-12-lidls-e500-million-sap-debacle/)

**Next:** [The parity pattern](../../patterns/06-parity.md) | [Rewrite vs strangle vs wrap](../../decide/rewrite-vs-strangle-vs-wrap.md) | [Post-mortems index](README.md)
