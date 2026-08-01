# Risk Register Template

**Exec summary.** A modernization risk register is a living, RAG-scored table of likelihood x impact, reviewed on a fixed cadence, with a named owner and a mitigation per risk. The UK Central Digital and Data Office standardized this for government legacy estates: score each risk 1-5 on likelihood and 1-5 on impact, multiply, and treat a score of 16 or above as red, requiring escalation [UK CDDO Legacy IT Risk Assessment Framework](https://gov.uk/government/publications/guidance-on-the-legacy-it-risk-assessment-framework/guidance-on-the-legacy-it-risk-assessment-framework). The register starts from the CDDO's seven legacy indicators, then grows with program-specific risks.

**Produced in:** the Score phase of the [artifact lifecycle](../playbook/README.md), maintained through every phase after.
**Owner:** program manager. **Signs off:** program sponsor or risk officer.

## The template

```markdown
# Risk Register: <program name>

Version: <x.y> | Date: <YYYY-MM-DD> | Owner: <name, role>
Review cadence: <weekly / fortnightly> | Next review: <YYYY-MM-DD>
Escalation rule: score >= 16 is Red and goes to <steering committee / sponsor> within <n> working days.

## Scoring

Likelihood 1-5 (1 = rare, 5 = almost certain) x Impact 1-5 (1 = negligible, 5 = severe).
RAG bands: 1-7 Green, 8-15 Amber, >= 16 Red (per UK CDDO convention).

## Register

| ID | Risk | Category | Likelihood (1-5) | Impact (1-5) | Score | RAG | Owner | Mitigation | Contingency if it fires | Status | Last reviewed |
|---|---|---|---|---|---|---|---|---|---|---|---|
| R-001 | Only two engineers can read the settlement batch COBOL; both eligible to retire in 2026 | Skills scarcity | 4 | 5 | 20 | Red | J. Rivera | Knowledge-capture sprints per the legacy knowledge map; pair every change | Contract retired SME on retainer; delay wave 3 | Open, escalated <YYYY-MM-DD> | <YYYY-MM-DD> |
| <R-nnn> | <risk statement: cause, event, consequence> | <category> | <1-5> | <1-5> | <LxI> | <G/A/R> | <name> | <action reducing likelihood or impact> | <pre-agreed plan B> | <Open / Mitigating / Closed> | <YYYY-MM-DD> |
```

## Starter checklist: the seven CDDO legacy indicators

The CDDO framework defines seven indicators of legacy risk [UK CDDO](https://gov.uk/government/publications/guidance-on-the-legacy-it-risk-assessment-framework/guidance-on-the-legacy-it-risk-assessment-framework). Seed the register by assessing each system in scope against all seven:

- [ ] Out-of-support software: any component past end of vendor support or public patching
- [ ] Expired or expiring contracts: supplier or licensing agreements lapsed or lapsing before program end
- [ ] Skills scarcity: knowledge concentrated in few people or a shrinking market (cross-reference the [legacy knowledge map](legacy-knowledge-map.md))
- [ ] Business-need mismatch: the system no longer meets the need it was built for
- [ ] Unsuitable hardware: hosting that cannot be maintained, scaled, or replaced
- [ ] Known vulnerabilities: unpatched CVEs or audit findings against the system
- [ ] Recent incidents: outages or data incidents attributable to the system in the last 12 months

Then add the program-execution risks that legacy indicators miss: cutover failure, parity gaps discovered late, dual-run cost overrun, key-vendor slippage, scope creep from "while we are in there" requests.

## Escalation rule

Any risk scoring 16 or above is Red and must be escalated to the steering committee within a fixed number of working days, with a decision recorded (accept, mitigate, transfer, or stop work). This mirrors the CDDO convention where a red rating triggers cross-government reporting [UK CDDO](https://gov.uk/government/publications/guidance-on-the-legacy-it-risk-assessment-framework/guidance-on-the-legacy-it-risk-assessment-framework). Do not tune the bands to keep the register green; tune the mitigations.

## Quality bar

- [ ] Every risk is a cause-event-consequence sentence, not a topic ("COBOL" is not a risk)
- [ ] Every risk has one named owner, never a team
- [ ] All seven CDDO indicators were assessed for every in-scope system, with n/a recorded where clean
- [ ] Red risks show an escalation date and a steering-committee decision
- [ ] The register is in version control and the review cadence is visible in the git history
- [ ] Closed risks stay in the file with closure rationale; they are evidence

Next: [legacy knowledge map](legacy-knowledge-map.md) | [rollback plan](rollback-plan.md) | [readiness scorecard](../assessment/readiness-scorecard.md)
