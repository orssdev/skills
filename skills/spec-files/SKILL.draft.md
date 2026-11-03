---
name: spec-files
description: DRAFT. Derives one X.spec.md per planned code file from the blueprint, written in a fixed pseudo-code layout and placed beside the file it describes (useHook.spec.md next to useHook.tsx). Use after blueprint approval, before building.
---

# spec-files (draft notes)

Phase 4. Turns blueprint and feature specs into per-file specs. This is where spec layout matters most; it was the biggest learning so far.

## Anchoring
`useHook.spec.md` sits next to `useHook.tsx`. One spec per code file.

## Layout (pseudo-code, not code)
Pseudo-code beats "code but not code": it states behavior and structure without committing to syntax, so a build subagent cannot drift from intent.

Frontmatter:
```yaml
status: draft | approved | built
depends_on: [relative/path/other.spec.md]
constitution: [architecture.md, style-guide.md]
```

Sections, in order:
1. Purpose: one or two lines.
2. Contract: inputs (required or optional, defaults), output, exports. Typed, not implemented.
3. Dependencies: imports and external state, linked to other specs by path.
4. State: declared variables and initial values.
5. Structure: nesting skeleton. UI: element tree with `(owns: ...)` for spacing. Logic: function list with signatures.
6. Behavior: numbered pseudo-code steps.
7. Errors and edge cases: table of condition and handling. Grilling output lands here.
8. Constraints: scalability and style rules.
9. Out of scope: what the file must not do, to stop subagents over-building.

## Pseudo-code dialect
Fixed vocabulary: `on`, `if`, `for each`, `call`, `emit`, `return`, `set`, `abort`. No language syntax (`await`, `.then`). Consistency lets build subagents read specs reliably. Dialect is defined in `.spec/constitution/dialect.md`.

Example fragment:
```
on query change:
  1. if length(query) < minChars: results = [], status = "idle", return
  2. start timer(delayMs)
  3. on timer fire: abort previous, call searchApi.search(query, signal)
```

UI structure fragment:
```
Card            (owns: p-4, gap-3, flex-col)
  Header        (owns: flex row, justify-between)
  Body          (owns: flex-1)
rule: children never set their own outer margin
```

## Rules learned
- Spec wins when spec and code disagree; a later sync step flags drift.
- `depends_on` in frontmatter lets build find parallel work without reading every spec.
- `status` lets a build run skip finished files.
- Behavior as numbered steps plus a case table is easy to verify against built code.

## Open questions
- One strict section set for every file type, or variants for component, hook, util, api?
- Should Structure for UI be mandatory only for components?
