# Legacy Knowledge Map Template

**Exec summary.** The legacy knowledge map is a tribal-knowledge risk inventory: for each system area, what exists only in people's heads, who those people are, how likely the knowledge is to walk out the door, and the plan to capture it before it does. Skills scarcity is one of the UK CDDO's seven formal legacy-risk indicators [UK CDDO Legacy IT Risk Assessment Framework](https://gov.uk/government/publications/guidance-on-the-legacy-it-risk-assessment-framework/guidance-on-the-legacy-it-risk-assessment-framework), and it is the one risk that compounds silently: every retirement converts "hard" to "impossible." The map turns a vague fear into a prioritized capture backlog, worked through interviews, pairing, and AI-assisted code archaeology.

**Produced in:** the Inventory phase of the [artifact lifecycle](../playbook/README.md), maintained until decommissioning.
**Owner:** tech lead. **Signs off:** engineering manager.

## The template

```markdown
# Legacy Knowledge Map: <program name>

Version: <x.y> | Date: <YYYY-MM-DD> | Owner: <name, role>
Review cadence: <monthly> | Feeds risk register entries: <R-nnn, R-nnn>

## Knowledge inventory

| ID | System area | Only-in-heads knowledge | Held by | Attrition risk | Business impact if lost | Priority | Capture plan | Status |
|---|---|---|---|---|---|---|---|---|
| K-003 | Settlement batch abend recovery | Which of the 14 restart points is safe depends on unwritten rules about the GL posting sequence; wrong choice double-posts | D. Murphy (retires 2026-09), partial: L. Zhang | High | Sev-1 recovery time goes from 2h to unknown; double-posting risk | 1 | Structured interviews x4 (done 2); pair L. Zhang on next 3 real abends; AI-assisted walkthrough of restart COBOL, verified by D. Murphy | In progress |
| <K-nnn> | <system area> | <what is undocumented: recovery procedures, why-it-is-this-way rationale, edge-case business rules, environment quirks, vendor contacts> | <name(s), with leave date if known> | <High / Medium / Low> | <what breaks and how badly> | <1-n> | <interview / pairing / shadow-on-incident / AI-assisted archaeology / runbook writing> | <Not started / In progress / Captured / Verified> |

## Attrition risk scale

| Level | Definition |
|---|---|
| High | Single holder, and retirement, resignation risk, or contract end within 18 months |
| Medium | Two holders, or single holder with no known departure horizon |
| Low | Three or more holders, or knowledge partially documented already |

## Capture methods, in order of cost

1. Structured interview: record it, transcribe it, file it next to the code. Cheapest, lossy.
2. Runbook writing: the holder writes or dictates the procedure; a non-holder executes it in a rehearsal to prove it works.
3. Pairing and shadow-on-incident: a designated inheritor works every relevant change and incident with the holder. Highest fidelity, needs calendar-months.
4. AI-assisted archaeology: use LLM agents to generate explanations, call graphs, and business-rule candidates from the code itself, then have the holder correct them. Correction is faster than authorship, and the holder's red ink is the highest-value knowledge on the map. Method and prompts: [AI legacy archaeology](../ai/legacy-archaeology.md).
5. Characterization tests: pin the behavior itself so the system can answer questions people no longer can. See [characterization test plan](characterization-test-plan.md).

## Status definitions

| Status | Meaning |
|---|---|
| Captured | Artifact exists (doc, recording, test, annotated explanation) |
| Verified | A non-holder used the artifact to do the task successfully, without the holder in the room |

Captured is not done. Verified is done.
```

## Running the map

1. **Start from the incident log and the org chart, not the code.** Ask: which incidents required a specific person? Whose vacation makes releases stop? Those names seed the map.
2. **Priority = attrition risk x business impact,** worked top-down; the map is a backlog, not a museum.
3. **Feed the [risk register](risk-register.md).** Every High attrition risk on a critical area is a register entry with a score; K-IDs and R-IDs cross-reference.
4. **Budget real time.** Knowledge capture fails as a side-of-desk activity; put named hours per sprint against priority-1 items.
5. **Verify before the holder leaves, not after.** The verification run is the only proof the capture worked while correction is still possible.

## Quality bar

- [ ] Every critical system area was assessed, with "no tribal knowledge found" recorded where clean
- [ ] Every High attrition risk has a capture plan with named inheritor and dates
- [ ] Known departure dates are recorded, and priority-1 items are Verified before them
- [ ] AI-generated explanations are marked as verified or unverified by a holder
- [ ] Map items cross-reference risk register IDs
- [ ] Review cadence is visible in version control history

Next: [risk register](risk-register.md) | [AI legacy archaeology](../ai/legacy-archaeology.md) | [characterization test plan](characterization-test-plan.md)
