# The twelve failure categories

Every category below has killed real programs. Use them as a checklist against a user's plan: for each one, decide whether their plan addresses it, ignores it, or actively walks into it.

Scoring guidance per category: **covered** (the plan has a specific, named mechanism), **thin** (acknowledged but no mechanism), **absent** (not mentioned), **walking into it** (the plan does the thing that causes the failure).

---

## Understanding the old system

### 01. Nobody knows how it works
Decades of undocumented logic; original authors gone. The rules live in code that no living person can fully explain.

**Look for in their plan:** a named comprehension workstream with time and people attached, before build. Archaeology, characterization tests, or a knowledge-capture effort.

**Walking into it, any of these:**
- **Assess goes straight to build.** No step between assessment and construction for understanding what the system actually does, and no time or people named for it.
- **Existing documentation is treated as accurate.** Specs, data dictionaries or wikis cited as the source of truth with no step to verify them against the running system.
- **Comprehension is assigned to the build team as they go.** Understanding is expected to happen incidentally during development, so it is nobody's deliverable and has no date.
- **The vendor is expected to work it out.** The plan assumes an integrator or a tool will discover the rules, outsourcing the one thing you cannot afford to not own.

### 02. The people who knew have left
Skills cliff. The few remaining experts are also the people the rest of the program needs, so they become the bottleneck.

**Look for:** named people per subsystem, an attrition risk assessment, capture-before-they-leave activity, and SME time explicitly budgeted rather than assumed free.

**Walking into it, either of these:**
- **Critical path runs through one or two people with no capture.** The plan depends on named individuals and has no activity to extract what they know before they become unavailable.
- **SME time assumed free.** Experts appear as consulted but with no allocated hours, so their availability is a hope rather than a commitment. They are usually also needed by every other workstream.

---

## Proving correctness

### 03. The numbers do not match
Data migrates cleanly and quietly stops meaning the same thing. Semantic mismatch, not technical failure. Lidl wrote off roughly $590M (€500M) on a purchase-price versus retail-price assumption.

**Look for:** a reconciliation strategy naming the grain (every record, or sampled), and treatment of semantics as a workstream, not a mapping exercise.

**Walking into it, any of these:**
- **Data migration described as movement or transformation.** Extract, map and load, with no mention of whether a field still means the same thing afterwards.
- **Validation means row counts and totals.** Success defined as the right number of records arriving, which two systems can satisfy while disagreeing on every value underneath.
- **A package's assumptions are unchecked.** A product adopted without anyone verifying its data model against the legacy system's actual semantics. This is the Lidl mechanism exactly.
- **Reports and spreadsheets are out of scope.** Only the core is in the migration, so the consuming layer that applies its own logic is assumed to follow along.

### 04. We cannot prove it is right
Plenty of testing, no evidence anyone will sign. Testing that demonstrates the new system works, rather than that it matches.

**Look for:** an explicit definition of what "correct" means, who signs it, and what evidence they see. Parallel running, output comparison, agreed expected answers.

**Walking into it, any of these:**
- **UAT is the correctness gate.** Business users clicking through the new system is the evidence, rather than a comparison against what the old system produced.
- **No comparison against legacy at all.** Testing proves the new system works on its own terms, never that it agrees with the system it replaces.
- **Testing is the last phase.** Positioned after build, which makes it the compressible item when the date approaches. This is the HealthCare.gov mechanism.
- **Nobody is named as the signer.** Evidence will be produced but no individual accepts it, so no one is on the hook for the judgement.

---

## Execution and architecture

### 05. One weekend, no way back
Big-bang cutover with untested rollback. TSB moved 5.2 million customers in a single weekend at a cost of roughly $1.3B (£1B).

**Look for:** incremental migration by population or slice, a rehearsed rollback, and pre-agreed abort criteria with a named decision-maker.

**Walking into it, any of these:**
- **A single cutover date for everything.** One event moves the whole population, so there is no wave to learn from and no partial state to fall back to.
- **Rollback described as restore from backup.** A recovery procedure rather than a routing change, which means it has probably never been executed and will take unknown hours.
- **No rehearsal mentioned anywhere.** Neither the cutover nor the rollback is scheduled to be practised before the real thing.
- **No abort criteria, or no named owner of the call.** Nothing states what would make you stop, or who decides, so under pressure the default is always to press on.

### 07. Starting over never finishes
The rewrite trap. FBI's Virtual Case File scrapped $170M and never deployed.

**Look for:** incremental replacement with the legacy system live throughout, and value delivered before the end.

**Walking into it, either of these:**
- **A full rewrite with one delivery at the end.** Everything is replaced and nothing reaches production until the end, so there is no feedback and no partial value. The FBI Virtual Case File mechanism, $170M scrapped.
- **The legacy system is switched off before the new one is proven.** The plan retires the old system on a date rather than after evidence, which removes both the thing you compare against and the thing you fall back to. Once it is off, parity is unprovable and rollback is impossible.

### 10. Microservices you did not need
Over-modernization. Complexity added faster than value, then a quiet retreat to a monolith.

**Look for:** target architecture justified by a specific constraint, and an explicit decision about what is NOT being changed.

**Walking into it:**
- **Patterns named without the problems they solve.** The target lists microservices, events or a service mesh with no statement of which constraint each one addresses, which usually means they were chosen because they are current.

---

## Money, politics and people

### 06. It costs many times the estimate
Order-of-magnitude escalation. Queensland Health went from about $4M to past $900M (AU$6.2M to AU$1.2B+).

**Look for:** a cost model that includes the comprehension work, the evidence infrastructure, parallel running, and the long tail. A stated contingency.

**Walking into it:**
- **Costed as build effort only.** No budget line for comprehension, evidence infrastructure or parallel running, so the expensive half of the work is invisible until it arrives. Queensland Health: about $4M became past $900M.

### 08. Nobody owns the outcome
Accountability spread thin enough that no one can be wrong. Present in HealthCare.gov (no empowered integrator) and Post Office Horizon (institutional denial).

**Look for:** one named accountable owner, a decision-rights matrix, and a named person who can stop the program.

**Walking into it, any of these:**
- **Governance by committee.** A steering group is named as the decision-maker, which means no individual can be wrong and therefore no individual will stop it.
- **Correctness sign-off has no named person.** The plan says the business will sign off, or QA will approve, without naming who. A role is not an owner.
- **The delivery owner also owns correctness.** One person accountable both for shipping on time and for the numbers being right, so the incentive is to declare victory.
- **Nobody is named who can stop it.** No stop authority appears anywhere, so once it is moving there is no mechanism to halt it.

### 09. A vendor ends up owning your core
Handing away the capability you cannot buy back. Birmingham City Council went from £19M to £144M+ on an over-customized ERP.

**Look for:** retained internal ownership of domain knowledge and the parity evidence, plus exit terms.

**Walking into it:**
- **The integrator owns the design or the evidence.** The vendor holds the target architecture or the test evidence, so the capability leaves when they do. Birmingham City Council: £19M became £144M+.

---

## The modern era

### 11. What AI genuinely cannot do
Agents are strong at explaining legacy code, weaker at converting it reliably. Treating AI output as verified is the failure.

**Look for:** AI used for comprehension with human ratification, and execution-based verification of anything it generates.

**Walking into it:**
- **Automated translation as the migration strategy.** A tool or model converts the code and human review is the only check, with no execution-based comparison of outputs. Reading code cannot establish semantic equivalence; running it and comparing values can.

### 12. Doing nothing is a decision too
Deferral has a bill. California EDD's deferred COBOL estate met a pandemic load spike, contributing to roughly $20B in fraud.

**Look for:** the cost of inaction quantified alongside the cost of the program.

**Walking into it, any of these:**
- **The business case compares only delivery options.** Doing nothing never appears as a priced alternative, so the program is judged against other programs rather than against reality.
- **No failure mode named under stress.** Nobody has answered what breaks if load doubles or a peak arrives. California EDD had not, and met a pandemic: roughly $20B in fraud.
- **End-of-life dependencies untracked.** No list of unsupported runtimes with the date support ends, so the real deadline stays invisible.
- **The cost of waiting is never revisited.** Assessed once and left, when deferral compounds quietly and last year's number is always too low.

---

## How to report

Never report all twelve as equally weighted. Rank by **what would actually kill this specific program**, based on what the plan says. Three absent categories that compound (no comprehension work, no correctness definition, big-bang cutover) matter far more than eight thin ones.
