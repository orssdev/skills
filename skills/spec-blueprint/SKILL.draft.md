---
name: spec-blueprint
description: DRAFT. Turns prompt.md into a blueprint through grilling and pair-programming with the developer, producing blueprint.md or a dir of split feature specs. Use after the prompt is written and before per-file specs, when the user wants edge cases and architecture worked out.
---

# spec-blueprint (draft notes)

Phase 3. Interactive: grill plus pair-programming with the dev.

## Purpose
Resolve edge cases and architecture decisions before any file-level spec exists.

## Input
- `prompt.md`
- `.spec/constitution/` (read `index.md` first, load only relevant files)

## Output
- Small project: a single `blueprint.md`.
- Larger: a dir of split files, one `feature.spec.md` per feature.

A feature spec is the index and glue for a feature:
- files that will exist (with one-line purpose each)
- how they connect, data flow
- shared types
- dependency graph and build order
- edge cases found during grilling

## Spec levels (decided)
Hybrid:
| Level | Role |
|---|---|
| per file (`X.spec.md` beside `X.ts`) | source of truth for building one file |
| per feature (`feature.spec.md`) | index, flow, shared types, build order |
| constitution (`.spec/constitution/`) | global rules and conventions |

- Small project: skip the feature level, use constitution plus per-file specs.
- Multi-feature project: use all three.
- No per-type-folder specs (hooks, components, api). Those are conventions and go in the constitution.

## Rules learned
- Reuse the `grilling` skill for edge-case questioning.
- Feature and file specs live next to the code so they move with it. Only the constitution lives in `.spec/`.
- Blueprint records the dependency graph; the build phase depends on it to find parallel work.

## Open questions
- Should the skill pick small vs large layout automatically from project size, or ask the user?
