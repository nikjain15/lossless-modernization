# Claude agents for legacy-code archaeology

*The signature innovation of the [Lossless Modernization](../README.md) playbook. Closely tied to [Pattern 03: Taming stored-procedure logic](../patterns/03-taming-stored-procedures.md).*

---

## Exec summary

The single hardest input to modernizing a 30-year-old financial platform was understanding logic that no documentation described: dense stored procedures whose original authors were long gone. So instead of only reading it by hand, we **built Claude agents and skills into an interrogation workflow**: an expert asks the agent questions about the legacy code, forms hypotheses about what it does, tests those hypotheses against both the code and the *live legacy product's actual behavior*, and extracts each confirmed rule into a reviewable form. Every extracted rule was then **validated with the business stakeholders** who owned its intent.

This is code archaeology turned on the modernization itself: applying AI not to the new product, but to *recovering the meaning of the old one*. It is genuinely novel, and it is employer-safe to describe generically because the innovation is the *method*, not any specific procedure.

The leadership takeaway: the bottleneck in legacy modernization is comprehension, and comprehension is exactly what modern AI agents are good at accelerating, provided a human owns the sign-off.

---

## The problem it solves

Thirty years of business logic lived inside stored procedures. The rules were in the data layer, undocumented, patched over decades, and understood in full by nobody currently on the team. Manual line-by-line reading works but is slow, and worse, it is hard to *review*: one engineer's mental model of a 2,000-line procedure is not something a business stakeholder can check. The comprehension bottleneck gated the entire program.

## The innovation: the interrogation loop

**This was not a batch pipeline where an agent summarizes a procedure and someone files the summary.** It was an interactive interrogation, run by a practitioner who owned the outcome, in a loop:

1. **Ask.** Point the agent at a legacy procedure and interrogate it: what does this branch do, when does it fire, what feeds this value, what happens on a month-end, what happens when the price is stale?
2. **Hypothesize.** Form a concrete claim about the behavior: "this branch zeroes accrual for holding type X on record dates."
3. **Test the hypothesis, twice.** First against the code, by tracing real examples through the logic with the agent. Then against reality, by exercising the *live legacy product* to observe its actual behavior. The code tells you what is written; the running system tells you what is true.
4. **Hunt the edges.** Push deliberately into the corners: unusual dates, boundary quantities, rare instrument types, the cases nobody would think to mention in a requirements meeting.
5. **Record.** Each confirmed rule goes into a structured, human-readable extraction: the responsibilities, the branches, the calculations, the special cases, with the un-inferable ones flagged **intent unknown**.

The output is not just faster comprehension. It is *reviewable and verified* comprehension: a structured artifact a business stakeholder can read and confirm, where every rule has already survived a test against the real system, rather than an engineer's private mental model.

## What the agent gets wrong (and why the loop exists)

The interrogation loop is not ceremony. It exists because every one of these failure modes showed up in practice:

- **Confident but wrong until tested.** The agent's explanation of a branch can sound completely right and still not survive tracing a real example through the code, or a check against the live product's behavior. Plausibility is not correctness; the hypothesis test is mandatory.
- **Missed cross-procedure interactions.** An agent analyzing one procedure well can still miss that two procedures interact through a shared table, a trigger, or batch ordering. Estate-level behavior does not live in any single file, and context windows do not hold an estate [DataStealth, 2026](https://datastealth.io/blogs/mainframe-modernization-claude-code-cobol).
- **Cannot judge intent.** The agent can establish *what* the code does, never *why*. Whether a strange rule is a bug or a deliberate regulatory decision is a question only the business can answer; every such branch goes to sign-off.
- **Chokes on size.** The largest, gnarliest procedures had to be decomposed into pieces before the agent could analyze them reliably. Budget for that decomposition work.

These are the documented limits of LLMs on legacy code generally (see [AI in legacy modernization](./README.md)); the loop turns them from silent risks into visible, testable steps.

## The human-in-the-loop that makes it safe

The agent proposes; **the business confirms.** Every extracted rule is validated with the business stakeholders who understand its original intent, and signed off. This is what recovers the forgotten historical reasons, and what consciously retires the ones that no longer apply. The agent never has authority over what the logic *should* be; it accelerates the recovery of what it *is*, and humans decide what to do with it.

This sits squarely inside the reliability model of [Pattern 05](../patterns/05-ai-in-workflows.md) and [Pattern 07](../patterns/07-reliability-under-llm.md): the agent assists, deterministic parity testing validates the replicated behavior, and humans approve. An extracted rule is not trusted because the agent produced it; it is trusted because (a) the business signed off on its intent and (b) the [parity harness](../patterns/parity-harness-deepdive.md) proves the replication matches the legacy behavior exactly.

## Why it is genuinely novel

Most "AI for code" tooling points forward: generating new code, autocompleting, reviewing diffs. This points *backward*: using AI to recover the intent of undocumented legacy so it can be faithfully preserved. The novelty is the combination:

- AI applied to **comprehension of legacy**, not generation of new code.
- Extraction into a **reviewable artifact** that non-engineers can validate.
- A **business-sign-off loop** that turns AI-extracted logic into trusted, agreed requirements.
- Downstream **parity proof** that the replication is behavior-exact.

It reframes the LLM from "coding assistant" to "translator of institutional memory that time nearly erased."

## Industry context

The industry is converging on the same conclusion from independent directions. Academic research consistently finds that LLMs are stronger at comprehension of legacy code than at converting it: multi-agent approaches for explaining undocumented COBOL are the lowest-risk, highest-adoption AI use case [arXiv 2507.02182](https://arxiv.org/html/2507.02182v1), and comparative studies find comprehension gains outpace conversion reliability [arXiv 2411.14971](https://arxiv.org/abs/2411.14971); [arXiv 2508.19663](https://arxiv.org/abs/2508.19663). On the vendor side, AWS Transform's "Reimagine" pattern makes the same move at product scale: extract business rules and generate documentation from the mainframe estate first, then hand the recovered intent to agentic coding tools [AWS, 2025](https://aws.amazon.com/blogs/migration-and-modernization/reimagine-your-mainframe-applications-with-agentic-ai-and-aws-transform/). Archaeology before translation is becoming the industry norm; the method on this page is that norm with an explicit business-sign-off loop and a [parity proof](../patterns/parity-harness-deepdive.md) attached. See [AI in legacy modernization](./README.md) for the full landscape and its documented limits.

## A generic worked example

A 30-year-old procedure computes income accrual with day-count conventions, a stale-price special case, and one branch that zeroes accrual for a narrow class of positions on specific dates.

1. A **Claude skill** reads the procedure and produces a first-pass extraction: three responsibilities (price selection, accrual, posting), the day-count rules per instrument type, the stale-price handling, and, flagged as **intent unknown**, the zeroing branch.
2. The practitioner **interrogates** the extraction: traces a stale-price day through the code with the agent, then runs the equivalent case on the live legacy product to confirm the observed behavior matches the extracted rule. One hypothesis fails (the day-count convention switch fires on a different boundary than the agent first claimed) and the extraction is corrected. Engineers then use the verified extraction to draft the corresponding microservices.
3. The **intent-unknown** branch goes to the business, which identifies it as a legitimate regulatory treatment for a specific holding type. It is documented and deliberately preserved.
4. The [parity harness](../patterns/parity-harness-deepdive.md) then proves the new accrual service matches the legacy procedure exactly across the relevant scenarios, including the regulatory branch.

What would have been weeks of one engineer squinting at SQL became a reviewable extraction that the business could validate directly, with the risky branch caught and consciously handled rather than silently carried or dropped.

## Pitfalls / anti-patterns

- **Trusting the extraction without business validation.** A plausible replication can be subtly wrong. Intent sign-off is mandatory.
- **Letting the agent decide what logic *should* be.** It recovers what the logic *is*; humans decide what it should become.
- **Skipping the parity proof.** Extraction plus sign-off establishes intent; only the parity harness proves behavior-exactness.
- **Hiding the unknowns.** The value is partly in the agent flagging what it *cannot* infer. Suppressing that removes the most important signal.
- **Over-claiming.** This accelerates and de-risks comprehension; it does not remove the need for rigorous human review and parity testing.

## Checklist

- [ ] Agents/skills built to read legacy procedures and extract logic into a reviewable form
- [ ] Extraction run as an interrogation loop: ask, hypothesize, test against code AND live legacy behavior, hunt edges, record
- [ ] Every agent claim about behavior verified by tracing a real example or exercising the legacy product, never accepted on plausibility
- [ ] Large procedures decomposed before analysis; cross-procedure interactions (shared tables, triggers, batch ordering) checked explicitly
- [ ] Extractions include explicit "intent unknown" flags for un-inferable branches
- [ ] Every extracted rule validated with business stakeholders for intent and signed off
- [ ] Agent never holds authority over what the logic *should* be
- [ ] Replicated behavior proven behavior-exact by the parity harness
- [ ] Forgotten historical/regulatory reasons recovered or consciously retired, with sign-off
- [ ] Innovation described generically, method not proprietary content

---

*Related: [Pattern 03, Taming stored procedures](../patterns/03-taming-stored-procedures.md) · [Pattern 05, AI agents in workflows](../patterns/05-ai-in-workflows.md) · [Pattern 07, Reliability under an LLM](../patterns/07-reliability-under-llm.md) · [The Parity Harness](../patterns/parity-harness-deepdive.md) · [Glossary](../GLOSSARY.md)*
