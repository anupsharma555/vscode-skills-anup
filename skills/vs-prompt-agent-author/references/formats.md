# Format selection and authoring references

Read only the relevant official format specification before authoring. Community examples are design references, not authoritative schemas. The compatibility observations below were reviewed on 2026-09-24 and must be refreshed when implementing against a host.

| Artifact | Typical Copilot repository location | Details to verify |
| --- | --- | --- |
| Task prompt | `.github/prompts/<name>.prompt.md` | Optional name, description, argument-hint, agent, model, tools; supported invocation and input syntax |
| Custom agent | `.github/agents/<name>.agent.md` | Description, name, tools, target-specific fields, invocation controls, optional handoffs |
| Scoped instructions | `.github/instructions/<name>.instructions.md` | Description and applicable `applyTo` patterns; use the instruction-author workflow for substantive authoring |
| Portable skill | A host-recognized skill folder with `SKILL.md` | Required name and description; discovery locations differ by host |

Current VS Code documentation says prompt files are not loaded by Agent Host and remain available to the Local agent. Check the user's actual host and current documentation before recommending a prompt file or migration. A Markdown filename alone does not establish discovery. A `.agent.md` profile does not become a Codex agent merely by copying it into a folder.

Prompt and agent bodies should share a clear task contract, but their metadata is not interchangeable. Do not paste host-specific prompt variables into a portable skill without explaining how the runtime supplies the input. Resolve relative links from the generated file's destination, not from the original example.

Official references:

- [VS Code prompt files](https://code.visualstudio.com/docs/agent-customization/prompt-files)
- [VS Code custom agents](https://code.visualstudio.com/docs/agent-customization/custom-agents)
- [VS Code custom instructions](https://code.visualstudio.com/docs/agent-customization/custom-instructions)
- [GitHub custom agent configuration](https://docs.github.com/en/copilot/reference/custom-agents-configuration)
- [Codex skills](https://developers.openai.com/codex/skills)

Design references, independently adapted rather than installed:

- [Prompt authoring example](https://github.com/trsdn/github-copilot-agent/blob/main/.github/prompts/copilot-new-prompt.prompt.md)
- [Custom agent authoring example](https://github.com/trsdn/github-copilot-agent/blob/main/.github/prompts/copilot-new-agent.prompt.md)

## Useful trial cases

Try the requested artifact on one realistic input, one missing-input case, and a boundary relevant to its job. For a test author, check whether it distinguishes generated tests from executed tests. For a document author, check whether it preserves missing facts rather than fabricating setup commands or licensing. Use drafts and synthetic values where executing the real workflow would exceed authorization.
