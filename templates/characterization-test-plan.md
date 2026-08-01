# Characterization Test Plan Template

**Exec summary.** Characterization tests pin down what legacy code actually does, not what anyone thinks it does. Michael Feathers defined the practice in Working Effectively with Legacy Code: write a test, let it fail, copy the actual output into the assertion, and you now have a tripwire around current behavior [Feathers, 2004](https://www.goodreads.com/en/book/show/44919.Working_Effectively_with_Legacy_Code); [key points summary](https://understandlegacycode.com/blog/key-points-of-working-effectively-with-legacy-code/). The plan below is Feathers-style: find the seams, capture current behavior as golden masters, set coverage goals by risk not by percentage, and make the suite a hard gate on every refactoring change. These tests answer "did we change behavior," which is a different question from "is the behavior correct"; the [parity report](parity-report.md) inherits their outputs as evidence.

**Produced in:** the Build Parity Evidence phase of the [artifact lifecycle](../playbook/README.md), before any refactoring or translation begins.
**Owner:** tech lead of the component. **Signs off:** engineering lead.

## The template

```markdown
# Characterization Test Plan: <component / app name>

Version: <x.y> | Date: <YYYY-MM-DD> | Owner: <name, role>
Sign-off: <engineering lead, date>
Rule in force: no refactoring commit merges unless the characterization suite passes.

## 1. Target seams

A seam is a place where behavior can be observed or altered without editing
the code at that place (Feathers). List where the component can be gripped.

| Seam | Type | What can be captured there | Harness approach |
|---|---|---|---|
| Nightly fee batch: input files in, GDG output files out | Process boundary | Full input/output file pairs per run | Run batch in isolated LPAR against copied inputs; diff outputs |
| <seam location> | <process boundary / API / DB write / message queue / subroutine call> | <observable inputs and outputs> | <how the harness attaches> |

## 2. Current-behavior capture method

| Item | Value |
|---|---|
| Capture source | <production runs / replayed production inputs / synthesized edge inputs> |
| Recording mechanism | <file snapshots, DB before/after images, API record-replay proxy, CDC log> |
| Sensitive data handling | <masking / tokenization applied, per <policy link>; golden masters contain no raw PII> |
| Determinism controls | <frozen clock, fixed seeds, sorted outputs, sequence-number normalization> |
| Known nondeterminism accepted | <fields excluded from comparison, each listed with reason> |

## 3. Golden master storage

| Item | Value |
|---|---|
| Location | <repo path or artifact store, e.g. git LFS at tests/golden/> |
| Versioning | Masters versioned with the code they characterize; commit sha recorded per capture |
| Refresh policy | Masters change ONLY via reviewed PR that cites a discrepancy ID or accepted difference (see parity report); never regenerated to make a red build green |
| Provenance record | Per master: source run date, input population, capture tool version |

## 4. Coverage goals by risk

Coverage is bought where behavior change hurts, not spread evenly.

| Risk tier | Definition | Coverage goal | Example scope |
|---|---|---|---|
| Critical | Money movement, regulatory output, irreversible writes | Every code path reachable from the seam; edge-case corpus reviewed by SME | Fee calculation, settlement postings |
| High | Customer-visible outputs | All main paths + known edge families | Statements, advisor reports |
| Medium | Internal, reconcilable downstream | Happy path + error paths | Staging transforms |
| Low | Logging, cosmetic | Smoke only, documented as accepted risk | <example> |

Current status: <n> of <n> critical paths pinned; corpus: <n> scenarios.

## 5. How the suite gates refactoring

- CI job <name/link> runs the full characterization suite on every PR touching <paths>
- A red suite blocks merge; there is no override label
- A behavior change that is INTENDED must arrive as: failing test + golden-master
  update + discrepancy or accepted-difference ID in the PR description
- Suite runtime budget: <n> min full, <n> min smoke subset for pre-push
- The suite transfers: the same corpus runs against the NEW implementation
  during parity testing, becoming input to the parity report
```

## Method notes

1. **Let the test tell you the answer.** Assert something wrong, run, copy the real output into the assertion. The system is the spec [Feathers, 2004](https://www.goodreads.com/en/book/show/44919.Working_Effectively_with_Legacy_Code).
2. **Bugs get pinned too.** If current behavior looks wrong, characterize it anyway and open a discrepancy; the business decides via the [parity report](parity-report.md) resolution flow whether the bug is load-bearing.
3. **Prefer coarse seams first.** A whole-batch file diff catches more per hour of effort than unit tests carved out of untestable code; go finer only where coarse diffs cannot localize failures.
4. **AI can draft the corpus, execution certifies it.** LLM-generated scenario suggestions are a fast way to enumerate edge families, but only captured execution output counts as a golden master; see [AI legacy archaeology](../ai/legacy-archaeology.md).

## Quality bar

- [ ] Every target seam has a working harness, demonstrated by a deliberately broken run going red
- [ ] Golden masters are versioned, provenance-stamped, and free of raw sensitive data
- [ ] Master refresh requires a reviewed PR citing a discrepancy or accepted-difference ID
- [ ] Coverage goals are stated per risk tier, and the critical tier is at goal before refactoring starts
- [ ] The suite is a merge-blocking CI gate with no override path
- [ ] Nondeterministic fields excluded from comparison are each listed with a reason

Next: [parity report](parity-report.md) | [strangler fig pattern](../patterns/02-strangler-fig.md) | [AI legacy archaeology](../ai/legacy-archaeology.md)
