# Lossless Modernization

Contributor guide for the Lossless Modernization playbook: a written field guide, not a codebase. This document explains what the repository is, how it is organized, the format every pattern doc follows, the voice and style conventions all prose must meet, and how to propose changes.

## Project overview

Lossless Modernization is a field playbook for modernizing money-critical legacy systems into AI-native cloud platforms without losing a byte of logic or a cent of accuracy. It is a collection of Markdown documents: a hub README, a set of pattern docs, a glossary, and a closing essay. The audience is engineering and product leaders who are modernizing the systems their business actually runs on, plus the architects and practitioners who will do the work. Contributors extend and refine the writing; there is no application to build or run.

## Repository structure

This is a documentation-only repository. Every file is Markdown, and the whole thing is meant to be read on GitHub.

- `README.md`: the hub. It states the thesis, the myth the playbook busts, the signature moves, the pattern index table, the shareable reference numbers, and the pointers into every other document. Any new pattern must be linked here or it effectively does not exist.
- `patterns/`: one Markdown file per pattern. Numbered patterns (`01-parity.md` through `07-reliability-under-llm.md`) form the ordered core sequence. Unnumbered files (`parity-harness-deepdive.md`, `claude-agents-for-legacy-archaeology.md`) are signature deep-dives referenced from the hub and from the relevant numbered patterns.
- `GLOSSARY.md`: definitions of the domain terms used across the playbook (parity harness, strangler-fig, idempotent replay, UDA, and so on). New jargon introduced in a pattern belongs here too.
- `MYTH-BUSTER.md`: the closing essay that argues the central thesis. It is prose, not a pattern, so it does not follow the seven-section format.
- `LICENSE`: MIT.

## The two-layer pattern-doc format

Every numbered pattern doc is written in two layers so a single file serves two very different readers.

1. **Exec summary** at the top, for CTOs and engineering leaders deciding whether and how to modernize. Three or four tight paragraphs that state the stakes and the leadership takeaway, no implementation detail.
2. **Architect and practitioner depth** below, for the people who will do the work.

The depth layer always uses the same seven fixed sections, in this exact order:

1. **Problem**: the situation and the hard question it forces.
2. **When it applies**: the conditions under which this pattern is the right tool, and when its rigor is overkill.
3. **The approach**: the method itself, usually as an ordered or layered sequence.
4. **A worked example**: one concrete, generic scenario that shows the approach in motion. Keep it employer-safe and invented, never a real client case.
5. **Pitfalls and anti-patterns**: the ways teams get this wrong, stated plainly.
6. **Decision framework**: an ordered set of questions a reader asks to decide whether they are ready.
7. **Checklist**: a task list a practitioner can work through.

Close each pattern with a short footer linking the next pattern, any relevant deep-dive, and the glossary. Deep-dive docs may deviate from the seven sections where the material demands it, but they keep the same exec-summary-then-depth shape and the same voice.

## Writing and voice conventions

The prose is the product. Match the register of the existing docs.

- **Senior and precise.** Write as an experienced architect talking to peers. Make claims you can defend. Prefer the specific to the vague.
- **Positive and forward-looking.** These are contributor and reader guides, not war stories. State what to do and why it works.
- **Generic and employer-safe.** Every example is sanitized and generalized. No proprietary code, no employer names, no client identifiers, no internal system names. Reference numbers that already appear in the README are the only shareable figures; do not invent new ones.
- **No em dashes.** Use commas, colons, or periods instead.
- **No hyphen as a sentence separator.** Do not use a spaced hyphen (space, hyphen, space) to join clauses; rewrite with a comma, colon, or period. Compound-word hyphens such as event-driven, real-time, and strangler-fig are correct and expected.
- **Consistent domain terms.** Use the vocabulary defined in `GLOSSARY.md`. If you introduce a new term, define it there in the same pass.
- **Markdown that renders cleanly on GitHub.** Use tables, task lists, and blockquotes as the existing docs do. Keep relative links working.

## Contributing with AI tooling

Contributors are encouraged to draft and refine with Claude Code and other AI agents; that workflow is part of the point of this playbook. Treat the agent as a writing and research partner: it drafts, you own the judgment. Every claim, number, and example still needs a human author who stands behind it. Do not describe the shipped playbook as auto-generated, and do not paste raw prompt transcripts into the docs. The output is finished prose that reads as if a senior practitioner wrote it, because one signed off on it.

## Build, test, and commands

There is no build, no test suite, and no package manager here. This is a prose repository. The only meaningful automated check a contributor should run before opening a PR is a style scan of the files they touched, confirming zero em dashes and zero spaced-hyphen separators, and a visual check that Markdown renders correctly on GitHub and that all relative links resolve.

## Commit and PR guidelines

- **Branch** off `main` with a short, descriptive name (for example `add-pattern-08` or `revise-parity-example`).
- **Commit messages** are plain, imperative, and scoped to one logical change (for example `Add decision framework to cutover pattern`).
- **One concern per PR.** A new pattern, a glossary expansion, and a README restructure are three PRs, not one.
- **Keep the hub in sync.** If you add or rename a pattern, update the `README.md` index table and any cross-links in the same PR.
- **Style is a merge gate.** A PR that introduces an em dash or a spaced-hyphen separator does not merge until it is clean.
- **Merge with squash** into `main` and delete the branch, so history stays one commit per change.

## Security and secrets

There are no environment variables, credentials, or secrets in this repository, and none should ever be added. The content is deliberately generalized so that nothing here reflects any specific employer's proprietary systems, code, or data. If you find text that could identify a real client, system, or dataset, treat removing it as a priority fix.
