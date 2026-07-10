# learning-vault

> **AI agents:** Read [`AGENT.md`](AGENT.md) first — it has the full project context, current course status, conventions, and workflow. This file (CLAUDE.md) is the legacy Claude Code tool config.

Personal course-notes vault. Each note is a distilled understanding of one video, written for active recall (not a transcript archive) and cross-linked across courses. Full rationale in the root `README.md`.

## How a note gets made

1. User watches a video, jots raw/messy notes, and optionally shares screenshots of anything the instructor drew or showed on screen.
2. User shares: raw notes + video link (+ screenshots, if the instructor used a diagram/example/analogy) + which course it belongs to.
3. Understand the actual material being taught — the raw notes are a pointer to what was covered, not the source to copy. Read any screenshots closely: the instructor's own examples/analogies are often the most memorable part of the video and should be captured in the note. If something is referenced but not fully visible or given (e.g. an analogy cut off in a screenshot), say so explicitly instead of guessing at it.
4. Write the note using [`templates/note-template.md`](templates/note-template.md): TL;DR, Core Concepts, How This Connects, Self-Test. Keep it to roughly one screen — if it's growing past that, it's turning back into a transcript instead of a distillation.
5. Save to `<course>/notes/NN-slug.md` (numbered in watch order). Update that course's own `README.md` progress table, the root `README.md` course table, and — if the video introduced a concept that will resurface in other courses — add it to [`_meta/glossary.md`](_meta/glossary.md) so later notes link back instead of re-explaining it.
6. Commit and push to `origin main` (`https://github.com/Wajid16/learning-vault.git`) unless told otherwise.

Full process detail: [`_meta/workflow.md`](_meta/workflow.md).

## Structure

- One top-level folder per course. A course folder only gets created once that course is actually being started — no scaffolding ahead of time for courses not yet begun.
- `non-technical/` holds non-technical subjects (writing, language, freelancing, etc.) in the same format, kept separate from the technical courses at the root.
- `_meta/glossary.md` — shared concepts referenced across more than one course.
- `templates/note-template.md` — the structure every note follows.

## Current courses

- **Technical:** `llm-evals` (in progress), `rag`, `mcp`, `langgraph`, `langchain`, `fastapi`, `docker`, `pydantic`, `n8n` (not started yet)
- **Non-technical:** `non-technical/scientific-writing`, `non-technical/ielts`, `non-technical/english`, `non-technical/freelancing` (not started yet)
