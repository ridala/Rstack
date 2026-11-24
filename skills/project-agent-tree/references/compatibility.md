# Launcher compatibility

## Explicit child settings in T3 Code

The globally installed skill launched all four roles in a T3 Code Beta 0.1.11 checkout without a project `.codex/` directory. T3 completion records provided the executed model and launch options. Codex turn records independently showed the model and reasoning effort.

| Role | Executed model | Recorded effort | T3 tier option | Task outcome |
| --- | --- | --- | --- | --- |
| Explorer | `gpt-6.2-sol` | low | priority | Located both shipped skills and their entry points. |
| Researcher | `gpt-6.2-sol` | low | priority | Traced the tier option to the installed T3 adapter. |
| Worker | `gpt-6.2-sol` | high | default | Implemented a tier normalizer in a disposable directory. An independent check passed eight assertions. |
| Reviewer | `gpt-6.2-astra` | high | default | Identified conflicting launcher instructions and a missing prerequisite in the README. |

Codex did not expose the effective backend tier in these turn records. All four children inherited full filesystem access. The inspection-only roles followed instructions, and the Worker completed its assigned edit. These trials did not establish sandbox enforcement.

### Repeat the acceptance check

Use a checkout without project role files. Start the coordinator with settings that differ from the roles being tested. Invoke the installed skill with a concrete task for each role, leaving model and tier out of the prompt. Give the Worker an owned scratch file. Use an inspection-only inventory, a sourced lookup, and a diff with a known discrepancy for the other roles.

For each child, compare its launch record to the bundled role file and check its actual deliverable. Inspect the executed model, reasoning effort and tier option separately. Record any field the execution trace omits. A child name, a plausible answer, or the coordinator’s settings alone cannot pass this check. This follows OpenAI’s guidance to evaluate both the actions taken and the outcome. [Testing Agent Skills Systematically with Evals](https://developers.openai.com/blog/eval-skills/)

## Earlier built-in subagent trial

In a checkout with no project `.codex/` directory, a coordinator read the globally installed skill and received a request to inventory the repository’s skills. It launched one Explorer, collected its report, and verified the two skill entry points. This trial exercised default child settings and an inspection-only assignment. It did not test an enforced filesystem sandbox.

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

These results come from the supplied live audit. The documentation update did not rerun the agents. The optional preset has not been tested in T3 Code or with other Codex CLI versions.

## Verify a launcher for the optional preset

These checks apply when the preset's specific settings are required. Ordinary skill invocation passes the role’s model, effort, and tier at launch and uses the host’s available permission controls.

Before delegating project work with this preset:

1. Check the actual child model, reasoning effort, service tier, and effective permissions through launcher metadata or another trustworthy configuration record. Asking a model to identify itself is not sufficient.
2. In a disposable test directory, confirm the launcher enforces read-only access for Explorer, Researcher, and Reviewer. A prompt saying "read-only" is not enforcement. Do not test write restrictions against real project files.
3. Confirm the Worker can edit only within its permitted workspace and that its approval policy matches the intended project settings.
4. Confirm the launcher loads each role's instructions and can resolve the installed `unslop` dependency.
5. Record the client version, checks actually run, observed settings, and anything that remains unverified.

If Root cannot confirm a required setting, report which setting the launcher failed to confirm. Root can inspect the files and run existing checks. Any implementation still needs a Worker that meets the requirements. Do not automatically start separate CLI sessions to bypass host orchestration rules.

Subagents may not create further agents unless the root assignment explicitly authorizes it. Host rules may impose tighter limits and always take precedence.
