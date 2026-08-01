# RACI Template

**Exec summary.** A RACI matrix assigns Responsible, Accountable, Consulted, and Informed across the workstreams of a modernization program, and AWS Prescriptive Guidance lists it among the standard migration governance artifacts [AWS Prescriptive Guidance glossary](https://docs.aws.amazon.com/prescriptive-guidance/latest/migration-aws-environment/apg-gloss.html). The rule that makes it work: exactly one A per row. Modernization programs fail this test constantly, because legacy ownership is ambiguous by nature: the system predates everyone in the room. Writing the matrix forces the argument about who owns parity sign-off and who owns the rollback call to happen in a workshop instead of on cutover night.

**Produced in:** program setup, alongside the Plan Waves phase of the [artifact lifecycle](../playbook/README.md).
**Owner:** program manager. **Signs off:** program sponsor.

## The template

```markdown
# RACI: <program name>

Version: <x.y> | Date: <YYYY-MM-DD> | Owner: <name, role>
Sign-off: <sponsor name, date>

Legend: R = Responsible (does the work), A = Accountable (one per row, owns the outcome),
C = Consulted (two-way, before the fact), I = Informed (one-way, after the fact).

Roles: Sponsor = <name> | PgM = <name> | Chief Arch = <name> | Eng Lead = <name> |
Biz Owner = <name> | QA/Parity Lead = <name> | Ops Lead = <name> | Sec/Risk = <name> | Vendor = <firm, name>

| Workstream / decision | Sponsor | PgM | Chief Arch | Eng Lead | Biz Owner | QA/Parity Lead | Ops Lead | Sec/Risk | Vendor |
|---|---|---|---|---|---|---|---|---|---|
| Application inventory and scoring | I | A | R | C | C | I | C | C | R |
| 7R disposition per application | I | C | A | C | C | I | I | C | C |
| Business case (directional and detailed) | A | R | C | I | C | I | I | C | I |
| Risk register upkeep and escalation | I | A | C | C | C | I | C | R | I |
| Dependency mapping | I | C | A | R | I | I | R | I | C |
| Wave plan and sequencing | C | A | R | C | C | I | C | I | C |
| Characterization test suites | I | I | C | A | I | R | I | I | R |
| Parity harness build and runs | I | I | C | R | C | A | I | I | C |
| Accepted-difference approval | I | I | C | I | A | R | I | I | I |
| Cutover runbook and rehearsal | I | C | C | R | C | C | A | C | C |
| Go / no-go decision | C | A | C | C | C | C | C | C | I |
| Rollback invocation during cutover | I | I | I | C | A | C | R | I | I |
| Legacy decommissioning | I | A | C | R | C | I | R | C | I |
| ADR approval | I | I | A | R | C | I | I | C | I |
| Knowledge capture (legacy knowledge map) | I | C | C | A | I | I | C | I | I |
| <workstream or decision> | <R/A/C/I> | <...> | <...> | <...> | <...> | <...> | <...> | <...> | <...> |
```

The letters above are a worked starting point, not gospel: keep the rows, argue about the letters in a workshop, and record what your program actually agrees. The two rows most worth the argument are accepted-difference approval (the business must hold the A, see [parity report](parity-report.md)) and rollback invocation (one A, pre-agreed, see [rollback plan](rollback-plan.md)).

## Rules

1. **One A per row, no exceptions.** Two As is zero As.
2. **A is a person via a role, not a committee.** Committees advise; a name decides.
3. **R without capacity is fiction.** If the Eng Lead is R on six concurrent rows, the matrix is a wish list; check against the wave plan timeline.
4. **C means before, I means after.** A stakeholder who finds out at the steering committee was I, whatever the matrix says; fix the matrix or the behavior.
5. **Revisit at every wave boundary.** Vendors roll off, teams rotate; a stale RACI is worse than none because it looks authoritative.

## Quality bar

- [ ] Every row has exactly one A
- [ ] Every role column maps to a named person in the header block
- [ ] Accepted-difference approval and rollback invocation rows exist and were explicitly debated
- [ ] The matrix was built in a workshop with the people named in it, not drafted and circulated
- [ ] Review date is set at the next wave boundary
- [ ] Vendor responsibilities match the contract's statement of work

Next: [wave plan](wave-plan.md) | [rollback plan](rollback-plan.md) | [templates index](README.md)
