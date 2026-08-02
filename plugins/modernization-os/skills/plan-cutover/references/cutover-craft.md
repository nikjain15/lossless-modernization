# Cutover craft

Everything here exists because a real program got it wrong at scale.

## Choosing the style

| Style | When it is defensible | What it costs | The failure it invites |
|---|---|---|---|
| **Incremental by population** | Almost always for money-critical systems. Move a subset of accounts, funds, customers or entities, prove it, expand | Slowest calendar, needs routing and dual-read plumbing | Very little. This is the default |
| **Parallel run then switch** | When outputs can be compared but traffic cannot be split | Runs two systems for weeks or months | Ending the run early under schedule pressure |
| **Phased by capability** | When the domain splits cleanly and boundaries are genuinely independent | Integration complexity while both halves live | Discovering the boundary was not clean after cutting |
| **Big bang** | When the system genuinely cannot be split and downtime is acceptable | One irreversible moment | TSB: 5.2 million customers, roughly $1.3B (£1B) |

Big bang is not always wrong. It is wrong when chosen for convenience rather than necessity. Push hard on whether the system truly cannot be split, because "it would be complicated" is not the same as "it is impossible".

## The gate

Cutover eligibility is not a date. Six conditions have to hold at once. This is the gate a
practitioner actually ran on a money-critical program, not a generic template.

1. **Parity threshold met.** Outputs reconcile at the required grain, with only documented,
   agreed differences remaining, at intermediate stages as well as final ones.
2. **Time in parallel served.** The slice has run alongside the legacy system long enough to
   have seen the rare cases: month-ends, period-ends, corporate actions, unusual days. A hard
   entry criterion, immune to schedule pressure, never a buffer to be compressed.
3. **Sign-off given, three ways.** Business owns the meaning of the numbers, architecture owns
   the design, engineering owns the delivery. Three signatures, three different kinds of risk.
4. **Defect position accepted.** An explicit rule on open defects: how many, at what severity,
   and **each one accepted by a named person**. This is precisely what TSB got wrong, going live
   with 4,424 of 34,671 defects open, and Queensland Health, going live with 2,422.
5. **Downstream readiness confirmed.** The consumers of the outputs, reports, downstream systems,
   operations and client-service teams, confirm they are ready. Not just the program team. A
   correct system that surprises its consumers still produces an incident.
6. **Rehearsal completed.** Both the cutover and the rollback have been rehearsed before the gate
   can pass. Not reviewed. Rehearsed.

If any one is missing, the slice is not eligible, regardless of how much the date matters.

## Why time in parallel cannot be compressed

The comparison usually looks clean soon after switch-on, because structural and obvious differences fall fast. What consumes the calendar is a stubborn long tail: rare states, period boundaries, records in conditions nothing creates anymore. A plan that assumes remaining work is proportional to the initial break count will declare victory around week three and be wrong.

Corollary for reporting: **raw break counts are a misleading progress metric**, because one rule difference can produce a hundred thousand breaks that all close at once. Track distinct unresolved root causes instead. That number is small, honest, and hard to game.

## Rollback

A rollback plan that has never been executed is a hypothesis. On the program this is drawn from,
three things made rollback real:

**Rehearsed before every cutover.** The reversal was executed on production-like data ahead of
each real switch. Not once at the start of the program: before each one.

**A route back by design, not a special procedure.** Because migration moved populations
incrementally, account and fund groups at a time, reverting meant changing routing for that
population rather than restoring a system. Structural reversibility beats a documented
procedure, because the mechanism is the same one used every day. If a plan's rollback is a
restore-from-backup, that is a different and much weaker thing.

**Objective, pre-agreed triggers.** Written thresholds that required no judgement in the moment,
with one named person able to call it.

The rest of a rollback plan follows from those:

- **Triggers** are objective. "Customer impact" is not a trigger. "More than N failed
  transactions in M minutes" is.
- **Authority** is one named person who can call it without convening anyone.
- **Window** is stated: how long after cutover rollback remains possible, and what ends it.
- **Data** is the hard part. What happens to records created in the new system during the
  window? Answer explicitly or the plan is decorative.

## The runbook

Every step has a number, an owner by name, an expected duration, a success check, and its own rollback trigger. Steps without success checks are wishes.

Structure that survives a bad night:

1. **Pre-cutover** (days before): freeze points, final reconciliation, sign-offs collected, rollback rehearsed, comms drafted
2. **Go / no-go** (hours before): all six gate conditions verified by name, decision recorded with a timestamp and who made it
3. **Cutover** (the window): numbered steps, each with owner, duration, success check, rollback trigger
4. **Verification** (immediately after): the specific checks that prove it worked, with expected values, not "confirm system is healthy"
5. **Stabilization** (days after): heightened monitoring, who is on call, what escalates, when the rollback window formally closes

## The tone to aim for

A good cutover is an anticlimax. If everything before it was done properly, the switch is a promotion of evidence rather than a leap of faith. When a plan reads as dramatic, the drama is usually standing in for missing evidence.

## Things that reliably go wrong

Observed in practice, not inferred. Check a plan against every one of these.

**1. Rollback never rehearsed.** The plan exists on paper and has never been executed, so nobody
knows whether it works or how long it takes. The most common fatal gap.

**2. No freeze on the legacy system.** Changes keep landing in the old system during the cutover
window, so the thing you reconciled against is no longer the thing you are switching from. Your
evidence silently expires while you are relying on it.

**3. Reconciliation stops at go-live.** Comparison is treated as a pre-cutover activity, so the
first divergence *after* the switch goes unnoticed because nobody is still comparing. The window
immediately after cutover is when you most need the harness running, and it is exactly when teams
turn it off.

**4. Known defects accepted with nobody named.** A count is agreed but no individual accepted each
one, so accountability for shipping them is diffuse. TSB went live with 4,424 of 34,671 open.
Queensland Health went live with 2,422.

**5. Downstream consumers find out late.** Reports, operations, support and clients discover the
change at the worst possible moment. A correct system that surprises its consumers still produces
an incident.

**6. One cutover team, no fresh shift.** The same exhausted people run the window, the
verification and the stabilization, so judgement degrades exactly when it matters most. Plan a
handover to rested people before the verification step, not after something goes wrong.

**7. The window has no defined end.** No stated time at which you stop and abort rather than
pressing on, so a slipping cutover runs into the business day by default. The decision to
continue past the window should be an explicit, named call, never a consequence of momentum.

**8. The team disperses the morning after.** No stabilization plan, so when the long tail arrives
in week two the people who understand it have moved on to something else.
