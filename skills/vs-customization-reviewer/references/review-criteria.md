# Targeted compatibility and quality checks

Choose the relevant host and artifact rather than applying every row. Current official documentation is the schema source; community prompts may lag it.

| Artifact | Useful checks |
| --- | --- |
| `AGENTS.md` | Correct scope, actual commands, inheritance/overrides, project-specific content, concise review rules |
| Copilot instructions | `.github/copilot-instructions.md` location; valid scoped-file metadata; matching and nonmatching `applyTo` examples |
| `.agent.md` | Host-required fields and useful description; intentional tool access; supported target and invocation controls; valid referenced handoffs |
| `.prompt.md` | Supported host; task inputs; referenced agent existence; prompt tool precedence; reusable output contract |
| `SKILL.md` | Name/description; clear trigger and exclusions; reachable references; declared dependencies; focused workflow |

Special checks:

- An omitted custom-agent tool list may grant all available tools. A missing or ignored tool can also make a promised action impossible. Verify host semantics before reporting either.
- A configuration in a resources directory may intentionally be a sample. Report it as inactive/unverified, not incorrectly installed, unless activation was intended.
- A README author must not invent a license. A security prompt's illustrative vulnerability is not a finding. A testing prompt must not claim run success from generated code.
- Unknown optional schema fields, deprecated formats, and user-level settings require host-specific evidence. Do not infer the installed editor version from the documentation website.
- Description requirements differ: GitHub's custom-agent schema requires it, while VS Code documents optional frontmatter. Recommend a clear description for usability without misclassifying its absence as invalid on every host.
- For linked scripts, separate entrypoint review from a full package review. State which executable surfaces were not inspected.

Official references:

- [VS Code customization model](https://code.visualstudio.com/docs/agents/concepts/customization)
- [VS Code custom agents](https://code.visualstudio.com/docs/agent-customization/custom-agents)
- [VS Code prompts and migration](https://code.visualstudio.com/docs/agent-customization/prompt-files)
- [VS Code instructions](https://code.visualstudio.com/docs/agent-customization/custom-instructions)
- [GitHub agent schema](https://docs.github.com/en/copilot/reference/custom-agents-configuration)
- [Codex instruction discovery](https://developers.openai.com/codex/guides/agents-md)
- [Codex skills](https://developers.openai.com/codex/skills)

Design reference: [Copilot setup audit](https://github.com/trsdn/github-copilot-agent/blob/main/.github/skills/copilot-setup-audit/SKILL.md). Use its categories selectively; do not equate a larger configuration inventory with a better setup.
