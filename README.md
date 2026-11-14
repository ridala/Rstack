# Rstack

Skills and practical resources I use for design and development, shared so others can inspect and use them. Skills live in `skills/`; future tools and resources will have their own directories when added.

## Skills

| Skill | Say | What it does |
| --- | --- | --- |
| [stageshow-figma](skills/stageshow-figma/SKILL.md) | “Use stageshow-figma” | Creates editable product illustrations and UI demonstrations in Figma. |

## Install

Requires Node.js 22.20 or later for the current Skills CLI.

```bash
npx skills add ridala/Rstack --skill stageshow-figma
```

List available skills without installing:

```bash
npx skills add ridala/Rstack --list
```

## Use

Connect your agent's Figma editing tools, then provide a target file or selection:

> Use stageshow-figma to create an editable 720 × 400 illustration showing an inbox conversation assigned to a teammate. Use the existing components and brand styles.

The skill installs instructions, not a Figma plugin. Prototype authoring and playback depend on the connected tools. The skill has not yet been evaluated end to end in a live Figma file.

## Maintenance

Maintained exclusively by [ridala](https://github.com/ridala). External contributions and pull requests are not accepted. Only the owner may modify this repository. Others may use copies under the license below.

## Credits

`stageshow-figma` is independently written and inspired by [StageShow by Benji Taylor](https://benji.org/stageshow) and the [original skill](https://www.skills.sh/benjitaylor/skills/stageshow). It does not include StageShow's React kit, scripts, examples, or assets. No affiliation or endorsement by StageShow or Figma is implied.

## License

[MIT](LICENSE)
