# Templates: The Modernization Artifact Library

**Exec summary.** Every serious modernization framework, from AWS Migration Acceleration Program to the UK CDDO risk framework, converges on the same set of a dozen deliverables. Vendors ship them as Word documents behind sales calls; consultancies ship them as slideware. This library ships them as free, coherent, version-controllable markdown. Copy any file into your program repo, fill the angle-bracket placeholders, and you have the same artifact a tier-one program would produce. Artifacts are evidence, not paperwork: each one exists to answer a question an auditor, regulator, or sponsor will eventually ask.

## The library

| Template | What it is | Produced in phase ([lifecycle](../playbook/README.md)) | Owner | Signs off | Canonical industry source |
|---|---|---|---|---|---|
| [Application inventory](application-inventory.md) | Per-app register with 7R disposition and TIME quadrant | Inventory and Score | Portfolio lead / enterprise architect | Program sponsor | [AWS Prescriptive Guidance, 7Rs](https://docs.aws.amazon.com/prescriptive-guidance/latest/strategy-migration/overview.html); [Gartner TIME model](https://www.leanix.net/en/wiki/apm/gartner-time-model) |
| [Risk register](risk-register.md) | RAG-scored likelihood x impact register with legacy indicators | Score (maintained through all phases) | Program manager | Program sponsor / risk officer | [UK CDDO Legacy IT Risk Assessment Framework](https://gov.uk/government/publications/guidance-on-the-legacy-it-risk-assessment-framework/guidance-on-the-legacy-it-risk-assessment-framework) |
| [Business case](business-case.md) | Directional then detailed TCO, NPV, ROI, payback | Score and Decide | Finance partner + program sponsor | CFO and CTO | [AWS Application Portfolio Assessment guide](https://docs.aws.amazon.com/pdfs/prescriptive-guidance/latest/application-portfolio-assessment-guide/application-portfolio-assessment-guide.pdf) |
| [ADR](adr.md) | One-page architecture decision record, Nygard format | Decide (and continuously) | Deciding architect | Architecture review | [Nygard template via adr.github.io](https://adr.github.io/) |
| [Dependency map](dependency-map.md) | App, data, and integration dependency record with Mermaid graph | Map Dependencies | Enterprise architect / infra lead | Chief architect | [AWS Application Discovery Service, 2016](https://aws.amazon.com/about-aws/whats-new/2016/05/now-available-aws-application-discovery-service/) |
| [Wave plan](wave-plan.md) | Apps grouped into migration waves with entry and exit criteria | Plan Waves | Migration lead | Program manager | [AWS large-migration playbook, wave planning](https://docs.aws.amazon.com/prescriptive-guidance/latest/large-migration-portfolio-playbook/wave-planning.html) |
| [Characterization test plan](characterization-test-plan.md) | Feathers-style plan to pin current behavior before changing code | Build Parity Evidence | Tech lead | Engineering lead | [Working Effectively with Legacy Code, Feathers, 2004](https://www.goodreads.com/en/book/show/44919.Working_Effectively_with_Legacy_Code) |
| [Parity report](parity-report.md) | Reconciliation evidence: match rates, discrepancy log, accepted differences, sign-off | Build Parity Evidence | Parity / QA lead | Business, architecture, and engineering (all three) | [Google Cloud Dual Run](https://cloud.google.com/blog/products/infrastructure-modernization/dual-run-by-google-cloud-helps-mitigate-mainframe-migration-risks); [UK GDS dark launching](https://www.gov.uk/service-manual/technology/moving-away-from-legacy-systems) |
| [Cutover runbook](cutover-runbook.md) | Numbered, timestamped, owned steps with rollback trigger per step | Runbook the Cutover | Cutover lead | Program manager + business owner | [AWS cutover runbook guidance](https://docs.aws.amazon.com/prescriptive-guidance/latest/cutover-runbook/welcome.html) |
| [Rollback plan](rollback-plan.md) | Pre-agreed triggers, authority, outage window, reversal steps | Runbook the Cutover | Cutover lead | Business owner | [AWS pre-cutover best practices](https://docs.aws.amazon.com/prescriptive-guidance/latest/best-practices-migration-cutover/pre-cutover-stage.html) |
| [RACI](raci.md) | Workstream x role responsibility matrix | Plan Waves (program setup) | Program manager | Program sponsor | [AWS Prescriptive Guidance migration glossary](https://docs.aws.amazon.com/prescriptive-guidance/latest/migration-aws-environment/apg-gloss.html) |
| [Legacy knowledge map](legacy-knowledge-map.md) | Tribal-knowledge risk inventory and capture plan | Inventory (maintained through all phases) | Tech lead | Engineering manager | [UK CDDO framework, skills-scarcity indicator](https://gov.uk/government/publications/guidance-on-the-legacy-it-risk-assessment-framework/guidance-on-the-legacy-it-risk-assessment-framework) |

## How to use these

1. **Copy the file into your program repo.** Do not link to this repo from your program docs; vendor the file so it evolves with your program.
2. **Fill the `<angle-bracket placeholders>`.** Every table ships with one filled example row. Replace it or keep it as a worked reference, but delete it before sign-off.
3. **Keep artifacts under version control.** A risk register in a spreadsheet nobody diffs is decoration. A register in git shows who changed which score, when, and why. Reviews happen in pull requests.
4. **Treat artifacts as evidence, not paperwork.** Each template exists because a regulator, auditor, steering committee, or incident review will one day ask the question it answers. If a section costs effort and answers no question, delete it and record why.
5. **Sign-offs are named humans with dates.** "Approved by the business" is not a sign-off. "J. Rivera, Head of Settlements, 2026-03-14" is.

## Quality bar for the library

- [ ] Every template copied into a program repo is under version control from day one
- [ ] Every placeholder is either filled or explicitly marked n/a with a reason
- [ ] Every sign-off block contains a named person and a date, never a team name alone
- [ ] Each artifact links to the lifecycle phase that produced it

Next: [the artifact lifecycle](../playbook/README.md) | [choose your strategy](../decide/choose-your-strategy.md) | [why modernizations fail](../why-modernizations-fail/README.md)
