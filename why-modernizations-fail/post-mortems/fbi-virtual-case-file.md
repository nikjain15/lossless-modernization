# FBI Virtual Case File: The $170M Rewrite That Never Shipped

**Exec summary:** The FBI's Virtual Case File (VCF) was meant to replace the obsolete Automated Case Support (ACS) system and drag the bureau's paper-based casework into the digital era. After the 9/11 attacks, scope and urgency exploded. Contractor SAIC delivered around 700,000 lines of code that the FBI judged so bug-ridden and functionally off target that the bureau scrapped the entire $170M project in April 2005, including $105M of unusable code [IEEE Spectrum, 2005](https://spectrum.ieee.org/who-killed-the-virtual-case-file); [CNN, 2005](https://www.cnn.com/2005/US/02/03/fbi.computers/). VCF is the canonical rewrite-trap case: churning requirements, a planned flash cutover, and no incremental delivery.

## By the numbers

| Metric | Value |
|---|---|
| Total spent | $170M |
| Unusable code written off | $105M |
| Lines of code delivered | ~700,000 |
| Deployed to production | Never |
| Project scrapped | April 2005 |
| Years until successor (Sentinel) shipped | 7 (2012, after switching to agile) |

## Timeline

| Date | Event |
|---|---|
| 2000-2001 | FBI launches the Trilogy modernization program; SAIC contracted for the user-application component that becomes VCF, replacing ACS [IEEE Spectrum, 2005](https://spectrum.ieee.org/who-killed-the-virtual-case-file) |
| Sep 2001 | Post-9/11, information-sharing failures make VCF a national priority; requirements and urgency balloon [IEEE Spectrum, 2005](https://spectrum.ieee.org/who-killed-the-virtual-case-file) |
| Dec 2003 | SAIC delivers VCF; the FBI identifies hundreds of deficiencies and refuses acceptance [IEEE Spectrum, 2005](https://spectrum.ieee.org/who-killed-the-virtual-case-file) |
| Feb 2005 | Inspector General and Congress publicly dissect the failure [CNN, 2005](https://www.cnn.com/2005/US/02/03/fbi.computers/) |
| Apr 2005 | FBI scraps VCF: $170M spent, $105M of unusable code [IEEE Spectrum, 2005](https://spectrum.ieee.org/who-killed-the-virtual-case-file) |
| 2006-2012 | Successor program Sentinel also struggles under waterfall delivery, then ships in 2012 after the FBI takes it in-house with an agile approach [InformationWeek, 2012](https://www.informationweek.com/it-sectors/fbi-s-sentinel-project-5-lessons-learned) |

## What went wrong

- **A big-bang rewrite with a moving target.** VCF aimed to replace ACS wholesale rather than incrementally. Requirements churned continuously as FBI priorities shifted post-9/11 and as a parade of leadership changes each reshaped the plan [IEEE Spectrum, 2005](https://spectrum.ieee.org/who-killed-the-virtual-case-file).
- **A planned flash cutover.** The bureau intended to switch off ACS and switch on VCF at once, an approach engineers criticized as needlessly risky for a mission-critical case system [IEEE Spectrum, 2005](https://spectrum.ieee.org/who-killed-the-virtual-case-file).
- **Requirements without a stable baseline.** Development proceeded without enterprise architecture or frozen specifications; the FBI changed requirements mid-build and SAIC kept building, billing time and materials [IEEE Spectrum, 2005](https://spectrum.ieee.org/who-killed-the-virtual-case-file); [Washington Post, 2006](https://www.washingtonpost.com/archive/politics/2006/08/18/rise-and-fall-of-the-virtual-case-file/f913d534c552e36df1e7078fbbd79f3d/).
- **Nothing shippable along the way.** After roughly three years, the delivered system was rejected in total. There was no intermediate slice in production generating feedback or value; the first real test was the final delivery [IEEE Spectrum, 2005](https://spectrum.ieee.org/who-killed-the-virtual-case-file).
- **The contrast that proves the point.** Sentinel finally shipped in 2012 after the FBI cut the team, took work in-house, and delivered in agile increments [InformationWeek, 2012](https://www.informationweek.com/it-sectors/fbi-s-sentinel-project-5-lessons-learned).

## Root causes (taxonomy)

| Category | How it showed up |
|---|---|
| [7. The rewrite trap](../README.md#7-the-rewrite-trap) | Wholesale replacement of ACS with feature parity as a moving target |
| [8. Governance failure](../README.md#8-governance-politics-and-accountability-failure) | Leadership turnover, no stable requirements baseline, weak contract oversight |
| [5. Cutover risk](../README.md#5-cutover-and-big-bang-risk) | Flash-cutover plan for a mission-critical national system |

## What would have prevented it

- **Strangling ACS instead of replacing it.** Route one workflow at a time (for example, digital case notes) through new components while ACS keeps running, retiring legacy function by function. See the [strangler fig pattern](../../patterns/02-strangler-fig.md).
- **The rewrite decision made consciously.** VCF chose "rewrite, big bang, everything" by default. A structured pass through [rewrite vs strangle vs wrap](../../decide/rewrite-vs-strangle-vs-wrap.md) forces the risk comparison before money moves.
- **Decision records to survive leadership churn.** With every scope change captured as an [ADR](../../templates/adr.md) with costs attached, requirement churn becomes visible and chargeable instead of silent.
- **Incremental acceptance tied to working software.** Contract milestones tied to deployed, verified slices rather than document deliverables. See the [wave plan template](../../templates/wave-plan.md) and [parity report template](../../templates/parity-report.md) for what "verified slice" means in practice.

## Lessons checklist

- [ ] Are we replacing a working system wholesale when we could strangle it function by function?
- [ ] Is any milestone payment tied to software running in production, or only to documents?
- [ ] Do we have a written requirements baseline, and is every change priced and logged?
- [ ] Would our program survive three leadership changes? What carries the decisions forward?
- [ ] Is there a flash cutover anywhere in the plan? What is the incremental alternative?

## Sources

- [IEEE Spectrum, Who killed the Virtual Case File?, 2005](https://spectrum.ieee.org/who-killed-the-virtual-case-file)
- [CNN, Report: FBI wasted millions on Virtual Case File, 2005](https://www.cnn.com/2005/US/02/03/fbi.computers/)
- [Washington Post, Rise and fall of the Virtual Case File, 2006](https://www.washingtonpost.com/archive/politics/2006/08/18/rise-and-fall-of-the-virtual-case-file/f913d534c552e36df1e7078fbbd79f3d/)
- [InformationWeek, FBI's Sentinel project: 5 lessons learned, 2012](https://www.informationweek.com/it-sectors/fbi-s-sentinel-project-5-lessons-learned)
- [SEBoK, FBI Virtual Case File system case study](https://sebokwiki.org/wiki/Federal_Bureau_of_Investigation_%28FBI%29_Virtual_Case_File_System)

**Next:** [Strangler fig pattern](../../patterns/02-strangler-fig.md) | [Rewrite vs strangle vs wrap](../../decide/rewrite-vs-strangle-vs-wrap.md) | [Post-mortems index](README.md)
