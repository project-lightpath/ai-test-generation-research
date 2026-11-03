# Jira Drafts: AI Test Generation

Status: Draft for review. Nothing in this folder has been published to Jira.

Creation status: The proposed Epic and ticket set was created in Jira on 2026-11-03 after explicit user authorization. All created issues use project `FLPATH` and label `lightwell`.

In these drafts, **ATG** means the AI Test Generation service/product and its proposed MVP Epic. It does not mean the temporary SSC development harness, the forked SSC repository, A&P/VPE, or the separately delivered final demo integration. All current repositories, forks, and Git/GitLab projects are temporary experiment locations; eventual product-project and repository convergence remains open.

Canonical implementation repository: <https://github.com/project-lightpath/ai-test-generation>. Jira descriptions now reference the relevant paths in this repository by workstream.

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

## Created Issue Map

- ATG MVP Epic: `FLPATH-5030`
- Final Demo Integration Epic: `FLPATH-5031`
- ATG child range: `FLPATH-5032` through `FLPATH-5052`
- Final Demo child range: `FLPATH-5053` through `FLPATH-5056`
- Shared Demo Environment updates under `FLPATH-4997`: `FLPATH-5057`, `FLPATH-5058`
- Shared Release updates under `FLPATH-4999`: `FLPATH-5059` through `FLPATH-5061`

## Jira Dependency Links

Meaningful blocker links were added in Jira. Representative dependency paths include:

- `FLPATH-5043` TG-1 blocks the downstream TG pipeline stories.
- `FLPATH-5032` VI-1 blocks the remaining VEX/policy intake stories.
- `FLPATH-5037` TF-1 blocks target-profile and feasibility work.
- `FLPATH-5045` through `FLPATH-5048` establish the Analyze -> Plan -> Code -> Execute sequence.
- `FLPATH-5030` blocks final-demo composition and shared release additions.
- `FLPATH-5053` through `FLPATH-5055` establish final-demo integration sequencing.
- `FLPATH-5057` blocks the shared environment integration task.
- `FLPATH-5059` and `FLPATH-5060` block shared release rehearsal `FLPATH-5061`.
- Existing A&P Epics `FLPATH-4997`, `FLPATH-4998`, and `FLPATH-4999` are linked to their dependent ATG/shared tasks.

## Tool Candidates Referenced by the Drafts

- SSC Aider/Claude Code task: current compatibility baseline.
- `ai-test-harness`: domain-harness candidate for adapters, differential execution, failure register, provenance, and self-verification.
- `fullsend-ai/test-creator` and internal test-plan-generator: bounded Analyze/Plan and deterministic evidence-gate references.
- LangGraph, Pydantic AI, and direct provider SDKs: implementation candidates evaluated by TG-S1, not selected architecture.
- VVAH/context-graph and CyberGym/SWT-Bench or similar benchmarks: bounded evidence/evaluation candidates, not assumed production dependencies.

These drafts require owner review, dependency confirmation, issue-type confirmation, and scope approval before any Jira operation.
