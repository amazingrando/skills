# skills

Agent skills by [Randy Oest](mailto:oest@amazingrando.com) — small, composable, and installable into any coding agent.

## Quickstart

Install with the [skills.sh](https://skills.sh) CLI:

```bash
npx skills@latest add amazingrando/skills
```

Pick the skills you want and which agents to install them on. That's it.

## What's in here

Each skill lives in its own folder under `skills/<category>/<skill-name>/` and
contains a `SKILL.md`. Skills are grouped into three categories:

- **[Engineering](./skills/engineering/)** — code work: building, debugging, testing, refactoring.
- **[Productivity](./skills/productivity/)** — non-code workflow tools: planning, writing, communication.
- **[Misc](./skills/misc/)** — one-off tools kept around but used rarely.

## Reference

<!-- List each installable skill here with a one-line summary and a link. -->

### Productivity

- **[example-skill](./skills/productivity/example-skill/SKILL.md)** — Template showing the required structure. Replace with your own.

## Adding a skill

1. Create a folder under the right category: `skills/<category>/<skill-name>/`.
2. Add a `SKILL.md` with `name` + `description` frontmatter (see the example skill).
3. Register the folder path in [`.claude-plugin/plugin.json`](./.claude-plugin/plugin.json).
4. Add it to the Reference list above.

Only skills listed in `plugin.json` get installed — a handy way to keep
work-in-progress skills in the repo without shipping them. If you want a staging
area, add a `skills/in-progress/` folder and simply leave those paths out of
`plugin.json`.

## License

[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) — see [LICENSE](./LICENSE).
