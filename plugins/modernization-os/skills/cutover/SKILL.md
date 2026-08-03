---
name: cutover
description: Produce a cutover runbook and rollback plan for a legacy modernization, with objective go/no-go gates, numbered owned steps, and rehearsed abort criteria. Use whenever a switchover from an old system to a new one is being planned or discussed: go-live, migration weekend, cutover, decommissioning the legacy system, moving customers or accounts or data across, big bang versus phased, parallel running, or a launch date for a replacement platform. Also use when a runbook, rollback plan, back-out plan or contingency plan is needed, or an existing cutover plan needs reviewing before a date is committed.
---

# Plan the cutover

Produce the two artifacts that decide whether a go-live is survivable: a runbook with numbered owned steps, and a rollback plan with rehearsed abort criteria. Written into their repository, reviewable by people who were not in the room.

This is the moment programs die. TSB moved 5.2 million customers in one weekend at a cost of roughly $1.3B (£1B). Queensland Health went live carrying 2,422 known defects because the old system was dying. Both hit their date.

## Before you start

Read `references/cutover-craft.md`. It covers style selection, the six-condition gate, why time in parallel cannot be compressed, rollback design, and the failures that recur. Do not work from memory.

## Step 1: establish the situation

Read `docs/modernization/STATE.md` and any existing plan, wave plan, or readiness assessment first. Do not ask for what is already written down.

Then establish, asking only what you cannot find:

- **What is moving**, and what stays. Populations, capabilities, or the whole system
- **Can traffic be split** by account, customer, entity, or region? This determines whether incremental is even available
- **What evidence exists** that the new system matches, and who has signed it
- **How long it has run in parallel**, and whether that period included period-ends and unusual days
- **Who can stop it**, by name
- **What downstream consumers exist**, whether they know, and whether they have confirmed readiness
- **The defect position**: how many are open, at what severity, and who has accepted each one
- **Whether the cutover and the rollback have been rehearsed**, and on what data
- **Whether the legacy system is frozen** during the window, or changes keep landing in it
- **Whether reconciliation continues after go-live**, or stops at the switch
- **Who runs verification and stabilization**, and whether they are the same exhausted people
- **When the window ends**, and who calls it if the cutover is slipping

If there is no comparison evidence at all, say so before going further. A runbook for an unverified system is a schedule for an incident. Offer to help design the evidence first.

## Step 2: challenge the style

If the plan is big bang, push on it once, properly. The question is not whether splitting would be complicated, it is whether it is genuinely impossible. Most big-bang cutovers are chosen for convenience and defended as necessity.

If it truly cannot be split, say so plainly and make the rollback correspondingly stronger. A defensible big bang needs a rehearsed rollback and a hard abort trigger, not optimism.

Record the choice and the reason. A style decision without a recorded reason gets relitigated at the worst possible moment.

## Step 3: define the gate

Six conditions, each written as an objective check with a named verifier. This is the gate I ran
on a $1.6T platform moving $4.5B in trades a day:

1. **Parity threshold**: what reconciles, at what grain, with which differences accepted and signed
2. **Time in parallel**: how long, and confirmation the period covered the rare cases
3. **Sign-off**: business, architecture, engineering, by name
4. **Defect position**: how many open defects are acceptable, at what severity, and each one
   accepted by a named person. Never a count alone
5. **Downstream readiness**: consumers of the outputs confirm they are ready, not just the program team
6. **Rehearsal**: both the cutover and the rollback have been rehearsed, not merely reviewed

Then write the go / no-go as something a person performs at a stated time, with the outcome
recorded. Not a meeting: a decision with a name and a timestamp attached.

Any condition that cannot be objectively verified is not a gate. Rewrite it until it can be.

## Step 4: write the artifacts

Show both drafts in the conversation first. Nothing is written into their repository until they have read them and said yes. On a yes, create `docs/modernization/cutover-runbook.md` and `docs/modernization/rollback-plan.md`, then update `docs/modernization/STATE.md`: record the cutover style as a decision, add the open questions, and add the drafting to history. The gate status lives in the runbook, and STATE.md points at it rather than copying it.

Where a real value is unknown, leave the placeholder and follow it with a suggestion marked as one, so the room has something to argue with rather than a blank: `<parity threshold: suggest 100% at trade level with a signed list of accepted differences, UNCONFIRMED>`. A suggestion is never written as a fact, it never fills a name, and every one appears in the open questions.

### Runbook

```markdown
# Cutover runbook: <what is moving>

**Style:** <incremental by population | parallel run then switch | phased | big bang>
**Why this style:** <one or two sentences, so nobody relitigates it at 2am>
**Window:** <date and time, timezone stated> · **Rollback window closes:** <when and why>

## Where this stands

<One paragraph, before any table. Whether the gate is currently met, what is outstanding, and
whether this cutover is safe to run on the stated date. Written so that someone who reads only
this paragraph is not misled.>

## Go / no-go

| Condition | How it is verified | Verified by | Status |
|---|---|---|---|
| Parity threshold met | | | |
| Time in parallel served | | | |
| Business sign-off | | | |
| Architecture sign-off | | | |
| Engineering sign-off | | | |
| Defect position accepted | | | |
| Downstream consumers ready | | | |
| Cutover rehearsed | | | |
| Rollback rehearsed | | | |

**Decision:** recorded by <name> at <timestamp>. Go / No-go.

## Pre-cutover (days before)

| # | Step | Owner | When | Success check |
|---|---|---|---|---|

## Cutover (the window)

| # | Step | Owner | Duration | Success check | Rollback trigger |
|---|---|---|---|---|---|

## Verification (immediately after)

| # | Check | Expected value | Owner | If it fails |
|---|---|---|---|---|

## Stabilization (days after)

| Day | Monitoring | On call | Escalation | Rollback still possible? |
|---|---|---|---|---|

## Communications

| Audience | What they are told | When | By whom |
|---|---|---|---|

---

*Produced with [Modernization OS](https://nikjain15.github.io/lossless-modernization/) v0.1.0 beta.*
```

### Rollback plan

```markdown
# Rollback plan: <what is moving>

## Where this stands

<One paragraph, before any table. Whether this rollback has been rehearsed, until when it is
actually possible, and what happens to data created after the switch. If any of the three is
unanswered, say that here rather than leaving it to be discovered in the tables.>

## Triggers

Objective and pre-agreed. No trigger may require judgement in the moment.

| Trigger | Threshold | Detected by | Automatic or manual |
|---|---|---|---|

## Authority

**<Name>** can call rollback without convening anyone. Deputy: **<name>**.

## Window

Rollback is possible until <point>. After that it is impossible because <reason, usually
that data exists only in the new system>.

## Data created after the switch

<What happens to it. Answer explicitly or this plan is decorative.>

## Reversal steps

| # | Step | Owner | Duration | Success check |
|---|---|---|---|---|

## Rehearsal

**Rehearsed on:** <date, on what data> · **Result:** <what happened, what was fixed>
**Not yet rehearsed:** <say so plainly if true. An unrehearsed rollback is a hypothesis.>

---

*Produced with [Modernization OS](https://nikjain15.github.io/lossless-modernization/) v0.1.0 beta.*
```

## Step 5: name what is missing

Close with the gaps, ranked. Be specific about which of the eight recurring failures in `references/cutover-craft.md` the current plan is exposed to, and what closes each one. Absence counts: a plan that says nothing about freezing the legacy system, continuing reconciliation after go-live, shift handover, or the end of the window is exposed to all four.

## Rules

- **Every step has an owner by name.** "The team" is not an owner.
- **Every step has a success check.** A step you cannot verify is a wish.
- **Objective triggers only.** "Significant customer impact" is not a trigger. A count over a window is.
- **Unrehearsed rollback must be labelled as such.** Never let a plan imply a rehearsal that did not happen.
- **Answer the data question.** What happens to records created after the switch, during the rollback window.
- **Never fill a name.** Owners, verifiers and the rollback authority are placeholders until a person says yes. A runbook that names the wrong person is worse than one that names nobody.
- **Thresholds and durations may carry a labelled suggestion.** Leave the `<placeholder>`, add a suggested value marked UNCONFIRMED, and list it as an open question. A suggestion gives the room something to argue with. A plausible invented value presented as agreed is dangerous.
- **Show before you write.** Draft both artifacts in the conversation, write on approval.
- **Never write a go decision.** You produce the gate; a human performs it.
- **No dashes in prose.** Use colons, commas, or periods.
