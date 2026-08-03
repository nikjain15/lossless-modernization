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

### 01. Knowledge of current behavior  ·  BLOCKING
**Read from code:** count of stored procedures, functions and triggers; the largest single unit; presence and coverage of tests over domain logic; age and density of comments; whether any specification document exists in the repo.
**Ask:** if your two most knowledgeable people left next month, what happens? Can anyone explain what the system does end to end? Is there a named person per subsystem?

**Green requires all four:**
1. **Captured in a form a non-engineer can review.** Not one engineer's mental model. A structured artifact a business stakeholder can read and confirm, because that is what makes ratification possible at all.
2. **Checked against the running system, not just the code.** Decades-old systems routinely behave differently from what the source appears to say, because of data state, job ordering, and configuration.
3. **Unknowns flagged explicitly rather than filled in.** Anything unexplainable is marked intent unknown and escalated, never quietly assumed. Those flags are the most valuable output, not a gap in it.
4. **Every rule ratified by whoever owns its meaning.** Business owners for policy, operators for observed behavior, long-tenured engineers for history. Signed, not merely discussed.

**Amber:** some of the above, or captured but unratified. **Red:** it lives in people's heads.

### 02. Access to the people who know
**Read from code:** contributor history and recency; how concentrated commits are in a few hands; how long since the busiest files were touched by anyone still active.
**Ask:** who are the two or three people you cannot do this without, and how much of their time do you actually have? Are they also needed elsewhere?

**Green requires all four:**
1. **Knowledge holders named per subsystem.** You can point at a person for each area of the estate, so gaps are visible rather than assumed covered.
2. **Their time committed in writing, not assumed free.** The scarce experts have allocated hours. They are usually also the people every other workstream needs, which is exactly what turns them into the bottleneck.
3. **Capture is underway, not planned.** Extraction of what they know is actively happening, so the program is not one resignation away from losing it.
4. **Attrition risk assessed per person.** Someone has asked, per individual, what happens if they leave and what that would cost, and written the answer down.

**Amber:** the people are known but their time is assumed rather than committed. **Red:** the critical path runs through individuals with no capture underway.

---

## Proving correctness

### 03. Data and semantic parity  ·  BLOCKING
**Read from code:** schema size and complexity; enum and flag columns that imply branching; nullable columns with business meaning; the presence of any reconciliation or comparison code.
**Ask:** for the three most important values your system produces, who defines what correct means? Has anyone checked that a field means the same thing in the target as in the source?

**Green requires all four:**
1. **Semantics documented per critical field.** What it means in the source and in the target, with any difference agreed and signed rather than discovered later. This is the Lidl failure: purchase price versus retail price, roughly $590M.
2. **A comparison mechanism exists and runs.** Not planned. Something running that compares values between old and new at a stated grain, producing output a person actually reads.
3. **Reconciled at every record, not sampled.** Every record at every level, including intermediate calculations, because two systems can agree on totals while disagreeing on everything underneath.
4. **The consuming layer is in scope.** Reports, spreadsheets and user-built tools are reconciled too, not assumed to follow from matching core values, because those consumers apply logic of their own.

**Amber:** a comparison exists but is sampled, core-only, or the semantics are undocumented. **Red:** validation means row counts.

### 04. Evidence that the new system matches  ·  BLOCKING
**Read from code:** any existing comparison harness, golden-master fixtures, snapshot tests, or characterization tests over the domain.
**Ask:** what evidence will you show, and who signs it? Would that person put their name on it today?

**Green requires all four:**
1. **Three named signatures: business, architecture, engineering.** Each owns a different kind of risk. Business owns what the numbers mean, architecture owns the design, engineering owns the delivery.
2. **Expected answers agreed with the business before running.** The scenario set and its expected answers are agreed up front, so a mismatch is a finding rather than a debate about what correct was supposed to be.
3. **Evidence produced on real production inputs over time.** Not curated test data. Real flow, long enough to have seen period-ends and unusual days, because the rare cases never appear in a test environment.
4. **Progress tracked as distinct unresolved root causes.** Not raw break counts: one rule difference can produce a hundred thousand breaks that all close at once. The honest number is small and hard to game.

**Amber:** testing exists but proves the new system works rather than that it matches. **Red:** UAT is the correctness gate.

---

## Execution and architecture

### 05. Cutover and reversibility  ·  BLOCKING
**Read from code:** deployment configuration; feature flags or routing that could support incremental migration; any rollback tooling; whether migrations are reversible.
**Ask:** how many populations move at once? Has the rollback been rehearsed on production-like data? Who can call the abort, and what triggers it?

**Green requires all four:**
1. **Migration is incremental by population.** Accounts, funds, customers or entities move in waves rather than everything at once, so no single moment is irreversible.
2. **Rollback rehearsed before every cutover.** Not once at the start of the program. Executed on production-like data ahead of each real switch.
3. **A route back by design, not a restore procedure.** Reverting is a routing change for that population, using the same mechanism used every day, rather than restoring a system from backup. Structural reversibility beats a documented procedure.
4. **Objective abort criteria with one named owner of the call.** Written thresholds requiring no judgement in the moment, and one person who can call it without convening anyone.

**Amber:** incremental with a documented but unrehearsed rollback. **Red:** one event, or rollback means restore from backup. This is the TSB shape, roughly $1.3B.

### 07. Scope discipline
**Read from code:** size of the estate; how much is being replaced versus wrapped; whether anything ships incrementally.
**Ask:** what are you deliberately not changing? What reaches production in the next quarter?

**Green requires:**
1. **An explicit written not-doing list.** What is deliberately unchanged is recorded, so scope creep becomes visible as a decision rather than as drift.

Incremental delivery is strongly desirable and is the structural defence against the rewrite trap, but it is treated here as a signal rather than a gate.

**Amber:** scope is bounded in conversation but not written down. **Red:** everything is in scope, and nothing reaches production for many quarters. FBI Virtual Case File: $170M scrapped, never deployed.

### 10. Target architecture justification
**Read from code:** current coupling and boundaries; whether the proposed boundaries follow the domain or the technology.
**Ask:** for each major architectural choice, what specific problem does it solve? What would you lose by not doing it?

**Green requires both:**
1. **Every architectural choice traces to a named constraint.** Each major decision names the specific problem it solves, so patterns are not adopted because they are current.
2. **The simpler option was considered and rejected on record.** An ADR showing the boring alternative was weighed, which is the practical guard against over-modernization.

**Amber:** the target is coherent but the reasoning lives in people's heads. **Red:** service boundaries follow the technology rather than the domain.

---

## Money, politics and people

### 06. Cost realism
**Read from code:** volume of logic to be understood, which is the usual source of underestimation.
**Ask:** does the budget include comprehension work, the evidence infrastructure, parallel running, and the long tail of rare cases? What is the contingency?

**Green requires all four:**
1. **The four usually-missing lines are costed.** Comprehension work, evidence infrastructure, parallel running, and the long tail of rare cases appear as budget lines, not absorbed into build effort.
2. **A named owner of the number.** One person accountable for the estimate, so it can be challenged and revised rather than treated as a given.
3. **Contingency stated as a figure.** An explicit percentage or amount agreed in advance, rather than discovered when it is needed.
4. **The cost of the status quo is in the same document.** The comparison is against doing nothing, not only between delivery options.

**Amber:** costed properly but with no contingency or no owner. **Red:** costed as build effort, with proving correctness invisible. Queensland Health: about $4M became past $900M.

### 08. Accountability  ·  BLOCKING  ·  never scorable from code
**Read from code:** nothing. This cannot be inferred from a repository. Ask, or leave unscored and flag it.
**Ask:** who is accountable if the numbers come out wrong? Who can stop the program? Is that the same person who is rewarded for shipping it?

**Green requires all four:**
1. **One named owner of correctness, separate from delivery.** A person, not a committee or a job title, accountable if the numbers come out wrong, and not the person rewarded for shipping on time.
2. **Stop authority independent of the delivery incentive.** Someone can halt the program whose own success is not measured by it going live. This is precisely what HealthCare.gov lacked, with no empowered integrator, and what Post Office Horizon lacked for two decades.
3. **Decision rights written down.** Who decides what, recorded, so it is not rediscovered under pressure at the worst possible moment.
4. **Testers and QA can block a release.** The people who see the evidence have the power to stop it. Queensland Health went live over tester objections, at roughly $900M.

**Amber:** an owner exists but shares the delivery incentive, or QA can raise concerns without blocking. **Red:** governance by committee, or correctness owned by whoever built it.

### 09. Retained ownership
**Read from code:** who wrote the recent domain logic, internal or vendor.
**Ask:** who will hold the domain knowledge and the test evidence at the end? Could you continue without your integrator?

**Green requires both:**
1. **You keep the domain knowledge and the evidence.** Internal ownership of the domain model and the parity evidence, so the capability does not leave with a vendor.
2. **You could continue without your integrator.** The concrete test of the above: if the supplier walked away next month, the program survives.

**Amber:** internal ownership is intended but the vendor currently holds the design or the evidence. **Red:** the integrator owns the target design, the test evidence, or the only people who understand the new system. Birmingham: roughly $24M (£19M) became roughly $180M+ (£144M+).

---

## The modern era

### 11. Discipline around AI use
**Read from code:** signs of generated code; whether generated output is covered by tests.
**Ask:** where are you using AI, and what verifies its output? Who ratifies a rule an agent recovered?

**Green requires both:**
1. **AI accelerates comprehension, humans ratify intent.** Agents recover what the code does; a human decides what it means and signs it. The agent never holds authority over what the logic should be.
2. **Anything AI replicates is proven by execution, not review.** Generated or translated output is verified by running it and comparing values, never by code review alone.

**Amber:** AI is used for comprehension but ratification is informal. **Red:** automated translation is the migration strategy, with review as the only check.

### 12. Cost of not acting
**Read from code:** end-of-life dependencies, unsupported runtimes, known vulnerabilities.
**Ask:** what does another year of the status quo cost, and what is the failure mode if load doubles?

**Green requires all four:**
1. **The status quo is quantified as a priced option.** Another year of doing nothing has a number attached, and it appears in the business case alongside the delivery options.
2. **A named failure mode under stress.** Someone has answered what breaks if load doubles or a peak arrives. California EDD had not, and met a pandemic.
3. **End-of-life dependencies tracked with dates.** Unsupported runtimes and libraries listed with the date support ends, so the deadline is external and undeniable.
4. **Reviewed on a cadence, not once.** Deferral compounds quietly, and the number from two years ago is always too low.

**Amber:** the risk is acknowledged but unpriced. **Red:** deferral is the implicit decision, with no stated consequence. California EDD: roughly $20B in fraud.

---

## Mapping red to an action

For every red, the report must state the smallest next action that would move it to amber. Not a
chapter to read: an action with an owner and a date. A scorecard that produces reading is a
diagnostic. A scorecard that produces owned actions is a tool.
