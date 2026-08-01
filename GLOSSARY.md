# Glossary

Shared vocabulary for the [Lossless Modernization](./README.md) playbook. Terms are grouped roughly by theme, but each entry stands alone.

---

### Parity
The property that the new system produces *identical* outputs to the legacy system for the same inputs, value by value, to the required grain. In money-critical modernization, parity is the binding constraint, not speed or cost. The *only* acceptable difference between old and new is one the business consciously agreed during requirements (or an approved product improvement). See [Pattern 01: Parity](./patterns/01-parity.md) and the [Parity Harness deep-dive](./patterns/parity-harness-deepdive.md).

### Intermediate parity
Agreement between old and new not just at the final output, but at every meaningful intermediate calculation stage along the way. Two systems can arrive at the same final number by different, and sometimes both-wrong, paths. Intermediate parity closes that gap by reconciling the steps, not only the result.

### Final parity
Agreement between old and new at the terminal, business-consumed outputs: the trades, positions, NAVs, and report values that downstream systems and people actually use. Required *in addition to* intermediate parity, never instead of it.

### What counts as a match
A reconciliation outcome where old and new values are considered equal for sign-off purposes. Data must match exactly. The only accepted differences are (a) a difference the business consciously agreed during requirements, or (b) an approved product improvement, including a legacy bug that the business signed off to *fix rather than replicate*. Rounding differences are **not** accepted unless a sound business rule was explicitly agreed. Timing differences are accepted only where overall values and trading accuracy per trading cycle are not compromised.

### Parity harness
The tooling and process that runs old and new side by side, captures their outputs, compares them value by value, triages discrepancies, and feeds the formal sign-off gates. It is the source of truth for whether the new system can be trusted. See the [deep-dive](./patterns/parity-harness-deepdive.md).

### Shadow run / parallel run
Running the new system alongside the still-live legacy system on real production inputs, without the new system's outputs driving any real-world action. The legacy system remains the source of truth; the new system's outputs are captured only for comparison. Sustained over **12+ weeks** in this program to build confidence across many trading cycles and edge cases.

### Chasing a gap
The rigorous, regressive workflow of running down a single discrepancy surfaced by the parity harness: reproduce it, work with the business to understand *why* the values differ, analyze the code to find the exact logic or calculation difference, decide whether old or new is correct, and resolve it, often across hundreds of scenarios to be sure no edge case is missed.

### Cutover
The controlled moment (or staged sequence) when the new system replaces the legacy system as the source of truth for a given slice of functionality. Gated on proven parity, time-in-parallel, and formal sign-off, with a ready rollback plan. See [Pattern 06: Cutover](./patterns/06-cutover.md).

### Strangler-fig
An incremental modernization strategy where new services are grown around a legacy system and gradually take over its responsibilities, until the legacy system can be retired, rather than a single "big bang" rewrite and switch. Named for the fig that grows around a host tree. See [Pattern 02](./patterns/02-strangler-fig.md).

### Stored procedure
Business logic written and executed *inside* the database (for example in SQL PL), rather than in an application tier. Common in decades-old financial systems: the rules live in the data layer. Extracting them faithfully is a central challenge. See [Pattern 03](./patterns/03-taming-stored-procedures.md).

### Role-based microservices
The target decomposition where each service owns one clear responsibility, and legacy stored-procedure logic is distributed across those services rather than lifted and shifted as one block. Enables independent scaling and independent [replay](#idempotent-replay).

### Event-driven architecture
A design where processing is triggered by events (a trade, a price update, a data feed) rather than by a scheduled nightly batch. Enables multiple intraday trading cycles and real-time visibility. See [Pattern 04](./patterns/04-event-driven-saga.md).

### Saga
A pattern for coordinating a multi-step business process across several services without a single distributed transaction, using a sequence of local steps and compensating actions. In this program, each step maps to a single-responsibility service.

### Idempotent replay
The ability to re-run a specific microservice for a specific input and get the same correct output, without harmful side effects, no matter how many times it runs. On failure, you replay just the affected service to regenerate the correct output, instead of a global rollback of the whole workflow.

### Cutover choreography
The ordered plan for how a cutover actually happens: sequencing, staged migration, shadow traffic, verification checkpoints, communication to upstream/downstream systems, and rollback triggers. See [Pattern 06](./patterns/06-cutover.md).

### UDA (User-Developed Application)
A tool, spreadsheet, model, or small application built and maintained by business users outside the formal engineering estate, often mission-important but under-governed. Modernizing UDAs means bringing that logic into supported, tested systems. This program modernized **35+** UDAs and **70+** reports.

### LLM-in-the-loop
An architecture where a large language model participates in a workflow but does not hold final authority: it assists, drafts, classifies, or investigates, while deterministic checks validate its output and humans approve any real action. See [Pattern 05](./patterns/05-ai-in-workflows.md) and [Pattern 07](./patterns/07-reliability-under-llm.md).

### Grounding
Constraining an AI agent's answers to real, retrieved source data rather than letting it generate from parametric memory, so responses can be traced back to an authoritative source. A core reliability control for [LLM-in-the-loop](#llm-in-the-loop) systems.

### Eval
A repeatable test of an AI agent's behavior against known-good expectations, used to measure quality, catch regressions, and bound reliability before and after deployment.

### Legacy-code archaeology
Recovering the intent and exact behavior of undocumented, decades-old code. In this program, accelerated by purpose-built Claude agents that read and replicate stored-procedure logic, with every extracted rule validated by business stakeholders. See the [dedicated doc](./ai/legacy-archaeology.md).

### Trading cycle
One intraday processing window (morning through afternoon) in which trades, price updates, and data feeds are processed. Parity and timing tolerances are evaluated *per trading cycle*: values and trading accuracy within a cycle must not be compromised.

### ASO (architecture / solution design artifacts)
The defined architecture diagrams and solution-design documentation that accompany a modernization, giving business, architecture, and engineering a shared, reviewable picture of the target system for sign-off.

### 7Rs
The strategy vocabulary for deciding what to do with each application: Rehost, Relocate, Replatform, Refactor/Re-architect, Repurchase, Retire, Retain. AWS's extension of Gartner's original 5Rs (2010). One R is chosen per application and recorded in the [application inventory](./templates/application-inventory.md) disposition matrix. See [Choose your strategy](./decide/choose-your-strategy.md).

### TIME model
Gartner's 2x2 portfolio assessment: Business Value versus Technical Fit yields Tolerate, Invest, Migrate, or Eliminate for each application. Used alongside the 7Rs to decide where modernization money goes. See [Choose your strategy](./decide/choose-your-strategy.md).

### Characterization test
A test that pins the *actual current behavior* of legacy code, whatever that behavior is, so any later change that alters it fails loudly. Michael Feathers' remedy (*Working Effectively with Legacy Code*, 2004) for his own definition: "legacy code is simply code without tests." Plan them with the [characterization test plan template](./templates/characterization-test-plan.md).

### Golden master
A recorded snapshot of a system's outputs for a fixed set of inputs, kept as the reference that all future runs are compared against. Characterization testing at dataset scale; the curated input sets in the [parity harness](./patterns/parity-harness-deepdive.md) play this role.

### Dark launch
Running the new system on real production requests without letting its outputs drive any real-world action, purely to compare against the old system. The UK GDS Service Manual's recommended technique for de-risking legacy replacement. Sibling of the [shadow run](#shadow-run--parallel-run).

### Dual run
Running old and new systems side by side on the same production transactions and reconciling their outputs to certify parity before cutover. Productized as Google Cloud's Dual Run service, built on technology from Santander's core-banking migration. The [parity harness](./patterns/parity-harness-deepdive.md) is this program's dual-run machinery.

### Anti-corruption layer (ACL)
A translation facade between the new system's domain model and the legacy system's, so legacy semantics do not leak into and corrupt the new design. From Eric Evans' *Domain-Driven Design* (2003); documented as a cloud pattern by Microsoft.

### Seam
A place in a codebase where you can alter behavior without editing the code at that place, for example an interface, an injection point, or a call boundary. Feathers' term for the footholds that make legacy code testable and incrementally replaceable.

### Event interception
Capturing the events or requests flowing into a legacy system so they can be mirrored to, or eventually diverted to, the new system. A Thoughtworks Patterns of Legacy Displacement pattern; the routing layer that makes the [strangler-fig](#strangler-fig) and the shadow run possible.

### Legacy mimic
Making the new system present legacy-shaped outputs, files, or interfaces so downstream consumers keep working unchanged during the transition. A Thoughtworks Patterns of Legacy Displacement pattern.

### Transitional architecture
Scaffolding built deliberately for the duration of the migration and thrown away afterward: interception layers, reconciliation feeds, temporary adapters. A Thoughtworks Patterns of Legacy Displacement pattern; budgeting for its construction *and* removal is part of the coexistence cost.

### Wave plan
The grouping of applications or slices into ordered migration waves by dependency, risk, and similarity, so cutovers happen in a deliberate sequence rather than all at once. See the [wave plan template](./templates/wave-plan.md).

### RAG rating
Red / Amber / Green scoring of risks or legacy assets. The UK CDDO Legacy IT Risk Assessment Framework standardizes this across government, with seven legacy indicators and "red" meaning a risk score of 16 or more. Used in the [risk register template](./templates/risk-register.md).

### ADR (architecture decision record)
A short document capturing one architecturally significant decision: title, status, context, decision, consequences (the Nygard format). A modernization program produces many irreversible-looking choices; ADRs make them reviewable years later. See the [ADR template](./templates/adr.md).

### Dependency map
The map of application-to-application, application-to-data, and application-to-infrastructure relationships. The prerequisite for slicing, wave planning, and knowing who breaks when you cut something over. Appears in the [playbook lifecycle](./playbook/README.md) between deciding and wave planning.

### Feature parity trap
The costly assumption that the new system must replicate *every feature* of the old one. Thoughtworks' Feature Parity pattern warns most legacy estates carry substantial unused functionality; rebuilding it all inflates scope and was a factor in failures like the FBI Virtual Case File. Distinct from output [parity](#parity): decide which capabilities survive first, then prove exact output parity on those.

### Big-bang cutover
Replacing the old system with the new one for everything, in one event. Concentrates all program risk into a single, hard-to-reverse moment; the anchor cautionary case is [TSB Bank, 2018](./why-modernizations-fail/post-mortems/tsb-bank.md). Thoughtworks names the deliberate, last-resort version Stop the World Cutover. Compare [cutover](#cutover) as practiced here: staged, gated, reversible.

### Evals-driven modernization
Building the business test regime the way AI teams build an eval set: define the test cases and their expected answers *with* the business before running the system, automate most of the suite, and run it continuously and regressively. Because the expected answer is agreed in advance, a mismatch is a finding, never a debate. The method behind the flagship program's [5,000+ scenario regime](./patterns/parity-harness-deepdive.md).

### Interrogation loop (legacy archaeology)
The working method of [AI legacy archaeology](./ai/legacy-archaeology.md): ask the agent about the legacy code, form a hypothesis about behavior, test it against the code and against the live legacy system's observed behavior, hunt the edge cases, then record the confirmed rule. Exists because an LLM's explanation can be confident and wrong until tested.
