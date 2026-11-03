# AI Test Generation Repository Layout

Status: Planning sketch for temporary experiment repositories. This is not a final product-repository decision.

## Purpose

Provide contributors with stable integration points while VI, TF, TG, and spike work proceeds in parallel. The layout keeps domain contracts and orchestration independent from provider adapters, model frameworks, execution systems, and temporary demo deployment files.

## Proposed Layout

```text
ai-test-generation/
  contracts/
    schemas/                         # Versioned request, stage, result, evidence schemas
    examples/                        # Small valid examples for contract tests
    compatibility/                   # Schema compatibility and migration tests

  src/atg/
    domain/                          # Driver-neutral domain types and status taxonomy
      objectives/
      plans/
      executions/
      evidence/
    application/                     # Use cases and stage orchestration
      admission/
      analyze/
      plan/
      code/
      execute/
      evaluate/
    workflow/                        # Checkpoints, state transitions, retries, callbacks
    gates/                           # Deterministic validation and classification gates
    provenance/                      # Digests, identities, manifests, supersession
    ports/                           # Stable interfaces; no vendor/framework types
      input.py
      policy.py
      repository.py
      framework.py
      model.py
      execution.py
      evidence.py
      source_control.py
    adapters/
      input/                         # VEX/VPE request adapters
      policy/                        # VPE decision adapter; optional bundle adapter
      repository/                    # SourceProvider and repository profiles
      framework/                     # Java 21/Quarkus native adapter first
      model/                         # OpenAI-compatible endpoint profiles and runners
      execution/                     # Tekton/provider adapters
      evidence/                      # Store, signer, verifier, publication adapters
      source_control/                # Conditional PR/MR compatibility adapter
    tools/                           # Bounded tool implementations and authorization
    config/                          # Non-secret profiles and environment configuration

  tests/
    unit/                            # Fast domain/application tests
    contract/                        # Port/schema tests using mocks and simulators
    component/                       # Adapter tests with local services or containers
    replay/                          # Recorded model/provider/execution replay tests
    integration/                     # Real endpoint/provider/evidence integration
    differential/                    # Base/candidate and environment-comparison tests
    evaluation/                      # Golden references and failure-register tests

  fixtures/
    vex/                             # Authoritative-shape and synthetic development fixtures
    policy/                          # VPE decision fixtures and obligations
    repositories/                    # Metadata only; immutable target refs live in manifests
    execution/                       # JUnit/log/environment replay artifacts
    golden/                          # Golden behavior and evidence references
    failure-register/                # Known failure and regression cases

  experiments/
    harness/                         # TG-S1 candidate harness probes; never domain authority
    model-endpoints/                 # Endpoint conformance probes and reports
    providers/                       # Execution/evidence provider probes

  deploy/
    local/                           # Temporary local development composition
    development-harness/             # Temporary SSC demo integration material
    final-demo/                      # Final-demo configuration when separately approved

  docs/
    architecture/                    # Contracts, boundaries, decisions, diagrams
    runbooks/                        # Local, development-harness, and final-demo operation
    contributor/                     # Parallel-path integration instructions
```

The implementation language and package names remain provisional. The directory boundaries are the important part: contributors should integrate through ports and versioned contracts rather than importing another workstream's adapter or framework directly.

## Parallel-Path Ownership

| Path | Primary locations | Owns | Must not own |
|---|---|---|---|
| VI: VEX and policy input | `contracts/schemas`, `src/atg/adapters/input`, `src/atg/adapters/policy`, `fixtures/vex`, `fixtures/policy` | Source-preserved VPE input, normalization, obligations, input findings | Test-generation strategy, repository commands, authoritative VEX publication |
| TF: target and framework | `src/atg/adapters/repository`, `src/atg/adapters/framework`, target manifests, framework component tests | Java 21/Quarkus profile, approved commands, feasibility, framework capabilities | VPE policy interpretation, model prompts, execution-provider implementation |
| TG: core pipeline | `src/atg/domain`, `src/atg/application`, `src/atg/workflow`, `src/atg/gates`, `src/atg/provenance` | Analyze/Plan/Code/Execute lifecycle, checkpoints, deterministic gates, state and evidence binding | Provider SDK types, temporary demo assumptions, direct repository mutation |
| TG-S1: harness evaluation | `experiments/harness`, `tests/replay`, `docs/architecture` | Candidate comparison, reuse/fork/reference findings, local probes | Production imports or contract changes to fit a candidate framework |
| TG-S2/TG-S3: provider/evidence decisions | `experiments/providers`, adapter contract tests, `docs/architecture` | Responsibility, store, signer, verifier, and retention findings | Unapproved production credentials or final ownership assumptions |
| Shared demo/final demo | `deploy/development-harness`, `deploy/final-demo`, `docs/runbooks` | GitOps composition, environment configuration, rollback, operator flow | ATG domain contracts or authoritative target selection |

## Integration Rules

- `contracts/` and `src/atg/ports/` are the shared seams. Changes require compatibility tests and an owner review from affected paths.
- Domain and application code may depend on ports, never on Aider, LangGraph, Pydantic AI, provider SDKs, Tekton, GitLab, or a temporary demo repository.
- Adapters implement ports and translate external types at the boundary. External SDK types must not leak into domain contracts.
- Each path may use contract-driven mocks, simulators, deterministic fakes, replay fixtures, or local containers where the boundary is meaningful.
- Real SSC/RHOAI/Tekton/SCM integration tests remain separate from component tests.
- `experiments/` can recommend reuse, fork, or replacement, but cannot become a hidden production dependency.
- `deploy/development-harness` is temporary. `deploy/final-demo` is separately approved composition; neither defines the ATG architecture.
- Secrets, credentials, and customer data never live in fixtures, experiments, source, or generated patches.
- Generated tests and repository patches are written only through authorized tools and approved paths.
- Every artifact used in differential evidence is content-addressed and traceable to the contract, source, command, environment, and tool identity that produced it.

## First Integration Sequence

1. TG-1 establishes schemas, ports, status taxonomy, and state transitions.
2. VI and TF add adapters and fixtures against those contracts.
3. TG-S1 exercises the vertical slice with a deterministic fake and the current endpoint without changing domain contracts.
4. TG-2 through TG-7 integrate the real adapters incrementally.
5. Shared demo and final-demo deployment consume published service interfaces through `deploy/` and do not import application internals.

## Repository Convergence

The current checkout, any SSC fork, and temporary Git/GitLab projects are experiment locations. Before productization, record the destination project, repository ownership, license and contribution terms, source-history migration, fork divergence/synchronization policy, release ownership, and deprecation/rollback plan.
