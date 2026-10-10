---
name: vs-make-agentsmd
description: Create, update, or audit a project's AGENTS.md after reviewing the entire selected workspace and all existing documentation. Use when the user wants Codex or another compatible coding agent to have accurate, complete project instructions; not for writing application code or a general README.
---

# Make project AGENTS.md

Create useful standing instructions for a fresh agent working in this project. The user's requested scope and depth govern the work. Do not use brevity or a generic template to omit an important project area. Produce a readable guide to decisions and workflows, not a file-tree dump.

## Resolve the destination before drafting

Identify the selected project root, Git root, current working directory, editor workspace folders when known, and intended agent harness. These may differ. Create or update `AGENTS.md` in the **selected project root** unless the user specifies another destination. For a project nested in a larger Git repository, name the exact proposed path and its scope; do not silently put the file at the parent Git root or broaden it to sibling projects. Check applicable parent, root, and nested `AGENTS.md` or `AGENTS.override.md` files before writing. Preserve useful existing instructions and user edits.

If the request is only to scope, assess, or draft a skill or instruction file, deliver that requested artifact without activating an `AGENTS.md`. A request to create or update the project instructions authorizes writing the file in the selected project root.

## Review the entire workspace first

Inventory the full selected workspace before choosing content. Include every top-level area and nested project, package, service, app, exercise, and reference solution. Use a bounded file inventory that excludes dependency caches, Git internals, build outputs, and other generated or vendored trees from close reading; still note those trees and their role. Inspect each authored area enough to understand what it does and whether its rules differ. Do not stop after one representative source flow if other major subsystems or cross-cutting concerns remain.

Find and **read all current and prior documentation** within the selected workspace before drafting: existing agent guidance, READMEs, contribution and architecture guides, design and requirements documents, assignment briefs, PDFs, and other documentation formats present. Check documentation indexes and linked local documents. For PDFs, extract text and inspect pages or figures visually when their layout or diagrams carry meaning. Record which documents are authoritative, historical, drafts, examples, generated, or conflicting. Do not promote an old document or a reference implementation into a current requirement without checking it against the request and current code.

Inspect manifests, package scripts and wrappers, CI, configuration examples, entry points, public interfaces, tests, and source paths for **every major capability found**. Trace enough code to explain where an agent should make changes. Explicitly check cross-cutting areas that affect work, such as authentication, authorization, security, data handling, errors, migrations, observability, and deployment, when present. Distinguish actual behavior from intended behavior and untested claims. Never copy secret values or private identifiers into the instructions or output.

If a document cannot be opened or a significant area cannot be inspected, name the gap and its effect. Resolve the gap before creating `AGENTS.md`; if it cannot be resolved, ask for the missing essential input. Proceed with an incomplete review only if the user explicitly authorizes that exception, and label the affected guidance unverified.

## Map coverage, then write

Before writing, make a working coverage map of the workspace's major areas and the user's requested requirements. For each area, decide whether the new `AGENTS.md` needs an actionable rule, a navigation pointer to an authoritative document, or no entry with a reason. The map is a completeness check; it need not become a separate file. A major subsystem may not disappear behind a generic label such as “follow the architecture.”

Write organized, project-specific instructions that let a new agent answer:

- What does this project contain, and which folder should I change for a given task?
- Which documentation and code are authoritative, and which are examples, old versions, generated outputs, or deliberate exercise gaps?
- Which patterns, interfaces, security and data boundaries, and error or response contracts must I preserve?
- Which exact setup, build, test, lint, run, and formatting commands exist; from which directory; with what prerequisites and side effects?
- What constitutes adequate verification for the kinds of changes this project expects, and what remains unproven by source inspection or offline tests?

Choose headings and detail to match the actual project. Include concrete paths, commands, and small examples when they change an agent's decisions. Explain consequential rules briefly. Link to deeper documents for long reference material, but do not use a link in place of a critical instruction an agent must notice. Do not invent commands, tool versions, deployment steps, policies, or test results. Do not add empty template sections. Keep adjacent instructions consistent and avoid duplicating inherited guidance.

For each command, inspect its wrapper or script before recommending it. Distinguish configured from successfully executed commands; run safe relevant checks when authorized. Never run destructive seeds, migrations, installs, deployments, or external changes merely to certify the instructions. State material preconditions and side effects. Preserve user limits on source edits, assignment help, private data, and live services.

## Review the saved result

After creating or updating `AGENTS.md` in the selected project root:

1. Compare it against the coverage map and **every reviewed documentation source**. Check that all major areas are represented or have a justified omission. Review accuracy, completeness, organization, and usefulness to a new agent, not only spelling or Markdown syntax.
2. Verify each named path, relative link, command, working directory, and claimed behavior. Reconcile conflicts with inherited or sibling guidance. Ensure the final file contains no secrets or real private identifiers.
3. Confirm the file is at the selected project root and the diff affects only the intended instruction file unless the user requested more.
4. When the intended host is available, verify it discovers the file and try a fresh-session task whose success depends on a project-specific rule. Discovery alone does not prove the agent will follow the instruction. Report separately what was written, statically verified, host-loaded, and behavior-tested.

If host discovery details matter, recheck the current official [Codex AGENTS.md guide](https://developers.openai.com/codex/guides/agents-md), [GitHub instruction support](https://docs.github.com/en/copilot/reference/custom-instructions-support), and [VS Code custom-instructions guide](https://code.visualstudio.com/docs/agent-customization/custom-instructions). Their rules differ by harness and feature; do not assume a file loads everywhere.

In the final handoff, give the file path, the substantive areas covered, the checks performed, and any unresolved gaps. Do not claim a complete review when any relevant workspace area or document remains unread.
