# Microcks for Quality Assurance --- Speaker Script

## Speaker guide

This script accompanies the **Microcks for Quality Assurance** deck.

The message for QA is not "replace real systems with mocks." The
opportunity is to add a **controlled simulation layer** to the existing
testing portfolio so QA can deliberately create conditions that are
difficult, slow, unsafe, or unreliable to reproduce with real
dependencies.

A typical pace is **1.5--2 minutes per slide**.

------------------------------------------------------------------------

## Slide 1 --- Test the System Before the System Exists

**Purpose:** Reframe mocking as a QA capability rather than development
plumbing.

**Speaker script**

This presentation is about a testing opportunity.

Today, much of our QA activity depends on real systems being available,
correctly configured, populated with the right data, and capable of
producing the condition we want to test.

That realism is important, and we should keep it. But it also limits
what QA can control.

Microcks gives us another layer: controlled simulation derived from the
same API agreement used by development.

The proposition is not "stop testing reality." It is: **when the test
requires a specific dependency condition, QA should be able to design
that condition instead of waiting for reality to produce it.**

That creates more control, broader scenario coverage, repeatability, and
earlier feedback.

**Transition:** Let's start with the constraints of the current model.

------------------------------------------------------------------------

## Slide 2 --- QA Is Testing the Product---and the Availability of Its Dependencies

**Purpose:** Make the current dependency problem explicit.

**Speaker script**

In our current topology, QA rarely tests one isolated system.

A test environment depends on backend services, legacy APIs, identity
systems, third parties, shared datasets, and sometimes other teams'
release schedules.

When one dependency is unavailable, QA waits. When shared state is
polluted, we reset. When specific data is required, we coordinate. And
when a failure condition is difficult to reproduce, we sometimes skip it
or test it manually in an artificial way.

So part of every campaign becomes environment management.

The key limitation is simple: **when a dependency controls the scenario,
QA does not fully control the test.**

Real-system testing remains essential, but it should not be our only way
to exercise dependency behavior.

**Transition:** We already compensate for this today, usually with local
mocks and stubs.

------------------------------------------------------------------------

## Slide 3 --- Ad-Hoc Mocks Create a Maintenance Problem

**Purpose:** Acknowledge current mocking practices and explain why
centralized contract-based mocks are different.

**Speaker script**

Mocks are not new to us.

Teams already create JSON stubs, local mock servers, scripts, hardcoded
responses, Postman examples, or temporary substitutes.

They solve immediate problems. But they tend to be local and
short-lived.

A mock may differ from the actual API contract. Nobody knows who owns
it. The API changes while the mock remains unchanged. Useful scenarios
are trapped inside one project or one person's machine. And the same
scenario is rebuilt repeatedly by different teams.

So the problem is not that we lack mocks. The problem is that **mock
behavior is often not managed as a shared testing asset.**

Microcks gives us an opportunity to centralize simulation around the API
contract and its maintained examples.

**Transition:** That enables a different way of designing campaigns.

------------------------------------------------------------------------

## Slide 4 --- From Dependency-Driven to Scenario-Driven Testing

**Purpose:** Introduce the core QA mindset change.

**Speaker script**

This is the central shift.

Dependency-driven testing starts with questions such as: What state is
the real system currently in? Can we create the condition? Can we
reproduce it tomorrow?

Scenario-driven testing starts somewhere else: **What condition do we
need to validate?**

We select the dependency behavior, run the scenario, observe the system
under test, and repeat it consistently.

This does not eliminate end-to-end testing. End-to-end tests answer
questions that simulation cannot answer: real connectivity, real
integration, infrastructure behavior, production-like data flows, and
full-system confidence.

Simulation answers another class of questions extremely well: **How does
our system behave when a dependency responds in a specific way?**

That is a new layer around our existing testing strategy.

**Transition:** Microcks provides a way to make that simulation shared
and maintainable.

------------------------------------------------------------------------

## Slide 5 --- One Managed Simulation Source

**Purpose:** Position Microcks within the existing contract-driven
topology.

**Speaker script**

The important difference from an ad-hoc mock is where the behavior comes
from.

Our OpenAPI contract and its examples remain the agreement. Microcks
consumes those artifacts and exposes working mocks from them.

That same contract is already relevant to backend, frontend, and mobile.
QA now becomes another active consumer of it.

Frontend and mobile can use the mock during development. Backend can
verify the real implementation for contract conformance. QA can build
campaigns around known, reusable dependency scenarios.

This means simulation is no longer disconnected test plumbing. It
becomes **shared, traceable, versioned behavior**.

When the API contract evolves, the simulation workflow has a natural
place to evolve with it.

**Transition:** Now let's look at what this makes possible for QA.

------------------------------------------------------------------------

## Slide 6 --- Campaign 1: Negative Paths on Demand

**Purpose:** Show immediate, concrete testing value.

**Speaker script**

The first opportunity is systematic negative-path testing.

Some conditions are easy to describe but surprisingly inconvenient to
reproduce with real systems.

We may want an unknown resource to return 404. We may want a provider to
fail with a 500. We may need an empty collection, a missing optional
property, a new enum value, or another boundary condition.

With a real dependency, creating these states can require special data,
coordination, code changes, or deliberate breakage.

With controlled simulation, these become selectable test conditions.

That changes negative testing from "test whatever failures we can
conveniently produce" to **a designed campaign with repeatable
coverage**.

It also makes regression much stronger because the same scenario can be
executed again after every relevant change.

**Transition:** The same idea applies to degraded service behavior.

------------------------------------------------------------------------

## Slide 7 --- Campaign 2: Resilience and Degraded Dependencies

**Purpose:** Expand the QA conversation from functional mocking to
resilience behavior.

**Speaker script**

Dependency behavior is not only about response payloads.

We also care about what happens when a dependency is slow, unavailable,
returns an error, or gives incomplete data.

Those conditions let QA validate timeouts, retries, loading states,
fallback UI, error mapping, and user recovery.

Microcks supports configurable mock response delays, so latency
scenarios can be made repeatable instead of depending on a naturally
slow environment.

This is particularly valuable for frontend and mobile because degraded
dependency behavior often creates user-experience defects that are
difficult to reproduce consistently.

The campaign question becomes: **How does the product degrade when the
dependency degrades?**

And now QA can run that question repeatedly.

**Transition:** Our migration creates another especially valuable
campaign family.

------------------------------------------------------------------------

## Slide 8 --- Campaign 3: Migration Compatibility

**Purpose:** Connect the QA deck to the migration/contract story from
the earlier presentations.

**Speaker script**

Earlier, we described migration as moving from a legacy agreement to a
new agreement.

QA can turn those differences directly into a migration campaign.

If the legacy system returned 200 with an empty result and the new API
returns 404, test that the consumer handles the new behavior.

If a field that was effectively always present becomes optional,
deliberately remove it.

If local timestamps become UTC with offsets, test timezone boundaries.

If legacy enum codes become descriptive values, test the mapping and any
unknown-value behavior.

This gives QA a very concrete role in contract migration: **prove that
intentional API changes are safely consumed.**

The Contract Migration Matrix from the earlier deck can effectively
become an input into QA campaign design.

**Transition:** Simulation also changes when QA can start.

------------------------------------------------------------------------

## Slide 9 --- Test Earlier Than the Integrated Environment

**Purpose:** Show the shift-left opportunity for QA.

**Speaker script**

Traditionally, QA feedback often begins when enough of the real
environment exists.

API design happens. Backend implementation progresses. An integrated
environment becomes available. Then QA can exercise the behavior.

With a contract-derived mock, we can move part of that feedback much
earlier.

Once the contract and examples are sufficiently mature, QA can start
exploring behavior before the real provider is complete.

That is important because QA often asks different questions from
developers.

What happens with missing data? What does the error look like? Can the
user recover? Is this behavior ambiguous? What happens at the boundary?

Those questions are much cheaper to answer while the API is still a
design artifact.

So QA becomes a participant in **behavior validation**, not only
post-implementation validation.

**Transition:** We can take the same principle into campaign
infrastructure.

------------------------------------------------------------------------

## Slide 10 --- Disposable Environments With Controlled Dependencies

**Purpose:** Introduce process-scoped Microcks as a testing
infrastructure opportunity.

**Speaker script**

Another opportunity is to make simulation part of disposable or
campaign-specific environments.

Imagine a test campaign creating an ephemeral environment for the system
under test, while its selected external dependencies are represented by
Microcks.

The campaign can choose a known dataset, a latency profile, or a failure
profile.

The environment exists for the test, produces controlled behavior, and
can then disappear.

Microcks documents process-scoped deployment patterns for use cases such
as QA campaigns, performance testing, and sandbox-as-a-service.

This can reduce contention around shared test environments and make
campaigns much more reproducible.

It also creates an interesting path toward parallel test execution
because campaigns are less dependent on shared external state.

**Transition:** This does not mean every test should move to mocks.

------------------------------------------------------------------------

## Slide 11 --- Expand the Portfolio; Don't Replace Reality

**Purpose:** Prevent over-rotation toward mocking.

**Speaker script**

A healthy strategy uses multiple levels of realism.

At the top, we still want critical end-to-end journeys against real
systems. Those prove that the complete system actually works together.

We also want selected integration testing with real dependencies where
infrastructure and actual interoperability matter.

Below that, controlled simulation gives us broad scenario coverage:
failures, edge cases, migration differences, and degraded behavior.

And contract or component testing gives us fast feedback at even smaller
boundaries.

The decision should be based on the question we are trying to answer.

**Use real systems where realism matters. Use simulation where control,
coverage, speed, and repeatability matter.**

The two strategies strengthen each other.

**Transition:** For this to work long-term, scenarios need ownership.

------------------------------------------------------------------------

## Slide 12 --- Turn Scenarios Into Maintained Assets

**Purpose:** Define QA's role and shared ownership.

**Speaker script**

The biggest risk is recreating our current ad-hoc mock problem inside a
new tool.

So scenarios need to become maintained assets.

QA should have a strong role in designing campaigns, identifying edge
cases, and creating reusable scenario datasets.

Backend maintains the provider contract and ensures examples remain
meaningful and the implementation conforms.

Frontend and mobile validate consumer behavior and identify scenarios
that matter from the user side.

Platform operates Microcks, environment provisioning, CI integration,
access, and reliability.

The shared asset is the **contract plus examples plus reusable QA
scenarios**.

A good scenario should survive the person who created it. And when the
contract changes, there should be an obvious workflow for deciding
whether that scenario changes too.

**Transition:** We can prove the value without transforming every
campaign at once.

------------------------------------------------------------------------

## Slide 13 --- Don't Wait for Reality. Design the Condition.

**Purpose:** Close with a concrete adoption proposition.

**Speaker script**

The opportunity for QA is more control over the conditions we test.

I would start with three campaign families.

First, **migration compatibility**: systematically test the known
differences between legacy and new behavior.

Second, **resilience**: latency, errors, partial responses, fallbacks,
and recovery.

Third, **negative paths**: rare or inconvenient states that are
difficult to manufacture in real dependencies.

Keep the critical end-to-end campaigns. Keep real-system integration
where it matters.

But add controlled simulation where it gives us better coverage and
repeatability.

The objective is not more mocks.

The objective is **more deliberate testing**.

**Final line:** **Don't wait for reality. Design the condition.**
