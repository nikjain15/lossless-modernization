# The readiness rubric

Twelve categories, each scored red, amber or green. Every category states what can be read from code and what has to be asked, because the two are not interchangeable.

## Scoring: red, amber, green

Three levels, deliberately. Six invites arguing over whether something is a 3 or a 4, when the
only decision that matters is whether it blocks a date.

| Level | Meaning | The test |
|---|---|---|
| **Red** | No mechanism exists, or the mechanism would not survive contact with the failure. Often nobody owns it | Could this category fail tomorrow with nothing to catch it? |
| **Amber** | Owned and underway, or working in one place, but not proven across the estate | Does it exist and work, but only partly, or only in theory? |
| **Green** | Working, with evidence, and someone would put their name on it | Would a third party accept the evidence? |

**Five categories hard-block a committed go-live date if they are red**, regardless of how good
everything else looks:

| # | Category | Why it blocks |
|---|---|---|
| **01** | Knowledge of current behavior | If nobody can explain what the old system does, there is nothing to be correct against, so everything downstream is unverifiable |
| **03** | Data and semantic parity | If a field does not mean the same thing, matching values prove nothing |
| **04** | Evidence that the new system matches | If you cannot show it matches and get it signed, no date is defensible |
| **05** | Cutover and reversibility | Without a rehearsed route back, the consequence of being wrong is unbounded |
| **08** | Accountability | If nobody is named accountable for correctness and nobody independent can stop it, the gate is decorative however good the evidence is |

Report the profile, never a single summary score. A program green on ten categories and red on
two is not eighty-three percent ready. It is one bad weekend from being a case study.

## Understanding the old system

### 01. Knowledge of current behavior
**Read from code:** count of stored procedures, functions and triggers; the largest single unit; presence and coverage of tests over domain logic; age and density of comments; whether any specification document exists in the repo.
**Ask:** can anyone in the organization explain what the system does end to end? Is there a named person per subsystem? What happens if they leave next month?
**Green looks like:** current behavior is captured in a form a non-engineer can review, and it has been checked against the running system.

### 02. Access to the people who know
**Read from code:** contributor history and recency; how concentrated commits are in a few hands; how long since the busiest files were touched by anyone still active.
**Ask:** who are the two or three people you cannot do this without, and how much of their time do you actually have? Are they also needed elsewhere?
**Green looks like:** knowledge holders are named, their time is committed in writing, and capture is underway rather than planned.

---

## Proving correctness

### 03. Data and semantic parity
**Read from code:** schema size and complexity; enum and flag columns that imply branching; nullable columns with business meaning; the presence of any reconciliation or comparison code.
**Ask:** for the three most important values your system produces, who defines what correct means? Has anyone checked that a field means the same thing in the target as in the source?
**Green looks like:** semantics are documented per critical field, differences are agreed and signed, and a comparison mechanism exists.

### 04. Evidence that the new system matches
**Read from code:** any existing comparison harness, golden-master fixtures, snapshot tests, or characterization tests over the domain.
**Ask:** what evidence will you show, and who signs it? Would that person put their name on it today?
**Green looks like:** a comparison runs on real inputs, produces a reviewable report, and three named parties sign it.

---

## Execution and architecture

### 05. Cutover and reversibility
**Read from code:** deployment configuration; feature flags or routing that could support incremental migration; any rollback tooling; whether migrations are reversible.
**Ask:** how many populations move at once? Has the rollback been rehearsed on production-like data? Who can call the abort, and what triggers it?
**Green looks like:** migration is incremental, rollback is rehearsed, abort criteria are written and a named person owns the call.

### 07. Scope discipline
**Read from code:** size of the estate; how much is being replaced versus wrapped; whether anything ships incrementally.
**Ask:** what are you deliberately not changing? What reaches production in the next quarter?
**Green looks like:** an explicit not-doing list, and value in production within a quarter.

### 10. Target architecture justification
**Read from code:** current coupling and boundaries; whether the proposed boundaries follow the domain or the technology.
**Ask:** for each major architectural choice, what specific problem does it solve? What would you lose by not doing it?
**Green looks like:** every choice traces to a named constraint, and the simplest option was considered and rejected on record.

---

## Money, politics and people

### 06. Cost realism
**Read from code:** volume of logic to be understood, which is the usual source of underestimation.
**Ask:** does the budget include comprehension work, the evidence infrastructure, parallel running, and the long tail of rare cases? What is the contingency?
**Green looks like:** all four are costed as line items, with a stated contingency and a named owner for the number.

### 08. Accountability
**Read from code:** nothing. This cannot be inferred from a repository.
**Ask:** who is accountable if the numbers come out wrong? Who can stop the program? Is that the same person who is rewarded for shipping it?
**Green looks like:** one named accountable owner, decision rights written down, and a stop authority independent of the delivery incentive.

### 09. Retained ownership
**Read from code:** who wrote the recent domain logic, internal or vendor.
**Ask:** who will hold the domain knowledge and the test evidence at the end? Could you continue without your integrator?
**Green looks like:** internal ownership of the domain model and the evidence, with exit terms agreed.

---

## The modern era

### 11. Discipline around AI use
**Read from code:** signs of generated code; whether generated output is covered by tests.
**Ask:** where are you using AI, and what verifies its output? Who ratifies a rule an agent recovered?
**Green looks like:** AI accelerates comprehension, humans ratify intent, and execution-based comparison verifies anything replicated.

### 12. Cost of not acting
**Read from code:** end-of-life dependencies, unsupported runtimes, known vulnerabilities.
**Ask:** what does another year of the status quo cost, and what is the failure mode if load doubles?
**Green looks like:** the status quo is quantified as an option with a price, and it appears in the business case.

---

## Mapping red to an action

For every red, the report must state the smallest next action that would move it to amber. Not a
chapter to read: an action with an owner and a date. A scorecard that produces reading is a
diagnostic. A scorecard that produces owned actions is a tool.
