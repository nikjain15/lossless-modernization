# Claude agents for legacy-code archaeology

*The signature innovation of the [Lossless Modernization](../README.md) playbook. Closely tied to [Pattern 03: Taming stored-procedure logic](./03-taming-stored-procedures.md).*

---

## Exec summary

The single hardest input to modernizing a 30-year-old financial platform was understanding logic that no documentation described: dense stored procedures whose original authors were long gone. So instead of only reading it by hand, we **built Claude agents and skills to read and replicate legacy stored-procedure logic**, extracting each rule into a reviewable form, then **validated every extracted rule with the business stakeholders** who owned its intent.

This is code archaeology turned on the modernization itself: applying AI not to the new product, but to *recovering the meaning of the old one*. It is genuinely novel, and it is employer-safe to describe generically because the innovation is the *method*, not any specific procedure.

The leadership takeaway: the bottleneck in legacy modernization is comprehension, and comprehension is exactly what modern AI agents are good at accelerating, provided a human owns the sign-off.

---

## The problem it solves

Thirty years of business logic lived inside stored procedures. The rules were in the data layer, undocumented, patched over decades, and understood in full by nobody currently on the team. Manual line-by-line reading works but is slow, and worse, it is hard to *review*: one engineer's mental model of a 2,000-line procedure is not something a business stakeholder can check. The comprehension bottleneck gated the entire program.

## The innovation

**Purpose-built Claude agents/skills that read and replicate legacy logic.** Rather than treat the LLM as a chat assistant, we built it into the archaeology workflow as a tool that:

1. **Reads** a legacy stored procedure.
2. **Extracts** its logic into a structured, human-readable description: the responsibilities, the branches, the calculations, the special cases.
3. **Proposes a faithful replication** of the behavior, suitable for the new [role-based microservices](./03-taming-stored-procedures.md).
4. **Surfaces the unknowns** explicitly: branches whose *intent* cannot be inferred from the code alone (the forgotten regulatory case, the mysterious special-case flag).

The output is not just faster comprehension. It is *reviewable* comprehension: a structured artifact a business stakeholder can read and confirm, rather than an engineer's private mental model.

## The human-in-the-loop that makes it safe

The agent proposes; **the business confirms.** Every extracted rule is validated with the business stakeholders who understand its original intent, and signed off. This is what recovers the forgotten historical reasons, and what consciously retires the ones that no longer apply. The agent never has authority over what the logic *should* be; it accelerates the recovery of what it *is*, and humans decide what to do with it.

This sits squarely inside the reliability model of [Pattern 05](./05-ai-in-workflows.md) and [Pattern 07](./07-reliability-under-llm.md): the agent assists, deterministic parity testing validates the replicated behavior, and humans approve. An extracted rule is not trusted because the agent produced it; it is trusted because (a) the business signed off on its intent and (b) the [parity harness](./parity-harness-deepdive.md) proves the replication matches the legacy behavior exactly.

## Why it is genuinely novel

Most "AI for code" tooling points forward: generating new code, autocompleting, reviewing diffs. This points *backward*: using AI to recover the intent of undocumented legacy so it can be faithfully preserved. The novelty is the combination:

- AI applied to **comprehension of legacy**, not generation of new code.
- Extraction into a **reviewable artifact** that non-engineers can validate.
- A **business-sign-off loop** that turns AI-extracted logic into trusted, agreed requirements.
- Downstream **parity proof** that the replication is behavior-exact.

It reframes the LLM from "coding assistant" to "translator of institutional memory that time nearly erased."

## A generic worked example

A 30-year-old procedure computes income accrual with day-count conventions, a stale-price special case, and one branch that zeroes accrual for a narrow class of positions on specific dates.

1. A **Claude skill** reads the procedure and produces a structured extraction: three responsibilities (price selection, accrual, posting), the day-count rules per instrument type, the stale-price handling, and, flagged as **intent unknown**, the zeroing branch.
2. Engineers use the extraction to draft the corresponding microservices.
3. The **intent-unknown** branch goes to the business, which identifies it as a legitimate regulatory treatment for a specific holding type. It is documented and deliberately preserved.
4. The [parity harness](./parity-harness-deepdive.md) then proves the new accrual service matches the legacy procedure exactly across the relevant scenarios, including the regulatory branch.

What would have been weeks of one engineer squinting at SQL became a reviewable extraction that the business could validate directly, with the risky branch caught and consciously handled rather than silently carried or dropped.

## Pitfalls / anti-patterns

- **Trusting the extraction without business validation.** A plausible replication can be subtly wrong. Intent sign-off is mandatory.
- **Letting the agent decide what logic *should* be.** It recovers what the logic *is*; humans decide what it should become.
- **Skipping the parity proof.** Extraction plus sign-off establishes intent; only the parity harness proves behavior-exactness.
- **Hiding the unknowns.** The value is partly in the agent flagging what it *cannot* infer. Suppressing that removes the most important signal.
- **Over-claiming.** This accelerates and de-risks comprehension; it does not remove the need for rigorous human review and parity testing.

## Checklist

- [ ] Agents/skills built to read legacy procedures and extract logic into a reviewable form
- [ ] Extractions include explicit "intent unknown" flags for un-inferable branches
- [ ] Every extracted rule validated with business stakeholders for intent and signed off
- [ ] Agent never holds authority over what the logic *should* be
- [ ] Replicated behavior proven behavior-exact by the parity harness
- [ ] Forgotten historical/regulatory reasons recovered or consciously retired, with sign-off
- [ ] Innovation described generically, method not proprietary content

---

*Related: [Pattern 03 - Taming stored procedures](./03-taming-stored-procedures.md) · [Pattern 05 - AI agents in workflows](./05-ai-in-workflows.md) · [Pattern 07 - Reliability under an LLM](./07-reliability-under-llm.md) · [The Parity Harness](./parity-harness-deepdive.md) · [Glossary](../GLOSSARY.md)*
