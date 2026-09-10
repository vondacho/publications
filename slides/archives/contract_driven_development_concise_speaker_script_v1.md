# Contract-Driven Development --- Concise Speaker Script

> **Format:** one core message + a few speaking cues per slide.\
> **Target pace:** roughly 45--75 seconds per slide.\
> **Rule:** explain the diagram; do not read the slide.

------------------------------------------------------------------------

# Part I --- Migrating the Agreement

## 1 --- Contract-Driven Development

**Core message:** Migration is not only replacing an API. It is
migrating an agreement.

-   Backend, frontend and mobile must converge on the same observable
    behavior.
-   Contract-first establishes that agreement early.
-   Contract-driven makes it executable.

**Transition:** Where does the friction come from?

## 2 --- Our Reality

**Core message:** Independent teams + an existing system + a new API
create expectation gaps.

-   Backend builds the future API.
-   Frontend/mobile already embody legacy assumptions.
-   The problem is not who is right; it is what behavior we agree to
    support.

**Transition:** We hear those gaps in a familiar sentence.

## 3 --- "But the old API did..."

**Core message:** Most migration friction is discovered too late.

-   Optional vs always present.
-   `404` vs legacy `200`.
-   `null` vs empty, renamed fields, timestamps, enums.
-   These are cheap decisions early and expensive fixes during
    integration.

**Key line:** **We don't need fewer disagreements. We need cheaper
disagreements.**

## 4 --- Three Sources of Truth

**Core message:** During migration, three truths coexist.

-   Legacy system: what it actually does.
-   Consumers: what they expect.
-   New specification: what we want.
-   The differences form the **migration gap**.

**Transition:** Which means the contract is bigger than the
specification.

## 5 --- The Hidden Contract

**Core message:** Existing applications contain undocumented contracts.

-   Nullability, defaults, ordering, errors, dates, pagination, enums.
-   OpenAPI captures the formal contract; consumer behavior exposes the
    implicit one.
-   We need to decide which assumptions survive the migration.

## 6 --- Migration = Migrating an Agreement

**Core message:** Preserve or change behavior intentionally.

-   Discover the existing agreement.
-   Decide what remains compatible and what changes.
-   Encode the future agreement explicitly.

**Key line:** **We don't have to preserve every legacy behavior. Every
important difference should be intentional.**

## 7 --- Contract-First

**Core message:** Agree on observable behavior before implementation
makes it expensive to change.

-   Backend brings provider/domain knowledge.
-   Frontend/mobile bring consumer expectations.
-   Review contract, examples, errors and edge cases together.

**Key line:** **Backend owns the implementation; the integration
agreement is shared.**

## 8 --- Contract-Driven

**Core message:** Contract-first defines the order; contract-driven
defines the system.

-   Contract drives mocks, tests, documentation and validation.
-   It becomes an executable development artifact.
-   Automation detects drift earlier than humans do.

## 9 --- Contract → Mock → Parallel Development

**Core message:** The agreed API can exist before the real API exists.

-   Microcks turns the contract and examples into a mock.
-   Frontend/mobile start immediately.
-   Backend implements independently.
-   Both sides work against the same target.

**Key line:** **The contract is the source of truth. Microcks makes it
executable.**

## 10 --- Contract Archaeology

**Core message:** Migration needs a deliberate discovery loop.

**Discover → Compare → Decide → Encode → Enforce**

-   Discover legacy behavior and consumer assumptions.
-   Compare with the new API.
-   Decide intentionally.
-   Encode in contract/examples.
-   Enforce through automation.

## 11 --- Contract Migration Matrix

**Core message:** Turn integration arguments into explicit migration
decisions.

-   Legacy behavior.
-   Consumer expectation.
-   New contract.
-   Decision and owner.

**Key line:** **A mismatch becomes a decision, not a surprise.**

## 12 --- Move Disagreement Left

**Core message:** Move feedback from integration time to contract-review
time.

-   Old: implement → deploy → integrate → discover mismatch → rework.
-   New: propose → review → mock → implement independently → verify.

**Key line:** **A 15-minute disagreement today can prevent days of
rework later.**

## 13 --- Contract Ready / Contract Done

**Core message:** An OpenAPI file existing does not mean the API is
ready.

**Ready:** examples, errors, nullability, status codes, migration
differences and consumer review are clear.

**Done:** specification, implementation, tests and consumer expectations
agree.

## 14 --- Contract Change Protocol

**Core message:** Contract evolution needs lightweight governance.

-   Contract change through Git.
-   Validate compatibility.
-   Update mock.
-   Review consumer impact where necessary.
-   Record migration decisions.

**Key line:** **Review the contract change before the implementation
makes it real.**

## 15 --- Agree First. Build Independently. Verify Continuously.

**Core message:** This is the operating model.

-   **Agree first.**
-   **Build independently.**
-   **Verify continuously.**

**Close:** **One contract. Shared expectations. Independent delivery.**

------------------------------------------------------------------------

# Part II --- Integrating Microcks

## 1 --- From Contract to Capability

**Core message:** Part I defined the operating model. Part II makes it
executable.

**Contract → Mock → Implement → Verify → Gate**

Microcks connects the contract to the development and delivery workflow.

## 2 --- Shared Contract Runtime

**Core message:** Microcks operationalizes the contract across teams.

-   Git/OpenAPI remains the source.
-   Consumers get mocks.
-   Backend gets conformance tests.
-   CI/CD gets a quality signal.

**Key line:** **Don't just install Microcks; connect it to decision
points.**

## 3 --- Git Remains the Source of Truth

**Core message:** Author and review contracts in Git; publish them to
Microcks.

**PR → validate → review → merge → import → mock/test**

-   Traceable.
-   Reviewable.
-   Automatable.

**Key line:** **Microcks consumes the contract; it does not replace
contract ownership.**

## 4 --- Examples Are Executable Behavior

**Core message:** Schemas define validity; examples make useful behavior
executable.

Focus examples on migration friction:

-   missing/optional fields;
-   `null` vs empty;
-   errors and status codes;
-   dates;
-   enums;
-   realistic edge cases.

**Key line:** **A mock is only as useful as the examples behind it.**

## 5 --- Nearshore Consumer Workflow

**Core message:** Frontend/mobile should not wait for backend
availability.

-   Review contract.
-   Consume stable Microcks mock.
-   Build and validate assumptions.
-   Raise mismatches early.
-   Switch base URL to the real API later.

**Key line:** **One client. Two endpoints. No rewrite.**

## 6 --- Backend Workflow

**Core message:** The real implementation must prove it satisfies the
agreement.

**Build → preview deployment → Microcks test → pass/fail**

If it fails: - fix implementation; or - explicitly change the contract.

**Key line:** **Never let implementation silently redefine the
contract.**

## 7 --- CI/CD

**Core message:** Make contract verification a normal pipeline gate.

-   Deploy preview.
-   Run Microcks tests / CLI.
-   Publish the result.
-   Fail → stop promotion.
-   Pass → continue.

**Key line:** **Contract conformance becomes as normal as unit tests.**

## 8 --- Environment Model

**Core message:** Consumers need stability; provider verification
benefits from ephemerality.

-   **Shared Microcks mock:** stable consumer endpoint.
-   **Preview API:** temporary backend environment.
-   Microcks verifies previews against the same contract.

**Key line:** **Stable mock, ephemeral provider.**

## 9 --- Security and Access

**Core message:** Treat Microcks as delivery-platform infrastructure.

-   SSO/OIDC for people.
-   Service accounts for automation.
-   Secrets outside specifications and pipelines.
-   Least-privilege network access.

Keep this boring and standardized.

## 10 --- Ownership

**Core message:** Tool ownership and contract ownership are different.

-   Backend: provider contract quality and implementation.
-   FE/mobile: consumer review and scenarios.
-   Platform: Microcks runtime and CI integration.
-   Governance: conventions and compatibility.

**Key line:** **Microcks exposes ownership; it doesn't replace it.**

## 11 --- Rollout

**Core message:** Start small and prove the workflow.

**1. Simulate** --- one migration API + realistic mock.\
**2. Verify** --- provider tests in CI.\
**3. Govern** --- compatibility, ownership and metrics.

Measure: - late integration defects ↓ - rework ↓ - integration lead time
↓ - pre-release detection ↑

**Key line:** **Start with one painful migration API.**

## 12 --- Contract → Mock → Implement → Verify → Gate

**Core message:** This is the complete integration pattern.

-   **Contract:** agree.
-   **Mock:** make it available.
-   **Implement:** work independently.
-   **Verify:** prove conformance.
-   **Gate:** prevent drift.

**Final close:**\
**Microcks is not the objective. Earlier feedback is.**

**One contract. Executable expectations.**

------------------------------------------------------------------------

# Three Messages to Remember

If time is short, reduce both presentations to these three statements:

1.  **Migration is the migration of an agreement---not only an API.**
2.  **Move disagreement left: make expectations executable before
    integration.**
3.  **Use Microcks to turn the contract into mocks, verification and
    delivery gates.**

**Final line:** **Agree first. Build independently. Verify
continuously.**
