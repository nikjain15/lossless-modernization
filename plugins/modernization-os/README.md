# Modernization OS

**A toolkit for modernizing systems to an AI-native platform. Without losing a cent.**

It installs into your repository, reads your actual code, and writes real artifacts into a `modernization/` folder. It keeps a `STATE.md` that carries the program's memory across months and team changes. It is not a chatbot that answers a question and forgets you.

Part of the [Lossless Modernization](https://nikjain15.github.io/lossless-modernization/) playbook. MIT licensed.

---

## Who this is for

You have just been handed a modernization of a system that cannot be allowed to break, and people are already asking for dates.

Or you have to defend a date, and you need to know whether it is defensible before you commit to it, in a form a steering committee will accept.

Or you have inherited decades of undocumented code, and you need to recover what the rules actually are before you touch anything.

## Why I built it

A playbook nobody runs changes nothing. Documents get read once, agreed with, and forgotten by the time the decisions are actually being made. What I wanted was the judgment available *inside* the program, at the moment someone is about to commit a date or sign off a cutover.

So the goal here is not more reading. It is to make modernization **simple and repeatable**, and **specific to your system** rather than general advice. Every question it asks is about your estate. Every artifact it writes is filled with your populations, your fields, your names, your open questions. General-purpose AI will happily write you a plausible migration plan for a system it has never looked at. That is the opposite of useful.

## What it does

| Skill | Ask it when | It produces |
|---|---|---|
| **modernize** | You are starting, or unsure what is next | `STATE.md`, and a route to the right skill |
| **assess-readiness** | Before committing to a date | `readiness.md`: twelve categories scored red, amber, green, with an owned action for every red |
| **review-plan** | You have a plan and want it stress-tested | `plan-review.md`: which documented failure your plan resembles, and the line in your plan that creates the resemblance |
| **plan-cutover** | You are approaching go-live | `cutover-runbook.md` and `rollback-plan.md`, behind a six-condition gate |

## What makes it different

**It arrives having read the autopsies.** Twelve failure categories and eight public failures with costs and sources, from TSB to Lidl to California EDD. So when it flags something, it does not say "this is risky". It says which program did this, what it cost, and the sentence in your plan that creates the resemblance. No general-purpose model can do that, because it has no library to compare you against.

**It checks the story against the system.** A plan is a story about a system. This reads the system: it counts your stored procedures, finds your batch jobs, and hunts the two things plans reliably miss. **Business rules living in spreadsheets and reports**, which no code-translation tool can see, so they vanish silently and nobody notices until a number drifts. And **components with no observable surface**, which cannot be verified by comparison because there is nothing to compare against.

**It outlives the people who start it.** These programs run for years and outlast the team that began them. `STATE.md` records what was decided, by whom, what is still open, what has been signed. Advice evaporates. A record accumulates.

**It can say no.** Five categories block a committed date when they are red: knowledge of current behavior, data and semantic parity, evidence that the new system matches, cutover and reversibility, and accountability. Ask for a cutover runbook with no correctness evidence and it will refuse, and tell you that a runbook for an unverified system is a schedule for an incident. A tool that always agrees with you is not a gate.

## Install

**As a plugin.** Add the marketplace, then install by name:

```
/plugin marketplace add nikjain15/lossless-modernization
/plugin install modernization-os
```

**Or copy the skills** into your own project:

```bash
git clone https://github.com/nikjain15/lossless-modernization.git
cp -r lossless-modernization/plugins/modernization-os/skills/* your-project/.claude/skills/
```

Both give you the same thing. Copying lets you read and fork the instructions first, which is reasonable for something about to review your architecture.

## Use it

Start broad and let it route:

> Help me modernize this system.

Or go straight to what you need:

> Review this modernization plan before I take it to the steering committee.
> Are we ready to commit to a go-live date?
> Write me a cutover runbook and rollback plan.

## Where the judgment comes from

The failure categories and the eight public failures are sourced from official inquiries, regulatory findings and audit reports. Costs are given in dollars with the original currency in brackets.

Everything else, the readiness criteria, the six-condition gate, the rollback design, the twenty-nine warning signs, comes from my own work: a $1.6T asset-management platform moving $4.5B in trades a day, a 12+ week production parallel run, and 5,000+ business scenarios whose expected answers were agreed with the business before anything ran.

## What is not built yet

This release covers readiness, plan review and cutover. Still to come: estate mapping, strategy selection, legacy-code archaeology, parity harness design, and eval building. The `modernize` skill will tell you honestly when the right next step is not something it can do yet.

## Contributing

Corrections are worth more than additions. If a criterion here is wrong, or you have a failure worth adding to the library, see [CONTRIBUTING.md](../../CONTRIBUTING.md).
