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

### Frontmatter limits

- `name`: max 64 chars; lowercase letters, numbers, hyphens only; no XML tags; must not contain `anthropic` or `claude`.
- `description`: non-empty, max 1,024 chars, no XML tags.
- Prefer gerund names (`processing-pdfs`); noun phrases (`pdf-processing`) or verb phrases (`process-pdfs`) are acceptable. Avoid vague names (`helper`, `utils`, `tools`) and stay consistent across the repo.

### Writing the description

The description is the trigger condition: the agent chooses among potentially 100+ skills using only `name` and `description`.

- State both what the skill does and when to use it ("Use when ...").
- Write in third person ("Extracts text from PDFs"), never "I can ..." or "You can ...". The description is injected into the system prompt.
- Include concrete trigger terms users would say: file types, tool names, task phrases, symptoms.
- Be specific. Bad: `Helps with documents`, `Processes data`. Good: `Extract text and tables from PDF files, fill forms, merge documents. Use when working with PDF files or when the user mentions PDFs, forms, or document extraction.`
- Put all "when to use" info in the description, not the body; the body only loads after the skill triggers.

### Body and structure

- Be concise: only add context the agent does not already have. Challenge every paragraph's token cost.
- Keep the `SKILL.md` body under 500 lines; split into sibling files (progressive disclosure) as it approaches that.
- Link reference files directly from `SKILL.md`, one level deep only; never chain reference -> reference.
- Reference files over 100 lines start with a table of contents.
- Name files descriptively (`form_validation_rules.md`, not `doc2.md`); group by domain (`reference/finance.md`).
- Use forward slashes in all paths.
- Match specificity to fragility: loose guidance where many approaches work, exact commands where an operation is fragile or order-sensitive.
- Give one default approach with an escape hatch, not a menu of options.
- Use one term per concept throughout the skill.
- No time-sensitive info ("before Aug 2025 ..."); put legacy material in an "old patterns" section.
- For multi-step tasks, give numbered steps (or a copyable checklist) and a validate -> fix -> repeat loop for quality-critical steps.
- Show output templates and concrete input/output examples when format matters.
- Scripts: state whether to run or read them, handle errors explicitly rather than deferring to the agent, justify any constants, and list required packages.
- Reference MCP tools by fully qualified name (`ServerName:tool_name`).

### Verification

- Define at least three realistic test scenarios before writing extensive docs; write the minimum content that fixes observed gaps.
- Test with small, mid, and large models (Haiku, Sonnet, Opus) and iterate on observed behavior.
- Check that the skill triggers on intended prompts and not on unrelated ones.

Source: https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices

## Workflow

- One skill per commit; scope is the skill name, e.g. `feat(my-skill): add skill`.
- After adding or renaming a skill, update the skill list in `README.md` if one exists.
- Verify discovery with `npx skills add . --list` before pushing.
