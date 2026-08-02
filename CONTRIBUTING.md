# Contributing

**Exec summary.** This is a reference repo in beta: the site is live and chapters are published one at a time as each passes review. Its value is accuracy, sourcing, and consistency, not volume. The most useful contributions are new post-mortems built on primary sources, new or improved templates, corrections with citations, and translations. Every claim must carry an inline source. The style guide below is short and enforced in review; PRs that follow it merge fast.

## What we want

In rough priority order:

1. **New post-mortems.** A modernization or migration failure, or a documented success, covering what happened, timeline, cost, root causes, and which pattern in this repo would have helped. Must be built on primary sources: official inquiry reports, auditor reports, regulator findings, court documents, or first-party engineering post-mortems. News coverage is fine as supporting color, not as the spine.
2. **New templates.** Artifacts a real program produces that the template library lacks. Copy-paste usable markdown, `<angle-bracket placeholders>`, one filled example row per table, and a named-person-plus-date sign-off block where sign-off applies.
3. **Corrections with sources.** A stat that is wrong, stale, or better-sourced than what we cite; a broken link; a pattern description that misstates the original author's intent. Cite the better source in the PR description.
4. **Sharper sourcing.** Several widely repeated statistics in this field circulate through vendor content with no traceable primary source. Tracing one to a primary document, or demonstrating that it cannot be traced, is a valuable PR on its own.
5. **Translations.** Full-file translations under a language directory (for example `translations/es/`). Keep file names identical to the English originals so links stay parallel.
6. **Diagrams.** Mermaid improvements to existing docs, or a diagram for a concept that lacks one.

What we do not want: link dumps without annotation, tool listings that read as advertising, AI-generated text pasted without verification, content about specific employers' proprietary systems, and unsourced opinion pieces.

## Quality bar

Every PR is reviewed against this list:

- [ ] **Every factual claim has an inline source** in the form `[Source Name, Year](URL)`. Program-specific numbers come only from the reference figures in [README.md](README.md), and are stated in dollars with the original currency in brackets.
- [ ] **Vendor-circulated stats are flagged honestly**, for example "widely attributed to Gartner," never laundered into hard fact.
- [ ] **No em-dashes or en-dashes in prose.** Use colons, commas, or periods.
- [ ] **Docs open with a 3-6 line exec summary**, then practitioner depth.
- [ ] **Major concepts get a Mermaid diagram** (` ```mermaid ` fenced, GitHub-native). Decision trees use `flowchart TD`, lifecycles `flowchart LR`, comparisons use tables.
- [ ] **Checklists are `- [ ]` items.** Templates use `<angle-bracket placeholders>` and include a filled example row.
- [ ] **Tone is practitioner-grade:** short sentences, numbers over adjectives, no marketing fluff, American English, sentence case for section headings.
- [ ] **Cross-links are relative** and every doc ends with a "Next" line linking 2-3 related docs.
- [ ] **Nothing invented.** No statistic, quote, or event that cannot be verified at its cited URL.

## How to submit a PR

1. Fork the repo and create a branch named for the change, for example `post-mortem/phoenix-payroll` or `fix/tsb-defect-count`.
2. Make the change. One topic per PR: a new post-mortem and three unrelated typo fixes are two PRs.
3. Run your text against the quality bar above. Reviewers will apply it literally.
4. Open the PR with a description that states what changed, why, and lists any new sources with one line each on their reliability.
5. Expect review feedback focused on sourcing and style. Substantive disagreements about a pattern's merits are welcome in the PR thread; the bar for changing a recommendation is evidence, not preference.

For large contributions (a new section, a new post-mortem), open an issue first with an outline so effort is not wasted on something out of scope.

## Licensing

This repo is released under the [MIT License](LICENSE). By submitting a PR you agree that your contribution is licensed under the same terms. Do not contribute content you do not have the right to license: no copied proprietary material, no confidential employer information, and no long verbatim excerpts from copyrighted books or paywalled reports. Summarize and cite instead.

**Next:** [README.md](README.md) | [the playbook site](https://nikjain15.github.io/lossless-modernization/)
