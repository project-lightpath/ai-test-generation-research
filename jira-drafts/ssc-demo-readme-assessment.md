# SSC Demo README Assessment

Source: [Spring Boot Lightwell FSI Demo README](https://gitlab-gitlab.apps.ocp-edge94.qe.lab.redhat.com/development/spring-boot-example-application/-/raw/main/README.md?ref_type=heads)

Status: Review-only analysis. No Jira changes were made.

## Confirmed Demo Profile

- Retail banking Spring Boot proof of concept.
- Java 17.
- Spring Boot 2.7.18.
- Maven 3.8+ with an explicit `settings.xml`.
- Ten vulnerable transitive dependency areas with Lightwell-remediated coordinate versions.
- `apply-rhlw-version.sh` and `revert-rhlw-version.sh` switch dependency coordinates without application-code changes.
- 121 tests: approximately 45 unit, 71 integration, and 5 regression tests.
- 95.1% line coverage and 78.1% branch coverage reported through JaCoCo.
- REST/OpenAPI application with customer, account, transfer, document, credit-check, XML statement, YAML configuration, JSON query, audit, and RBAC features.
- Existing SBOM and dependency-tree generation instructions.
- Existing presenter materials, build/run documentation, testing documentation, and agent instructions.

## What Changes

- The README does not change the authoritative ATG target: Java 21/Quarkus remains the MVP target selected with the A&P work.
- The current Spring Boot demo is a temporary development harness useful for integration, repository-profile discovery, fork evaluation, and compatibility testing, but it is not the ATG target fixture or a source of ATG design decisions.
- Its two dependency states and 121-test baseline are useful only if the team explicitly selects or forks this repository as an additional target.
- If selected later, the full-suite pass in both states must not be treated as proof that the vulnerability is reached or fixed.
- Active exploitation is not implied by the demo. Any vulnerability-focused test must use an approved safe validation strategy and remain within the ADR testing-only boundary.

## Reuse and Fork Opportunities

- Reuse or fork the Maven settings/profile and dependency-switch scripts after removing embedded or environment-specific credential assumptions.
- Reuse the existing test tiers, JaCoCo reports, OpenAPI contract, dependency tree, SBOM process, and presenter documentation as baseline artifacts.
- Genericize hard-coded Lightwell names, credentials, endpoints, repository paths, and demo-only assumptions in a temporary fork.
- Keep the original repository as a development baseline and rollback reference; the final demo configuration remains a separate delivery target modeled on this harness.
- Record that all current repositories and Git/GitLab projects are temporary until product-project and repository ownership converge.

## Draft Changes Required

- Keep the proposed ATG Epic and TF-1 task on the Java 21/Quarkus target profile.
- Treat Spring Boot README findings as optional SSC compatibility/fork tasks.
- If the Spring Boot repository is selected as an additional target, add a task to characterize safely testable behavior and whether strict base-fail/candidate-pass evidence is achievable.
- Add a fork/migration task covering source revision, ownership, license, destination project, credential removal, genericization, and rollback.
