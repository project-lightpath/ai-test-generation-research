# Proposed Epic: AI Test Generation Final Demo Integration

Status: Draft for review. Do not publish without owner approval.

Terminology: ATG refers to the AI Test Generation service/product. This Epic integrates the ATG MVP into the final demo configuration; it does not define the ATG service contracts or the temporary SSC development harness. Current repositories and Git/GitLab projects are temporary experiment locations pending product-project and repository convergence.

## Jira Metadata

| Field | Proposed value |
|---|---|
| Project | `FLPATH` (FlightPath) |
| Issue type | Epic |
| Summary | AI Test Generation Demo Integration |
| Labels | `lightwell` |
| Parent | None |
| Depends on | AI Test Generation MVP capability; Assessment & Prioritization outputs; shared Demo Environment and Release work |

## Goal

Integrate the completed AI Test Generation MVP into the final demo configuration delivered for the A&P and Trusted Software Supply Chain flow. The final configuration should be modeled on the current `ssc-demo` development harness where useful, but this Epic owns the final environment contract, deployment composition, operational readiness, and end-to-end demonstration boundary.

The current `ssc-demo` is development and compatibility material, not the target environment or a source of AI Test Generation design decisions.

## Scope

- Confirm final-demo integration contracts, ownership, deployment location, and versioned configuration.
- Deploy the AI Test Generation service, approved model endpoint, execution provider, evidence path, credentials, RBAC, and network policies through the final GitOps path.
- Connect the A&P/VPE-provided Java 21/Quarkus request to the AI Test Generation service.
- Demonstrate Analyze -> Plan -> Code -> Execute, human review/sign-off, and evidence delivery in the final demo.
- Validate rollback, cleanup, retention, and failure recovery in a clean-environment rehearsal.
- Preserve compatibility outputs only where required by the final demo; do not expand into general SCM/provider automation.

## Out of Scope

- Redefining the AI Test Generation service contracts or selecting its internal model/agent framework.
- Treating the current Spring Boot `ssc-demo` fixture as the authoritative ATG target.
- Broad SCM integration beyond the final demo's required compatibility seam.
- Replacing A&P/VPE prioritization or authoring VEX.

## Candidate Child Work

Detailed child tickets should be created after the final demo contract is available. Likely work includes:

- Final demo integration contract and ownership confirmation.
- GitOps deployment, configuration, secrets, RBAC, network, and execution-provider integration.
- VPE-to-ATG request and evidence-path composition.
- Final-demo end-to-end rehearsal, rollback, cleanup, and operator documentation.

These items should not duplicate ATG implementation Stories or shared Demo Environment/Release tasks; they coordinate and verify the final composition.

## Definition of Done

- The final demo configuration can receive the A&P-selected VPE Java 21/Quarkus request.
- The AI Test Generation MVP runs through its approved lifecycle with durable human review/sign-off.
- Base/candidate execution, evidence, limitations, and configured consumer results are visible through final-demo interfaces.
- Required credentials and network boundaries are GitOps-managed without secrets in source.
- A clean-environment rehearsal, rollback, cleanup, and recovery path are demonstrated.
- Ownership, versioning, support, and divergence from the current development harness are documented.
