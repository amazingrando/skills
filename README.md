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
contains a `SKILL.md`. Right now everything is under **design**:

- **[Design](./skills/design/)** — UX evaluation, design QA, and design-to-product comparison.

## Reference

### Design

- **[design-eval](./skills/design/design-eval/SKILL.md)** — Structured UX/UI evaluation grounded in Nielsen, Shneiderman, Gerhardt-Powals, Fogg (B=MAP), and Laws of UX.
- **[compare-design-to-product](./skills/design/compare-design-to-product/SKILL.md)** — Compare a Figma design to a live-product screenshot and report meaningful drift (not pixel-perfect diffs).

## Adding a skill

1. Create a folder under the right category: `skills/<category>/<skill-name>/`.
2. Add a `SKILL.md` with `name` + `description` frontmatter (see an existing skill).
3. Register the folder path in [`.claude-plugin/plugin.json`](./.claude-plugin/plugin.json).
4. Add it to the Reference list above.

Only skills listed in `plugin.json` get installed — a handy way to keep
work-in-progress skills in the repo without shipping them. If you want a staging
area, add a `skills/in-progress/` folder and simply leave those paths out of
`plugin.json`.

## License

[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) — see [LICENSE](./LICENSE).
