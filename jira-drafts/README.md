# Jira Drafts: AI Test Generation

Status: Draft for review. Nothing in this folder has been published to Jira.

In these drafts, **ATG** means the AI Test Generation service/product and its proposed MVP Epic. It does not mean the temporary SSC development harness, the forked SSC repository, A&P/VPE, or the separately delivered final demo integration. All current repositories, forks, and Git/GitLab projects are temporary experiment locations; eventual product-project and repository convergence remains open.

## Ticketing Defaults

- Project: `FLPATH` (FlightPath)
- Required label: `lightwell`
- Proposed ATG Epic: `AI Test Generation MVP`
- Existing shared Epics to update rather than duplicate: `FLPATH-4997` Demo Environment and `FLPATH-4999` Release
- Outcome identifiers: `VI-*`, `TF-*`, `TG-*`, and `TG-S*`

## Drafts

- `ai-test-generation-mvp-epic.md`: proposed Epic description and Definition of Done.
- `ai-test-generation-mvp-tickets.md`: proposed Stories, Tasks, and Spikes under the Epic.
- `shared-ap-epic-updates.md`: proposed additions to the existing A&P Demo Environment and Release Epics.
- `ai-test-generation-final-demo-integration-epic.md`: proposed cross-workstream Epic for integrating ATG into the separately delivered final demo configuration.
- `ssc-demo-readme-assessment.md`: confirmed demo profile, reuse opportunities, and implications for the ATG MVP fixture.
- `pre-publication-checklist.md`: inventory and approval gate required before any Jira operation.

## Tool Candidates Referenced by the Drafts

- SSC Aider/Claude Code task: current compatibility baseline.
- `ai-test-harness`: domain-harness candidate for adapters, differential execution, failure register, provenance, and self-verification.
- `fullsend-ai/test-creator` and internal test-plan-generator: bounded Analyze/Plan and deterministic evidence-gate references.
- LangGraph, Pydantic AI, and direct provider SDKs: implementation candidates evaluated by TG-S1, not selected architecture.
- VVAH/context-graph and CyberGym/SWT-Bench or similar benchmarks: bounded evidence/evaluation candidates, not assumed production dependencies.

These drafts require owner review, dependency confirmation, issue-type confirmation, and scope approval before any Jira operation.
