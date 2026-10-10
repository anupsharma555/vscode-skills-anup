# Choosing an instruction surface

Use the official host documentation to confirm current loading behavior. These references were reviewed on 2026-09-24; schemas and settings can change.

| Surface | Intended use | Authoring considerations |
| --- | --- | --- |
| Root `AGENTS.md` | Shared project guidance for compatible agents | Plain Markdown; no required YAML. Keep portable project facts and commands here. |
| Nested `AGENTS.md` | Folder-specific additions or overrides | Use for real subsystem differences. Verify how the host discovers nested files. |
| `.github/copilot-instructions.md` | Copilot repository-wide guidance | Place directly in `.github`, not `.github/copilot/`. Avoid contradictory duplication of AGENTS.md. |
| `.github/instructions/<name>.instructions.md` | Copilot guidance for selected files/tasks | Use supported frontmatter, including precise `applyTo` patterns when automatic matching is intended. |

Official documentation:

- [Codex AGENTS.md discovery and GitHub review rules](https://developers.openai.com/codex/guides/agents-md)
- [GitHub repository instructions](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/add-custom-instructions/add-repository-instructions)
- [VS Code custom instructions](https://code.visualstudio.com/docs/agent-customization/custom-instructions)

Codex documents a global-to-project instruction chain and per-directory override rules. Copilot support varies by feature and host. Keep portable content independent of a particular host setting; place host-specific configuration only where supported. Do not translate a platform example's commands into project requirements without checking the project.

Design references:

- [AGENTS.md authoring workflow](https://github.com/github/awesome-copilot/blob/main/skills/create-agentsmd/SKILL.md)
- [Vercel AI repository guidance](https://github.com/vercel/ai/blob/main/AGENTS.md): repository/package commands and architecture.
- [Cloudflare package guidance](https://github.com/cloudflare/agents/blob/main/packages/agents/AGENTS.md): public entry points and subsystem detail.
- [Awesome Copilot guidance](https://github.com/github/awesome-copilot/blob/main/AGENTS.md): source/generated content and artifact validation.

## Quality probes

Could a fresh agent identify where to work, which command to use, what it changes, and what success proves? Could it avoid a sibling project, a production database, an unimplemented exercise, and hand-editing generated output? If not, add the missing concrete instruction. Delete sections that merely restate generic software advice.
