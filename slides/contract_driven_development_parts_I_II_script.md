# Contract-Driven Development --- Presentation Script

## Speaker guide

This script accompanies the two-part presentation series:

-   **Part I --- Contract-Driven Development: Migrating the Agreement**
-   **Part II --- From Contract to Capability: Integrating Microcks**

The text is written as speaker notes rather than slide copy. Use it
conversationally; the goal is not to read every sentence verbatim. A
typical pace is **1.5--2.5 minutes per slide**, with extra time on the
workflow and migration slides.

------------------------------------------------------------------------

# Part I --- Contract-Driven Development: Migrating the Agreement

## Slide 1 --- Contract-Driven Development

**Purpose:** Set up the problem as an integration and migration problem,
not an API-documentation problem.

**Speaker script**

Today I want to talk about contract-first and contract-driven
development, but from the perspective of a problem we actually
experience.

We have a backend team providing a public REST API, and frontend and
mobile development performed by a nearshore team. At the same time, we
are moving from an existing system to a new platform and a new API
specification.

That sounds like a technical migration. But the difficult part is
usually not implementing endpoints. The difficult part is making sure
that everyone has the same understanding of what those endpoints mean
and how they behave.

The central idea of this presentation is simple: **migration is not only
replacing an API. It is migrating an agreement.**

Contract-first helps us establish that agreement earlier.
Contract-driven development goes further and makes the agreement
executable throughout development and delivery.

**Transition:** Before looking at the solution, let's look at where the
friction actually comes from.

------------------------------------------------------------------------

## Slide 2 --- Our Reality

**Purpose:** Establish the organizational and architectural boundaries.

**Speaker script**

Our delivery model has several independent moving parts.

The backend team designs and implements the new public REST API.
Frontend and mobile have already accumulated behavior and assumptions
from the existing system. The nearshore team needs enough stability to
develop independently, while the backend needs freedom to modernize the
platform.

During migration, those goals can conflict.

The backend may correctly implement the new specification and still
break an existing consumer. The consumer may correctly reproduce
existing behavior and still violate the intended new API model.

So the question is not, "Which team is right?" The useful question is,
**"Which behavior have we agreed to support?"**

That distinction changes the conversation from ownership and blame to an
explicit migration decision.

**Transition:** And we usually discover these decisions through a very
familiar sentence.

------------------------------------------------------------------------

## Slide 3 --- "But the old API did..."

**Purpose:** Make the pain recognizable.

**Speaker script**

This is where migration friction becomes visible.

The backend says, "This field is optional according to the new
specification." Frontend says, "But it has always been present."

The backend says, "A missing resource returns 404." Mobile says, "The
old system returned 200 with an empty result."

Or we change a field name, an enum, timestamp semantics, pagination
behavior, or the difference between `null`, an omitted property, and an
empty collection.

None of these examples is especially difficult to code. What makes them
expensive is discovering them late.

By the time they appear during integration or regression testing, code
exists on both sides, tickets are already considered complete, and
changing behavior requires coordination.

Our objective is therefore not to eliminate disagreement. **It is to
make disagreement happen earlier, when it is cheap.**

**Transition:** During migration, this happens because we are dealing
with more than one version of the truth.

------------------------------------------------------------------------

## Slide 4 --- Three Sources of Truth

**Purpose:** Introduce the migration gap.

**Speaker script**

At the beginning of a migration, we effectively have three sources of
truth.

First, there is the **legacy system's actual behavior**. Not what its
documentation says---the behavior consumers really see.

Second, there are the **existing frontend and mobile expectations**.
These applications contain assumptions that may never have been written
down.

Third, there is the **new API specification**, describing how we want
the future platform to behave.

Those three things will not automatically agree.

The space between them is what I call the **migration gap**. That gap
contains our compatibility issues, hidden assumptions, migration
decisions, and much of our rework.

A successful migration makes those differences explicit rather than
allowing integration testing to discover them accidentally.

**Transition:** This leads to an important observation about what an API
contract actually is.

------------------------------------------------------------------------

## Slide 5 --- The Hidden Contract

**Purpose:** Broaden "contract" beyond OpenAPI syntax.

**Speaker script**

An OpenAPI document is extremely valuable, but our real contract is
larger than the OpenAPI file.

The existing applications encode an implicit contract: nullability
assumptions, ordering, error semantics, default values, pagination, date
formats, enum values, authentication behavior, and sometimes even legacy
quirks.

If frontend code assumes a property always exists, that assumption is
part of the migration problem whether or not the old specification
documented it.

So when we create the new API contract, we should not simply ask, "Is
this OpenAPI valid?"

We should ask, **"Does this describe the observable behavior that
consumers need, and have we consciously decided where the new behavior
differs?"**

That is the difference between schema work and contract work.

**Transition:** Once we see the hidden contract, migration looks
different.

------------------------------------------------------------------------

## Slide 6 --- Migration = Migrating an Agreement

**Purpose:** Deliver the conceptual pivot.

**Speaker script**

This is the main idea of Part I.

A system migration is not complete because the new endpoint exists. It
is complete when producers and consumers have moved to a new, shared
agreement.

That agreement includes structure, but also behavior.

What does a missing resource mean? What is guaranteed to be present?
Which changes are intentionally breaking? How long will compatibility be
preserved? How should a consumer migrate?

Thinking this way changes our engineering objective.

Instead of trying to reproduce the legacy implementation, we identify
the legacy **agreement**, decide what survives, decide what changes, and
encode the result in the new contract.

This also gives us a much better way to discuss modernization. We do not
need to preserve every historical behavior. We need to make every
important difference **intentional**.

**Transition:** That is where contract-first enters the picture.

------------------------------------------------------------------------

## Slide 7 --- Contract-First

**Purpose:** Define contract-first as a collaborative ordering decision.

**Speaker script**

Contract-first means that the observable interface is agreed before
implementation becomes the de facto truth.

It does not mean that the backend writes a YAML file before writing Java
and then sends it to consumers.

The important word is **agreement**.

The backend brings implementation and domain knowledge. Frontend and
mobile bring consumer requirements and existing assumptions. Product or
architecture brings the intended future behavior.

Together, we review the contract, examples, error behavior, edge cases,
and migration differences before either side commits deeply to
implementation.

The backend can remain accountable for the public API. But the
integration agreement should not be created in isolation from its
consumers.

**Transition:** Contract-first tells us when to agree. Contract-driven
development tells us what to do with that agreement.

------------------------------------------------------------------------

## Slide 8 --- Contract-Driven

**Purpose:** Distinguish contract-first from contract-driven.

**Speaker script**

Contract-first is an ordering decision: contract before implementation.

Contract-driven development is an engineering system.

The contract becomes an input to multiple activities: documentation,
mocks, examples, provider verification, consumer development,
compatibility checks, and CI/CD gates.

That is the shift from a document that humans read to an artifact that
our delivery process can execute.

This matters because documentation alone cannot prevent drift.

If the implementation can change without the contract noticing, or the
contract can change without consumers noticing, we still discover
problems late.

The goal is an executable feedback loop around the shared agreement.

**Transition:** One of the first benefits of making the contract
executable is parallel development.

------------------------------------------------------------------------

## Slide 9 --- Contract → Mock → Parallel Development

**Purpose:** Introduce Microcks as an enabler, not the protagonist.

**Speaker script**

Once we have an agreed OpenAPI contract with useful examples, we can
create a realistic mock before the backend implementation is finished.

This is where Microcks enters our story.

Microcks can consume the API contract and expose a mock endpoint.
Frontend and mobile can build against that endpoint while the backend
implements the real service independently.

This changes an important dependency.

Today, consumers may wait for a backend deployment before they can
validate assumptions. With a contract-driven workflow, they can validate
the contract itself much earlier.

If the mock feels wrong to frontend or mobile, that is useful
information. We want that feedback while we are still discussing the
contract---not after the backend implementation has become expensive to
change.

Microcks is therefore not the source of truth. **The contract is the
source of truth; Microcks makes it executable.**

**Transition:** For migration, however, we need one additional
discipline before we declare the new contract correct.

------------------------------------------------------------------------

## Slide 10 --- Contract Archaeology

**Purpose:** Introduce a repeatable migration discovery process.

**Speaker script**

I call this **contract archaeology**.

Before finalizing a migrated API, we deliberately discover the behaviors
that matter.

The sequence is: **discover, compare, decide, encode, enforce.**

Discover what the legacy API actually does and what the existing
consumers depend on.

Compare that with the proposed new API.

For every meaningful difference, make a decision. Is this a behavior we
preserve? Is it intentionally changed? Do we need an adapter or
migration period?

Then encode the chosen behavior in the contract and examples.

Finally, enforce it with mocks, tests, compatibility checks, and the
delivery pipeline.

The important part is the word "decide." Contract-driven development
should not freeze the legacy system. It should make modernization
decisions explicit.

**Transition:** We need a lightweight artifact to capture those
decisions.

------------------------------------------------------------------------

## Slide 11 --- The Contract Migration Matrix

**Purpose:** Make migration disagreements operational.

**Speaker script**

The Contract Migration Matrix is intentionally simple.

For each relevant behavior, we record the legacy behavior, the existing
consumer expectation, the proposed new contract, and the decision.

For example, the legacy API might expose `customerNumber`, while the new
API uses `customerId`. That is not merely a field rename---it is a
consumer migration item.

The legacy system may return an empty array where the new model permits
`null`. We decide whether to preserve the empty array or explicitly
migrate consumers.

An unknown ID might move from a legacy 200 response to a proper 404.
Again, that can be a good change, but it should be an intentional change
with known consumer impact.

In practice I would add owner, affected consumers, target release, and
status.

The benefit is that disagreements become visible **migration
decisions**, rather than disappearing into chat messages and integration
bugs.

**Transition:** Now we can redesign the delivery workflow around earlier
decisions.

------------------------------------------------------------------------

## Slide 12 --- Move Disagreement Left

**Purpose:** Contrast late integration with early contract feedback.

**Speaker script**

The traditional flow is expensive.

Backend specification, backend implementation, deployment, consumer
integration---and only then do we discover a mismatch. That leads to a
ticket, clarification, changes, redeployment, and retesting.

The proposed flow moves the same disagreement earlier.

We propose the API, review the contract with consumers, encode examples,
publish a mock, and let frontend and mobile exercise the intended
behavior before the provider is complete.

The backend and consumer teams can then implement independently against
the same agreement.

Notice the objective: **we do not want fewer disagreements; we want
cheaper disagreements.**

A disagreement in a contract review may cost minutes. The same
disagreement discovered in mobile regression testing can cost days and
interrupt multiple teams.

**Transition:** To make this sustainable, we need a shared definition of
when a contract is actually ready.

------------------------------------------------------------------------

## Slide 13 --- Contract Ready / Contract Done

**Purpose:** Establish practical quality gates.

**Speaker script**

An API should not be considered ready simply because an OpenAPI file
exists.

"Contract Ready" means the contract is valid and sufficiently precise
for independent implementation.

That includes realistic request and response examples, explicit required
and optional properties, nullability, status codes, errors, enums,
pagination semantics, authentication behavior, migration differences,
consumer review, and a working mock.

Then we also need "Contract Done."

A backend ticket is not done merely because the implementation merged.
We want the specification, implementation, contract tests, compatibility
assessment, consumer validation, and migration decisions to agree.

This gives both sides a shared definition of integration readiness and
completion.

**Transition:** Those definitions only work if contract changes travel
through a predictable path.

------------------------------------------------------------------------

## Slide 14 --- Contract Change Protocol

**Purpose:** Recommend lightweight governance.

**Speaker script**

We do not need to start with a large API governance program.

We need a lightweight contract-change protocol.

An API change begins with a contract change in version control.
Automated validation and compatibility checks run. The mock is updated.
Affected consumers can review or validate the behavior. If there is
migration impact, the decision is recorded before the implementation is
treated as complete.

The key rule is: **review the contract change before---or at least
independently from---the implementation change.**

That lets reviewers reason about consumer impact without having to
reverse-engineer the intended API from backend code.

Governance should make delivery faster by preventing expensive
surprises. If it becomes ceremony without feedback, we have missed the
point.

**Transition:** So what does success look like?

------------------------------------------------------------------------

## Slide 15 --- Agree First. Build Independently. Verify Continuously.

**Purpose:** Close Part I and tee up Part II.

**Speaker script**

The operating model can be summarized in three lines.

**Agree first.** Make the observable behavior explicit before
implementation makes decisions expensive.

**Build independently.** Give backend, frontend, and mobile a shared
executable target so teams do not need to wait for one another.

**Verify continuously.** Use automation to detect when implementation or
contract drifts from the agreement.

The goal is not to introduce more API process. The goal is to reduce
integration friction, especially during migration.

Distance between teams should not create distance between expectations.

**One contract. Shared expectations. Independent delivery.**

Part II takes this operating model and makes it concrete: how we
integrate Microcks into Git, consumer development, backend verification,
and CI/CD.

------------------------------------------------------------------------

# Part II --- From Contract to Capability: Integrating Microcks

## Slide 1 --- From Contract to Capability

**Purpose:** Reconnect to Part I and introduce the implementation focus.

**Speaker script**

Part I established the operating principle: agree first, build
independently, and verify continuously.

Part II is about making that practical with Microcks.

The goal is not simply to install a new tool. The goal is to connect the
contract to the moments where teams make decisions.

We want the OpenAPI contract and its examples to drive three
capabilities: a mock that consumers can use, conformance tests that
providers can run, and a delivery gate that prevents accidental drift.

So the progression is straightforward: **contract, mock, implement,
verify, gate.**

**Transition:** Let's start with where Microcks belongs in the
architecture.

------------------------------------------------------------------------

## Slide 2 --- Microcks Becomes the Shared Contract Runtime

**Purpose:** Establish the target architecture.

**Speaker script**

Git remains where the contract is authored and reviewed.

Microcks sits downstream from that source of truth and turns the
contract into runtime capabilities.

For frontend and mobile, it provides a mock endpoint based on the agreed
contract and examples.

For backend, it provides conformance testing against a deployed
implementation.

For CI/CD, it provides a machine-readable pass or fail signal that can
participate in release decisions.

This is why I describe Microcks as a **shared contract runtime**.

It does not replace Git, OpenAPI review, or team ownership. It
operationalizes the agreement across the delivery lifecycle.

**Transition:** That separation between Git and Microcks is important
enough to make explicit.

------------------------------------------------------------------------

## Slide 3 --- Git Remains the Source of Truth

**Purpose:** Define the contract publication flow.

**Speaker script**

I recommend that teams continue to author the API contract in the same
version-controlled workflow as other source artifacts.

A pull request changes the OpenAPI specification and examples.
Validation runs. Review happens. The contract is merged. Then automation
imports or synchronizes the artifact into Microcks.

Microcks should consume the contract; it should not become the primary
place where the contract is manually edited.

This gives us traceability. We know which commit changed behavior, who
reviewed it, what compatibility discussion happened, and which version
was published.

The exact automation can depend on our platform model. We can use
Microcks import mechanisms, APIs, or `microcks-cli` where appropriate.

The principle matters more than the mechanism: **a contract reaches
Microcks through the reviewed Git path.**

**Transition:** But importing an OpenAPI schema alone does not
automatically produce a useful simulation.

------------------------------------------------------------------------

## Slide 4 --- Examples Turn a Schema Into a Useful Simulation

**Purpose:** Explain why examples are central to Microcks value.

**Speaker script**

A schema tells us what is structurally valid.

Examples tell us what we expect an interaction to look like.

That distinction is especially important during migration.

We should encode the cases that usually create friction: missing fields,
empty collections versus `null`, 404 versus legacy 200 behavior, date
and timezone semantics, enum evolution, and realistic error responses.

Microcks can use the contract and examples to expose useful mocks.

So examples should not be treated as decorative documentation. They are
part of our executable specification.

A mock with only a perfect happy path can actually hide migration risk.
The valuable mock is the one that lets consumers exercise the behaviors
we have explicitly agreed.

**Transition:** With those examples in place, the consumer workflow
changes significantly.

------------------------------------------------------------------------

## Slide 5 --- Nearshore Consumer Workflow

**Purpose:** Show how frontend/mobile use Microcks day to day.

**Speaker script**

This is one of the highest-value changes for our nearshore frontend and
mobile teams.

The contract is proposed and reviewed. Examples are agreed. Microcks
publishes a stable mock endpoint.

The consumer team configures its API base URL to point to that mock and
starts development.

If an expected behavior is missing or incorrect, the team raises the
mismatch immediately. We update the agreement before both sides have
invested heavily in incompatible implementations.

When the real backend becomes available, the consumer changes the
endpoint from mock to real.

The important design goal is **one client, two endpoints**. Switching
from Microcks to the real service should not require rewriting client
logic.

This gives the nearshore team independence without inventing its own
mock behavior.

**Transition:** In parallel, the backend gets a complementary workflow.

------------------------------------------------------------------------

## Slide 6 --- Backend Workflow: Prove Conformance

**Purpose:** Explain provider-side contract testing.

**Speaker script**

For backend, the contract becomes a verification target.

The backend builds the service and deploys it to a preview or test
environment.

Microcks then exercises that deployed endpoint according to the API
contract.

If the implementation conforms, the pipeline continues. If it does not,
we have useful feedback before promotion.

A failed test can mean two different things.

The implementation may be wrong relative to the agreed contract. In that
case, fix the implementation.

Or the contract itself may need to change because we discovered a
legitimate design issue. In that case, we return to the contract
workflow and make that decision explicitly.

What we should avoid is silently changing implementation behavior and
allowing the specification to drift behind it.

**Transition:** To make that repeatable, we connect the verification to
CI/CD.

------------------------------------------------------------------------

## Slide 7 --- Put It in CI/CD

**Purpose:** Show the automation pattern.

**Speaker script**

A contract gate should be boring, repeatable, and visible.

A typical pipeline can validate the contract, build the provider, deploy
a preview environment, invoke Microcks tests---commonly through
`microcks-cli` or the relevant automation interface---and collect the
result.

A failure blocks promotion. A pass allows the pipeline to continue.

The detailed report should remain accessible from the pull request or
pipeline so developers can understand what failed.

For machine-to-machine authentication, use dedicated service accounts
rather than personal credentials.

The exact command will depend on service name, version, test endpoint,
and test strategy. The important architectural point is that **contract
conformance becomes a normal delivery signal**, just like unit tests or
static analysis.

**Transition:** We also need to be deliberate about which environments
are stable and which are ephemeral.

------------------------------------------------------------------------

## Slide 8 --- Environment Model

**Purpose:** Separate consumer mock stability from provider test
dynamism.

**Speaker script**

I recommend separating two concerns.

The first is a **shared mock plane**. Frontend and mobile need a stable
URL backed by versioned contracts and agreed scenarios. They should not
have to chase a different mock URL for every backend branch.

The second is a **provider verification plane**. Backend pull requests
can deploy ephemeral or preview environments. Microcks tests those
environments and attaches the result to the delivery workflow.

This gives us stability where consumers need stability and ephemerality
where backend delivery benefits from it.

Branch-specific mocks can still exist when there is a real need to
preview a proposed contract change. But they should be intentional, not
the default consumer experience.

**Transition:** Once Microcks participates in delivery, we need to treat
it as platform infrastructure.

------------------------------------------------------------------------

## Slide 9 --- Integrate Safely

**Purpose:** Cover security and access without turning the deck into an
infrastructure manual.

**Speaker script**

Microcks is now part of the development and delivery path, so access and
credentials deserve the same discipline as the rest of our platform.

Human access should integrate with our identity model, for example SSO
or OIDC where applicable.

CI/CD should use named service accounts with least privilege.

Credentials for private Git repositories, secured APIs, or test
endpoints should come from the platform's secret-management
mechanism---not be embedded in API specifications or pipeline source.

Network policy also matters. Microcks must be able to reach the preview
endpoints it is expected to test, but that does not mean it needs broad
network access.

The principle is straightforward: **make contract testing automated
without making credentials or connectivity informal.**

**Transition:** Tooling also fails when nobody knows who owns which part
of the workflow.

------------------------------------------------------------------------

## Slide 10 --- Operating Model and Ownership

**Purpose:** Prevent Microcks from becoming an unowned platform tool.

**Speaker script**

Microcks does not remove ownership. It makes ownership boundaries more
visible.

The backend team owns contract quality from the provider side,
meaningful examples, and fixes when implementation does not conform.

Frontend and mobile participate in consumer review, identify missing
scenarios, and provide early feedback on proposed behavior.

The platform team owns the Microcks runtime, CI/CD integration,
authentication, connectivity, and operational reliability.

API governance or architecture can provide conventions, compatibility
rules, and an escalation path for important breaking changes.

The shared responsibility is the contract-change review and the
migration decision.

If everyone assumes "the Microcks team" owns contract quality, the tool
will become shelfware. The contract remains a product-team
responsibility.

**Transition:** We should introduce this model incrementally.

------------------------------------------------------------------------

## Slide 11 --- Rollout in Three Layers

**Purpose:** Recommend a pragmatic adoption sequence and metrics.

**Speaker script**

I would not roll out every capability across every API at once.

Start with one painful migration API.

**Phase one: simulate.** Import the contract, improve the examples,
publish a realistic mock, and connect frontend and mobile.

This alone tests whether early consumer feedback reduces integration
friction.

**Phase two: verify.** Deploy the provider to a preview environment, run
Microcks conformance tests from CI, and attach the result to the pull
request or pipeline.

**Phase three: govern.** Add compatibility rules, service accounts,
ownership conventions, and metrics once the workflow has demonstrated
value.

Measure outcomes, not tool usage.

Useful signals are fewer integration defects found late, fewer
clarification and rework tickets, shorter time from contract-ready to
consumer integration, and more provider conformance failures caught
before release.

**Transition:** That leaves us with a simple integration pattern.

------------------------------------------------------------------------

## Slide 12 --- Contract → Mock → Implement → Verify → Gate

**Purpose:** Close Part II with the operational model.

**Speaker script**

The full pattern is now simple.

**Contract:** agree on observable behavior and realistic examples.

**Mock:** make that behavior available immediately to frontend and
mobile.

**Implement:** allow backend and consumers to build independently.

**Verify:** test the real provider against the same agreement.

**Gate:** prevent accidental contract drift from reaching production
unnoticed.

Microcks is successful when teams stop discovering contract drift during
late integration.

The tool is not the objective. The objective is earlier feedback,
independent delivery, and a shared understanding that survives the
migration.

So the final message across both presentations is:

**One contract. Executable expectations.**

------------------------------------------------------------------------

# Optional Q&A Talking Points

## "Does this mean the backend loses ownership of the API?"

No. Backend can remain accountable for the public API and its
implementation. Contract-driven development distinguishes
**implementation ownership** from **agreement participation**. Consumers
should participate early when a contract change affects them.

## "Are we trying to preserve all legacy behavior?"

No. The objective is not legacy compatibility at any cost. Contract
archaeology makes differences explicit so we can deliberately
**preserve, adapt, deprecate, or break** behavior.

## "Why not just let frontend create its own mocks?"

Consumer-owned mocks are useful for isolated tests, but they can encode
the consumer's assumptions rather than the shared agreement. A Microcks
mock generated from the reviewed contract gives teams a common
behavioral target.

## "Is OpenAPI enough?"

OpenAPI is the foundation for the REST API contract, but useful
contract-driven development also needs meaningful examples and explicit
semantics around errors, nullability, status codes, enums, pagination,
dates, and migration behavior.

## "Does every pull request need frontend/mobile approval?"

Not necessarily. Consumer review should be proportional to impact.
Automated compatibility checks and clear ownership can keep
non-impacting changes lightweight. The goal is earlier feedback, not a
new approval bottleneck.

## "What happens when the implementation reveals that the contract is wrong?"

That is expected. Change the contract through the reviewed contract
workflow, update examples and migration decisions, republish it, and
then bring implementation and consumers back into conformance. The
important thing is to avoid silent drift.

## "Where should we pilot this?"

Choose one migration API with recurring integration friction, an active
frontend or mobile consumer, and enough upcoming change to demonstrate
the benefit. Avoid starting with either the easiest API or the entire
API estate.

------------------------------------------------------------------------

# Closing statement

Contract-driven development is not primarily about OpenAPI, Microcks, or
another layer of governance.

It is about changing **when** we discover that two teams understood the
same interface differently.

During migration, those differences already exist. Our choice is whether
we discover them deliberately while they are still cheap---or
accidentally during integration when they are expensive.

**Agree first. Build independently. Verify continuously.**
