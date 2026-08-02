# The twelve failure categories

Every category below has killed real programs. Use them as a checklist against a user's plan: for each one, decide whether their plan addresses it, ignores it, or actively walks into it.

Scoring guidance per category: **covered** (the plan has a specific, named mechanism), **thin** (acknowledged but no mechanism), **absent** (not mentioned), **walking into it** (the plan does the thing that causes the failure).

---

## Understanding the old system

### 01. Nobody knows how it works
Decades of undocumented logic; original authors gone. The rules live in code that no living person can fully explain.

**Look for in their plan:** a named comprehension workstream with time and people attached, before build. Archaeology, characterization tests, or a knowledge-capture effort.
**Walking into it:** a plan that goes from "assess" to "build" with no step for understanding current behavior, or one that assumes existing documentation is accurate.

### 02. The people who knew have left
Skills cliff. The few remaining experts are also the people the rest of the program needs, so they become the bottleneck.

**Look for:** named people per subsystem, an attrition risk assessment, capture-before-they-leave activity, and SME time explicitly budgeted rather than assumed free.
**Walking into it:** a plan whose critical path depends on one or two named individuals with no capture plan.

---

## Proving correctness

### 03. The numbers do not match
Data migrates cleanly and quietly stops meaning the same thing. Semantic mismatch, not technical failure. Lidl wrote off roughly $590M (€500M) on a purchase-price versus retail-price assumption.

**Look for:** a reconciliation strategy naming the grain (every record, or sampled), and treatment of semantics as a workstream, not a mapping exercise.
**Walking into it:** "data migration" described purely as movement or transformation, with validation meaning row counts.

### 04. We cannot prove it is right
Plenty of testing, no evidence anyone will sign. Testing that demonstrates the new system works, rather than that it matches.

**Look for:** an explicit definition of what "correct" means, who signs it, and what evidence they see. Parallel running, output comparison, agreed expected answers.
**Walking into it:** UAT as the correctness gate; "the business will test it"; no comparison against the legacy system at all.

---

## Execution and architecture

### 05. One weekend, no way back
Big-bang cutover with untested rollback. TSB moved 5.2 million customers in a single weekend at a cost of roughly $1.3B (£1B).

**Look for:** incremental migration by population or slice, a rehearsed rollback, and pre-agreed abort criteria with a named decision-maker.
**Walking into it:** a single cutover date for everything, rollback described as "restore from backup", or no rehearsal.

### 07. Starting over never finishes
The rewrite trap. FBI's Virtual Case File scrapped $170M and never deployed.

**Look for:** incremental replacement with the legacy system live throughout, and value delivered before the end.
**Walking into it:** a full rewrite with a single delivery at the end, or a plan where nothing ships for more than two quarters.

### 10. Microservices you did not need
Over-modernization. Complexity added faster than value, then a quiet retreat to a monolith.

**Look for:** target architecture justified by a specific constraint, and an explicit decision about what is NOT being changed.
**Walking into it:** service boundaries chosen by technology rather than by domain, or a target architecture that names patterns without naming the problems they solve.

---

## Money, politics and people

### 06. It costs many times the estimate
Order-of-magnitude escalation. Queensland Health went from about $4M to past $900M (AU$6.2M to AU$1.2B+).

**Look for:** a cost model that includes the comprehension work, the evidence infrastructure, parallel running, and the long tail. A stated contingency.
**Walking into it:** a plan costed as build effort only, with no line for proving correctness.

### 08. Nobody owns the outcome
Accountability spread thin enough that no one can be wrong. Present in HealthCare.gov (no empowered integrator) and Post Office Horizon (institutional denial).

**Look for:** one named accountable owner, a decision-rights matrix, and a named person who can stop the program.
**Walking into it:** governance by committee, steering groups without decision rights, or no named person for correctness sign-off.

### 09. A vendor ends up owning your core
Handing away the capability you cannot buy back. Birmingham City Council went from £19M to £144M+ on an over-customized ERP.

**Look for:** retained internal ownership of domain knowledge and the parity evidence, plus exit terms.
**Walking into it:** the integrator owning the target design, the test evidence, or the only people who understand the new system.

---

## The modern era

### 11. What AI genuinely cannot do
Agents are strong at explaining legacy code, weaker at converting it reliably. Treating AI output as verified is the failure.

**Look for:** AI used for comprehension with human ratification, and execution-based verification of anything it generates.
**Walking into it:** automated code translation as the migration strategy, with review as the only check.

### 12. Doing nothing is a decision too
Deferral has a bill. California EDD's deferred COBOL estate met a pandemic load spike, contributing to roughly $20B in fraud.

**Look for:** the cost of inaction quantified alongside the cost of the program.
**Walking into it:** a business case that only compares delivery options, never the status quo.

---

## How to report

Never report all twelve as equally weighted. Rank by **what would actually kill this specific program**, based on what the plan says. Three absent categories that compound (no comprehension work, no correctness definition, big-bang cutover) matter far more than eight thin ones.
