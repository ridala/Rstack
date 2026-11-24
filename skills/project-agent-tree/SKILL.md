---
name: project-agent-tree
description: Delegate repository tasks to subagents for investigation, implementation, research, or review. Use when the user invokes the agent tree or independent work benefits from delegation.
---

# Project agent tree

When the user invokes this skill to do repository work, launch a subagent for a concrete part of that work. Honor the requested role or choose the closest role below. For a small investigation, delegate the investigation itself. A question about the skill's installation or behavior can be answered directly.

## Launch and collect

1. Identify the question the child must answer or the files it owns. Inspect only enough context to give it a useful assignment. For independent tasks, give each child a distinct scope. Keep dependent steps in order.
2. Call the host's subagent tool (for example, Codex `spawn_agent`). Use the host's default child settings and an available built-in role. If the tool takes only a task, put the role and its instructions in the task. This workflow needs no project config or custom role registration.
3. Give the child the relevant paths, allowed actions, expected result, and stop condition. Explorer, Researcher, and Reviewer assignments are inspection only. Tell the child to leave files and external state untouched. A Worker may edit only its assigned files. Children should complete their own assignments unless explicitly asked to delegate further.
4. Use the host's wait or completion mechanism and collect the actual result. While a child works, handle a separate part of the task. Check the child's evidence or diff, run relevant checks, and integrate its findings into the answer.

If the skill was selected implicitly, delegate when an independent assignment would help. Keep trivial work in the root unless the user invoked the workflow or requested delegation. Respect any user or host restriction on spawning agents.

If the separate `$unslop` writing skill is available, use it for reports and updates. Otherwise use the user's writing preferences.

## Choose the assignment

- **Explorer** investigates repository state, entry points, bugs, or remaining work. Ask for findings with file evidence and unresolved questions. Example: “Inspect the backlog and build records. Identify what still blocks the first signed build. Cite the records, flag gaps, and leave files untouched.”
- **Worker** implements a bounded change. Assign explicit file or component ownership, preserve concurrent edits, and ask for the changed files and results of relevant checks. Parallel workers need separate ownership.
- **Researcher** answers a specific technical question from installed documentation or primary sources. Ask for sources, applicable versions, and uncertainties.
- **Reviewer** independently inspects a diff when requested or when a second review would materially reduce risk. Ask for findings ordered by severity with locations and verification gaps.

## Permissions and optional settings

Inspection-only describes the assignment. The host controls the child's effective permissions. When the user or project requires an enforced sandbox, verify that boundary before assigning the work. Honor any required model, provider, or other explicit settings. If the host cannot meet a requirement, report which one and continue only with work permitted in the root.

Use the [Codex preset guide](references/codex-setup.md) only when asked to configure custom roles. Its [compatibility notes](references/compatibility.md) apply to that preset. Leave project configuration alone during ordinary delegation. If the host lacks a delegation tool or rejects the launch, report what happened and which work the root completed. Only report a child result after the child returns it.
