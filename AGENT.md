# AGENT.md — AI Engineer Note Vault

> Read this file at the start of every new conversation before doing anything else.
> This is the single source of truth for the project structure, conventions, and current state.

---

## What This Project Is

A personal learning vault for the **CampusX (Nitish Singh) AI Engineer roadmap** — a 1+ year structured path from Python fundamentals through to Agentic AI and LLM production systems. Each video gets two notes: a **long deep-dive note** and a **short recall card**. Notes are written in Markdown, stored in a Git repo, and cross-linked to prevent siloed knowledge.

**Repo:** `https://github.com/Wajid16/ai-engineer-vault.git`
**Local root:** `c:\Users\Me\Documents\AI-Engineer-Vault\`
**Branch:** `main` — commit and push after every session.

---

## How a Note Session Works

### Where to find the inputs

- **Transcript** → `_inbox/transcript.md` — the user pastes the raw YouTube auto-generated transcript here. **After writing the notes, clear this file** (leave only the header comment, no transcript text).
- **Diagrams** → `_inbox/diagrams/` — the user drops image files here. **After embedding each image in the long note, delete the source file** from this folder. Do not leave images behind after use.
- **Video link** — always provided in the user's chat message (it's not in the transcript). You **always need the video link** — if the user hasn't provided one, ask before proceeding.
- **Video title / session name** — provided in the user's chat message.
- **Course name** — provided in the user's chat message.

### Handling YouTube auto-captions

YouTube auto-captions have **no punctuation and no paragraph breaks** — they're a wall of run-on text. When reading them:
- Don't try to correct grammar. Read for meaning and topic coverage.
- Ignore filler words ("uh", "um", "you know", "right") and repeated phrases.
- Use the structure of the *topic* (not the structure of the captions) to organize the note sections.
- If a section of captions is unclear, use your knowledge of the topic to fill in what was likely being explained, and note it as "inferred from context" if genuinely uncertain.

### What you produce
For each video session:

1. **Long note** → `<course>/notes/NN-slug.md` — deep, unlimited depth, covers **everything** the instructor discussed (why, what, how, examples, analogies, interview angles, code). Use [`templates/long-note-template.md`](templates/long-note-template.md).
2. **Short note** → Append a section to `<course>/notes/quick-recall.md` — quick overview card: a standalone card for 60-second refresher. Use [`templates/short-note-template.md`](templates/short-note-template.md).
3. **Update** `<course>/README.md` — add the new session to the progress table (linking to the long note and the section anchor in `notes/quick-recall.md`).
4. **Update** `_meta/glossary.md` — if the video introduced a concept that will recur in other courses, add it here (one entry per term, cross-linked back to the note where it first appeared). Only cross-cutting concepts — not course-specific details.
5. **Update the Course Status table** in this file (`AGENT.md`) — increment the note count for the course.
6. **Clean the inbox** — clear `_inbox/transcript.md` (restore to header-only state) and delete any diagram files from `_inbox/diagrams/` that were used.
7. **Commit and push** to `origin main`.

### New Course Setup
When the user starts a new course, they will provide a topic outline in the conversation. The agent must:
1. Create the new course directory under the correct phase folder (e.g. `03-ai-engineer/langchain/` or `04-deployment/fastapi/`).
2. Create the course's `README.md` file and paste the provided outline there.
3. Create the initial `notes/quick-recall.md` file, starting with `# <Course Name> — Quick Recall` as the main header.
4. Update the course status tables in `AGENT.md` and `README.md` (root).
5. Use this course-specific `README.md` outline during the course to track what has been covered so far and what is left.

### Numbering
Notes are numbered in **watch order** within each course: `01`, `02`, `03`, ... Each note section inside `notes/quick-recall.md` uses the same number/header for easy linking.

---

## File Naming

```
<course>/notes/01-short-descriptive-slug.md          ← long note
<course>/notes/quick-recall.md                       ← combined quick recall cards (single file)
<course>/assets/01-description-of-diagram.png        ← embedded image
<course>/README.md                                   ← course progress table
```

All slugs: lowercase, hyphens only, no spaces, max ~5 words.

---

## Assets Convention

When diagrams are present in `_inbox/diagrams/`:
- Copy/move each image to `<course>/assets/<session-number>-<brief-description>.<ext>`
- In the long note, reference as: `![Diagram: brief description](../assets/01-description.png)`
- Always write a caption sentence below the image explaining **what it shows and why it matters**.
- **Delete the original** from `_inbox/diagrams/` after embedding — this folder is a staging area, not storage.

---

## Outdated Content Flagging

When you identify something in the transcript that is deprecated, superseded, or no longer best practice, add an inline callout in the long note under a `## ⚠️ Outdated Flags` section:

```markdown
> ⚠️ **[OUTDATED]** The tutor uses `openai.ChatCompletion.create()` — deprecated in `openai>=1.0.0`.
> **Use instead:** `client.chat.completions.create()` with the new `openai` client object.
```

Flag sparingly — only when something would actively mislead someone following the note today. Don't flag style choices or minor API name changes that still work.

---

## Cross-Linking Rules

- **Keep notes self-contained.** Do NOT link topics or notes from one course to notes in another course (e.g., do not link a LangGraph note to an MCP or LLM Evals note).
- **Within-course links:** You can link to other notes *within the same course* (e.g., `[note 03](../notes/03-langchain-vs-langgraph.md)`) if they directly build on each other.
- **Glossary linking:** You can link to the global glossary in `_meta/glossary.md` for shared, cross-cutting technical concepts (e.g., `[structured output](../../_meta/glossary.md#structured-output)`). Do not link directly between different courses.

---

## Current Course Status

| Course | Folder | Status | Long Notes | Short Notes |
|---|---|---|---|---|
| Python for AI Engineering (CampusX) | `00-prerequisites/python/` | 🟡 In progress | 4 | 4 |
| LLM Evals (CampusX) | `03-ai-engineer/llm-evals/` | 🟡 In progress | 4 | 0 |
| RAG (CampusX) | `03-ai-engineer/rag/` | ⚪ Not started | 0 | 0 |
| MCP (CampusX) | `03-ai-engineer/mcp/` | 🟡 In progress | 2 | 0 |
| LangGraph (CampusX) | `03-ai-engineer/langgraph/` | 🟡 In progress | 14 | 0 |
| LangChain (CampusX) | `03-ai-engineer/langchain/` | ⚪ Not started | 0 | 0 |
| FastAPI (CampusX) | `04-deployment/fastapi/` | 🟡 In progress | 4 | 4 |
| Docker (CampusX) | `04-deployment/docker/` | 🟡 In progress | 1 | 0 |
| Pydantic (CampusX) | `04-deployment/pydantic/` | ⚪ Not started | 0 | 0 |
| n8n | `03-ai-engineer/n8n/` | ⚪ Not started | 0 | 0 |

> Update this table after every session. When a course is fully complete, mark it ✅.

---

## AI Engineer Roadmap — Phase Overview

This is the full learning path. Track per-topic progress inside each course's own `README.md`.

| Phase | Topic Area | Courses | Status |
|---|---|---|---|
| 0 | **Python Foundations** | Python for AI Engineering | 🟡 In progress |
| 1 | **Maths for ML** | Linear Algebra, Calculus, Probability & Stats | ⚪ Not started |
| 2 | **Machine Learning** | 100 Days of ML | ⚪ Not started |
| 3 | **Deep Learning & NLP** | DL fundamentals, Transformers, NLP | ⚪ Not started |
| 4 | **Tooling & Infrastructure** | FastAPI, Docker, Pydantic | 🟡 In progress |
| 5 | **LLM Ecosystem** | LangChain, RAG | ⚪ Not started |
| 6 | **Agentic AI** | LangGraph, MCP | 🟡 In progress |
| 7 | **Evaluation & Production** | LLM Evals | 🟡 In progress |
| 8 | **Automation** | n8n | ⚪ Not started |

Note: Some Phase 5–7 courses were started before finishing Phase 0–4. That's fine — the roadmap is a guide, not a constraint.

---

## Ground Rules for Notes

1. **Long note = unlimited depth.** Cover every sub-topic the instructor discussed: why, what, how, analogies, code examples, interview angles. If the instructor used an analogy or example, include it — those are the most memorable parts.
2. **Short note = quick overview.** Key terms, key takeaways, one-liners, appended as a section to `<course>/notes/quick-recall.md`. Not a summary of the long note — a standalone card the user reads when they want a 60-second refresher.
3. **"Added Context" is allowed** in the long note — if something the instructor said is outdated or there's a clearly better modern approach, note it under `## Added Context`. Don't editorialize heavily; keep it factual.
4. **Code examples must run.** If the instructor showed code, include it exactly (or corrected if it's broken by a deprecated API). Add a comment if you've corrected something.
5. **Interview angles are not optional.** For every technical concept, ask: "How would an interviewer probe this?" Include the likely question and the answer.
6. **Practice questions at the end** of every long note — 3–5 exercises or questions the reader can't answer from memory alone.

---

## Key Files & Folders

| Path | Purpose |
|---|---|
| `AGENT.md` *(this file)* | Agent context — read first every conversation |
| `README.md` | Human-facing project overview + course table |
| `_inbox/transcript.md` | Paste YT transcript here — agent clears after use |
| `_inbox/diagrams/` | Drop diagram images here — agent deletes after embedding |
| `_meta/glossary.md` | Shared cross-course concept dictionary |
| `_meta/workflow.md` | Human-readable process description |
| `templates/long-note-template.md` | Template for deep-dive notes |
| `templates/short-note-template.md` | Section block template appended to quick-recall.md |
