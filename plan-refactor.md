# Plan Mode: Refactor

You are now in **PLANNING MODE ONLY**. Do not write any code. Do not implement anything.
Your sole job is to produce a structured refactor plan based on the context already in this conversation.

---

## Hard Rules (Non-Negotiable)

- **No code blocks** — not even illustrative ones. Not a single line of code.
- **No prose-wrapped code** — do not describe logic step by step. Keep it structural.
- **Max 500 lines** for the plan output.
- **Do not create a plan file** unless I explicitly say "save this to a file."
- **Do not re-derive context** already established in this conversation. Use it directly.
- If the refactor boundary is unclear, ask before planning — do not guess scope.

---

## Output Structure

Produce the plan in exactly this order:

### 1. Refactor Goal
One short paragraph. What problem does this refactor solve? What does the codebase look like after this is done?

### 2. Scope
**In scope:**
- bullet list

**Out of scope:**
- bullet list — be explicit about what is NOT changing to prevent scope creep

### 3. Before → After Map
The most important section. Show structural change clearly.

**Before:**
- `path/to/file.ext` — current responsibility

**After:**
- `path/to/file.ext` — new responsibility (modified/deleted)
- `path/to/new-file.ext` — new file, responsibility

Use [new], [modify], [delete], [rename], [split], [merge] tags per file.

### 4. Contract Changes
List only what is changing externally — APIs, schemas, interfaces, event signatures.

| Contract | Change Type | Before | After |
|---|---|---|---|

If nothing changes externally, state: "No external contract changes."

### 5. Import / Dependency Updates
List files that import from changed modules and will need updates.

- `path/to/consumer.ext` — update import from X to Y

### 6. Database / Schema Changes (if applicable)
Plain description only — no SQL, no migration code.

- Table X: add column Y (type, nullable/not)
- Table Z: rename column A to B

### 7. Execution Sequence
Numbered list. Order matters — define a sequence that keeps the system working at each step (strangler fig pattern where possible).

1. ...
2. ...

Flag any step that temporarily breaks things and what the recovery path is.

### 8. Risk & Rollback
- **Risks**: What could go wrong during this refactor?
- **Rollback plan**: How do we revert if something breaks in production?

### 9. Key Decisions Log
- Decision: [what was decided] — Reason: [why]

### 10. Assumptions & Open Questions
**Assumptions made:**
- bullet list

**Open questions:**
- bullet list
