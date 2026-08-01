# Business Case Template

**Exec summary.** Modernization business cases come in two passes, and confusing them kills programs. First a directional business case: two to four weeks, coarse as-is TCO versus to-be estimate, good enough to decide whether to fund detailed analysis [AWS directional business case](https://docs.aws.amazon.com/prescriptive-guidance/latest/application-portfolio-assessment-guide/directional-business-case.html). Then a detailed business case: NPV, ROI, payback period, and a 3-to-5-year cash flow, built app by app from the portfolio assessment [AWS Application Portfolio Assessment guide](https://docs.aws.amazon.com/pdfs/prescriptive-guidance/latest/application-portfolio-assessment-guide/application-portfolio-assessment-guide.pdf). The directional case buys permission to do the work that produces the detailed case. Do not spend six months polishing NPV before anyone has agreed the problem is worth solving.

**Produced in:** the Score and Decide phases of the [artifact lifecycle](../playbook/README.md).
**Owner:** program sponsor with a finance partner. **Signs off:** CFO and CTO.

## The template

```markdown
# Business Case: <program name>

Version: <x.y> | Date: <YYYY-MM-DD> | Owner: <name, role>
Stage: <Directional | Detailed> | Finance partner: <name>
Sign-off: CFO <name, date> | CTO <name, date>

# Part 1: Directional business case (2-4 weeks of effort, decision: fund detailed analysis or stop)

## Problem statement

<3 lines: what breaks, by when, and what it costs to do nothing.
Example: "Core settlement runs on hardware out of vendor support in <year>.
Two of three engineers who can change it retire within 24 months. Run cost
is $<n>M/yr and rising <n>% annually.">

## As-is annual TCO (coarse, order of magnitude)

| Cost line | Annual cost | Source / confidence |
|---|---|---|
| Infrastructure and hosting (incl. mainframe MIPS / licenses) | $2.1M | Finance actuals, high confidence |
| Vendor support and maintenance contracts | $<n> | <contract register / estimate> |
| Run team (FTEs x loaded cost) | $<n> | <HR data> |
| Incident and outage cost (last 12 months) | $<n> | <incident records x cost model> |
| Risk carry: out-of-support penalty, audit findings, cyber exposure | $<n> | <flag: estimated> |
| **Total as-is** | **$<n>** | |

## To-be estimate (range, not point)

| Scenario | One-time cost (range) | To-be annual run cost | Time to value |
|---|---|---|---|
| <e.g. Replatform + selective refactor> | $<low> to $<high> | $<n> | First wave live in <n> months |
| <alternative scenario> | $<low> to $<high> | $<n> | <n> months |
| Do nothing (baseline) | $0 | $<n, rising> | n/a; risk profile in risk register |

## Non-financial drivers

- <regulatory deadline, vendor end-of-support date, key-person risk, product velocity>

## Directional recommendation

<One paragraph: which scenario to investigate in detail, and what the
detailed analysis must resolve. Decision requested: fund <n> weeks of
detailed assessment at $<n>.>

# Part 2: Detailed business case (built after portfolio assessment)

## Assumptions register

| # | Assumption | Value | Source | Sensitivity if wrong |
|---|---|---|---|---|
| A-01 | Discount rate | 9% | Corporate finance standard | NPV swings $<n> per point |
| <A-nn> | <assumption> | <value> | <source> | <impact> |

## 5-year cash flow

| Line | Yr 0 | Yr 1 | Yr 2 | Yr 3 | Yr 4 | Yr 5 |
|---|---|---|---|---|---|---|
| One-time: build, migrate, dual-run infra, training | (4.2) | (3.1) | (1.0) | 0 | 0 | 0 |
| As-is run cost avoided (ramps with waves) | 0 | 0.8 | 2.4 | 4.0 | 4.2 | 4.4 |
| To-be run cost | 0 | (0.6) | (1.1) | (1.4) | (1.4) | (1.5) |
| Productivity / revenue effects (flag basis) | 0 | 0.2 | 0.9 | 1.5 | 1.8 | 1.8 |
| **Net cash flow** | **(4.2)** | **(2.7)** | **1.2** | **4.1** | **4.6** | **4.7** |
| Cumulative | (4.2) | (6.9) | (5.7) | (1.6) | 3.0 | 7.7 |

<All figures $M. Replace the example numbers; keep the line structure.>

## Headline metrics

| Metric | Value | Basis |
|---|---|---|
| NPV at <n>% discount rate | $<n>M | Cash flow above |
| ROI over 5 years | <n>% | (cumulative net / total invested) |
| Payback period | <n> months from program start | First cumulative-positive month |
| Dual-run premium | $<n>M over <n> months | Parallel-run infra and reconciliation effort, explicitly funded |

## Sensitivity

| Scenario | NPV impact |
|---|---|
| Migration takes 25% longer | $<n>M |
| Dual-run extends <n> extra months | $<n>M |
| Only <n>% of planned decommission savings land | $<n>M |

## Benefits realization

| Benefit | Owner | Measured by | Reported when |
|---|---|---|---|
| Legacy contract exit | <name> | Contract register | At each wave decommission |
| <benefit> | <name> | <metric> | <cadence> |
```

## Rules that keep the case honest

1. **Savings land when legacy is decommissioned, not when the new system goes live.** Dual-run periods cost double; put the premium in the case explicitly.
2. **Ranges in the directional case, sensitivities in the detailed case.** A single-point estimate at week 2 is fiction with a currency symbol.
3. **The do-nothing baseline is a rising line, not zero.** Out-of-support risk and skills scarcity compound; cross-reference the [risk register](risk-register.md).
4. **Name a benefits owner per line.** Benefits without owners are rounding errors waiting to be reallocated.

## Quality bar

- [ ] Directional case took weeks, not months, and ends with a single funding decision
- [ ] Every as-is cost line has a source; estimates are flagged as estimates
- [ ] Dual-run / parallel-run premium appears as its own funded line
- [ ] NPV, ROI, and payback all trace to the same cash-flow table
- [ ] Sensitivity table covers schedule slip and decommission shortfall
- [ ] Each benefit has a named owner and a measurement, tied to wave decommission dates

Next: [application inventory](application-inventory.md) | [wave plan](wave-plan.md) | [choose your strategy](../decide/choose-your-strategy.md)
