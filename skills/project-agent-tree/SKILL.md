---
name: project-agent-tree
description: Delegate repository tasks to subagents for investigation, implementation, research, or review. Use when the user invokes the agent tree or independent work benefits from delegation.
---

# Project agent tree

## Root's role

As Root, turn the user's goal into assignments. Tell the user who owns the current task, what you have verified, and what comes next. When work is blocked, explain why. Ask the user for a decision or action only when it requires their input.

You can read code, inspect diffs, and run existing tests and checks. Limit your own file edits to Markdown and HTML documentation, such as a README or a test report. Assign every implementation change to a Worker, including one-line fixes, test edits, and changes to application HTML. Run checks in verification mode when they offer to fix files or update snapshots.

When the user invokes the tree for repository work, give a child a concrete assignment. Honor a requested role. Delegate even a small investigation to an Explorer. You can answer questions about the skill and write documentation yourself. When the skill applies implicitly, delegate independent inspection when it helps. Respect user and host limits on delegation.

## Launch and collect

1. Identify the question the child must answer or the files it owns. Inspect only enough context to give it a useful assignment. For independent tasks, give each child a distinct scope. Keep dependent steps in order.
2. Read the selected role file and launch it with the settings below. Use the installed skill directory as the base for relative paths. This works without project configuration or a registered role name.
3. Give the child the relevant paths, allowed actions, expected result, and stop condition. Explorer, Researcher, and Reviewer assignments are inspection only. Tell the child to leave files and external state untouched. A Worker may edit only its assigned files. Children should complete their own assignments unless explicitly asked to delegate further.
4. Collect the child's result through the host's completion mechanism. Check its evidence or diff and run the relevant checks. If a check fails and needs a code change, give the failure to the responsible Worker. Rerun the check after the fix and report the result.

If the separate `$unslop` writing skill is available, use it for reports and updates. Otherwise use the user's writing preferences.

## Configure the child launch

Read the [Explorer](assets/codex/agents/explorer.toml), [Researcher](assets/codex/agents/researcher.toml), [Worker](assets/codex/agents/worker.toml), or [Reviewer](assets/codex/agents/reviewer.toml) file for the assignment. Use its `model`, `model_reasoning_effort`, and `service_tier` as child launch parameters. Include its role instructions in the brief when the launcher does not load the file. Leave the running root's settings alone. Explicit user settings take precedence.

Choose the launch tool using the host's routing rules. On T3, use native spawn only when the host routes the assignment there and every required model setting can be set directly or is known to match through inheritance. A missing tier field with unknown inheritance does not qualify. For explicit user-selected settings or a profile that native spawn cannot establish, use T3’s `delegate_task`:

1. Call `orchestrator_capabilities` before the first delegation in the thread, following the host's discovery rules. Look up the provider, model, and advertised option values.
2. Set `target.providerInstanceId` and `target.model`. Pass both `reasoningEffort` and `serviceTier` in `target.options`. With T3’s Codex catalog, request `priority` for Fast and `default` for Standard. Passing Standard explicitly matters when the root is on Fast.
3. Follow the launch result’s completion instructions. For a pending T3 delegate, honor its `next` field.

On another host, use its equivalent child launch controls. If no permitted launcher supports a required setting, identify the field and ask before substituting a profile.

Check the returned model and options against the role. Flag a mismatch before using the result. If a field is absent from execution metadata, distinguish the requested setting from what the host confirmed.

## Choose the assignment

- **Explorer** investigates repository state, entry points, bugs, or remaining work. Ask for findings with file evidence and unresolved questions. Example: “Inspect the backlog and build records. Identify what still blocks the first signed build. Cite the records, flag gaps, and leave files untouched.”
- **Worker** implements a bounded change. Assign explicit file or component ownership, preserve concurrent edits, and ask for the changed files and results of relevant checks. Parallel workers need separate ownership.
- **Researcher** answers a specific technical question from installed documentation or primary sources. Ask for sources, applicable versions, and uncertainties.
- **Reviewer** independently inspects a diff when requested or when a second review would materially reduce risk. Ask for findings ordered by severity with locations and verification gaps.

## Permissions and optional settings

Carry the file's sandbox and approval settings into the launch where the host supports them. T3 runtime modes do not express the TOML filesystem sandbox or Codex approval policy. Under inherited permissions, include the role’s action limits in its brief (for Explorer, no edits or approval requests), and disclose any unenforced limits. Inspection-only describes the assignment. When the user or project requires an enforced sandbox, verify that boundary before assigning the work. Honor any required model, provider, or other explicit settings. If the host cannot meet a requirement, report which one and continue only with work permitted in the root.

Use the [Codex preset guide](references/codex-setup.md) only when asked to configure custom roles. Its [compatibility notes](references/compatibility.md) apply to that preset. Leave project configuration alone during ordinary delegation. If the host blocks a launch, report what happened, what you completed, and which assignment still needs a child. Only report a child result after the child returns it.
