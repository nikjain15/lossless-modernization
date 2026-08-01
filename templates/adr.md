# Architecture Decision Record (ADR) Template

**Exec summary.** An ADR is a one-page record of one architecturally significant decision: what was decided, in what context, and what it costs. Michael Nygard's five-section format (Title, Status, Context, Decision, Consequences) is the most widely adopted, used in roughly 723 public template repos, ahead of every alternative [adr.github.io](https://adr.github.io/), [ADR templates](https://adr.github.io/adr-templates/). In a modernization program ADRs matter double: the legacy system is largely the residue of decisions nobody wrote down, and you are about to make a hundred more. Number them, never delete them, supersede them.

**Produced in:** the Decide phase of the [artifact lifecycle](../playbook/README.md), and continuously whenever a significant decision lands.
**Owner:** the deciding architect or tech lead. **Signs off:** architecture review (Status moves from Proposed to Accepted).

## The template

```markdown
# ADR-<NNN>: <Short Noun Phrase Title>

## Status

<Proposed | Accepted | Deprecated | Superseded by ADR-<NNN>>
Date: <YYYY-MM-DD> | Deciders: <names>

## Context

<What forces are at play: technical constraints, business deadlines, team skills,
regulatory requirements. Neutral language. A reader in three years should
understand why this was hard.>

## Decision

<One decision, stated in the active voice: "We will ...">

## Consequences

<Everything that becomes easier, harder, or newly required because of this
decision. Include the negative ones; an ADR with only upsides is marketing.>
```

## Filled example

```markdown
# ADR-004: Strangle the Fee Engine Instead of Rewriting It

## Status

Accepted
Date: 2026-02-11 | Deciders: N. Jain, R. Chen, A. Okafor

## Context

The fee engine is 410k lines of COBOL processing $4.5B in daily trade flow.
The platform must leave the mainframe before hardware support ends. A full
rewrite was estimated at 30 months with no production value until the end,
and the business cannot accept a big-bang cutover after reviewing comparable
failures (TSB, 2018). The engine has no test suite; behavior is specified
only by its own output. Two SMEs who understand the batch flow retire within
two years. We evaluated: full rewrite with big-bang cutover, wholesale code
conversion (COBOL to Java transpilation), and incremental strangler fig
replacement behind a routing facade (Fowler, 2004:
https://martinfowler.com/bliki/StranglerFigApplication.html).

## Decision

We will replace the fee engine incrementally using the strangler fig pattern.
A routing facade will intercept fee-calculation requests; fee families migrate
one at a time to new services, each certified by a parity harness against
legacy outputs before it takes live traffic. Legacy remains the system of
record for any fee family not yet certified.

## Consequences

- Value ships incrementally: the first fee family can cut over in months,
  not at month 30, and each slice is individually rollback-able.
- Risk drops: every slice carries its own parity report; blast radius is one
  fee family, not the platform.
- We accept the cost of transitional architecture: the facade, dual-run
  infrastructure, and reconciliation jobs are throwaway work that must be
  built well anyway.
- Legacy and new run in parallel for 12+ weeks per slice; infrastructure
  spend rises during the transition and must be in the business case.
- The facade becomes a temporary single point of failure and needs its own
  runbook and capacity testing.
- Superseding note: if parity certification proves a fee family is simpler
  than believed, ADR-009 may authorize wholesale conversion for the tail.
```

## Conventions

1. **One decision per ADR.** If the Decision section contains "and," consider splitting.
2. **Immutable history.** Never edit an accepted ADR's decision; write a new one and mark the old Superseded. The trail is the value.
3. **Sequential numbering, one directory.** `docs/adr/NNN-title.md` in the program repo. The index is `ls`.
4. **Write it within a week of deciding.** ADRs reconstructed months later record what people wish they had thought.
5. **Link ADRs from the artifacts they shape.** The [wave plan](wave-plan.md) and [cutover runbook](cutover-runbook.md) should cite the ADRs behind their structure.

## Quality bar

- [ ] Title is a short noun phrase naming the decision, not the problem
- [ ] Status is one of the four values, with date and deciders
- [ ] Context is neutral: a person who opposed the decision would agree it is fairly stated
- [ ] Decision is one sentence of active voice before any elaboration
- [ ] Consequences include at least one genuine downside
- [ ] The file lives in the program repo under sequential number, in version control

Next: [rewrite vs strangle vs wrap](../decide/rewrite-vs-strangle-vs-wrap.md) | [templates index](README.md) | [business case](business-case.md)
