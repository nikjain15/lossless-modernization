---
name: readiness
description: Score a legacy modernization red, amber or green across twelve categories, combining evidence read from the codebase with a guided interview for what code cannot reveal. Use when anyone is considering, scoping or starting work on an old system: replacing or rewriting a legacy platform, coming off a mainframe or an end-of-life runtime, a core system replacement, or inheriting undocumented code. Also use when asked whether they are ready, for a readiness assessment, maturity score or gap analysis, what is missing before committing to a date, whether a date is defensible, or for a baseline to show a steering committee.
---

# Assess modernization readiness

Score a program's readiness to modernize a system that cannot be allowed to break. The output is a red, amber, green baseline plus an owned action for every red, written into their repository.

Two sources of truth, and they are not interchangeable:

- **The code** tells you the size and shape of the problem: how much undocumented logic exists, where rules hide, whether anything can currently be verified.
- **The people** tell you whether the organization can survive it: who is accountable, who signs correctness, whether the budget covers proving anything.

The categories that most often kill programs are the second kind, and they cannot be read from a repository. Never score them from inference.

Work in that order. Read the estate, score what the estate can settle, show them that much, and only then interview for the categories the code cannot reach. A program should see something real about its own system before it is asked ten uncomfortable questions.

## Before you start

Read `references/scorecard.md`. It defines the red, amber, green levels, the five categories that hard-block a date, and per category what is readable from code versus what must be asked. Do not work from memory.

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

## Step 2: score what the estate can settle, and show it

Before asking anything, score every category the code can genuinely settle, each with the finding behind it. Show that partial scorecard in the conversation, and be explicit about the rest: name each category you cannot score yet, and the question that would settle it.

This is the moment the assessment earns the interview. They see counts from their own repository, not a questionnaire.

Never stretch the code to cover a people category. `references/scorecard.md` says per category what is readable and what must be asked. Categories 08 and 09 in particular are never scorable from a repository. An unscored category is honest; an inferred one corrupts the baseline.

## Step 3: interview for what code cannot show

Ask only for what is still unscored, in small batches, not as a questionnaire.

**Open with this one.** It is the single question I have found exposes an unready program
fastest:

> **If your two most knowledgeable people left next month, what happens?**

It works because it tests comprehension without asking about comprehension. A ready program
answers with artifacts: extracted rules, characterization tests, a knowledge map. An unready
one answers with names, or with silence. Follow the answer wherever it goes before moving on.

Then, in rough priority order, whichever of these are still open:

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

If they stop answering partway, publish what you have. A scorecard with four categories marked "not assessed, needs an answer from the sponsor" is a usable baseline. A scorecard with four categories quietly guessed is not.

## Step 4: write the assessment

Show the draft in the conversation first. Nothing is written into their repository until they have read it and said yes. On a yes, write `docs/modernization/readiness.md` and update `docs/modernization/STATE.md` with the assessment date in history, any decision made along the way, and the open questions. Create both if absent. The scores and the reds stay in `readiness.md`: STATE.md points at it rather than copying it.

Where a real value is unknown, leave the placeholder and follow it with a suggestion marked as one, so a committee has something to argue with rather than a blank: `<owner: suggest the Head of Finance Operations, UNCONFIRMED>`. A suggestion is never written as a fact, and every one of them is repeated in the open questions.

```markdown
# Readiness assessment: <program name>

**Assessed:** <date> · **Estate inspected:** yes/partly/no · **Interview completed:** yes/partly

## Verdict

<One paragraph, plain English, before any table. What this program is ready for, what it is not
ready for, and the single thing most likely to hurt it. Written so that someone who reads only
this paragraph is not misled.>

## The profile

| Group | Categories | Reds | Verdict |
|---|---|---|---|
| Understanding the old system | 01, 02 | | |
| Proving correctness | 03, 04 | | |
| Execution and architecture | 05, 07, 10 | | |
| Money, politics and people | 06, 08, 09 | | |
| The modern era | 11, 12 | | |

## Can you commit to a date?

<Direct answer. Any red in 01, 03, 04, 05 or 08 means no, whatever the rest of the profile
looks like. Name which one blocks and what would clear it.>

## Scores

| # | Category | R/A/G | Evidence | Smallest next action | Owner |
|---|---|---|---|---|---|

## What the estate showed

<Numbers found. Rules outside the code, with filenames. Components with no observable
surface. What could not be inspected.>

## The three reds to fix first

1. <Category, why first, the action, who owns it>
2.
3.

## Open questions

<Anything unanswered that would change a score, with who can answer it. Every UNCONFIRMED
suggestion made above appears here too.>

---

*Produced with [Modernization OS](https://nikjain15.github.io/lossless-modernization/) v0.1.0 beta.*
```

## Rules

- **Never average the twelve.** Report the profile. One red in a blocking category outweighs ten greens.
- **Every score cites evidence.** A finding from the code, or a direct answer from the interview. Never inference.
- **Never score 08 or 09 from the code.** Accountability and retained ownership are unreadable from a repository. Ask, or leave unscored and say why. 08 is a blocking category, so an unscored 08 must be flagged, never quietly skipped.
- **Every red gets an owned action** with a name and a date, not a reading recommendation.
- **Blocking reds are stated first.** Categories 01, 03, 04, 05 and 08 block a committed date when red. Say so in the verdict paragraph, before anything else.
- **Suggestions are labelled.** Any value you supply rather than receive carries UNCONFIRMED and appears in the open questions. Never let a suggestion read as a finding.
- **Show before you write.** Draft in the conversation, write on approval.
- **Report what you could not check.** Distinguish "they have no tests" from "I could not find tests".
- **Do not flatter.** The point of a baseline is that it is uncomfortable and true.
- **No dashes in prose.** Use colons, commas, or periods.
