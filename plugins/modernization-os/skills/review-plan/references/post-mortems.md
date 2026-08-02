# Eight documented failures

Use these to name the shape a user's plan resembles. Naming a specific, sourced failure is far more persuasive than describing a risk in the abstract.

**Rule: only claim a resemblance when the plan actually shares the mechanism.** "Your cutover has TSB's shape" is only fair if they are moving a large population in a single event with untested rollback. Do not stretch a match for rhetorical effect, and say plainly when a plan resembles none of them.

Dollar figures are approximate conversions at the time of the event, with the original currency in brackets.

---

## TSB Bank, UK, 2018
**Cost:** roughly $1.3B (£1B) in total damage, plus the CEO's job.
**Mechanism:** a single-weekend migration of 5.2 million customers to a new core banking platform. Went live carrying 4,424 of 34,671 logged defects still open. Customers were locked out for weeks.
**The shape:** one irreversible event, a fixed date, and known defects accepted at go-live.
**Match this when:** the plan has a single cutover for a large population, rollback is untested or undefined, or go-live criteria are date-based rather than evidence-based.
**Source:** Slaughter and May independent review, 2019.

## Queensland Health, Australia, 2010
**Cost:** about $4M planned became past $900M over eight years (AU$6.2M to AU$1.2B+). IBM barred from state contracts.
**Mechanism:** payroll replacement went live after ten aborted attempts, carrying 2,422 known defects, under pressure to escape a dying system. Produced roughly 35,000 pay anomalies. Requirements were never adequately defined for the most complex payroll in the state.
**The shape:** go-live driven by the old system's fragility rather than the new one's readiness, over tester objections.
**Match this when:** the driver for the date is legacy risk rather than new-system evidence, or when the plan has no mechanism for testers to block a release.
**Source:** Queensland Health Payroll System Commission of Inquiry, 2013.

## HealthCare.gov, US federal, 2013
**Cost:** $464M planned, $824M+ actual.
**Mechanism:** end-to-end testing compressed from months into weeks to hold a politically fixed launch date. No empowered systems integrator across many vendors. Site failed at launch; six enrollments on day one.
**The shape:** a fixed external date, testing as the compressible item, and diffuse accountability across suppliers.
**Match this when:** the date is externally fixed and immovable, testing is the last phase, or no single party owns end-to-end integration.
**Source:** Harvard D3 case study, 2016, and contemporaneous federal reporting.

## FBI Virtual Case File, US federal, 2000 to 2005
**Cost:** $170M scrapped, including $105M of unusable code. Never deployed.
**Mechanism:** a full big-bang rewrite with continuously churning requirements and no incremental delivery.
**The shape:** replace everything, deliver at the end, requirements never frozen.
**Match this when:** the plan is a complete rewrite with a single delivery, or nothing reaches production for many quarters.
**Source:** IEEE Spectrum, 2005.

## Lidl SAP (eLWIS), Germany, 2011 to 2018
**Cost:** roughly $590M (€500M) written off after seven years.
**Mechanism:** the legacy system keyed inventory on purchase price; the new standard product keyed on retail price. The semantic mismatch drove endless customization until the program was abandoned.
**The shape:** a data model whose meaning differs from the old one, discovered after build began.
**Match this when:** data migration is treated as mapping and movement, or a package's assumptions have not been checked against the legacy system's actual semantics.
**Source:** Computer Weekly, 2018.

## Post Office Horizon, UK, 1999 to 2025
**Cost:** roughly 900 wrongful prosecutions, £1B+ in redress, decades of ruined lives.
**Mechanism:** the institution treated its system as correct by definition and prosecuted its own staff rather than investigate discrepancies.
**The shape:** no route for evidence to overturn an institutional assumption; discrepancies attributed to users.
**Match this when:** there is no mechanism to escalate a suspected system error, or when accountability for correctness sits with the same party that built the system.
**Source:** Computer Weekly investigation and the statutory inquiry.

## Birmingham City Council, UK, 2022 onward
**Cost:** £19M became £144M+, estimated £216.5M by 2026. Contributed to the council declaring effective bankruptcy.
**Mechanism:** heavy customization of a cloud ERP broke core accounting functions; the council could not close its books.
**The shape:** customizing a package until it becomes a bespoke system nobody supports, with a vendor holding the knowledge.
**Match this when:** a package is being customized to preserve existing process, or the integrator holds the target design and the test evidence.
**Source:** The Register and council reporting, 2026.

## California EDD, US state, 2020
**Cost:** roughly $20B in fraud plus a claims backlog crisis.
**Mechanism:** modernization of a COBOL-era unemployment system was repeatedly deferred. The estate met a once-in-a-century load spike and could not cope.
**The shape:** deferral as the implicit decision, with no quantified cost of inaction.
**Match this when:** the business case compares delivery options but never the status quo, or when the plan has no stated consequence for slipping another year.
**Source:** California State Auditor, 2020.

---

## Reporting the match

Give at most three matches, strongest first. For each: name the case, state the shared mechanism in one sentence, quote the specific thing in their plan that creates the resemblance, and give the counter-practice. If a plan matches none, say so and name instead the category from the taxonomy that is least covered.
