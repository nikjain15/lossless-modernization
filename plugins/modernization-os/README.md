# Modernization OS

**A toolkit for modernizing systems that cannot be allowed to break.**

It works on your own repository. It reads your real code, writes real artifacts into a `modernization/` folder, and keeps a `STATE.md` that carries the program's memory across months and team changes. It is not a chatbot that answers questions and forgets.

Part of the [Lossless Modernization](https://nikjain15.github.io/lossless-modernization/) playbook. MIT licensed.

---

## What it does

| Skill | Ask it when | It produces |
|---|---|---|
| **modernize** | You want to start, or you are unsure what is next | `modernization/STATE.md`, and a route to the right skill |
| **assess-readiness** | Before committing to a date | `modernization/readiness.md`: twelve categories scored red, amber, green, with an owned action for every red |
| **review-plan** | You have a plan and want it stress-tested | `modernization/plan-review.md`: which documented public failure your plan resembles, and the line in your plan that creates the resemblance |
| **plan-cutover** | You are approaching go-live | `modernization/cutover-runbook.md` and `rollback-plan.md`, with a six-condition gate |

## Install

**As a plugin.** Add the marketplace, then install by name:

```
/plugin marketplace add nikjain15/lossless-modernization
/plugin install modernization-os
```

**Or copy the skills.** Clone the repo and copy the skill folders into your own project:

```bash
git clone https://github.com/nikjain15/lossless-modernization.git
cp -r lossless-modernization/plugins/modernization-os/skills/* your-project/.claude/skills/
```

Both give you the same thing. Copying lets you read and fork the instructions, which some people prefer for something that is going to review their architecture.

## Use it

Start broad and let it route:

> Help me modernize this system.

Or go straight to what you need:

> Review this modernization plan before I take it to the steering committee.
> Are we ready to commit to a go-live date?
> Write me a cutover runbook and rollback plan.

## What makes it different

**It judges, rather than generates.** Generic AI writes a plausible migration document. What it cannot do is tell you your cutover has TSB's shape, because it does not have a sourced library of documented failures to compare against. Every finding here points at a specific case with a cost and a source.

**It reads your estate, not just your plan.** Where the repository is available, it counts stored procedures, finds batch jobs, and looks for the two things plans routinely miss: **business rules living in spreadsheets and reports**, which no code-translation tool can see, and **components with no observable surface**, which cannot be verified by comparison because there is nothing to compare against.

**It remembers.** `STATE.md` records what was decided, by whom, and what is still open. A modernization runs for months and outlasts the people who started it. A stateless tool gives advice; this one accumulates a record.

**It will tell you no.** Five categories hard-block a committed date when red: knowledge of current behavior, data and semantic parity, evidence that the new system matches, cutover and reversibility, and accountability. Ask for a cutover runbook without correctness evidence and it will say plainly that a runbook for an unverified system is a schedule for an incident.

## Where the judgment comes from

The failure categories and the eight public post-mortems are sourced from official inquiries, regulatory findings and audit reports. Costs are given in dollars with the original currency in brackets.

Everything else, the readiness criteria, the go/no-go gate, the rollback design, the warning signs, comes from practice on a money-critical modernization program: a $1.6T asset-management platform moving $4.5B in trades a day, with a 12+ week production parallel run and 5,000+ business scenarios whose expected answers were agreed with the business up front.

## What is not built yet

The first release covers readiness, plan review and cutover. Still to come: estate mapping, strategy selection, legacy-code archaeology, parity harness design, and eval building. The `modernize` skill will tell you honestly when the right next step is not something it can do yet.

## Contributing

Corrections are worth more than additions. If a criterion here is wrong, or you have a failure worth adding to the library, see [CONTRIBUTING.md](../../CONTRIBUTING.md).
