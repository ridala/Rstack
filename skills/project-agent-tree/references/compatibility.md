# Launcher compatibility

## Rstack live test on Codex CLI 0.172.0

The reported Rstack audit installed the skill from GitHub into a clean project. Codex read the skill and loaded its role preset after the user trusted the project. All four named roles completed a task.

| Role | Model and reasoning | Actual speed | Actual permissions | Difference from preset |
| --- | --- | --- | --- | --- |
| Explorer | Correct | Fast | Workspace write access | Expected read-only access |
| Researcher | Correct | Fast | Workspace write access | Expected read-only access |
| Worker | Correct | Fast | Workspace write access | Expected standard speed |
| Reviewer | Correct | Fast | Workspace write access | Expected standard speed and read-only access |

The test reproduced inheritance of the lead's speed and write permissions on 0.172.0. Role model and reasoning settings took effect. The read-only settings and Worker and Reviewer speed settings did not.

A separate Worker launched with explicit settings created the requested file successfully. This confirms that Worker task completed. It does not prove that the named-role launcher honors permission settings or that a separate read-only role would enforce them.

These results come from the supplied live audit. The documentation update did not rerun the agents. Other launchers, including T3 Code, and other Codex CLI versions are untested.

## Verify a launcher

Before delegating project work with this preset:

1. Check the actual child model, reasoning effort, service tier, and effective permissions through launcher metadata or another trustworthy configuration record. Asking a model to identify itself is not sufficient.
2. In a disposable test directory, confirm the launcher enforces read-only access for Explorer, Researcher, and Reviewer. A prompt saying "read-only" is not enforcement. Do not test write restrictions against real project files.
3. Confirm the Worker can edit only within its permitted workspace and that its approval policy matches the intended project settings.
4. Confirm the launcher loads each role's instructions and can resolve the installed `unslop` dependency.
5. Record the client version, checks actually run, observed settings, and anything that remains unverified.

The lead must check the permissions the launcher actually granted, rather than assuming the role file took effect. If the lead cannot confirm enforced read-only access for Explorer, Researcher, or Reviewer, the lead must handle that task itself and report the limitation. If any other required setting is ignored or unconfirmed, keep the task in the lead. Do not automatically start separate CLI sessions to bypass host orchestration rules.

Subagents may not create further agents unless the root assignment explicitly authorizes it. Host rules may impose tighter limits and always take precedence.
