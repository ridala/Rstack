# Launcher compatibility

## Reported source-project observation

The source setup records a test with Codex CLI 0.172.0. Named roles used their declared models and reasoning efforts, but children inherited the root's Fast tier and `danger-full-access` sandbox. Worker and Reviewer therefore received the Fast tier, and the intended read-only roles had write access.

This is a reported observation from the source setup. It was not reproduced while packaging the Rstack draft and should not be treated as a guarantee about every launcher or version.

## Verify a launcher

Before delegating project work with this preset:

1. Check the actual child model, reasoning effort, service tier, and effective permissions through launcher metadata or another trustworthy configuration record. Asking a model to identify itself is not sufficient.
2. In a disposable test directory, confirm the launcher enforces read-only access for Explorer, Researcher, and Reviewer. A prompt saying “read-only” is not enforcement. Do not test write restrictions against real project files.
3. Confirm the Worker can edit only within its permitted workspace and that its approval policy matches the intended project settings.
4. Confirm the launcher loads each role's instructions and can resolve the installed `unslop` dependency.
5. Record the client version, checks actually run, observed settings, and anything that remains unverified.

If the launcher ignores a required field or cannot provide enough evidence, keep the task in the root and explain the limitation. Do not automatically start separate CLI sessions to bypass host orchestration rules.

Subagents may not create further agents unless the root assignment explicitly authorizes it. Host rules may impose tighter limits and always take precedence.
