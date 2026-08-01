# Wave Plan Template

**Exec summary.** A wave plan groups applications into ordered migration waves so that dependencies move together, easy wins come early, and no wave is too large to roll back. AWS's large-migration playbook, the closest thing to an industry standard, groups waves by three forces: dependency (apps that call each other move together), priority (business urgency and deadlines), and similarity (same stack, same pattern, same team) [AWS large-migration playbook, wave planning](https://docs.aws.amazon.com/prescriptive-guidance/latest/large-migration-portfolio-playbook/wave-planning.html). Every wave has explicit entry criteria (you may start) and exit criteria (you may call it done). Wave 1 is deliberately small and low-risk: it exists to prove the machinery, not to deliver value.

**Produced in:** the Plan Waves phase of the [artifact lifecycle](../playbook/README.md), after the [dependency map](dependency-map.md) is credible.
**Owner:** migration lead. **Signs off:** program manager.

## The template

```markdown
# Wave Plan: <program name>

Version: <x.y> | Date: <YYYY-MM-DD> | Owner: <name, role>
Inputs: application inventory v<x.y>, dependency map v<x.y>
Grouping logic: dependency first, then priority, then similarity (AWS large-migration playbook).

## Wave summary

| Wave | Theme | Apps | Pattern(s) | Planned start | Planned cutover | Actual cutover | Status |
|---|---|---|---|---|---|---|---|
| 1 | Pilot: prove pipeline and runbook on low-risk apps | ReportViewer, FeeLookup | Rehost | <YYYY-MM-DD> | <YYYY-MM-DD> | <YYYY-MM-DD or n/a> | Done |
| <n> | <theme> | <app list> | <7R pattern(s)> | <date> | <date> | <date or n/a> | <Planned / In progress / Done> |

## Wave <n>: <theme>

**Apps in wave:** <list, with 7R disposition each>
**Why grouped:** <dependency cluster / shared stack / shared deadline>
**Dependencies on earlier waves:** <what must already be live>
**Dependencies held back:** <what stays on legacy and how the seam is bridged during the wave>

### Entry criteria (all must be true before wave starts)

- [ ] Exit criteria of wave <n-1> met and signed
- [ ] Landing zone / target environment ready and tested for this wave's stack
- [ ] Characterization tests or parity harness in place for each app in the wave
- [ ] Cutover runbook drafted per app; rollback plan agreed
- [ ] Wave team named and available; freeze windows booked with the business
- [ ] Open Red risks touching this wave have steering-committee acceptance

### Exit criteria (all must be true before wave closes)

- [ ] All apps cut over or consciously deferred with a recorded decision
- [ ] Parity report signed for each cutover app (match rate at or above target)
- [ ] Hypercare period (<n> days) completed with no Sev-1/Sev-2 attributable to the wave
- [ ] Legacy instances for this wave decommissioned or scheduled with a date
- [ ] Retro held; runbook and templates updated with lessons
- [ ] Actuals (dates, effort, incidents) recorded in this document

### Lessons carried forward

| From wave | Lesson | Change made |
|---|---|---|
| 1 | DNS TTL was 24h, delayed rollback test | TTL lowered to 300s two weeks before every cutover |
| <n> | <what surprised us> | <what we changed in the runbook or plan> |
```

## Sequencing rules that survive contact with reality

1. **Dependencies trump priority.** An urgent app that calls three unmigrated systems is not ready, whatever the sponsor says. Bridge the seam or move the cluster together.
2. **Wave 1 is a rehearsal.** Pick apps where failure is cheap. The AWS playbook uses early waves to calibrate estimates for later ones [AWS wave planning](https://docs.aws.amazon.com/prescriptive-guidance/latest/large-migration-portfolio-playbook/wave-planning.html).
3. **Cap wave size by rollback capacity, not ambition.** If you cannot revert every app in the wave inside the agreed outage window, the wave is too big.
4. **Similarity buys speed only after the pattern is proven.** Batch the twenty look-alike apps in a later wave, once the first of their kind is live.
5. **Replan after every wave.** A wave plan that never changes is a plan nobody is reading.

## Quality bar

- [ ] Every app in the inventory appears in exactly one wave, or in an explicit "not migrating" list with rationale
- [ ] Every wave has entry and exit criteria as checkboxes, not prose
- [ ] Wave 1 is small, low-risk, and explicitly labeled a pilot
- [ ] Cross-wave dependencies are named, with the bridging approach for each seam
- [ ] Actual dates are recorded next to planned dates; variance feeds the next replan
- [ ] The plan cites the inventory and dependency-map versions it was built from

Next: [cutover runbook](cutover-runbook.md) | [dependency map](dependency-map.md) | [application inventory](application-inventory.md)
