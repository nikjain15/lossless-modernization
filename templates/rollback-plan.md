# Rollback Plan Template

**Exec summary.** A rollback plan is the pre-agreed answer to "how do we get back," written and rehearsed before anyone needs it. AWS treats a rollback plan with an agreed outage window, trigger conditions, and reversal steps as a mandatory pre-cutover deliverable [AWS pre-cutover best practices](https://docs.aws.amazon.com/prescriptive-guidance/latest/best-practices-migration-cutover/pre-cutover-stage.html). The three things that turn a rollback from a disaster into a Tuesday: numeric trigger conditions decided in daylight, one named human with authority to call it, and a declared point of no return after which rollback stops being an option and forward-fix becomes the only path.

**Produced in:** the Runbook the Cutover phase of the [artifact lifecycle](../playbook/README.md), alongside the [cutover runbook](cutover-runbook.md).
**Owner:** cutover lead. **Signs off:** business owner (they own the outage window and the trigger thresholds).

## The template

```markdown
# Rollback Plan: <app / wave name>

Version: <x.y> | Date: <YYYY-MM-DD> | Owner: <name, role>
Paired cutover runbook: <link, version>
Rehearsed on: <YYYY-MM-DD> | Rehearsal result: <pass / issues, link>
Business sign-off: <name, role, date>

## Decision authority

| Role | Name | Authority |
|---|---|---|
| Rollback decision maker | M. Osei, Head of Trading Ops | Sole authority to invoke rollback; reachable on <phone> for the full window |
| <role> | <name> | <can recommend / can invoke / must be informed> |

One person invokes. Everyone else recommends. Write down who.

## Trigger conditions (any one is sufficient)

| # | Trigger | Threshold | Measured by | Auto-alert? |
|---|---|---|---|---|
| 1 | Transaction error rate on new system | > 0.5% of volume for 15 consecutive minutes | Dashboard <link>, alert <id> | Yes |
| 2 | Reconciliation break vs control totals | Any unexplained break > <amount / count> | Recon job <link> | Yes |
| 3 | Cutover overrun | Step <n> not verified by <hh:mm> | Runbook timestamps | No, cutover lead watches |
| <n> | <condition> | <numeric threshold, not "significant issues"> | <tool / query> | <yes/no> |

## Agreed outage window

- Maximum additional outage the business accepts for a rollback: <n> hours, agreed by <name> on <date>
- Rollback must therefore start no later than <hh:mm> to complete inside the window
- Blackout constraints: <market open, batch deadlines, regulatory cut-times>

## Reversal steps

| # | Step | Owner | Planned duration | Actual timestamp | Verification |
|---|---|---|---|---|---|
| 1 | Re-point routing to legacy (<flag / DNS / LB>) | <name> | 10 min | <hh:mm> | Legacy serving 100%; dashboard <link> green |
| 2 | Re-enable legacy schedulers and interfaces | <name> | 15 min | <hh:mm> | All feeds heartbeating |
| 3 | Quarantine transactions accepted by new system during the window | <name> | 30 min | <hh:mm> | Quarantine count matches gateway log count |
| <n> | <step> | <name> | <duration> | <hh:mm> | <observable check> |

## Data reconciliation after rollback

The hard part is never the routing switch; it is the transactions that landed on the new system while it was live.

- Capture window: every write to the new system between <cutover step> and <rollback step> is identified by <mechanism: CDC log, gateway journal, dual-write log>
- Replay or re-key: <how those transactions get into legacy: automated replay via <tool> / manual re-key by <team> with 4-eyes check>
- Reconciliation proof: control totals and row counts legacy vs captured set, signed by <business role> before the next business cycle opens
- Customer / user comms: <who is told what if any transaction is delayed or re-requested>

## Point of no return

**Declaration:** after <event, e.g. "the first overnight settlement batch completes on the new system" or "step 14 of the runbook">, rollback is no longer possible inside the agreed window. From that point the strategy is forward-fix under incident management.

- Declared by: <cutover lead name> during the window, announced on the bridge and logged
- Beyond it, the paired incident process is: <link to major-incident procedure>
- Business owner acknowledged this boundary at sign-off: <name, date>

## Post-rollback actions

- [ ] Comms sent per the runbook comms plan (pre-drafted rollback message)
- [ ] Incident review scheduled within <n> days; findings feed the parity report discrepancy log
- [ ] Root cause fixed and re-verified in the parity harness before a new cutover date is set
- [ ] This plan updated with actual durations from the rollback
```

## Quality bar

- [ ] Triggers are numeric thresholds, not adjectives
- [ ] Exactly one named person can invoke rollback, and they were reachable for the whole window
- [ ] The outage window was agreed by the business in writing before cutover night
- [ ] The rollback was rehearsed end to end, including the data reconciliation step
- [ ] The point of no return is a specific event, declared aloud and logged when passed
- [ ] Transactions captured on the new system have a defined path back to legacy

Next: [cutover runbook](cutover-runbook.md) | [parity report](parity-report.md) | [why modernizations fail](../why-modernizations-fail/README.md)
