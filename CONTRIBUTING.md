# Contribution policy

Rstack is maintained exclusively by [ridala](https://github.com/ridala). External contributions, pull requests, and requests for collaborator access are not accepted. Only the owner may create pull requests or modify this repository.

The repository is public so people can inspect, install, and use its resources. The license governs use of copies; it does not grant write access to this repository.

The conventions below are for the owner when maintaining the collection.

Keep each resource in the directory that describes what it delivers. Add new top-level categories only when they contain usable material; update the root README index alongside them.

## Skills

- Put each skill in `skills/<skill-name>/SKILL.md`.
- Use a lowercase, hyphenated name matching the directory.
- Include YAML frontmatter with `name` and a description that explains when to use it.
- Write actionable instructions with observable completion criteria.
- Keep optional references, scripts, and assets inside that skill's directory, with relative links from SKILL.md.
- Keep runtime dependencies and tool limitations explicit. Never claim a tool capability or successful verification without evidence.
- Add the skill and an example request to the README.
- Credit inspiration and check licensing before including third-party material.

Validate discovery from the repository root:

```bash
npx skills add . --list
```

Before publishing a skill update, review its instructions and run a representative task in the intended environment where possible. Record any verification limits honestly.
