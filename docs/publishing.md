# Publishing skills

Rstack uses the standard `skills/<name>/SKILL.md` layout recognized by the Skills CLI. No custom discovery configuration or npm package is required.

Each skill must have YAML frontmatter containing its name and description. Keep skill names unique within this repository.

## Verify the public source

```bash
npx skills add ridala/Rstack --list
```

## Install a specific skill

```bash
npx skills add ridala/Rstack --skill stageshow-figma
```

The CLI prompts for the destination agent. Installation configures instructions, not access to external services.

## skills.sh listing

According to the skills.sh FAQ, public skills appear through anonymous telemetry from CLI installations. A repository push or discovery-only check is not a registration. Indexing time and leaderboard placement are controlled by skills.sh.

Use real installations to establish distribution; do not create artificial install counts. Users may disable telemetry, so not every installation contributes to listing data.

## Official references

- [Creating skills](https://github.com/vercel-labs/skills/blob/main/docs/creating-skills.md)
- [Skills CLI](https://www.skills.sh/docs/cli)
- [Listing FAQ](https://www.skills.sh/docs/faq)

Documentation checked on 2026-11-14. Consult the current upstream documentation before changing publishing behavior.
