---
name: example-skill
description: A template skill showing the required structure. Replace this with one of your own. Use when you want a starting point for a new skill, or mention "example skill".
---

# Example Skill

This is a template. Delete it once you've added your own skills.

## How a skill works

Everything above the second `---` is YAML frontmatter. Two fields matter:

- **name** — must match the folder name (lowercase, hyphenated).
- **description** — the single most important line. The agent reads only the
  description to decide *whether* to load this skill, so write it as a trigger:
  what the skill does, then "Use when the user...". Pack in the words and phrases
  a user would actually say.

Everything below the frontmatter is the skill body — the instructions the agent
follows once the skill fires. Write it like you'd brief a capable teammate.

## Progressive disclosure (optional)

For longer skills, keep `SKILL.md` short and move detail into sibling files that
the body points to, e.g. "See [details.md](details.md) for edge cases." The agent
only opens them when needed, which saves context. You can also add a `scripts/`
folder next to this file for any helper scripts the skill runs.

## Checklist for a new skill

1. Create a folder under the right category (`engineering/`, `productivity/`, `misc/`).
2. Add a `SKILL.md` with `name` + `description` frontmatter.
3. Add the folder's path to `.claude-plugin/plugin.json`.
4. Link it in the top-level `README.md` reference list.
