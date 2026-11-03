---
name: spec-build
description: DRAFT. Plans and executes the build from approved specs, grouping independent files and fanning out subagents to save context. Use when specs are approved and the user is ready to generate code.
---

# spec-build (draft notes)

Phase 5. Reads specs, plans, then builds with subagents.

## Flow
1. Read feature spec(s) and every per-file spec's frontmatter (`status`, `depends_on`). Skip `built` files.
2. Build the dependency graph and group files with no mutual dependencies.
3. Present the plan (groups, order, subagent count) to the user.
4. For each group, spawn subagents in parallel. Each gets only:
   - its own `X.spec.md`
   - the constitution files listed in its frontmatter
   - the specs it `depends_on`, for contracts only
5. After each group, verify against the spec (contract, errors table), set `status: built`.
6. Report anything that diverged from a spec.

## Why subagents
Each file's context stays small, which saves tokens. Use as many as the graph allows.

## Rules learned
- Invoked manually, when the user is comfortable. Never auto-run after spec generation.
- Spec wins over code on conflict; do not silently edit specs to match code.
- Pass subagents the minimum context; the routing table in `constitution/index.md` picks the rules.
- Run code-simplifier on non-trivial output before calling the work done.

## Open questions
- Add a `spec-sync` phase to detect drift between specs and code after edits?
- Verification step: per-subagent self-check, or a separate reviewer pass per group?
- Cap on parallel subagents?
