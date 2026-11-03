# Proposed Epic: AI Test Generation MVP

Status: Created in Jira; this file remains the review/source copy for `FLPATH-5030`.

Created Jira issue: `FLPATH-5030`.

## Jira Metadata

| Field | Proposed value |
|---|---|
| Project | `FLPATH` (FlightPath) |
| Issue type | Epic |
| Summary | AI Test Generation MVP |
| Labels | `lightwell` |
| Parent | None |
| Dependencies | `FLPATH-4997` Demo Environment; `FLPATH-4998` Assessment & Prioritization Pipeline; `FLPATH-4999` Release; proposed Final Demo Integration Epic |

## Goal

Deliver a Java 21/Quarkus, VPE-driven AI Test Generation capability that runs the approved `Analyze -> Plan -> Code -> Execute` lifecycle and integrates with the final demo configuration modeled on the current SSC development harness. The service consumes authoritative VPE evidence, generates repository-native tests, executes the exact approved test against immutable base and candidate subjects in approved isolated workers, and produces owner-reviewed evidence with explicit sign-off, limitations, and blocked, inconclusive, or stated-gap outcomes.

## Scope and Boundaries

In scope:

- VPE-provided VEX finding and policy decision intake.
- Java/Maven/JUnit repository and framework support.
- Durable checkpoints, human review, deterministic quality gates, and failure-register validation.
- Isolated base/candidate execution through the approved execution provider.
- Evidence, provenance, differential classification, and integration with the final demo configuration.
- Reuse or fork of current SSC demo implementation patterns where this reduces MVP work, without allowing the development harness to redefine service design.
- Components independently testable where boundaries are meaningful, with contract-driven mocks/simulators, deterministic fakes/replay fixtures, and documented integration boundaries.

Out of scope:

- Rewriting authoritative VPE/Lightwell vulnerability records or publishing VEX.
- Production-code modification, merge approval, release approval, or unattended operation.
- Broad SCM provider automation beyond the human-reviewed PR or approved equivalent required for test delivery.
- A second vulnerability scanner or authoritative risk score.
- Additional language/framework adapters beyond the Java-first MVP.

## Implementation Outcomes

- VI-1 through VI-5: VEX and policy input Stories.
- TF-1 through TF-5: target fixture, repository profile, and native framework Stories.
- TG-1 through TG-7: pipeline, execution, evaluation, and evidence Stories.
- TG-S1 through TG-S3: implementation, execution-provider, and evidence/signing Spikes.
- Shared development-environment and release work is proposed as additions to `FLPATH-4997` and `FLPATH-4999`, not duplicate ATG implementation Stories. Final-demo composition is tracked by the proposed Final Demo Integration Epic.

## Dependency and Blocker Summary

- **Blocks ATG target work:** A&P selection of the authoritative Java 21/Quarkus fixture, VPE VEX format/version and delivery contract, and evaluated policy-decision schema.
- **Blocks differential execution:** immutable base/candidate subjects, repository/framework profile, execution-provider responsibility, and target preconditions.
- **Blocks final evidence acceptance:** evidence owner/sign-off policy, configured evidence consumer/store, retention, and verification path.
- **Blocks final-demo acceptance:** the ATG MVP capability, A&P outputs, shared Demo Environment, Release integration, and the separate Final Demo Integration Epic.
- **Does not block core ATG design:** current SSC harness quirks, provider-specific SCM publication, cryptographic attestation unless required by the selected consumer, and final RHOAI deployment choice.

## PoC Scope

- One VPE-provided Java VEX finding.
- The authoritative Java 21/Quarkus fixture/profile selected with the A&P work.
- One immutable base/candidate pair.
- One approved model endpoint profile.
- One approved execution provider, evaluated first through the SSC/Tekton environment.
- One human-reviewed end-to-end run against the A&P-selected Java 21/Quarkus fixture plus required negative and failure-register cases.
- A focused behavior test or explicit limitation establishing whether strict base-fail/candidate-pass evidence is possible; the existing full suite passing in both dependency states is baseline data only.

## Integration Rules

- Use versioned contracts and content-addressed evidence references.
- Require independently testable components to have unit, contract, and failure-mode tests using appropriate mocks, simulators, fakes, or replay fixtures without the complete platform deployment.
- Keep component validation separate from integrated SSC/RHOAI/Tekton validation; passing a mock, simulator, or replay test does not prove platform integration.
- Treat repository content, external descriptions, and generated code as untrusted input.
- Keep model/controller and repository-execution planes separate.
- Do not hold execution workers while waiting for human review.
- Deterministic gates own validation, command selection, execution classification, and result normalization.
- Synthetic fixtures may support contract and development tests, but the MVP end-to-end input is the VPE-provided finding.
- Use the current SSC demo as a baseline and rollback reference, not as immutable architecture.

## Definition of Done

- The complete lifecycle runs after stage-zero preflight and failure-register checks.
- The approved native test is executed against both immutable subjects in isolated workers.
- Results bind to exact source, test, patch, command, environment, image, model, and tool identities.
- Differential evidence distinguishes validated, reproduced, fixed behavior, not reached, blocked, inconclusive, and stated-gap outcomes.
- Human review is durable and resumable; retries and callbacks are idempotent.
- Evidence is published through the approved evidence path, linked to the VPE statement, and explicitly signed off by the responsible owner with limitations acknowledged.
- Cryptographic attestation is included only if required by the selected evidence consumer.
- Generated tests are delivered through a human-reviewed PR or explicitly approved equivalent when required by the final demo configuration.
- The flow is demonstrated in the final demo configuration, with the current SSC harness used only as development and rollback reference material.
