# skills

A public repo of agent skills, installed via `npx skills add orssdev/skills`.

## Structure

- Each skill lives in `skills/<skill-name>/` and must contain a `SKILL.md`.
- `<skill-name>` is kebab-case and must match the `name` in the `SKILL.md` frontmatter.
- Supporting files (scripts, references, assets) go inside the skill's own directory; skills must not depend on files outside it.

## SKILL.md rules

- Frontmatter requires `name` and `description`.
- `description` states what the skill does and when to trigger it; it is what an agent uses to decide relevance, so make it specific.
- Keep `SKILL.md` focused; move long reference material into sibling files and link to them.

## Workflow

- One skill per commit; scope is the skill name, e.g. `feat(my-skill): add skill`.
- After adding or renaming a skill, update the skill list in `README.md` if one exists.
- Verify discovery with `npx skills add . --list` before pushing.
