# Plan Mode: Learning Project

You are now in **PLANNING MODE ONLY**. Do not write any code. Do not implement anything.
Your sole job is to produce a structured plan for a hands-on learning project.

**Concept / Topic being learned:** $ARGUMENTS

---

## Hard Rules (Non-Negotiable)

- **No code blocks** — not even illustrative ones. Not a single line of code.
- **Max 500 lines** for the plan output.
- **Do not create a plan file** unless I explicitly say "save this to a file."
- **Scope is ruthlessly constrained** to the concept in `$ARGUMENTS`. If something doesn't directly exercise that concept, it goes in the exclusions list.
- The goal of this project is **learning through building**, not shipping a product. Simplicity over completeness.
- If the concept boundary is ambiguous, ask before planning.

---

## Output Structure

Produce the plan in exactly this order:

### 1. Learning Goal
One short paragraph. What specific understanding or skill should exist after this project is done? What does mastery of `$ARGUMENTS` look like in practice?

### 2. Project Idea
One short paragraph describing the minimal project that best exercises the concept. Should be simple enough to finish in a focused session, complex enough to surface real nuances of the concept.

### 3. What This Project Intentionally Excludes
Critical section. List everything that is deliberately out of scope to keep focus sharp.

- No authentication (unless auth IS the concept)
- No production error handling beyond basics
- No deployment
- [add concept-specific exclusions]

This list prevents scope creep and keeps the learning signal clean.

### 4. Concept Coverage Map
Map the key sub-topics of `$ARGUMENTS` to the parts of the project that exercise them.

| Sub-concept | Where it gets exercised |
|---|---|
| e.g. streaming responses | e.g. chat endpoint handler |

This ensures the project actually covers what it claims to teach.

### 5. Component Inventory
Minimal list of files/modules needed. Every component must justify its existence by exercising the concept.

- `path/to/file.ext` — [new] — what it does and which sub-concept it exercises

### 6. Data Contracts
Only what's needed. Tables or bullets only, no code.

### 7. Build Sequence
Numbered list ordered for maximum learning — earlier steps should build foundational understanding that later steps depend on.

1. ...
2. ...

### 8. Stretch Goals (Optional)
Things to add only after the core concept is working and understood. Clearly separated from the main build.

- Stretch: ...

### 9. Key Concepts to Observe While Building
Bullet list of things to pay attention to, experiment with, or intentionally break to deepen understanding. This is the learning-specific section that makes this command different from plan-new.

- e.g. "Observe how context window fills up — intentionally exceed it and see what happens"
- e.g. "Try switching between streaming and non-streaming to feel the UX difference"

### 10. Assumptions & Open Questions
**Assumptions made:**
- bullet list

**Open questions:**
- bullet list
