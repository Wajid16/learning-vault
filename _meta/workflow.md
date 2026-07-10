# How notes get made

This repo is a learning vault — the goal is active recall 6 months later, not archiving transcripts. Each video session produces two notes: a **long deep-dive** and a **short cheat-sheet**.

> **For the AI agent:** Read [`AGENT.md`](../AGENT.md) first — it has everything needed (context, current status, conventions, naming rules). This file is for the human.

---

## The Loop (per video session)

1. **Watch the video.** You don't need to take notes if you're providing the transcript.

2. **Hand it to the agent.** Provide:
   - The video **transcript** (paste as text — YouTube auto-captions work fine)
   - The **video link** (YouTube URL)
   - The **video title / session name**
   - The **course name** (must match an existing folder, or say it's new)
   - Any **diagram images** the instructor drew or showed on screen (attach the files)

3. **The agent produces:**
   - **Long note** → `<course>/notes/NN-slug.md` — deep coverage of everything discussed
   - **Short note** → `<course>/notes/NN-slug-short.md` — cheat-sheet / quick-reference
   - **Updated** `<course>/README.md` (new row in the progress table)
   - **Updated** `ROADMAP.md` (any newly covered items ticked off)
   - **Updated** `_meta/glossary.md` (if a new cross-course term was introduced)
   - **Git commit + push** to `origin main`

4. **You review.** Correct anything the agent misunderstood (the transcript + links are the source of truth, not the agent's prior knowledge). Push a fixup commit if needed.

---

## Ground Rules

### Long note
- **Unlimited depth.** Cover every topic the instructor discussed: why it exists, what it is, how it works, the instructor's analogies and examples (these are the most memorable parts), code, and interview angles.
- One `##` section per major topic block the instructor covered.
- Include **practice questions** at the end — things the reader can't answer from memory alone.
- If the instructor's content is outdated/deprecated, flag it under `## ⚠️ Outdated Flags` with the current correct approach.
- Template: [`templates/long-note-template.md`](../templates/long-note-template.md)

### Short note
- **Standalone cheat-sheet.** Someone should be able to skim it in 60 seconds and remember what the video was about.
- Key terms, one-liner definitions, 3–7 bullet points of what matters most.
- Not a summary of the long note — a complementary quick-reference.
- Template: [`templates/short-note-template.md`](../templates/short-note-template.md)

### Cross-linking
- **Link, don't repeat.** If a concept was explained in a previous note, link to it.
- Cross-course concepts → define in `_meta/glossary.md`, link from every note that uses it.

### Diagrams
- Save to `<course>/assets/<NN>-<description>.<ext>`
- Reference as `![Diagram: description](../assets/NN-description.png)` in the long note.
- Always write a caption: what the diagram shows and why it matters.

---

## File Naming

```
<course>/notes/01-short-descriptive-slug.md          ← long note
<course>/notes/01-short-descriptive-slug-short.md    ← short recall card
<course>/assets/01-description-of-diagram.png        ← diagram image
<course>/README.md                                   ← course progress table
```

Notes numbered in **watch order** within each course.
