# Lossless Modernization

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)

**From thirty-year-old legacy to an AI-native platform. Without dropping a cent.**

The open playbook for modernizing systems that cannot be allowed to break: banks, governments, insurers, healthcare, ERP, mainframes. Any system where an output drifting by a penny, a record, or a case is a real-world incident.

### Read it at [nikjain15.github.io/lossless-modernization](https://nikjain15.github.io/lossless-modernization/)

---

## Status: beta, written in the open

The site is live. The chapters are being written and reviewed one at a time, and each one goes public only after a full review pass, rather than shipping a large body of unreviewed material at once.

**Live now**

- [The playbook](https://nikjain15.github.io/lossless-modernization/): the four-stage sequence, the twelve sourced failure categories, and the twelve artifacts a money-critical program produces
- [The post-mortem library](https://nikjain15.github.io/lossless-modernization/post-mortems.html): eight documented failures, costed and sourced, each mapped to the practice that would have caught it

**Landing next**

- Legacy-code archaeology: recovering intent from undocumented logic with AI agents, under human sign-off
- The parity harness: proving a modernized system matches value by value, including reports and spreadsheets
- The flagship case study: a $1.6T asset-management platform, sanitized
- The parity report and legacy knowledge map templates
- The full pattern catalogue, the decision trees, and the readiness scorecard
- Claude Skills and an MCP server, so your own agent can work the playbook

## Why this exists

Most writing on legacy modernization stops at "do not break it," which is a constraint rather than a destination. This playbook covers both halves: getting to an event-driven, API-first platform with AI agents embedded in workflows that used to be manual, and proving every value still matches on the way there.

Three ideas run through all of it:

1. **Parity is the contract.** Outputs match value by value at intermediate and final stages. The only acceptable difference is one the business consciously agreed and signed.
2. **No migration tool can read a spreadsheet.** Decades of business rules end up in macros, reports, and user-built applications. Code-only translation structurally cannot see them, so those rules vanish silently and nobody notices until a number drifts.
3. **AI translates, evidence certifies.** Agents are genuinely good at recovering what undocumented code does, and that is where they belong. What proves the new system is right is running both systems and comparing every value.

## The failure record

- **79% of application modernization projects fail**, at an average cost of $1.5M and 16 months [vFunction/Wakefield, 2022](https://info.vfunction.com/hubfs/Download%20Assets/Wakefield-Report-2022-Why-App-Modernization-Projects-Fail.pdf)
- TSB's big-bang core banking migration cost roughly **$1.3B (£1B)** and the CEO's job [Slaughter and May review, 2019](https://www.techmonitor.ai/leadership/digital-transformation/slaughter-and-may-tsb)
- Queensland Health's payroll replacement went from about **$4M to past $900M** (AU$6.2M to AU$1.2B+) [Commission of Inquiry, 2013](https://cabinet.qld.gov.au/documents/2013/aug/health%20payroll%20response/Attachments/Report.pdf)

These are not technology failures. They are failures of understanding, verification, and cutover discipline, which is what the playbook is organized around.

## Sourcing standard

Every factual claim carries an inline source. Statistics that circulate through vendor content without a traceable primary source are flagged as such rather than repeated as fact. Monetary figures lead in dollars with the original currency in brackets, converted approximately at the time of the event.

All program detail is generalized and sanitized: no employer named, no proprietary code, no client data.

## Contributing

Corrections are worth more than additions. If a claim here is wrong, a source is weak, or you have a post-mortem worth adding, see [CONTRIBUTING.md](./CONTRIBUTING.md).

## Author

By [Nik Jain](https://www.linkedin.com/in/niktechnologist/). Twelve years modernizing platforms across asset management, auto-tech and ed-tech, organizations up to 450+ people, and Forbes 30 Under 30 Asia. A hands-on leader across product, program and technical delivery, architecture included, through to the agentic AI-native platform itself.

## License

[MIT](./LICENSE). Use it, adapt it, ship it.
