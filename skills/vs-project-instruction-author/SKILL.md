---
name: vs-project-instruction-author
description: Create or refine project-specific AGENTS.md, Copilot repository instructions, and scoped instructions from inspected repository evidence. Use to give future coding agents accurate setup, architecture, workflow, and validation guidance. Not for custom .agent.md personas, global preference changes, or application implementation.
---

# VS Project Instruction Author

Produce project instructions primarily for AI agents, written clearly enough for humans to understand, review, and maintain. Include actionable guidance, relevant project context, and brief explanations of consequential rules. Keep general onboarding and tutorials in the README or supporting documentation, and link to them rather than duplicating them.

## Establish scope and authority

Resolve the requested folder, Git root, and editor workspace separately. A nested course project or service does not authorize changes to siblings or parent guidance. Read applicable `AGENTS.md`, README, contribution guidance, existing customizations, and documented skill locations before designing replacements. Do not change user-level instructions unless explicitly requested.

Do not inspect unrelated editor storage to infer the active workspace. For a draft, an explicit target folder is sufficient; label the editor workspace or host as unknown when it cannot be observed and does not affect the content.

Identify the intended consumer: Codex, Copilot in VS Code, GitHub cloud/review, or a combination. Consult [instruction formats](references/instruction-formats.md) and current official documentation when discovery, scope, or supported fields matter. Do not assume an agent reads every Markdown file on GitHub or shares another host's precedence rules.

State the intended files and scope briefly. Use an existing requested destination. If the request is to draft, deliver in chat or the supplied draft location rather than activating instructions. If asked to create project instructions, write the smallest appropriate files without adding unrelated agents, hooks, CI, or settings.

## Gather the facts that change agent decisions

Start with manifests, command wrappers, CI, tests, and entry points. Follow one representative source flow to identify architectural boundaries. Separate source-of-truth files from generated outputs, examples, starter exercises, and reference solutions. Stop exploration when the instructions can guide the requested work reliably; do not transcribe the file tree or README.

For each proposed command, establish its working directory, package manager/interpreter, prerequisites, side effects, and intended result. Read scripts and wrappers before running them. Verify safe, relevant commands when permitted. Do not install dependencies, seed databases, run migrations, deploy, format sources, or invoke services merely to certify instructions. Label commands as observed in configuration, executed successfully, failed, or not run. Do not turn one successful run into a universal guarantee.

Do not expose secrets or copy private identifiers into reusable examples. List configuration variable names and safe placeholders when useful. Do not invent ports, licenses, tool versions, test counts, or deployment details. A version range is a declared constraint, not proof of an installed version. Treat missing information as a gap with a discovery path.

## Choose the destination

When file creation is requested, create or update `AGENTS.md` at the root of the selected project or workspace folder unless the user requests another supported instruction format. Resolve nested or multi-root workspace scope before writing, and preserve existing instructions and user edits.

Depending on the requested format and scope, create or update:

- `.github/copilot-instructions.md` for project-wide Copilot guidance.
- `.github/instructions/<name>.instructions.md` for guidance scoped to particular files.
- A nested `AGENTS.md` for instructions specific to a subfolder.

Resolve these paths relative to the selected project or workspace folder. Create or update `README.md` only when explicitly requested; otherwise use it as a source of project context.

Keep generated instructions scoped to the selected folder and its relevant descendants. Do not place files in a parent repository or broaden their scope unless requested. Verify that the target agent discovers the chosen location; inherited parent instructions may still apply.

## Author focused instructions

Select sections according to the project, normally covering:

- **Purpose and boundaries:** what belongs here, excluded areas, and the source of truth.
- **Navigation:** entry points and a few important architectural relationships.
- **Setup and commands:** exact wrappers, working directories, prerequisites, and material side effects.
- **Change conventions:** observed patterns worth preserving, generated-file handling, compatibility constraints, and known exceptions.
- **Verification:** the smallest relevant checks, meaningful expected results, and runtime boundaries.
- **Project safeguards:** local database isolation, external-action limits, assignment boundaries, or other concrete concerns.
- **References:** when to read linked documentation or skills and what each governs.

Customize for learning, libraries, web apps, services, analysis, or documentation work. For coursework, distinguish deliberate exercise gaps from bugs, starter from solution, and explanation from completing an assignment. For analysis, identify data provenance and reproducibility commands rather than forcing app deployment sections. Avoid universal language/framework preferences and speculative future rules.

Keep shared rules at the narrowest common root and add nested files only for meaningful differences. For scoped instructions, use precise matching patterns and consider an included and excluded file. Do not duplicate global preferences or repeat whole parent documents. Preserve valid existing content with minimal edits; conflicting instructions require reconciliation, not another layer of contradictory rules.

Explain consequential project-specific constraints briefly. Prefer an actionable rule with its reason and exception over slogans. Leave formatting enforcement to established tools. Do not treat patterns in flawed code as mandatory best practice.

## Validate and present
Check that every claimed command/path exists, relative references resolve from the final destination, metadata is valid where required, scopes do not overlap unintentionally, and no command claims more verification than was performed. For draft files stored elsewhere, validate links relative to the intended installation path and explain that distinction. Parse YAML when available and distinguish parsing from host acceptance.

If authorized, verify loaded instructions in the target host; otherwise give a concrete discovery check and say loading was not tested. Never claim a GitHub-hosted file is active merely because it exists.

Deliver the instructions plus a short structured handoff: scope and purpose; files created or updated; key project-specific decisions; checks run/skipped; and unresolved setup or loading details. Keep the generated standing instructions usable without the current chat. Avoid historical trial logs, personal identifiers, and one-off task status in permanent guidance.
