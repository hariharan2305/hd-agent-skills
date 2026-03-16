---
name: learning-insights
description: "Use when the user says /capture-insight, /polish-insight, 'capture this insight', 'save this insight', 'polish this insight', 'create linkedin post', 'turn this into a post', 'this is a good insight', or wants to save a learning moment or convert a saved insight into LinkedIn posts. Triggers on any mention of capturing learnings, saving aha moments, or generating content from past learning sessions."
---

# Learning Insights

Capture raw learning insights from conversations and polish them into LinkedIn posts that sound like the user, not like AI.

Two commands:
- `/capture-insight <intent>` — save a raw insight card from the current conversation
- `/polish-insight <filename>` — append LinkedIn post variations to an existing raw insight card

All insights are stored in `~/Documents/projects/learning-insights/` (a fixed location, independent of which project you're working in). Insights are organized into project subdirectories based on which project the conversation was happening in.

---

## Directory Structure

```
~/Documents/projects/learning-insights/
├── INDEX.md                              (global index across all projects)
├── resources/
│   └── voice_samples.md                 (user's actual published LinkedIn posts)
├── ai_engineering/
│   ├── 2026-03-16_recursive-vs-semantic-chunking.md
│   └── ...
├── some_other_project/
│   └── ...
```

**Project detection:** Determine the project name from the current working directory's git repo root folder name. If not in a git repo, use the current directory name. Use this as the subdirectory name under `~/Documents/projects/learning-insights/`.

**Auto-creation:** If `~/Documents/projects/learning-insights/`, the project subdirectory, or `~/Documents/projects/learning-insights/resources/` don't exist, create them automatically.

---

# /capture-insight

Extract a raw learning insight from the current conversation and save it as a structured markdown file.

This is a **capture tool, not a content generator**. The goal is to preserve the authentic learning journey — the confusion, the questions, the moment it clicked — so it can later be polished into a LinkedIn post.

## Invocation

`/capture-insight <intent describing what to capture>`

**Example:** `/capture-insight the part about why recursive chunking beats semantic chunking on small corpora`

The intent scopes which part of the conversation to focus on. Ignore everything unrelated to the intent.

## Process

### 1. Parse the intent and find the relevant conversation turns

Read the user's intent. Scan the conversation for exchanges that match — the user's clarifying questions, their confusion points, and the AI responses that resolved them. Skip conversation turns unrelated to the intent.

### 2. Extract the raw insight

From the relevant turns, extract:

**Topic:** A clear, specific topic label. Not vague — "Why recursive chunking outperforms semantic on small corpora" not "chunking stuff".

**The Struggle:** What was the user confused about or trying to understand? What didn't click initially? Use their actual words and phrasing. This section is the most important — it's what makes the insight relatable to others.

**The Drill-Down:** The specific clarifying questions the user asked, written as a progression. The sequence matters — it shows the thinking process from surface-level to deep understanding. Write in first person as if the user is telling the story.

**The Aha Moment:** The specific explanation or framing that made it click. What was the key mental model shift? What analogy or reframing resolved the confusion? Keep it at the same complexity level the user was engaging at — don't simplify or sophisticate.

**The One-Liner:** Distill into a single punchy sentence. This seeds the LinkedIn hook later. Write it in the user's voice, not polished marketing speak.

### 3. Preserve the user's voice

When writing the raw card:
- Use the same vocabulary the user used (if they said "beats" don't write "outperforms")
- Match their sentence complexity — short direct sentences stay short and direct
- Keep their analogies and metaphors
- If they used casual language ("this is wild", "wait so basically..."), keep that energy
- Do NOT clean up or formalize their language — rawness is the point

### 4. Detect project and create file

- Determine the project name from the current working directory (git repo root folder name, or current dir name if not in a git repo)
- Create `~/Documents/projects/learning-insights/<project_name>/` if it doesn't exist
- Create `~/Documents/projects/learning-insights/resources/` if it doesn't exist

**Filename:** `YYYY-MM-DD_<slug>.md` where slug is a short kebab-case version of the topic (max 5 words).

**Example:** `~/Documents/projects/learning-insights/ai_engineering/2026-03-16_recursive-vs-semantic-chunking.md`

### 5. Write the file

```markdown
# <Topic>

**Date:** YYYY-MM-DD
**Project:** <project_name>
**Status:** raw
**Context:** <1-line description of what the user was working on when this insight came up>

---

## The Struggle

<What the user was confused about, in their own words and phrasing. 2-4 sentences.>

## The Drill-Down

<The sequence of clarifying questions, written as a natural progression. Not a Q&A transcript — more like "First I wondered X. Then when I heard Y, I pushed further on Z." First person, user's voice.>

## The Aha Moment

<The explanation or framing that made it click. Concrete, not abstract. Written at the complexity level of the conversation.>

## The One-Liner

> <Single punchy sentence capturing the core insight. User's voice.>

---

*Raw insight captured from conversation. Run /polish-insight to generate LinkedIn post variations.*
```

### 6. Update the global index

Create or update `~/Documents/projects/learning-insights/INDEX.md`. Append a new row. If the file doesn't exist, create it with the header. Newest entries first.

```markdown
# Learning Insights Index

| Date | Project | Topic | Status | File |
|------|---------|-------|--------|------|
| YYYY-MM-DD | project_name | Topic name | raw | [filename](<project_name>/filename) |
```

## Rules

- NEVER fabricate or embellish. If the user didn't express confusion, don't invent a struggle.
- NEVER add technical details that weren't in the conversation.
- If the intent is ambiguous or no clear insight matches it, ask the user to clarify.
- One insight per file. Multiple insights = multiple invocations.
- Keep the raw card under 400 words. If it needs more, it's probably two insights.

---

# /polish-insight

Take a raw insight card and append polished LinkedIn post variations to the **same file**. The posts must sound like the user — this is the hard part and the whole point.

## Invocation

`/polish-insight <filename or path>`

**Examples:**
- `/polish-insight 2026-03-16_recursive-vs-semantic-chunking.md`
- `/polish-insight ai_engineering/2026-03-16_recursive-vs-semantic-chunking.md`

If just a filename is given, search across all project subdirectories in `~/Documents/projects/learning-insights/`. If ambiguous (same filename in multiple projects), ask the user to specify.

## Process

### 1. Read the raw insight card

Read the file. Check if it already has a "## LinkedIn Post Variations" section. If yes, ask the user if they want to regenerate.

### 2. Study the user's voice

Read `~/Documents/projects/learning-insights/resources/voice_samples.md`.

**If voice samples exist (5+ posts):**
- Analyze: sentence length, vocabulary level, use of questions, paragraph breaks, emoji usage (or absence), how they open posts, how they close posts
- Note their formality level, first person usage, bullet points vs flowing text
- Pay attention to what they DON'T do — no emojis means no emojis, no "Let me explain..." means never use that
- Mirror their patterns confidently

**If fewer than 5 samples or none:**
- Fall back on the user's voice as captured in the raw card (Struggle and Drill-Down sections)
- Keep vocabulary simple and direct
- Avoid LinkedIn AI cliches: "Here's the thing", "Let me break this down", "Game-changer", "Unpopular opinion", "I was today years old", "Stop.", "Read that again."
- Default to short sentences, conversational tone

### 3. Generate 2-3 post variations

Each post MUST:
- Stay under 3000 characters (LinkedIn text post limit)
- Have a strong hook in the first 1-2 lines (visible before "...see more")
- Use line breaks generously — LinkedIn is mobile-first, walls of text get scrolled past
- Sound like a human sharing a genuine learning, not a thought leader performing expertise

**Available formats (pick 2-3 that fit the insight):**

**Narrative / Story:**
Hook (the surprising thing) → Context/situation → What you assumed → What's actually true → Why it matters → Takeaway

**Interview Q&A:**
A realistic interview question → Why it's tricky → The answer explained clearly → What this reveals about the concept → The deeper understanding

**System / Technical breakdown:**
Hook (counterintuitive claim) → Problem setup → How it actually works → The non-obvious detail → Practical implication

**Myth-buster:**
Common belief → Why everyone thinks this → What actually happens → Evidence/experience → Corrected mental model

Do NOT force every insight into every format. If only 2 formats work, do 2.

### 4. Append to the same file

Add below the existing raw content. Do NOT modify the raw section.

```markdown

---

## LinkedIn Post Variations

**Polished on:** YYYY-MM-DD
**Voice samples used:** <number of samples available, or "none">

### Variation 1: <format name>

<the actual post content, ready to copy-paste>

---

### Variation 2: <format name>

<the actual post content, ready to copy-paste>

---

### Variation 3: <format name> (if applicable)

<the actual post content, ready to copy-paste>
```

### 5. Update the index

Change Status from `raw` to `polished` for this file's row in `~/Documents/projects/learning-insights/INDEX.md`.

## Voice Matching Rules (non-negotiable)

1. **No vocabulary inflation.** Match the user's reading level. "Use" not "utilize". "Start" not "commence". "Show" not "demonstrate".

2. **No LinkedIn cringe.** Never: one-word-sentence hooks ("Stop."), fake vulnerability, humble-bragging, "agree?", excessive emoji, hashtag walls, tagging random people, "Let that sink in", "Read that again".

3. **Match energy, not just words.** Excited raw insight = excited post. Measured raw insight = measured post.

4. **Genuine hooks only.** First line creates curiosity through: a surprising fact, a counterintuitive claim you can back up, or a question the reader can't immediately answer. Not through clickbait.

5. **End with value, not engagement bait.** Close with the actual takeaway or a thought-provoking implication. Not "What do you think?" or "Drop a comment below."

## Rules

- NEVER add technical claims not in the raw insight. Posts are based on what the user actually learned.
- NEVER make the user sound more expert than the raw card suggests. Learning energy, not retrospective authority.
- If the raw insight is thin (vague struggle, weak aha moment), tell the user the card needs more substance before polishing.
- No placeholder text, no "[insert your experience here]". Everything must be complete and ready to copy-paste.
