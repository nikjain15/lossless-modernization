# Cutover Runbook Template

**Exec summary.** A cutover runbook is the minute-by-minute script for moving production traffic from old to new: numbered steps, one owner per step, planned time, actual timestamp, success criteria, verification method, and a rollback trigger per step. AWS publishes cutover runbooks as a first-class deliverable with exactly this structure: activities, timeline, owners, and success criteria per step [AWS cutover runbook guidance](https://docs.aws.amazon.com/prescriptive-guidance/latest/cutover-runbook/welcome.html). The discipline is simple: if a step has no owner, no verification, and no trigger, it is not a step, it is a hope. The runbook is rehearsed at least once before the real night.

**Produced in:** the Runbook the Cutover phase of the [artifact lifecycle](../playbook/README.md), one per application or wave.
**Owner:** cutover lead. **Signs off:** program manager and business owner, before the rehearsal.

## The template

```markdown
# Cutover Runbook: <app / wave name>

Version: <x.y> | Cutover date: <YYYY-MM-DD> | Window: <start> to <end> (<timezone>)
Cutover lead: <name, phone> | Deputy: <name, phone>
Rollback decision authority: <name, role> (see rollback plan v<x.y>)
Bridge: <call link / channel> | Status page: <link>
Rehearsed on: <YYYY-MM-DD> | Rehearsal result: <pass / issues, link>

## Pre-cutover checklist (complete by T-24h)

- [ ] Parity report signed at target match rate (link: <parity report>)
- [ ] Rollback plan signed and rollback rehearsed end to end
- [ ] Full data backup taken and restore verified, not just taken
- [ ] Change freeze active on legacy from <date/time>
- [ ] Downstream and upstream system owners confirmed on the bridge or on call
- [ ] Comms drafted and pre-approved for: success, delay, rollback
- [ ] DNS TTLs / feature flags / routing weights pre-staged
- [ ] Go / no-go meeting held at T-<n>h; decision recorded: <Go / No-go, by name, time>

## Cutover steps

| # | Step | Owner | Planned (T+) | Actual timestamp | Success criteria | Verification method | Rollback trigger for this step |
|---|---|---|---|---|---|---|---|
| 1 | Stop inbound batch scheduler on legacy | A. Okafor | T+0:00 | <hh:mm or n/a> | Scheduler idle, zero in-flight jobs | Ops console shows 0 running; screenshot to bridge | In-flight jobs still running after 20 min |
| 2 | Final incremental data sync legacy to target | <name> | T+0:20 | <hh:mm> | Row counts and control totals match | Reconciliation script <link> output posted to bridge | Any control-total mismatch |
| 3 | Switch routing to target (<flag / DNS / LB weight>) | <name> | T+0:45 | <hh:mm> | Target serving 100% of traffic | Dashboard <link>: error rate < <n>%, p95 < <n> ms | Error rate > <n>% for 10 min |
| <n> | <action, one action per row> | <one name> | <T+h:mm> | <hh:mm> | <observable outcome> | <how verified, by what tool or query> | <condition that invokes the rollback plan> |

## Post-cutover verification (before declaring success)

- [ ] Business smoke tests passed, executed by business users, results linked
- [ ] First end-to-end business cycle (e.g. overnight batch, first settlement) reconciled against expectations
- [ ] Monitoring green for <n> hours; hypercare rota active for <n> days
- [ ] Success comms sent; legacy decommission date confirmed

## Comms plan

| Audience | Channel | Trigger | Message owner | Pre-drafted text |
|---|---|---|---|---|
| Ops and support teams | <channel> | Window open, window closed, any rollback | <name> | <link> |
| Business stakeholders | <email list> | Go decision, success, delay > <n> min, rollback | <name> | <link> |
| End users / advisors | <status page> | Only if user-visible impact | <name> | <link> |

## Decision log (filled live during the window)

| Time | Decision | Options considered | Decided by |
|---|---|---|---|
| <hh:mm> | <what was decided> | <what else was on the table> | <name> |
```

## Rules of the night

1. **One owner per step.** Two names means nobody.
2. **Actual timestamps are filled live.** The gap between planned and actual is the input to the next rehearsal.
3. **Rollback triggers are pre-agreed numbers, not judgment calls at 3 a.m.** The trigger fires, the [rollback plan](rollback-plan.md) executes, the debate happens tomorrow.
4. **Rehearse the whole runbook, including the rollback.** AWS treats testing the runbook before cutover as a baseline practice, not an option [AWS pre-cutover best practices](https://docs.aws.amazon.com/prescriptive-guidance/latest/best-practices-migration-cutover/pre-cutover-stage.html).
5. **The runbook is the single channel of truth.** If it happened and is not in the decision log, it did not happen.

## Quality bar

- [ ] Every step has exactly one named owner and a measurable success criterion
- [ ] Every step's verification names the tool, query, or dashboard used
- [ ] Every step has a rollback trigger, or an explicit "past point of no return" marker
- [ ] The pre-cutover checklist includes a verified restore, not just a backup
- [ ] A full rehearsal happened, with its date and result recorded in the header
- [ ] Comms for success, delay, and rollback were drafted before the window opened

Next: [rollback plan](rollback-plan.md) | [parity report](parity-report.md) | [cutover strategy](../decide/cutover-strategy.md)
