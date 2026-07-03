# How notes get made

This repo isn't a transcript archive — the goal is to actually retain the material and to be able to skim a note 6 months later and have it click back into place. That means each note is a **distilled understanding**, not a copy of raw notes.

## The loop

1. **Watch the video**, jot down raw/messy notes as you normally would — no formatting effort, just capture.
2. **Hand it to Claude**: paste the video link + your raw notes, and say which course/topic it belongs to.
3. **Claude does not just reformat your raw notes.** It should understand the actual subject the video covers (using your notes as a pointer to what was said, not as the source of truth to copy) and write the note from that understanding, using [`templates/note-template.md`](../templates/note-template.md).
4. Claude saves it to `<category>/<course>/notes/NN-slug.md` (numbered in watch order) and updates that course's `README.md` progress table.
5. You review, correct anything Claude misunderstood, commit.

## Ground rules for the notes themselves

- **Short.** If a note is pushing past one screen, it's turning back into a transcript. Cut it.
- **Cross-link, don't repeat.** If `mcp` and `pydantic` both touch schema validation, the second note links to the first (or to `_meta/glossary.md`) instead of re-explaining it. This is the main fix for "I learned this five times and it never stuck" — the notes should visibly connect instead of living in five separate silos.
- **Self-test section is not optional filler.** It's the part you actually use when recalling. Questions should be things you can't answer from the title alone.
- **New shared term (JSON schema, embedding, container, tool call, etc.) → goes in `_meta/glossary.md`** the first time it comes up, then every later note just links to it.

## File naming

- Course folder: `category/course-name/`
- Notes: `category/course-name/notes/01-short-slug.md`, `02-short-slug.md`, ... in the order you watched them.
- Course `README.md` holds the progress table + a one-line "what this course is" blurb.
