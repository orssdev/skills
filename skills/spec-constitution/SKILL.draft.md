---
name: spec-constitution
description: DRAFT. Creates the project's global rules in .spec/constitution/ (architecture, security, testing, style, pseudo-code dialect) before any blueprinting. Use once per project, or when the user wants to set, extract, or update project-wide conventions for spec-driven development.
---

# spec-constitution (draft notes)

Phase 1 of the spec-driven flow. Runs once per project (or once per org, then inherited). Not per feature.

## Purpose
Settle global rules once so blueprint, spec, and build phases never re-decide them.

## Output
```
.spec/constitution/
  index.md          routing table: "touching X -> load these files"
  architecture.md   stack, folder layout, design patterns
  security.md       auth, sanitization, secrets
  testing.md        coverage targets, naming, TDD expectations
  style-guide.md    formatting, lint, naming
  dialect.md        the fixed pseudo-code vocabulary used in specs
  (optional) components.md, hooks.md, api.md   per-type conventions
```

## Why split by domain
- Context efficiency: a subagent loads only the files relevant to its task.
- Ownership: domains can be updated independently.
- Reuse: copy or symlink the dir across repos.

## Modes
- Interview mode (new project): grill the user (reuse the `grilling` skill) on each domain.
- Extract mode (existing repo): read lint config, folder structure, and existing code, draft rules, ask the user to approve. Propose rather than ask blank questions.

## Rules learned
- `index.md` is a routing table, not prose. Spec and build phases read it to pick files per task.
- Each per-file spec lists the constitution files it needs in its frontmatter (`constitution: [...]`), rather than the agent guessing.
- Per-type conventions (hooks, components, api) live here, not in per-folder specs. A "hooks spec" would just be a style guide.
- Constitution files are rules, not behavior. Behavior belongs in feature and file specs.

## Open questions
- Single `constitution.md` for small projects, split only past a size threshold?
- Inheritance mechanism for shared org rules (copy, symlink, or a `extends:` line)?
