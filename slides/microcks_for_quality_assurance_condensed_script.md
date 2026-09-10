# Microcks for Quality Assurance --- Condensed Speaker Script

> **Target pace:** 45--75 seconds per slide.\
> Explain the visual; land the bold line.

------------------------------------------------------------------------

## 1 --- Test the System Before the System Exists

**Core message:** Add controlled simulation to the QA portfolio.

-   Real systems remain essential.
-   But QA should not always depend on reality producing the condition
    we need.
-   Microcks makes dependency behavior controllable and repeatable.

**Key line:** **Don't wait for reality. Design the condition.**

## 2 --- QA Is Testing the Dependencies Too

**Core message:** Real dependencies limit test control.

-   Availability, shared state and test data create waiting and
    coordination.
-   Rare failures are difficult to reproduce.
-   Environment management becomes part of every campaign.

**Key line:** **When a dependency controls the scenario, QA does not
fully control the test.**

## 3 --- Ad-Hoc Mocks

**Core message:** We already mock---but the assets are fragmented.

-   Local stubs and scripts solve immediate needs.
-   They drift from the contract.
-   Ownership and reuse are weak.

**Key line:** **Turn mocking from test plumbing into a maintained
testing asset.**

## 4 --- Scenario-Driven Testing

**Core message:** Start with the condition we want to validate.

-   Choose dependency behavior.
-   Run on demand.
-   Repeat identically.

**Key line:** **Mocks complement end-to-end testing; they do not replace
it.**

## 5 --- Microcks for QA

**Core message:** One shared simulation source derived from the API
agreement.

-   OpenAPI + examples → Microcks.
-   QA gets reusable scenarios.
-   Consumers get mocks.
-   Backend gets conformance testing.

**Key line:** **Shared, traceable, reusable simulation.**

## 6 --- Negative-Path Campaigns

**Core message:** Make difficult failures selectable.

Test on demand: - 404 / 500 / 429; - missing fields; - empty results; -
new enums.

**Key line:** **Test the failures we design---not only the failures we
can conveniently create.**

## 7 --- Resilience Campaigns

**Core message:** Control degraded dependency behavior.

Test: - latency and timeouts; - errors; - partial data; - retries and
fallbacks; - loading and recovery UX.

**Key line:** **How does the product degrade when the dependency
degrades?**

## 8 --- Migration Compatibility

**Core message:** Turn migration differences into QA scenarios.

-   Legacy vs new status codes.
-   Optional fields.
-   timezone semantics.
-   enum migration.

**Key line:** **Every intentional contract change can become a test
case.**

## 9 --- Earlier QA

**Core message:** QA can challenge behavior before the real backend is
complete.

-   Contract + examples create the mock.
-   QA starts before the integrated environment.
-   Design problems are cheaper to change.

**Key line:** **Move QA feedback from implementation time to design
time.**

## 10 --- Disposable Environments

**Core message:** Campaigns can own their dependency conditions.

-   Ephemeral system under test.
-   Controlled Microcks dependencies.
-   Known dataset, latency or failure profile.
-   Reproducible and parallelizable.

**Key line:** **The environment adapts to the campaign---not the
campaign to the environment.**

## 11 --- Testing Portfolio

**Core message:** Choose realism according to the question.

-   E2E: real systems, critical journeys.
-   Integration: selected real dependencies.
-   Simulation: broad controlled scenarios.
-   Contract/component: fast boundary feedback.

**Key line:** **Reality for realism. Simulation for control.**

## 12 --- Maintained Testing Assets

**Core message:** Avoid rebuilding the ad-hoc mock problem.

-   QA designs campaigns and edge cases.
-   Backend maintains contract quality.
-   Consumers contribute important scenarios.
-   Platform operates Microcks.

**Key line:** **A scenario should survive the person who created it.**

## 13 --- Start With Three Campaigns

**Core message:** Prove the value on high-leverage cases.

1.  **Migration compatibility**
2.  **Resilience / latency**
3.  **Negative paths**

Keep real-system testing and add controlled simulation around it.

**Final line:** **More control. More coverage. Earlier feedback.**

------------------------------------------------------------------------

# Three Messages to Remember

1.  **Mocks are not a replacement for real-system testing; they add
    controllability.**
2.  **Microcks turns contract-based simulation into a shared QA
    capability instead of ad-hoc plumbing.**
3.  **QA can design conditions that are difficult to reproduce with real
    dependencies---and test them earlier and repeatedly.**

**Close:** **Don't wait for reality. Design the condition.**
