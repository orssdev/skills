# skills

A collection of agent skills, installable with the [`skills`](https://github.com/vercel-labs/skills) CLI.

## Install

Install every skill in this repo:

```bash
npx skills add orssdev/skills
```

Install a single skill:

```bash
npx skills add orssdev/skills --skill <skill-name>
```

List what's available without installing:

```bash
npx skills add orssdev/skills --list
```

## Layout

```
skills/
└── <skill-name>/
    ├── SKILL.md        # required: frontmatter + instructions
    └── ...             # optional: scripts, references, assets
```

Each skill's `SKILL.md` starts with frontmatter:

```markdown
---
name: <skill-name>
description: What the skill does and when an agent should use it.
---
```

## Adding a skill

1. Create `skills/<skill-name>/SKILL.md` (name must match the directory).
2. Commit and push to `main`.
3. Install it with `npx skills add orssdev/skills --skill <skill-name>`.

## License

[MIT](LICENSE)
