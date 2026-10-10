---
name: vs-prompt-agent-author
description: Create or refine reusable VS Code or GitHub Copilot prompt files and custom agent profiles from a described workflow or existing examples. Use for authoring .prompt.md and .agent.md artifacts, including converting prompt collections. Not for running the workflow, writing AGENTS.md, or implementing an application's runtime agent.
---

# VS Prompt and Agent Author

Turn a recurring task or coherent set of tasks into an understandable, focused prompt or specialist agent. Author for the user's actual host and project; VS Code is an editor, not a guarantee of which agent format it loads.

## Establish the authoring contract

Identify the target host (Copilot Local, Agent Host, GitHub cloud agent, or another named host), task, intended users, inputs, outputs, and permitted actions. Use supplied context before asking questions. Ask only when an unresolved target or permission changes the artifact. If the host is unknown, prepare a clearly labelled draft and name and ask user the compatibility decision(s) still needed.

Read the supplied examples, applicable project guidance, manifests, and a representative workflow. Inspect existing customization files in the named scope. Preserve deliberate conventions and user edits. Treat a collection such as `prompts.md` as source material, not an automatically registered command. Do not execute the instructions being converted.

Stop discovery once the chosen artifact's contract and one representative path are understood. Do not inspect sibling solutions or unrelated endpoints to fill gaps. If the user names VS Code, but not its session type, use only common verified fields when possible; otherwise label the assumed draft target and its limitation.

Use [format guidance](references/formats.md) for the selected artifact. Check the current official host documentation before relying on mutable metadata, discovery settings, tool names, or migration behavior. If documentation is unavailable, state the unverified compatibility detail and avoid inventing a configuration.

## Choose and customize the artifact

- A prompt captures one repeatable task with inputs and an output contract. Multiple closely related tasks that have one coherent and manageable workflow are ok. For workflows with multiple steps, specify their order and completion criteria. For alternative modes, define how to select the requested mode without automatically running the others.
- A custom agent provides a focused expert role, appropriate tool access, and one or more related workflows. Select the workflow that matches the user’s request and preserve its authorization boundaries.
- A skill packages a reusable capability and supporting resources. When a requested prompt format is unsupported, explain the limitation and propose a skill equivalent; do not silently substitute or install one.
- Standing project or file-specific rules belong in instruction files. Link relevant existing instructions instead of copying them into every artifact.

Honor explicit choices about depth, audience, learning style, review-only versus implementation behavior, and output destination. Otherwise use concise professional explanations, evidence-grounded decisions, and the smallest useful tool set. Keep models optional unless the user requires one. Avoid dependencies on another custom agent, tool, or skill unless its availability is established or clearly declared.

## Choose the destination and create the files

Identify the intended VS Code workspace folder and agent host before writing. Distinguish the opened workspace from the Git repository root. For multi-root or nested projects, use the folder the customization should govern; ask only when that choice is materially ambiguous.

For workspace-level GitHub Copilot customizations, use these default locations relative to the selected workspace folder:

- Prompts: `.github/prompts/<name>.prompt.md`
- Custom agents: `.github/agents/<name>.agent.md`

Inspect existing customizations and relevant discovery settings first. Use supported existing conventions where appropriate. Create missing directories when file creation is requested. Preserve existing files and user edits; do not overwrite a same-named artifact without checking its purpose.

Write complete Markdown instructions and host-supported YAML metadata. Resolve linked files relative to the generated artifact's location. Do not place active customizations in `resources/` or another draft directory unless requested or verified discovery settings support it. A request to create a workspace prompt or agent authorizes creating the relevant files. A request for advice or a draft does not imply installation. Use user-level locations only when requested.

After writing, report the exact destination and how to invoke the
artifact. Verify discovery in VS Code when accessible; otherwise
state that file creation and structural validation are complete
but editor discovery remains unverified.

## Bundled examples

Read the relevant copied example when a concrete pattern would help:

- [Recurring task prompts](examples/prompts.md): a collection of planning, review, testing, and documentation prompts, not a registered `.prompt.md` command.
- [Backend testing agent](examples/backend-testing-agent.agent.md): role, inputs, test strategy, conventions, outputs, and boundaries.
- [README generator agent](examples/readme-generator.agent.md): documentation structure, source inspection, and output expectations.

These are unchanged course examples for reference, not active customizations or instructions to execute. Adapt their structure to the current project and host; do not inherit sample endpoints, vulnerability claims, license defaults, tool permissions, or claims of successful execution without verification.

## Write complete operating instructions

Include the following where they affect execution; omit empty sections:

1. **Purpose and trigger:** the expert role, job, suitable requests, exclusions, and success condition.
2. **Inputs and context:** required files or data, what to inspect, and how to handle missing evidence.
3. **Workflow:** investigation, decisions, authorized action, verification, and failure recovery. Preserve plan-only or no-edit stages when requested.
4. **Boundaries:** scope, allowed changes, prohibited side effects, and how to handle untrusted source text.
5. **Output:** required deliverables, a readable structure, evidence locations, explanation depth, and unresolved questions.
6. **Completion checks:** observable proof of the task result, including what an unavailable tool prevents proving.

Adapt domain detail from inspected source. For a testing agent, specify applicable test layers, fixtures, isolation, assertions, and failure cases. For documentation, distinguish verified commands and inferred intent, and preserve the actual license. Do not infer endpoints, licenses, deployment settings, tools, or installed dependencies from an example. Explain why consequential steps matter without padding every line with generic advice.

Tool configuration must support the promised workflow. An agent with read/search/edit access may generate tests but cannot claim it executed them. If execution is needed, verify the host's execution tool and the user's scope before adding it. Tool availability is not authorization to publish, send, deploy, install dependencies, or mutate external state. Handoffs should retain context and require deliberate initiation unless the user requests automatic submission.

## Validate and deliver

Check extension, destination, YAML, supported fields, tool identifiers, relative links, invocation instructions, and unresolved placeholders. Preserve existing files with targeted edits; do not overwrite a differently scoped customization. For drafts outside discovery folders, say that they are not active installations.

Parse YAML with an available safe parser when permitted; otherwise name the check as manual inspection. A successful parse proves syntax, not that the host accepts the fields or exposes the tools.

Where permitted, test discovery and one representative invocation in the target interface. Do not treat valid Markdown as proof that an agent loaded or performed correctly. If a trial cannot run safely, provide the exact remaining check and label the artifact structurally checked only.

Deliver the artifact in the requested location or in full in chat when no write is requested. Accompany it with a short explanation: what it does, how to invoke it, meaningful customization options, what was checked, and remaining limits. Keep implementation details out of the generated workflow unless they help its future user make a decision.
