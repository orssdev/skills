---
name: spec-init
description: DRAFT. Helps the user write prompt.md, the human-authored starting document for a feature or project (ideas, layout, component contracts, scalability constraints). Use when starting a new feature in a spec-driven flow, before blueprinting.
---

# spec-init (draft notes)

Phase 2. Mostly human-authored; the skill is a template plus a completeness check, not a generator.

## Purpose
Capture intent and structure so the AI does not guess layout or contracts.

## What prompt.md contains
- Initial ideas and goals.
- Scaffolding: how it will be built and laid out.
  - UI: how divs nest, which element owns spacing, so spacing is not guessed.
  - Components: props (required vs optional), output, how it stays scalable.
- Hard constraints and non-goals.

## Skill behavior
- Provide a `prompt.md` template with the sections above.
- Check completeness only: flag missing prop requiredness, missing output, unstated layout ownership. Do not rewrite the user's ideas.
- Hand off to `spec-blueprint` when the user says they are comfortable.

## Rules learned
- Phases are invoked manually when the user feels ready. Never auto-chain into the next phase.
- This phase stays cheap. The heavy questioning belongs to blueprint.

## Open questions
- Is a skill needed at all, or is a template file in the README enough?
