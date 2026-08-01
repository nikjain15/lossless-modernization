# Application Inventory Template

**Exec summary.** The application inventory is the first artifact every framework demands: one row per application, scored for business value and technical fit, with a 7R disposition and a TIME quadrant. It is the source of truth that the business case, dependency map, and wave plan all derive from. Gartner's original 5Rs [Gartner, 2010](https://www.gartner.com/en/documents/1485116), AWS's 7Rs [AWS Prescriptive Guidance](https://docs.aws.amazon.com/prescriptive-guidance/latest/strategy-migration/overview.html), and the Gartner TIME model [LeanIX explainer](https://www.leanix.net/en/wiki/apm/gartner-time-model) all reduce to the same move: one explicit, defensible decision per application, written down.

**Produced in:** the Inventory and Score phases of the [artifact lifecycle](../playbook/README.md).
**Owner:** portfolio lead or enterprise architect. **Signs off:** program sponsor.

## The template

```markdown
# Application Inventory: <program name>

Version: <x.y> | Date: <YYYY-MM-DD> | Owner: <name, role>
Scoring rubric version: <x.y> | Sign-off: <name, role, date>

## Inventory

| App | Business capability | Owner (business / tech) | Users | Tech stack | Size (LOC or objects) | Change freq (releases/yr) | Business value (1-5) | Technical fit (1-5) | 7R disposition | Rationale (1 line) | TIME quadrant | Depends on | Depended on by | Vendor / support deadline |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| TradeCalc | Trade lifecycle: fee calculation | R. Chen / A. Okafor | 1,200 ops staff | COBOL 85, DB2, JCL batch | 410k LOC, 220 copybooks | 4 | 5 | 1 | Refactor | Core fee logic is a differentiator; platform is out of support 2027 | Migrate | MktDataFeed, RefDataHub | SettleEngine, 14 reports | IBM z14 support ends <YYYY-MM> |
| <app name> | <capability> | <biz owner> / <tech owner> | <count and type> | <languages, DB, OS> | <LOC or object count> | <n> | <1-5> | <1-5> | <Rehost / Relocate / Replatform / Refactor / Repurchase / Retire / Retain> | <one-line why> | <Tolerate / Invest / Migrate / Eliminate> | <upstream apps> | <downstream apps> | <date or n/a> |
```

## Scoring rubric

Score every application on two axes before assigning a disposition. Keep the rubric in the same file so scores are auditable.

**Business value (1-5)**

| Score | Meaning |
|---|---|
| 5 | Revenue-critical or regulatory-mandatory; outage halts the business |
| 4 | Supports a core capability; outage degrades the business within a day |
| 3 | Important to one function; workarounds exist for days |
| 2 | Convenience; duplicate capability exists elsewhere |
| 1 | Nobody can name an active user |

**Technical fit (1-5)**

| Score | Meaning |
|---|---|
| 5 | Supported stack, tested, documented, staffed, deployable on demand |
| 4 | Supported stack with minor debt; releases routine |
| 3 | Aging stack; releases possible but slow and risky |
| 2 | Out-of-support components or single-person knowledge; releases feared |
| 1 | Cannot be safely changed; no tests, no docs, no owner |

**Mapping scores to TIME** [Gartner TIME model via LeanIX](https://www.leanix.net/en/wiki/apm/gartner-time-model):

| Business value | Technical fit | Quadrant | Typical 7R dispositions |
|---|---|---|---|
| High (4-5) | High (4-5) | Invest | Retain, Replatform |
| High (4-5) | Low (1-3) | Migrate | Refactor, Replatform, Repurchase |
| Low (1-3) | High (4-5) | Tolerate | Retain, Rehost |
| Low (1-3) | Low (1-3) | Eliminate | Retire, Repurchase |

The 7R disposition is a decision, not a score: quadrants suggest candidates, the rationale column carries the argument. See [choose your strategy](../decide/choose-your-strategy.md) for the full decision tree.

## Quality bar

- [ ] Every application in scope has a row; "we found 30 percent more apps than the CMDB listed" is the norm, so reconcile against network scans and finance records, not just the CMDB
- [ ] Every row has a named business owner and a named tech owner, not a team name
- [ ] Every disposition has a one-line rationale a new joiner could understand
- [ ] Scores were calibrated in a workshop, not assigned by one person
- [ ] Vendor and support deadlines are dates, not "soon"
- [ ] Dependencies cross-reference the [dependency map](dependency-map.md)
- [ ] Sign-off block is a named person and date

Next: [dependency map](dependency-map.md) | [business case](business-case.md) | [wave plan](wave-plan.md)
