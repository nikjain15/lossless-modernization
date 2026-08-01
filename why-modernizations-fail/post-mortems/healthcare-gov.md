# HealthCare.gov: Sixty Contracts, No Integrator

**Exec summary:** HealthCare.gov launched on 1 October 2013 as the federal insurance marketplace for 36 states. It crashed within two hours; six people nationwide enrolled on day one [USDS, 2016](https://www.usds.gov/report-to-congress/2016/healthcare-dot-gov/); [Harvard D3, 2016](https://d3.harvard.edu/platform-rctom/submission/the-failed-launch-of-www-healthcare-gov/). Cost grew from $464M to $824M [Harvard D3, 2016](https://d3.harvard.edu/platform-rctom/submission/the-failed-launch-of-www-healthcare-gov/). The build was split across 60 contracts and 33 companies with no systems integrator; CMS assumed that role without the capability [HHS OIG, 2016](https://oig.hhs.gov/reports/all/2016/healthcaregov-case-study-of-cms-management-of-the-federal-marketplace). Leadership had 18 written warnings and launched anyway. The rescue "tech surge" fixed the site in about ten weeks and led to the creation of the US Digital Service.

## By the numbers

| Metric | Value |
|---|---|
| Planned cost | $464M |
| Actual cost | $824M+ |
| Contracts / companies involved | 60 / 33 |
| Systems integrators appointed | 0 |
| Written warnings before launch | 18 |
| Time to first crash on launch day | ~2 hours |
| Enrollments on day one, nationwide | 6 |

## Timeline

| Date | Event |
|---|---|
| 2010 | Affordable Care Act mandates a federal marketplace with a fixed statutory launch date [Harvard D3, 2016](https://d3.harvard.edu/platform-rctom/submission/the-failed-launch-of-www-healthcare-gov/) |
| 2011-2013 | Build split across 60 contracts, 33 companies; CGI Federal holds the main build contract; CMS acts as its own integrator [HHS OIG, 2016](https://oig.hhs.gov/reports/all/2016/healthcaregov-case-study-of-cms-management-of-the-federal-marketplace) |
| Sep 2013 | CGI warns CMS of open risks and issues: "there is not enough time built in to allow for adequate performance testing" [House Oversight Committee, 2013](https://oversight.house.gov/release/obamacare-contractor-warned-hhs-september-healthcare-gov-problems) |
| 1 Oct 2013 | Launch for 36 states; site crashes within two hours; 6 enrollments on day one [USDS, 2016](https://www.usds.gov/report-to-congress/2016/healthcare-dot-gov/) |
| Oct-Dec 2013 | "Tech surge": private-sector engineers plus CMS staff and contractors stabilize the site using SRE-style practices [NPR, 2013](https://www.npr.org/sections/alltechconsidered/2013/10/22/239220962/the-healthcare-gov-tech-surge-is-racing-against-the-clock); [USDS, 2016](https://www.usds.gov/report-to-congress/2016/healthcare-dot-gov/) |
| Jan 2014 | CMS moves to replace CGI Federal as lead contractor [Fox News, 2014](https://www.foxnews.com/politics/obama-administration-cutting-ties-with-healthcare-gov-contractor) |
| 2014 | US Digital Service created, directly out of the tech surge experience [USDS, 2016](https://www.usds.gov/report-to-congress/2016/healthcare-dot-gov/) |

## What went wrong

- **No empowered integrator.** Sixty contracts, 33 companies, and no single party responsible for making the pieces work together. CMS kept the integrator role for itself despite lacking the engineering capacity [HHS OIG, 2016](https://oig.hhs.gov/reports/all/2016/healthcaregov-case-study-of-cms-management-of-the-federal-marketplace).
- **Testing compressed to nothing.** End-to-end integration testing planned for months was compressed to a fraction as deadlines slipped rightward into the fixed launch date [Harvard D3, 2016](https://d3.harvard.edu/platform-rctom/submission/the-failed-launch-of-www-healthcare-gov/). The prime contractor said in writing there was not enough time for adequate performance testing [House Oversight Committee, 2013](https://oversight.house.gov/release/obamacare-contractor-warned-hhs-september-healthcare-gov-problems).
- **Warnings ignored.** Leadership received 18 written warnings about readiness and proceeded anyway; the launch date was political, not empirical [Harvard D3, 2016](https://d3.harvard.edu/platform-rctom/submission/the-failed-launch-of-www-healthcare-gov/).
- **The rescue used ordinary engineering discipline.** The tech surge team worked from monitoring, prioritized bottlenecks, and shipped iterative fixes, standard site-reliability practice that the original program never institutionalized [USDS, 2016](https://www.usds.gov/report-to-congress/2016/healthcare-dot-gov/).
- **Cost.** $464M planned, $824M+ actual [Harvard D3, 2016](https://d3.harvard.edu/platform-rctom/submission/the-failed-launch-of-www-healthcare-gov/).

## Root causes (taxonomy)

| Category | How it showed up |
|---|---|
| [8. Governance failure](../README.md#8-governance-politics-and-accountability-failure) | No integrator, fragmented accountability across 33 companies |
| [4. Testing and verification gaps](../README.md#4-testing-and-verification-gaps) | End-to-end and performance testing compressed to near zero |
| [5. Cutover risk](../README.md#5-cutover-and-big-bang-risk) | Statutory big-bang launch date, everything live for 36 states at once |

## What would have prevented it

- **A named, empowered integrator.** One party owning end-to-end behavior, with authority over all 60 contracts. This is a [RACI](../../templates/raci.md) problem before it is a technical one.
- **Incremental exposure instead of a national big bang.** A phased rollout (states, cohorts, or capabilities in waves) with a [wave plan](../../templates/wave-plan.md) would have surfaced the failures at survivable scale. See [cutover strategy](../../decide/cutover-strategy.md).
- **Testing as a gate, not a phase to squeeze.** Performance and end-to-end testing tied to written go/no-go criteria. See the [characterization test plan template](../../templates/characterization-test-plan.md).
- **The rescue proves the counterfactual.** A small team using monitoring, incident review, and iterative fixes stabilized in ten weeks what a $800M program could not launch, which is the strongest argument that method, not money, was the missing ingredient [USDS, 2016](https://www.usds.gov/report-to-congress/2016/healthcare-dot-gov/).

## Lessons checklist

- [ ] Is there exactly one named owner of end-to-end system behavior across all vendors?
- [ ] Does our launch scope have a smaller viable first slice, or are we betting everything on day one?
- [ ] Are performance and integration test gates written down with numbers, and who can waive them?
- [ ] What is our channel for contractor warnings to reach the go-live decision maker unfiltered?
- [ ] If launch fails, do we have monitoring good enough to find the bottleneck in hours, not weeks?

## Sources

- [HHS OIG, HealthCare.gov: case study of CMS management of the federal marketplace, 2016](https://oig.hhs.gov/reports/all/2016/healthcaregov-case-study-of-cms-management-of-the-federal-marketplace)
- [USDS, Stabilizing and improving HealthCare.gov, 2016](https://www.usds.gov/report-to-congress/2016/healthcare-dot-gov/)
- [Harvard D3, The failed launch of HealthCare.gov, 2016](https://d3.harvard.edu/platform-rctom/submission/the-failed-launch-of-www-healthcare-gov/)
- [House Oversight Committee, contractor warned HHS in September, 2013](https://oversight.house.gov/release/obamacare-contractor-warned-hhs-september-healthcare-gov-problems)
- [NPR, The HealthCare.gov tech surge, 2013](https://www.npr.org/sections/alltechconsidered/2013/10/22/239220962/the-healthcare-gov-tech-surge-is-racing-against-the-clock)

**Next:** [RACI template](../../templates/raci.md) | [Cutover strategy](../../decide/cutover-strategy.md) | [Post-mortems index](README.md)
