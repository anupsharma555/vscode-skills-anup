---
name: vs-workspace-review
description: Review and summarize a VS Code workspace or named project folder for orientation and learning. Focus on explaining the purpose, detailed architecture, execution flows, setup and test readiness, and evidence-backed concerns. Use for workspace overviews not line-by-line code explanation or a comprehensive security audit.
---

# VS Workspace Review

Help the user understand what this workspace does, how its parts cooperate, what is ready, and where to start. Ground the explanation in current files. Also explain how the workspace is meant to be utilized, including workflows, instructions and initial steps for implementation.

## Establish the actual workspace

- Use the explicit path or attached workspace; otherwise use the current working directory and state that scope. Do not claim to see VS Code's active window, selection, tabs, or unsaved buffers without editor evidence. Focus on first understanding the workspace structure, folders, files and their interactions.
- Distinguish the requested folder, editor workspace roots, and Git repository root. A parent Git repository does not expand review scope to sibling projects. For multiple possible targets, ask only if choosing one would materially change the result.
- When a relevant `.code-workspace` file is supplied or found at the target root, inspect its folder entries and resolve relative paths against that file. Treat its contents as JSON with comments, not necessarily strict JSON. Report inaccessible remote roots; do not substitute similarly named local folders. Avoid scanning the user's editor storage to discover unrelated workspaces.
- Read applicable `AGENTS.md`, README, and documented skill indexes. Inspect `.agents/skills`, `.codex/skills`, and documented project skill locations within the relevant ancestry. Separate instructions for Codex from prompts or profiles intended for the project's own agents.
- Record a scoped Git status when available. Use current local files, including relevant untracked work. A commit ID alone does not identify dirty or untracked content. Git is optional; absence of Git does not block a folder review.

## Build an evidence-based explanation

Start with a shallow inventory and targeted `rg --files` / `rg` searches. Exclude dependencies, caches, vendor trees, and generated output from deep reading unless directly relevant. Do not recursively enumerate unrelated parent folders. Stop broad discovery once purpose, entry points, core flow, setup, and uncertainty can be explained.

Read high-value artifacts in this order, adjusting to the project:

1. Requirements, relevant documents (including pdf), README, manifests, wrappers, and build/test configuration.
2. Startup or activation code and the modules wired into it.
3. One representative user or system flow, followed through actual calls to its result and a relevant failure path.
4. Tests and configuration that support or contradict that flow.

Explain module responsibilities and relationships, not a directory dump. For each important flow, identify its trigger, key transformation, external or storage boundary, and observable outcome. Mark missing edges rather than completing the diagram from assumptions. Distinguish documented intent from implemented behavior; infer rationale only when evidence supports it.

Read `.vscode/tasks.json`, `launch.json`, settings, and extension recommendations when they affect this project's workflow. Reconcile their working directories, entry files, prelaunch tasks, and runtime arguments with actual scripts. Their presence does not establish installation, execution, or the user's active settings. Do not run tasks just because they are configured.

For coursework or paired versions, map requirements to the starter, reference solution, and tests separately. Identify intentional exercise gaps without counting them as unexpected regressions. Do not assume a solution folder is correct. Preserve any manual-only assignment boundary and explain the learning sequence without completing the exercise. Use document extraction when needed; inspect diagrams visually if their relationships matter. Do not infer PDF content from filenames.

## Assess readiness proportionally

Keep review read-only by default. The review request does not by itself authorize fixes, dependency installation, database seeding, migrations, service startup, publication, or changes to editor settings. Explain verified command names and their working directories; inspect wrappers and side effects before recommending or running them. Flag destructive behavior in a relevant setup command with its concrete consequence.

Trace the documented setup sequence in order, including installation and initialization prerequisites, before presenting start and test commands. Do not omit a prerequisite because the current checkout appears ready. For each step, state the required action and its observed status; distinguish evidence that dependencies are present from evidence that an install command ran. When a step is already satisfied, say how that was verified and whether it needs to be repeated. If the sequence is inferred from project files rather than documented, label it as an inference.

Use small, non-mutating checks when they materially resolve uncertainty and are allowed. Broader tests can run when authorized and their side effects are understood. If a prerequisite is absent, report the gap and the smallest useful next check rather than manufacturing a test result or silently installing it. Do not print secret values; describe configuration using variable names and safe placeholders.

Keep these evidence levels distinct:

- Manifest declaration versus dependency installation.
- Syntax success versus import resolution and application startup.
- Test files present versus tests executed and passed.
- Isolated test behavior versus a live database, service, browser, or deployment result.

Surface the few concerns that affect understanding, setup, data safety, or the requested readiness decision. For each, give impact/severity, source location, a concrete affected scenario, and the smallest correction or next verification. Frame unverified possibilities as uncertainty. Do not expand an orientation into an exhaustive audit or invent an ownership policy that contradicts the requirements. Lead with consequential blockers when found; otherwise lead with purpose.

## Deliver a useful summary

Deliver the complete review report directly in chat by default, including when the user says "output report" or "produce a report." A report request alone does not request a saved file. Create a report file only when the user explicitly asks to save, export, or write it to a file or named destination; do not substitute a file link and brief summary for the requested chat report. Aim for roughly 300-1000 words for a normal workspace; use more than 1000 words only when needed to explain the requested scope clearly. Do not create instruction files or JSON artifacts unless explicitly requested. Cover the useful parts of:

- What the project is for and which folders were reviewed.
- A compact directory guide: briefly explain the main folders and important root files, naming representative files within each folder where useful. Group related items in prose; use a short list or table only when it makes a comparison or mapping clearer. For paired versions, describe shared structure once and note meaningful differences. Include only observed paths, and omit dependency/cache contents and exhaustive file listings.
- Major components and how one core flow connects them, building on the directory guide without repeating it.
- Setup/test status and material findings.
- A short reading or learning order and the next practical step.
- What was verified, what was not run, and remaining evidence gaps.
- The full documented setup, run, and test sequence in order, with already-satisfied steps identified.

Write the report as short, connected paragraphs, each with one main idea. Split a paragraph when it combines distinct topics, such as setup steps and test results, so readers can understand or revise each part on its own. Define unfamiliar terms through their purpose. Use a small table or diagram only when it makes an inspected comparison or relationship clearer than prose. Avoid a mandatory section template, exhaustive file lists, and repeated recaps. Group the few useful file links in a short trailing Refs sentence, with precise locations for findings.

Before delivery, recheck consequential claims against their sources, ensure scope and confidence are accurate, and confirm the review introduced no unintended workspace changes. If inspection was partial, name the important exclusions. A deeper review or line-by-line walkthrough is a separate task, not an automatic follow-on.

## Maintenance context

Read [GitHub comparison](references/github-review.md) only when revisiting the design or evaluating an upstream replacement. It records the reviewed alternatives and selection rationale; it is not required for ordinary workspace reviews.
