---
name: assess-readiness
description: Score a legacy modernization program's readiness 0 to 5 across twelve categories, combining evidence read from the codebase with a guided interview for what code cannot reveal. Use when the user is starting or considering a modernization, asks whether they are ready, wants a readiness assessment or maturity score, wants to know what is missing before committing to a date, or needs a baseline to show a steering committee.
---

# Assess modernization readiness

Score a program's readiness to modernize a system that cannot be allowed to break. The output is a scored baseline plus an owned action per weak category, written into their repository.

Two sources of truth, and they are not interchangeable:

- **The code** tells you the size and shape of the problem: how much undocumented logic exists, where rules hide, whether anything can currently be verified.
- **The people** tell you whether the organization can survive it: who is accountable, who signs correctness, whether the budget covers proving anything.

The categories that most often kill programs are the second kind, and they cannot be read from a repository. Never score them from inference.

## Before you start

Read `references/scorecard.md`. It defines the 0 to 5 scale, and per category what is readable from code versus what must be asked. Do not work from memory.

## Step 1: read the estate

Work in their repository and gather evidence. Record actual findings with numbers, not impressions.

- Stored procedures, functions, packages, triggers: how many, and how large is the biggest
- Batch jobs, schedulers, cron entries, JCL: what runs overnight, and in what order
- Tests over domain logic specifically, not overall coverage
- Any existing comparison, reconciliation, snapshot or characterization tests
- Spreadsheets, macros, `.xls*`, and user-built tools referenced from code or config
- Reports and their embedded queries
- Schema shape: size, flag and enum columns that imply branching, nullable columns carrying meaning
- Deployment and rollback tooling, feature flags, routing that could support incremental migration
- End-of-life runtimes and unsupported dependencies
- Contributor history: how concentrated is knowledge, and are those people still active

Two findings deserve their own callout because plans routinely miss them:

**Rules living outside the code.** Spreadsheets, macros and reports frequently hold real business logic. No code-translation tool can read a spreadsheet, so those rules disappear silently in a code-only migration. If you find them, name the files.

**Components with no observable surface.** A process with no screen, no report, and no output anyone inspects cannot be verified by comparison, because there is nothing to compare against. Building that observability is a prerequisite, not a nicety. Flag every such component you find.

## Step 2: interview for what code cannot show

Ask in small batches, not as a questionnaire.

**Open with this one.** A practitioner who has led these programs names it as the single
question that exposes an unready program fastest:

> **If your two most knowledgeable people left next month, what happens?**

It works because it tests comprehension without asking about comprehension. A ready program
answers with artifacts: extracted rules, characterization tests, a knowledge map. An unready
one answers with names, or with silence. Follow the answer wherever it goes before moving on.

Then, in rough priority order:

1. **Who is accountable if the numbers come out wrong?** One name, not a committee, and not the
   same person rewarded for shipping.
2. **Who can stop this program?**
3. **For your three most important outputs, who defines what correct means?**
4. **What evidence will you show at go-live, and who signs it? Would they sign it today?**
5. **Did the date come before the plan?** Ask it directly. A committed date that predates the
   scope is one of the three strongest predictors of failure.
6. **Does the budget include comprehension work, evidence infrastructure, parallel running, and the long tail?**
7. **How many populations move at once, and has rollback been rehearsed?**
8. **What are you deliberately not changing?**
9. **What does another year of the status quo cost?**

If the user cannot answer one, that is data. Score it accordingly and record it as an open question rather than guessing. Do not pad a score to be kind: an inflated baseline is worse than no baseline, because decisions get made against it.

## Step 3: score and write

Score all twelve, 0 to 5, each with the evidence behind it. Write to `modernization/readiness.md` and update `modernization/STATE.md` with the date, the red categories, and the open questions. Create both if absent.

```markdown
# Readiness assessment: <program name>

**Assessed:** <date> · **Estate inspected:** yes/partly/no · **Interview completed:** yes/partly

## The profile

| Group | Categories | Reds | Verdict |
|---|---|---|---|
| Understanding the old system | 01, 02 | | |
| Proving correctness | 03, 04 | | |
| Execution and architecture | 05, 07, 10 | | |
| Money, politics and people | 06, 08, 09 | | |
| The modern era | 11, 12 | | |

## Can you commit to a date?

<Direct answer. Any red in correctness (03, 04) or cutover (05) means no, whatever the total.>

## Scores

| # | Category | Score | Evidence | Smallest next action | Owner |
|---|---|---|---|---|---|

## What the estate showed

<Numbers found. Rules outside the code, with filenames. Components with no observable
surface. What could not be inspected.>

## The three reds to fix first

1. <Category, why first, the action, who owns it>
2.
3.

## Open questions

<Anything unanswered that would change a score, with who can answer it.>
```

## Rules

- **Never average the twelve.** Report the profile. One zero in correctness outweighs ten fives.
- **Every score cites evidence.** A finding from the code, or a direct answer from the interview. Never inference.
- **Never score 08 or 09 from the code.** Accountability and retained ownership are unreadable from a repository. Ask or leave unscored.
- **Every red gets an owned action**, not a reading recommendation.
- **Report what you could not check.** Distinguish "they have no tests" from "I could not find tests".
- **Do not flatter.** The point of a baseline is that it is uncomfortable and true.
- **No dashes in prose.** Use colons, commas, or periods.
