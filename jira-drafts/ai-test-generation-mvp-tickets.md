# Proposed Tickets: AI Test Generation MVP

Status: Draft for review. Do not publish without owner approval.

All tickets below use:

- Project: `FLPATH`
- Label: `lightwell`
- Parent: proposed `AI Test Generation MVP` Epic

## Dependency and Blocker Matrix

The following relationships should be represented as Jira links when tickets are created. `blocks` means the downstream item should not be considered implementation-ready until the upstream item is resolved or explicitly waived. Some relationships are discovery dependencies rather than hard execution gates.

| Item | Blocked by / prerequisite | Blocks or informs |
|---|---|---|
| VI-1 | Authenticated VPE/platform request envelope and target identity contract | VI-2, VI-3, VI-4, TG-1, TG-2 |
| VI-2 | A&P/VPE decision on authoritative VEX format/version and retrieval/authentication (AP-S3) | VI-4, TF-1, TG-3, final-demo integration |
| VI-3 | A&P/VPE evaluated policy decision schema (AP-S1) | VI-4, TG-2, TG-3, TG-4, TG-7 |
| VI-4 | VI-1, VI-2, VI-3 | TG-3, TG-4, TF-4 |
| TF-1 | A&P-selected Java 21/Quarkus fixture and base/candidate source | TF-2, TF-3, TF-4, TF-5, TG-6, TG-7 |
| TF-2 | TF-1 repository/profile and approved source access | TF-3, TF-4, TG-3, TG-5 |
| TF-3 | TF-1 and TF-2 framework/profile capabilities | TG-5, TG-6 |
| TF-4 | TF-1, TF-2, TF-3, execution-provider capability decision | TG-4, TG-6 |
| TF-5 | TF-1 through TF-4 | TG-5, TG-6, TG-7 |
| TG-1 | ADR contract constraints; shared workflow/run-state ownership | TG-2 through TG-7, TG-S2, TG-S3 |
| TG-2 | TG-1; platform readiness and execution/evidence capability ownership | VI-1, TG-3, TG-4, TG-5, TG-6 |
| TG-3 | VI-4, TF-1, TF-2, TG-1/TG-2 | TG-4, TF-4 |
| TG-4 | TG-3, TF-4, TG-1/TG-2 | TG-5, TG-S2 |
| TG-5 | TG-3, TG-4, TF-3, TG-1/TG-2 | TG-6, TG-7 |
| TG-6 | TG-5, TF-1 through TF-4, execution responsibility decision (TG-S2/AP-S2) | TG-7, REL-1, final-demo integration |
| TG-7 | TG-6, TG-S1 evaluation criteria, golden/failure fixtures | REL-1, final-demo integration |
| TG-S1 | Representative vertical slice and approved endpoint profiles | TG-5, TG-7; informs implementation choices but should not block contracts |
| TG-S2 | Shared execution-provider decision and AP-S2 coordination (FLPATH-5018) | TG-6, TG-2, final-demo integration |
| TG-S3 | Evidence owner/consumer and FLPATH-4999 release integration | REL-1, final-demo integration |
| REL-1 updates | TG-7, TG-S3, configured evidence consumer | Final-demo integration and release rehearsal |
| Final Demo Integration Epic | ATG MVP capability, A&P outputs, FLPATH-4997, FLPATH-4999 | Final end-to-end rehearsal and operational acceptance |

### Cross-cutting blocker rules

- The A&P-selected Java 21/Quarkus fixture blocks target-specific estimation; the current Spring Boot SSC harness does not remove that dependency.
- VPE VEX format and policy schema decisions block authoritative end-to-end intake; synthetic fixtures may unblock local contract tests only.
- Evidence owner/sign-off and consumer decisions block final publication acceptance, but not initial evidence-record contract work.
- The current SSC harness can support development and compatibility work; it does not unblock final-demo acceptance.
- Cryptographic attestation is not a prerequisite unless the selected evidence consumer requires it; owner sign-off and limitations acknowledgment are MVP requirements.

## VEX and Policy Input

### VI-1 - Admit and validate VPE driver requests

Issue type: Story

Summary: Validate and admit VPE driver requests for test generation

Description:

Normalize the authenticated VPE/platform request, validate target and evidence references, resolve immutable base/candidate identities, enforce authorization, and make request receipt idempotent.

Acceptance criteria:

- Invalid, unauthorized, stale, conflicting, or incomplete requests produce explicit findings.
- Duplicate delivery does not create a second run.
- Immutable repository, revision, artifact, and VPE evidence identities are retained.
- No model, repository, or execution work begins after failed admission.

### VI-2 - Ingest source-preserved VEX

Issue type: Story

Summary: Ingest and normalize the VPE-provided VEX finding

Description:

Implement the VPE-selected VEX format/version adapter. Preserve the original document, digest, statement identity, issuer, product identity, retrieval provenance, and normalization findings.

Acceptance criteria:

- The VPE-provided VEX format/version is validated explicitly.
- Unsupported versions and unmapped identities fail closed.
- Normalized fields trace to source content or an explicit identity mapping.
- Synthetic fixtures are clearly marked as non-authoritative test inputs.

### VI-3 - Ingest evaluated VPE policy decisions

Issue type: Story

Summary: Ingest typed VPE policy decisions and obligations

Description:

Accept content-addressed VPE policy decisions with reasons, obligations, evaluator identity, revision, and provenance. Compose them with local execution and safety policy deterministically.

Acceptance criteria:

- Invalid, expired, denied, or indeterminate decisions fail closed.
- Unknown obligations are rejected or routed to review.
- Local safety policy cannot be overridden by an upstream allow decision.
- Policy source text is not passed to the model as authority.

### VI-4 - Derive driver-neutral test objectives

Issue type: Story

Summary: Derive evidence-backed test objectives from VPE input

Description:

Map VEX and policy inputs to typed `TestObjective` records while preserving uncertainty, limitations, upstream references, and disposition requirements.

Acceptance criteria:

- Every objective has attributable evidence references.
- `not_affected`, `fixed`, `under_investigation`, and missing-status cases retain upstream meaning.
- Missing or conflicting context produces an explicit gap or review outcome.
- The service does not create an authoritative vulnerability score.

### VI-5 - Maintain VEX contract and development fixtures

Issue type: Task

Summary: Maintain VEX contract, negative, and development fixtures

Description:

Create version-pinned fixtures for contract tests, supported statuses, invalid documents, unsupported versions, and identity conflicts. Fixtures are development aids and cannot substitute for VPE evidence in the MVP end-to-end run.

Acceptance criteria:

- Fixtures are content-addressed and versioned.
- Each fixture identifies whether it is authoritative or synthetic.
- Invalid and unsupported cases are covered by automated tests.

## Target and Framework

### TF-1 - Deliver immutable Java target fixture

Issue type: Story

Summary: Provide immutable Java base and candidate subjects

Description:

Use the authoritative Java 21/Quarkus fixture/profile selected with the A&P work. Materialize the upstream state as base and the fixed/remediated state as candidate, with immutable source/artifact identities, intended-change references, and VPE evidence mappings. The SSC Spring Boot FSI demo is a compatibility baseline and optional fork source, not the authoritative ATG target.

Acceptance criteria:

- Base and candidate identities resolve to immutable revisions or artifact digests.
- The fixture builds reproducibly under the selected Java 21/Quarkus profile and records required credential references without embedding credentials.
- The intended change and VPE finding are traceable to the fixture.
- The selected fixture's test and coverage measurements are captured as baseline evidence, not as proof of vulnerability remediation.
- Repository-profile and framework-adapter tests run locally without the full SSC demo deployment where those boundaries are independently testable.

### TF-1a - Characterize focused differential behavior

Issue type: Task

Summary: Determine whether the SSC demo supports a safe strict differential test

Description:

Review the selected Java 21/Quarkus fixture's affected behavior and existing coverage. Identify a safe, authorized behavior test that should differ between the base and candidate states, or document why strict fix-pinning is not reachable for the current fixture.

Acceptance criteria:

- The task does not rely on the full suite passing in both states as fix evidence.
- Any focused test has an explicit expected base/candidate relationship and approved validation strategy.
- If no defensible relationship is available, record `not_reached`, `inconclusive`, or `stated_gap` with the reason.
- Active exploitation is not introduced by this task.

### TF-2 - Build the Java repository profile

Issue type: Story

Summary: Discover and validate the Java repository profile

Description:

Implement read-only discovery for module layout, framework, Maven settings/mirror, fixtures, toolchain, existing tests, and approved commands.

Acceptance criteria:

- Repository content cannot authorize commands or credentials.
- The profile is bound to immutable source identity.
- Missing, stale, or conflicting profile facts produce explicit findings.

### TF-3 - Implement native Maven/JUnit adapter

Issue type: Story

Summary: Implement the native Java test framework adapter

Description:

Implement framework discovery, capability declaration, generated-test validation, focused execution commands, collection checks, and result normalization.

Acceptance criteria:

- The adapter declares supported and unsupported capabilities explicitly.
- Generated tests are validated against repository conventions.
- Commands are selected from approved profile data, not model output.

### TF-4 - Assess feasibility and target preconditions

Issue type: Story

Summary: Gate test strategies on target feasibility

Description:

Determine which validation layers are safe and technically possible for each objective, including immutable subjects, reproducible builds, equivalent environments, and clear criteria.

Acceptance criteria:

- Feasibility constrains Plan and cannot claim validation.
- Unsupported layers become `not_evaluable`, blocked, or stated-gap outcomes.
- Base/candidate prerequisites are checked before execution.

### TF-5 - Validate Java MVP capabilities

Issue type: Task

Summary: Validate Java profile and adapter capabilities

Description:

Create the Java validation matrix covering profile accuracy, command approval, framework capability, feasibility, collection, and abstention behavior.

Acceptance criteria:

- The matrix covers positive, negative, and unsupported cases.
- Capability gaps are recorded as evidence.
- Results are reproducible from versioned fixtures.

## Test Generation Pipeline

### TG-1 - Define domain contracts and run state

Issue type: Story

Summary: Define versioned AI Test Generation contracts and run state

Description:

Define request, evidence, objective, plan, checkpoint, feedback, generation, execution, quality, provenance, preflight, compatibility, and signed differential record contracts.

Acceptance criteria:

- Schemas and state transitions are versioned and tested.
- Invalid inputs, duplicate events, stale decisions, and supersession are covered.
- Contracts do not depend on a selected orchestration or model framework.
- Where the contract boundary is meaningful, a standalone local contract-test command runs without cluster, SCM, model, or execution-provider access.
- Contract-driven mocks, simulators, deterministic fakes, or replay fixtures cover valid and failure paths for independently testable interfaces.

### TG-2 - Implement preflight and run admission

Issue type: Story

Summary: Implement stage-zero readiness checks and run admission

Description:

Verify schemas, adapters, endpoint capabilities, identity, repository access, execution provider, artifact store, evidence path, signing path, and failure-register cases before request-specific work.

Acceptance criteria:

- Required preflight failure produces a terminal record and no downstream evidence.
- Admission creates one durable run identity and is idempotent.
- Readiness checks record versions, identities, timestamps, and limitations.

### TG-3 - Analyze repository and context

Issue type: Story

Summary: Analyze repository context and identify test objectives

Description:

Perform read-only repository analysis, combine supplied and discovered context with provenance, inventory existing tests and coverage, and produce evidence-backed objective candidates.

Acceptance criteria:

- Every cited symbol, call site, existing test, and behavior has a source or evidence reference.
- The Analyze checkpoint includes assumptions, gaps, and review materials.
- Repository content cannot silently become authoritative policy.

### TG-4 - Plan tests and support human review

Issue type: Story

Summary: Produce reviewable test plans with durable checkpoints

Description:

Generate typed plan candidates, apply deterministic citation and safety gates, persist the review checkpoint, and support approve, revise, reject, and resume decisions.

Acceptance criteria:

- Human decisions are authenticated, scoped, durable, and idempotent.
- Execution capacity is released while waiting.
- Resume after controller restart uses the exact approved plan digest.

### TG-5 - Generate and validate native tests

Issue type: Story

Summary: Generate bounded native tests with exact patch provenance

Description:

Generate tests through bounded repository tools, validate syntax/format/compile/collection/assertion quality, and record exact patch and materialized-test identities.

Acceptance criteria:

- Only approved test paths can be modified.
- Generated content is bound to the approved plan and patch digest.
- Repair attempts are bounded and terminate explicitly.

### TG-6 - Execute isolated base/candidate tests

Issue type: Story

Summary: Execute differential tests in isolated workers

Description:

Run the exact approved test independently against immutable Java 21/Quarkus base and candidate subjects through the approved execution provider. Normalize framework results, logs, commands, environment, and provenance artifacts.

Acceptance criteria:

- Controller/model and repository execution credentials are separate.
- Base and candidate results have independent manifests and environment comparisons.
- Setup, collection, timeout, and infrastructure failures cannot become passing comparisons.
- Cleanup occurs only after artifacts and callbacks are durably recorded.

### TG-7 - Evaluate quality and differential evidence

Issue type: Story

Summary: Apply deterministic quality, differential, and golden-reference gates

Description:

Evaluate generated-test quality, objective coverage, differential relationships, evidence completeness, failure-register cases, endpoint conformance, and held-out behavior.

Acceptance criteria:

- A strict fix-pinning claim requires an approved focused test with expected base failure and candidate fixed behavior; the existing 121-test full-suite pass is baseline evidence only.
- Both-pass, both-fail, environment mismatch, patch drift, and missing-side cases receive explicit classifications.
- Golden-reference and failure-register results are retained with provenance.
- Quality and differential classifiers have local tests using replayed execution records before live provider integration; tightly coupled provider behavior is tested at the nearest meaningful integration boundary.

## Spikes

### TG-S1 - Evaluate implementation harness options

Issue type: Spike

Summary: Evaluate the AI Test Generation implementation harness

Description:

Run one vertical slice using an explicit state machine, deterministic fake model, and current approved endpoint. Evaluate direct SDKs, Pydantic AI, LangGraph, and reuse/fork/reproduction of `ai-test-harness` only against concrete lifecycle and quality needs.

Acceptance criteria:

- Recommends a stack per layer and reusable components.
- Records licensing, ownership, maintenance, security, and portability findings.
- Defines reconsideration triggers and does not change domain contracts to fit a framework.

### TG-S2 - Determine execution-provider responsibility split

Issue type: Spike

Summary: Determine service and Tekton execution responsibilities

Description:

Coordinate with A&P AP-S2 to determine worker ownership, callbacks, cancellation, cleanup, artifact retention, and human-wait behavior.

Acceptance criteria:

- Compares service-owned, Tekton-owned, and hybrid options.
- Identifies required changes to the shared FLPATH-4997 Demo Environment Epic.
- Produces a recommended responsibility matrix.

### TG-S3 - Select evidence ownership and sign-off path

Issue type: Spike

Summary: Select evidence ownership, review/sign-off, and optional integrity-verification path

Description:

Evaluate the evidence record, responsible owner/reviewer, approval and supersession states, configured store, verification API, retention, and policy/evidence consumer integration. Treat cryptographic attestation as optional integrity infrastructure, not as the definition of approval.

Acceptance criteria:

- Identifies the minimum viable evidence ownership, review/sign-off, and verification path.
- Defines who can approve results and acknowledge limitations.
- Distinguishes owner sign-off from optional cryptographic attestation.
- Defines the evidence references required by the shared FLPATH-4999 Release Epic.
- Records unresolved ownership and integration decisions.
