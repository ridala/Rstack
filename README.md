# Rstack

A growing collection of skills and practical resources for design and development, by [ridala](https://github.com/ridala).

## Skills

| Skill | Purpose | Requirements |
| --- | --- | --- |
| [stageshow-figma](skills/stageshow-figma/SKILL.md) | Editable product illustrations and UI demonstrations in Figma | An agent with connected Figma editing tools; prototype capabilities vary |

### Install

Requires Node.js 22.20 or later, according to the current [Skills CLI documentation](https://github.com/vercel-labs/skills).

```bash
# Discover available skills without installing
npx skills add ridala/Rstack --list

# Install the Figma skill (choose your agent when prompted)
npx skills add ridala/Rstack --skill stageshow-figma
```

This installs agent instructions. It does not install a Figma plugin or grant Figma access. Connect your agent's Figma tools separately.

### Use

Ask your agent to use `stageshow-figma`, provide a target Figma file or selection, and describe the output:

> Use stageshow-figma to create an editable 720 × 400 product illustration in this Figma file. Show an inbox conversation assigned to a teammate. Use the existing components and brand styles. Create a static composition first; animate it only if the connected tools support it.

The skill has not yet been evaluated end to end against a live Figma file. It requires the agent to distinguish verified playback from static state designs.

## Repository layout

```text
skills/       Installable agent skills, each with its own SKILL.md
docs/        Repository documentation and publishing notes
```

Future tools, templates, and examples can live in separate top-level directories when they exist. Only reusable agent instructions belong in `skills/`; the repository root stays a general resource index.

## Maintenance

Rstack is maintained exclusively by [ridala](https://github.com/ridala). External contributions and pull requests are not accepted. The repository is public for inspection, installation, and use; only the owner may modify it.

See the [contribution policy](CONTRIBUTING.md) and [publishing guide](docs/publishing.md).

## Credits and license

The Figma skill is independently written and inspired by [StageShow by Benji Taylor](https://benji.org/stageshow). Rstack is not affiliated with or endorsed by StageShow or Figma. See [credits](CREDITS.md).

Original Rstack material is available under the [MIT License](LICENSE). Third-party assets, if added later, retain their own licenses.
