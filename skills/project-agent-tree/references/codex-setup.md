# Codex setup

This skill contains instructions and an optional Codex configuration preset. Installing instructions does not register the roles or change model settings.

## Dependencies

Install `unslop` from its maintainer when desired:

```sh
npx skills add backnotprop/pstack --skill unslop
```

Source: [backnotprop/pstack](https://github.com/backnotprop/pstack). Its [MIT license](https://github.com/backnotprop/pstack/blob/main/LICENSE) credits Lauren Tan. Rstack links to this dependency and does not bundle its text. A local copy may differ from the current upstream version.

The agent also needs delegation tools and access to the selected models. Confirm both before enabling the preset.

## Preset

| Role | Model | Reasoning | Service tier | Sandbox |
| --- | --- | --- | --- | --- |
| Root | `gpt-6.2-sol` | medium | fast | Existing project policy |
| Explorer | `gpt-6.2-sol` | low | fast | read-only |
| Researcher | `gpt-6.2-sol` | low | fast | read-only |
| Worker | `gpt-6.2-sol` | high | default | workspace-write |
| Reviewer | `gpt-6.2-astra` | high | default | read-only |

These are the author's chosen settings, not a guarantee of model availability. Do not silently replace unavailable models. Root permissions and unspecified approval settings remain subject to the host and project policy.

## Apply to a project

Use this procedure only when the user asks to configure a target project.

1. Inspect its existing `.codex/config.toml`, `.codex/agents/`, and repository instructions. Preserve existing settings and role registrations.
2. Use [config.example.toml](../assets/codex/config.example.toml) as a merge reference. Its relative `agents/*.toml` paths assume the merged file lives in the target project's `.codex/` directory.
3. Copy the four [role templates](../assets/codex/agents/) into the target project's `.codex/agents/`. If a name exists, inspect and merge it instead of overwriting it.
4. Confirm the selected models, feature flags, and fields are supported by the installed client. Preserve the preset unless the user chooses a replacement.
5. Start a fresh session and verify its actual configuration before delegating useful work. Follow the checks in [compatibility](compatibility.md).

If the project wants this workflow referenced in `AGENTS.md`, add a short pointer to the installed skill. Preserve all project-specific instructions. A Claude instructions file does not activate Codex TOML settings.

Do not copy project-wide instructions from the source app. This package contains no simulator, app migration, storage, signing, or release configuration.

## Verification status

The Rstack draft has static file and discovery checks only. The author reported launcher inheritance findings from Codex CLI 0.172.0; the Rstack package has not been verified in a fresh agent session. Reading CLI help or parsing TOML does not establish runtime behavior.

Official references:
- [Subagents](https://developers.openai.com/codex/subagents/)
- [Configuration reference](https://developers.openai.com/codex/config-reference/)
