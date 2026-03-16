# Plan Mode: New Product / Feature Build

You are now in **PLANNING MODE ONLY**. Do not write any code. Do not implement anything.
Your sole job is to produce a structured plan based on the context already in this conversation.

---

## Hard Rules (Non-Negotiable)

- **No code blocks** — not even illustrative ones. Not a single line of code.
- **No prose-wrapped code** — do not write logic disguised as English ("it will iterate through the list and call..."). Keep it architectural.
- **Max 500 lines** for the plan output.
- **Do not create a plan file** unless I explicitly say "save this to a file."
- **Do not re-derive context** that is already established in this conversation. Use it directly.
- If something is unclear, ask before planning — do not assume and bury the assumption silently.

---

## Output Structure

Produce the plan in exactly this order:

### 1. Goal & Success Condition
One short paragraph. What are we building and what does "done" look like?

### 2. Scope
**In scope:**
- bullet list

**Out of scope (v1):**
- bullet list

### 3. Tech Stack Decisions
| Concern | Choice | Rationale |
|---|---|---|
| e.g. Auth | e.g. JWT | e.g. stateless, no session store needed |

Only include decisions that were explicitly discussed or are non-obvious. Do not list the entire stack.

### 4. Component Inventory
List every file/module that needs to be **created or modified**. One line per component.

Format:
- `path/to/file.ext` — [new/modify] — one-line description of its responsibility

### 5. Data Contracts
Define what data flows between components. Use tables or bullet points only. No code.

For each contract:
- **Name** of the data object
- **Fields**: name, type, short description
- **Direction**: which component produces it, which consumes it

### 6. API Surface (if applicable)
| Method | Endpoint | Request | Response |
|---|---|---|---|

Keep field descriptions as plain types — no code, no JSON blocks.

### 7. Build Sequence
Numbered list. Each step = one logical unit of work the agent can execute independently.

1. ...
2. ...

Dependencies must be respected — nothing should appear before what it depends on.

### 8. Phase Breakdown
**MVP (ship this first):**
- bullet list of what's in MVP

**Post-MVP / v2:**
- bullet list of what's intentionally deferred

### 9. Key Decisions Log
Bullet list of architectural decisions made and why. This is the most important section for future reference.

- Decision: [what was decided] — Reason: [why]

### 10. Assumptions & Open Questions
**Assumptions made:**
- bullet list

**Open questions (unresolved):**
- bullet list — flag anything that needs a decision before building starts
