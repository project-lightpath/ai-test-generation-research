# Proposed Updates to Existing A&P Epics

Status: Draft for review. Do not publish without A&P and ATG owner approval.

All proposed additions use project `FLPATH` and label `lightwell`. These are updates to existing Epics, not new ATG Epics.

## FLPATH-4997: Demo Environment

### Proposed task: Fork and genericize SSC demo implementation

Issue type: Task

Summary: Fork and genericize SSC demo components for AI Test Generation integration

Description:

Evaluate the existing SSC demo repository and manifests as reusable implementation material. If selected, fork the required pipelines, tasks, GitOps resources, and integration components; remove demo-specific assumptions; and place the fork in a temporary experiment project while recording the eventual product-project and repository-convergence decision.

Acceptance criteria:

- Source revision, license, ownership, temporary destination project, retained components, removed assumptions, and divergence policy are recorded.
- The fork exposes provider-neutral interfaces where required.
- Baseline and rollback references to the existing SSC demo remain available.
- Forked repository and temporary ATG repository ownership are explicit, with eventual product ownership left as a recorded decision.

### Proposed task: Add ATG service integration environment

Issue type: Story

Summary: Add ATG service, model, worker, artifact, and credential integration to the final shared demo environment

Acceptance criteria:

- The final demo configuration, modeled on the current development harness, configures ATG service deployment, approved model endpoint, isolated workers, artifact/evidence store, Secrets, RBAC, and network policies through GitOps.
- The final demo can prepare, run, reset, and roll back without destructive manual edits.
- ATG-specific acceptance does not duplicate shared cluster, registry, repository, or CI setup.

## FLPATH-4999: Release

### Proposed task: Add ATG reviewed evidence and sign-off to the shared release

Issue type: Story

Summary: Include AI Test Generation evidence, owner sign-off, and verification in the shared release

Acceptance criteria:

- The release includes the ATG differential evidence record, generated-test artifact, owner sign-off, verifier path, and policy/evidence provenance.
- Cryptographic attestation is included only when required by the selected release/evidence consumer.
- Evidence remains resolvable after worker and PipelineRun cleanup.
- Any required SCM attachment is fail-closed and matches the approved, executed, and reviewed patch digest.

### Proposed task: Add ATG flow to shared demo composition

Issue type: Story

Summary: Compose the VPE-to-AI-Test-Generation flow into the shared SSC demo

Acceptance criteria:

- The VPE-provided VEX finding can initiate the ATG Java 21/Quarkus flow in the final demo configuration.
- Human review/sign-off, isolated base/candidate execution, differential evidence, and rollback are demonstrated.
- The final demo status surface points to canonical ATG evidence.

### Proposed task: Extend shared release and clean-environment rehearsal

Issue type: Task

Summary: Release and rehearse the integrated A&P and AI Test Generation flow

Acceptance criteria:

- Versioned deployment artifacts, image, SBOM, configuration, and troubleshooting documentation are complete.
- A clean-environment rehearsal validates the integrated A&P and ATG path in the final demo configuration modeled on the development harness.
- Ownership, upgrade, cleanup, rollback, and failure recovery procedures are documented.
