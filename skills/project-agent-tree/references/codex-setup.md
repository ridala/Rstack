# Codex setup

For ordinary use, invoke the installed skill in a session with a subagent tool. The root reads the bundled role file and passes its model, reasoning effort, and tier to the child launcher. The Root row below applies only when starting a session with the optional project preset. Use this guide to register the roles in a project.

## Writing skill

The Writer requires `unslop`. Install it from its maintainer if it is missing.

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
| Writer | `gpt-6.1-terra` | high | fast | workspace-write |

These are the author's chosen settings, not a guarantee of model availability. Do not silently replace unavailable models. Root permissions and unspecified approval settings remain subject to the host and project policy.

## Apply to a project

Use this procedure only when the user asks to configure a target project.

1. Inspect its existing `.codex/config.toml`, `.codex/agents/`, and repository instructions. Preserve existing settings and role registrations.
2. Use [config.example.toml](../assets/codex/config.example.toml) as a merge reference. Its relative `agents/*.toml` paths assume the merged file lives in the target project's `.codex/` directory.
3. Copy the [role templates](../assets/codex/agents/) into the target project's `.codex/agents/`. If a name exists, inspect and merge it instead of overwriting it.
4. Confirm the selected models, feature flags, and fields are supported by the installed client. Preserve the preset unless the user chooses a replacement.
5. Have the user trust the target project in Codex before the first launch that should load the preset. Codex skips the project role configuration until the user trusts that project. Installing the skill does not establish project trust.
6. Start a fresh session and verify its actual configuration before delegating useful work. Follow the checks in [compatibility](compatibility.md).

If the project wants this workflow referenced in `AGENTS.md`, add a short pointer to the installed skill. Preserve all project-specific instructions. A Claude instructions file does not activate Codex TOML settings.

Do not copy project-wide instructions from the source app. This package contains no simulator, app migration, storage, signing, or release configuration.

## Verification status

The reported Rstack live audit passed a clean install from GitHub into a clean project with Codex CLI 0.172.0. Codex read the skill and loaded the role preset after the user trusted the project. Explorer, Researcher, Worker, and Reviewer each completed a task with the intended model and reasoning level. The Writer was added after that audit.

All four roles inherited the lead's Fast speed and workspace write access. Explorer, Researcher, and Reviewer therefore had write access despite their read-only settings. Worker and Reviewer ran at Fast rather than their configured standard speed. A separate Worker launched with explicit settings created the requested file successfully. That result does not establish read-only enforcement for other roles.

See [compatibility](compatibility.md) for the reproduced behavior and the checks required before delegation. The compatibility notes also describe T3 launches using explicit child settings.

Official references:
- [Subagents](https://developers.openai.com/codex/subagents/)
- [Configuration reference](https://developers.openai.com/codex/config-reference/)
