---
name: project-agent-tree
description: Coordinate substantial repository work with bounded explorer, worker, researcher, and conditional reviewer agents. Use when delegation would save time or improve confidence; skip small tasks that the root can finish directly.
---

# Project agent tree

Use the separately installed `$unslop` skill before conversational writing. Resolve it through the current agent's skill catalog, not a machine-specific path. Apply it to progress updates, assignments, reports, and final answers. If it is missing, report the missing dependency and follow the user's writing instructions. Do not install dependencies without authorization.
Use this Skill for substantial repository work that has independent investigation, implementation, or research tasks. Keep small changes, formatting, trivial lookups, and simple one-file work in the root.

The root remains responsible for scope, decisions, integration, verification, and the final answer. Treat every subagent report as evidence to inspect, not as an automatic conclusion. Repository instructions and user authorization apply to every role.

## Setup and model selection

The workflow can guide an agent with delegation tools. The optional Codex preset defines role models and permissions. Installing this skill does not activate that preset or change the current session's model.

For first-time setup, read [Codex setup](references/codex-setup.md). Before delegating with a new launcher or version, read [compatibility](references/compatibility.md).

Use the configured model and reasoning effort for each role. If the launcher cannot honor them, report the limitation and keep the task in the root. A user must authorize any substitution. Host tool instructions control how agents are launched, awaited, and cancelled. Never bypass those instructions with another launcher or CLI.

## Root workflow

Understand the request and inspect the current state before delegating. Decide whether another agent would save time or improve confidence. Split only independent, useful work. Give each agent a bounded task, the smallest useful context, a clear deliverable, and a stop condition. Give each worker explicit file or component ownership.

Run independent read-only tasks in parallel. Run dependent tasks in order. Parallel workers must have non-overlapping ownership. Use isolated worktrees when repository instructions require them. Do not assign the same question or files to several agents unless an independent read-only review is intentional.

Collect all results and compare the cited evidence. Resolve conflicts by inspecting the disputed files or running the relevant check. Inspect every changed file, run final verification, and give the user one coherent answer.

## Roles and result formats

### Explorer

Use the explorer for bounded repository investigation when files, entry points, dependencies, or the cause of a bug are unclear. It may use read-only checks to reproduce or narrow a bug and find existing patterns. The root handles any edits or assigns them to a Worker when repository rules allow it.

Its report must include findings, file and line evidence when useful, the likely cause or conclusion, risks and unknowns, and the recommended next action.

### Worker

Use a worker for bounded implementation. Assign files or a component with no overlap between parallel workers. The worker follows existing conventions, preserves user and concurrent changes, avoids unrelated cleanup, updates relevant tests, and runs checks tied to its change.

Its report must include what changed, files changed, checks run, results, assumptions, and remaining risks or unfinished work. A worker must not claim a check passed unless it ran.

### Researcher

Use the researcher only when the task needs current official documentation, APIs, configuration formats, version-specific behavior, standards, or another primary technical source. It checks repository files and installed documentation first. It browses only when those sources do not answer the question. It does not edit project files.

Its report must include a direct answer, sources, version or date details, confirmed facts, inferences or uncertainties, and the recommended action.

### Reviewer

The reviewer is optional and expensive. Use it when the user requests an independent review or when a change affects authentication, authorization, permissions, secrets, payments, deletion, or another security boundary. Also use it for changes across several architectural areas, a difficult bug that remains uncertain, failed implementation or verification, or a serious risk of data loss or production outage.

Do not use the reviewer for routine edits, small fixes, formatting, or normal one-file changes. It independently inspects the actual diff and surrounding code. It checks correctness, regressions, unsafe assumptions, security, missing tests, and simpler fixes. It does not rewrite the change unless the root assigns a separate implementation task.

Its report must list findings by severity with file and line evidence, missing tests, remaining risk, and one verdict: `approve`, `approve with minor concerns`, or `request changes`.

No subagent may create another agent unless the root task explicitly authorizes it.

## Assignment templates

Explorer:

```text
Inspect [specific area or problem] using read-only checks. Do not edit files, create artifacts, change local or remote state, or request write access. Return findings, evidence, likely cause, risks, and the next action. Stop when [completion condition].
```

Worker:

```text
Implement [specific change]. You own [files or component]. Do not modify unrelated files. Add or update tests and run [checks]. Return changed files, test results, assumptions, and remaining risks.
```

Researcher:

```text
Research [specific question] using official or primary sources. Return the answer, sources, version details, confirmed facts, uncertainties, and the recommended action. Do not edit project files.
```

Reviewer:

```text
Review [specific change] independently. Focus on correctness, regressions, security, and missing tests. Return findings ordered by severity with file references, then give a verdict.
```

Add a precise completion condition to every template. Stop delegating when direct root work is easier.

## Failure handling

If an agent fails, times out, or returns weak evidence, retry once with a narrower task when that would help. Otherwise finish the work in the root. If agents disagree, compare their evidence and verify the disputed point directly. Keep user changes intact during recovery.

Check the launched session's model, reasoning effort, service tier, instructions, and permissions against the role configuration when the launcher exposes that evidence. A role name or prompt is not proof that the settings took effect. Confirm enforced read-only access before assigning work to Explorer, Researcher, or Reviewer. If required settings cannot be enforced or confirmed, finish the task in the root and report the limitation. Use an alternative launch method only when the host supports it and the user has authorized any change in provider, model, or settings.

Never claim a test passed unless it ran. Never claim a fresh session loaded this setup unless a fresh session was tested. If unrelated global configuration breaks a validation command, do not edit it. Retry with the installed CLI's user-config isolation option and report the limitation.

## Final verification

Before replying to the user:

- Confirm the result matches the requested scope and repository instructions.
- Inspect every changed file and the combined diff.
- Confirm parallel workers had no overlapping edit ownership.
- Check subagent claims against their cited files and command results.
- Run checks appropriate to the change and report the exact results.
- Resolve review findings or report them as remaining risks.
- Confirm no unrelated files changed.
- State any model substitution, failed check, untested behavior, or required owner action.
