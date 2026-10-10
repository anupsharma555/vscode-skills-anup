---
name: vs-test-gap-reviewer
description: Audit the active workspace, or an explicitly scoped feature, route, change, or project area, for missing or weak behavioral tests and propose prioritized test cases. Use when asked what tests are missing or whether existing coverage proves the intended behavior. Read-only by default; not general bug hunting, automatic test generation, or a percentage-coverage campaign.
---

# VS Test Gap Reviewer

Identify which important behaviors lack convincing protection and explain the smallest tests that would improve confidence. Judge assertions and observable behavior, not filenames or line coverage alone.

## Set scope and evidence

Honor an explicitly named feature, folder, PR, branch, or file scope. Otherwise, review the entire active workspace supplied by the editor or task context. Establish its roots before starting; if only a working folder is available, state that assumption rather than claiming to see the editor. Include all supplied workspace roots unless the user narrows the scope; ask only when the intended roots remain materially ambiguous. Do not expand to a parent Git repository, sibling workspaces, or external symlink targets.

Inventory every workspace folder and classify its files for testing relevance, including relevant hidden configuration and untracked source. Review all relevant first-party source, existing tests, fixtures, schemas, scripts, manifests, build/test configuration, CI definitions, and requirements or documentation needed to establish behavior. Trace the testable behaviors in each area and map them to direct and indirect test protection. Assess starter and reference projects separately, distinguishing intentional exercise gaps from missing regression protection.

Exclude dependency/vendor internals, version-control internals, caches, and generated build outputs from routine content review. Inspect them only when a specific testing question requires it; use their source or generator where available. Do not read secret values. List meaningful exclusions and their reasons rather than treating excluded files as reviewed or as testing gaps.

Prioritize higher-risk areas first, but use priority to order the review, not to stop after a sample. Maintain a coverage map of workspace areas and relevant files: inspected, excluded with reason, or pending. Continue through the full relevant scope. If access, time, or context limits prevent completion, label the review partial and identify the exact remaining areas and next pass; never present inventory alone as a completed behavioral review.

Read relevant project context, guidance, manifests, wrappers, test configuration, fixture setup, and CI to understand the aims of the project. Identify the established framework and test levels without installing anything. For changes, obtain the actual diff/base; if unavailable, review the named current files and disclose the missing comparison. Preserve read-only scope unless the user explicitly requests implementation.

Do not claim tests passed, coverage improved, or a suite is runnable from file inspection. Existing coverage reports need their revision, scope, and run context; stale reports are leads, not current proof.

## Map behavior to assertions

1. Trace the selected behavior from its input to observable output, state change, or error. Distinguish requirements from current implementation and unresolved intent.
2. Identify direct and indirect tests, including route/integration tests, shared fixtures, generated cases, and tests outside a mirrored directory. An absent same-name test is not proof of missing coverage.
3. Inspect what each relevant test asserts, what it mocks, and what its setup makes impossible to fail. Note tests that call code without checking outcomes, mock away the relevant boundary, or merely restate implementation logic.
4. Examine meaningful success, rejection, boundary, state-transition, and failure cases. Include authentication/ownership, malformed input, persistence, concurrency, and external failures only when the inspected contract makes them relevant.
5. Prioritize gaps by plausible user impact and exposure. A code bug belongs in this report only to explain the missing regression protection; avoid turning the review into an unrelated security or quality audit.

Use a compact internal mapping: behavior → source → existing assertions → gap → proposed proof. When a behavior is unspecified, recommend clarifying its contract rather than encoding a guessed requirement. Do not call an intentional unimplemented exercise a regression.

## Recommend valuable tests

For each material gap, give:

- The concrete scenario and expected observable result.
- Source and existing-test evidence, including the search boundary for an absence claim.
- Why the current tests would miss it and the consequence.
- The lowest suitable test layer and any fixture/isolation needs.
- What failure the new test would catch, distinct from tests already present.

Prefer small examples or a short scenario table over large unsolicited test files. Use units for isolated logic, integration tests for real boundaries, and browser tests for behavior only the UI can prove. Mock external boundaries only when they are not the subject of the test. Avoid universal coverage percentages, tests of framework guarantees, duplicate edge-case lists, and blanket mandates to install tools.

## Verify within the requested boundary

Inspect commands and setup side effects before running discovery or focused existing tests. Default to static review when execution would write caches/artifacts, connect to services, download binaries, or exceed a read-only request. Use a confirmed non-writing mode if available; otherwise report why execution was skipped. Do not seed databases, add dependencies, run formatters, or edit production code to make an audit easier.

Distinguish confirmed missing assertions from likely gaps requiring a broader search. A mock-based test does not establish actual persistence, authorization through middleware, browser behavior, or live-service correctness. Record actual commands and results if run. Do not invent coverage percentages or count tests without measuring them.

## Deliver a readable review

Order findings from highest to lowest importance. Within each priority level, rank by likely impact, frequency of exposure, and weakness of existing test protection. Explain the ranking briefly when it is not obvious.

Lead with the coverage conclusion and highest-value next test. Provide a short prioritized table: behavior/scenario, evidence, current protection, proposed test, and impact. Use High for consequential unprotected behavior, Medium for meaningful edge cases, and Low for maintainability or low-impact gaps; avoid severity inflation.

Include a compact workspace coverage summary showing each project or major area reviewed, meaningful exclusions, and any pending files or areas. Distinguish review completeness from test execution and passing behavior. Finish with execution status and the smallest next action. Explain unfamiliar test concepts in plain language. Deliver in chat unless a saved report was requested. If the inspected behavior is already adequately covered, say so and avoid inventing more tests.

Design reference: [test gap audit](https://github.com/github/awesome-copilot/blob/main/skills/test-gap-audit/SKILL.md). This workflow is intentionally a scoped review; it does not require that package's optional scanner or replace the repository's testing conventions.
