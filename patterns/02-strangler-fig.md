# Pattern 02, Strangler-fig decomposition

*Part of the [Lossless Modernization](../README.md) playbook.*

---

## Exec summary

You cannot stop a trillion-dollar platform to rebuild it, and you should not try to rewrite it all at once and flip a switch. The strangler-fig approach grows the new system *around* the old one, taking over responsibilities piece by piece while the legacy system keeps running as the source of truth, until the old system can finally be retired.

The sequencing that worked on a large asset-management / trading platform: build the **shared foundation and common microservices first** (the parts common across all fund types), then fan out the fund-specific logic **in parallel**. Throughout, the **old system stayed the source of truth**; the new ran alongside in shadow/parallel for weeks; and a slice was only declared "done" when it met three criteria together, parity threshold, time-in-parallel, and business sign-off.

The leadership takeaway: incremental is not slower, it is safer *and* faster to trust. Big-bang rewrites of money-critical systems fail on the trust problem, not the code problem.

---

## Problem

A large, monolithic legacy system encodes decades of business logic and cannot go down. A full rewrite-and-switch ("big bang") concentrates all risk into a single irreversible moment, exactly the moment you can least afford to get wrong. How do you modernize continuously while the business keeps running on the old system?

## When it applies

- The legacy system is mission-critical and must stay live throughout.
- The system is large enough that a single cutover would be unmanageably risky.
- Responsibilities can be carved into slices that can each be proven and cut over independently.
- You have (or can build) the [parity](./01-parity.md) machinery to prove each slice before it takes over.

## The approach

1. **Build the shared foundation first.** Identify the microservices whose responsibilities are *common across fund types* (or your domain's equivalent shared concerns), and build those first. They are the base every fund-specific slice will stand on.
2. **Fan out in parallel.** With the common foundation in place, build the fund-specific logic as parallel workstreams. Because they share the foundation, they do not each reinvent it, and they can progress simultaneously across a distributed team.
3. **Keep the old system as the source of truth.** New services run **alongside** the legacy system in shadow/parallel mode. The legacy system continues to drive real-world outcomes; the new services' outputs are captured and reconciled, not yet trusted.
4. **Prove over time.** Each slice runs in parallel for weeks, reconciled against the legacy system via the [parity harness](./parity-harness-deepdive.md), until it has been seen across enough trading cycles and edge cases.
5. **Cut over slice by slice.** Once a slice is proven, cut it over from old to new (see [Pattern 06](./06-cutover.md)), then move on. The blast radius of any one cutover is one slice, not the whole platform.

### "Done" criteria for a slice

A slice is done only when **all three** hold:

- **Parity threshold** met (per [Pattern 01](./01-parity.md)): outputs reconcile, with only business-agreed differences.
- **Time-in-parallel** satisfied: it has run alongside the legacy system long enough to have seen the tail.
- **Business sign-off** obtained: business, architecture, and engineering agree it is ready.

Two out of three is not done. A slice with perfect parity that has only run for three days has not seen a month-end. A slice that has run for months but still shows unexplained gaps is not proven.

## A generic worked example

A fund-accounting monolith serves several fund types (say, equity, fixed-income, and multi-asset). Rather than rewrite it wholesale:

- **Foundation first:** build common microservices for pricing ingestion, reference data, position keeping, and a reconciliation feed. These are shared by every fund type.
- **Fan out:** three parallel teams build the fund-type-specific valuation and accrual logic on top of the shared services.
- **Shadow:** each fund type's new pipeline runs in parallel with the monolith, outputs reconciled nightly, then intraday, against the legacy source of truth.
- **Cut over incrementally:** equity funds reach all three "done" criteria first and cut over. Fixed-income, which has thornier edge cases (amortization schedules, corporate actions), stays in parallel longer. Multi-asset follows once its dependencies are proven.

At every moment, some fund types are running on new and some on old, and the platform as a whole never goes down.

## Pitfalls / anti-patterns

- **Big-bang temptation.** "It will be cleaner to just switch everything at once." It concentrates all risk into the one event you cannot afford to fail.
- **Building fund-specific logic before the foundation.** Leads to duplicated, inconsistent shared logic across slices and painful later reconciliation.
- **Letting the new system become a second source of truth early.** Until a slice is cut over, the old system is authoritative. Two live sources of truth is a reconciliation nightmare.
- **Declaring "done" on parity alone.** Without time-in-parallel and sign-off, you have a match, not proven trust.
- **Slices too large.** If a slice is so big that its cutover is itself a big bang, re-slice it.
- **Ignoring the coexistence cost.** Running old and new in parallel has real operational overhead; budget for it rather than rushing to end it.

## Decision framework

1. **Can the system tolerate any downtime for a switch?** If no, strangler-fig is effectively mandatory.
2. **What is genuinely common vs. slice-specific?** Build the common foundation first; it de-risks everything downstream.
3. **What is the smallest slice that can be independently proven and cut over?** Prefer smaller slices; they shrink blast radius.
4. **Which slice should go first?** Favor a slice that exercises the shared foundation and has manageable edge cases, so you validate the base early.
5. **Is this slice done?** Only if parity + time-in-parallel + sign-off all hold.

## Checklist

- [ ] Shared foundation / common microservices identified and built first
- [ ] Slice-specific workstreams fanned out in parallel on the shared base
- [ ] Old system remains the single source of truth until each slice cuts over
- [ ] Each new slice runs in shadow/parallel and reconciles via the parity harness
- [ ] "Done" defined as parity threshold **and** time-in-parallel **and** business sign-off
- [ ] Cutover performed slice by slice, blast radius limited to one slice
- [ ] Coexistence (old + new running together) is operationally supported and budgeted
- [ ] No slice cut over on parity evidence alone

---

*Previous: [Pattern 01, Parity](./01-parity.md) · Next: [Pattern 03, Taming stored procedures](./03-taming-stored-procedures.md) · [Glossary](../GLOSSARY.md)*
