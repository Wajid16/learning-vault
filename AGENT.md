# AGENT.md — AI Engineer Note Vault

> Read this file at the start of every new conversation before doing anything else.
> This is the single source of truth for the project structure, conventions, and current state.

---

## What This Project Is

A personal learning vault for the **CampusX (Nitish Singh) AI Engineer roadmap** — a 1+ year structured path from Python fundamentals through to Agentic AI and LLM production systems. Each video gets two notes: a **long deep-dive note** and a **short recall card**. Notes are written in Markdown, stored in a Git repo, and cross-linked to prevent siloed knowledge.

**Repo:** `https://github.com/Wajid16/learning-vault.git`
**Local root:** `c:\Users\Me\Documents\course-notes\`
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
2. **Short note** → `<course>/notes/NN-slug-short.md` — quick overview card: the user reads this when they want a fast refresher without opening the long note. Use [`templates/short-note-template.md`](templates/short-note-template.md).
3. **Update** `<course>/README.md` — add the new session to the progress table (both notes, with links).
4. **Update** `ROADMAP.md` — tick off any roadmap items that were covered in this session.
5. **Update** `_meta/glossary.md` — if the video introduced a concept that will recur in other courses, add it here (one entry per term, cross-linked back to the note where it first appeared). Don't add course-specific implementation details — only cross-cutting concepts.
6. **Clean the inbox** — clear `_inbox/transcript.md` (restore to header-only state) and delete any diagram files from `_inbox/diagrams/` that were used.
7. **Commit and push** to `origin main`.

### Numbering
Notes are numbered in **watch order** within each course: `01`, `02`, `03`, ... Short notes get the same number with a `-short` suffix: `01-slug-short.md`.

---

## File Naming

```
<course>/notes/01-short-descriptive-slug.md          ← long note
<course>/notes/01-short-descriptive-slug-short.md    ← short recall card
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

- **Don't repeat, link.** If a concept was explained in a previous note or in the glossary, link to it — don't re-explain it.
- **Glossary first.** If a term crosses course boundaries (e.g., "structured output", "checkpointing", "embeddings"), define it in `_meta/glossary.md` and link from every note that uses it.
- **Within-course links:** use relative paths, e.g., `[note 03](../notes/03-langchain-vs-langgraph.md)`.
- **Cross-course links:** use relative paths from the repo root, e.g., `[glossary entry](../../_meta/glossary.md#term)`.

---

## Current Course Status

| Course | Folder | Status | Long Notes | Short Notes |
|---|---|---|---|---|
| Python Core (CampusX) | `python/` | 🟡 In progress | 1 | 0 |
| LLM Evals (CampusX) | `llm-evals/` | 🟡 In progress | 4 | 0 |
| RAG (CampusX) | `rag/` | ⚪ Not started | 0 | 0 |
| MCP (CampusX) | `mcp/` | 🟡 In progress | 2 | 0 |
| LangGraph (CampusX) | `langgraph/` | 🟡 In progress | 14 | 0 |
| LangChain (CampusX) | `langchain/` | ⚪ Not started | 0 | 0 |
| FastAPI (CampusX) | `fastapi/` | ⚪ Not started | 0 | 0 |
| Docker (CampusX) | `docker/` | 🟡 In progress | 1 | 0 |
| Pydantic (CampusX) | `pydantic/` | ⚪ Not started | 0 | 0 |
| n8n | `n8n/` | ⚪ Not started | 0 | 0 |
| Scientific Writing | `non-technical/scientific-writing/` | 🟡 In progress | 5 | 0 |
| IELTS | `non-technical/ielts/` | ⚪ Not started | 0 | 0 |
| English | `non-technical/english/` | 🟡 In progress | 2 | 0 |
| Freelancing | `non-technical/freelancing/` | ⚪ Not started | 0 | 0 |

> Update this table after every session. When a course is fully complete, mark it ✅.

---

## Full AI Engineer Roadmap

The roadmap is tracked in detail in [`ROADMAP.md`](ROADMAP.md). High-level phase overview:

| Phase | Topic Area | Courses |
|---|---|---|
| 0 | **Python Foundations** | Python Core |
| 1 | **Maths for ML** | Linear Algebra, Calculus, Probability & Stats |
| 2 | **Machine Learning** | 100 Days of ML |
| 3 | **Deep Learning & NLP** | DL fundamentals, Transformers, NLP |
| 4 | **Tooling & Infrastructure** | FastAPI, Docker, Pydantic |
| 5 | **LLM Ecosystem** | LangChain, RAG |
| 6 | **Agentic AI** | LangGraph, MCP |
| 7 | **Evaluation & Production** | LLM Evals, MLOps basics |
| 8 | **Automation** | n8n |

Note: You started some Phase 5–7 courses before finishing Phase 0–4. That's fine — the roadmap is a guide, not a hard constraint.

---

## Ground Rules for Notes

1. **Long note = unlimited depth.** Cover every sub-topic the instructor discussed: why, what, how, analogies, code examples, interview angles. If the instructor used an analogy or example, include it — those are the most memorable parts.
2. **Short note = cheat-sheet only.** Definitions, key facts, one-liner explanations. Not a summary of the long note — a standalone quick-reference.
3. **"Added Context" is allowed** in the long note — if something the instructor said is outdated or there's a clearly better modern approach, note it under `## Added Context`. Don't editorialize heavily; keep it factual.
4. **Code examples must run.** If the instructor showed code, include it exactly (or corrected if it's broken by a deprecated API). Add a comment if you've corrected something.
5. **Interview angles are not optional.** For every technical concept, ask: "How would an interviewer probe this?" Include the likely question and the answer.
6. **Practice questions at the end** of every long note — 3–5 exercises or questions the reader can't answer from memory alone.

---

## Key Files & Folders

| Path | Purpose |
|---|---|
| `AGENT.md` *(this file)* | Agent context — read first every conversation |
| `ROADMAP.md` | Master AI Engineer roadmap checklist |
| `README.md` | Human-facing project overview + course table |
| `_inbox/transcript.md` | Paste YT transcript here — agent clears after use |
| `_inbox/diagrams/` | Drop diagram images here — agent deletes after embedding |
| `_meta/glossary.md` | Shared cross-course concept dictionary |
| `_meta/workflow.md` | Human-readable process description |
| `templates/long-note-template.md` | Template for deep-dive notes |
| `templates/short-note-template.md` | Template for quick-overview recall cards |
