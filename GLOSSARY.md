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
Recovering the intent and exact behavior of undocumented, decades-old code. In this program, accelerated by purpose-built Claude agents that read and replicate stored-procedure logic, with every extracted rule validated by business stakeholders. See the [dedicated doc](./patterns/claude-agents-for-legacy-archaeology.md).

### Trading cycle
One intraday processing window (morning through afternoon) in which trades, price updates, and data feeds are processed. Parity and timing tolerances are evaluated *per trading cycle*: values and trading accuracy within a cycle must not be compromised.

### ASO (architecture / solution design artifacts)
The defined architecture diagrams and solution-design documentation that accompany a modernization, giving business, architecture, and engineering a shared, reviewable picture of the target system for sign-off.
