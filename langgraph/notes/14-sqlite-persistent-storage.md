# Making the Chatbot's Memory Permanent (SQLite Checkpointer)

**Course:** LangGraph (CampusX) · **Video:** [Video 14](https://youtu.be/c6a47iX5JkU?si=RaPJzoEUrrNDiGqM) · **Watched:** 2026-07-07

## TL;DR
Fixes the limitation flagged at the end of [[13-resume-chat-feature]]: `InMemorySaver` stores everything in RAM, so refreshing the page or restarting the app wipes every conversation. Swapping in `SqliteSaver` — a checkpointer backed by a real SQLite database file — makes chat history survive restarts, with almost no code change: the checkpointer object is the only thing that changes on the backend, and the frontend needs exactly one fix (load existing threads from the database on startup instead of assuming there are none).

## Core Concepts

- **Three checkpointer tiers in LangGraph** — `InMemorySaver` (RAM-backed, used through [[13-resume-chat-feature]] — fine for demos, wiped on restart); `SqliteSaver` (a small file-based database — good for prototyping, what this video uses); a Postgres-backed saver (production-grade, for real deployments). The tier only changes *where* checkpoints are saved — everything else about persistence from [[10-persistence-deep-dive]] (checkpoints per superstep, thread IDs) stays the same.

- **Backend change — swap the checkpointer, nothing else:**
  1. Install the external package `langgraph-checkpoint-sqlite` (not yet built into core LangGraph).
  2. `import sqlite3`, `conn = sqlite3.connect("chatbot.db", check_same_thread=False)` — creates (or opens) a SQLite database file in the project directory. `check_same_thread=False` is required because SQLite restricts a connection to the thread that created it by default, but this app will use the same connection across multiple conversations/threads — so that restriction is deliberately disabled.
  3. `from langgraph.checkpoint.sqlite import SqliteSaver`, then `checkpointer = SqliteSaver(conn)`.
  4. Everything downstream — `graph.compile(checkpointer=checkpointer)`, `.invoke()`, `.stream()`, `.get_state()` — is completely unchanged.

- **Verifying it actually persists** — sending a message, fully closing the program, and re-running it still lets `"what is my name?"` on the same `thread_id` recall context from the earlier run — something that would silently fail with `InMemorySaver` since that program's RAM is gone.

- **Visualizing the database directly** — a VS Code extension ("SQLite Viewer") lets you open `chatbot.db` and see every checkpoint grouped by thread. Confirms the superstep-per-checkpoint rule from [[10-persistence-deep-dive]] concretely: one logical conversation turn in this graph (`START → chat_node → END`) produces **3** checkpoints, not 1 — matching the graph's 3 supersteps.

- **`checkpointer.list(None)` — listing every thread that already exists** — the checkpointer object exposes a `.list()` method returning a generator of checkpoint tuples; calling `.list(None)` (instead of passing a specific thread's config) returns *every* checkpoint across *all* threads in the database. A new backend utility, `retrieve_all_threads()`, loops over this generator, pulls `checkpoint.config["configurable"]["thread_id"]` from each item, and collects them into a **`set`** (deliberately, since multiple checkpoints per conversation would otherwise produce duplicate thread IDs) before returning it as a list.

- **The one necessary frontend change** — previously (in [[13-resume-chat-feature]]), `st.session_state["chat_threads"]` was correctly initialized as an empty list on page load, because there was no permanent storage to have anything in it. Now that storage is durable, that assumption is wrong: the frontend must query the backend for pre-existing threads at startup. Fix: initialize `chat_threads` via `retrieve_all_threads()` instead of `[]` — so the sidebar shows every past conversation (with full history, since thread IDs map straight back into the database) immediately on load, even after a complete restart.

## How This Connects
- Directly resolves the limitation called out at the end of [[13-resume-chat-feature]] — same sidebar/thread UI, now backed by durable storage instead of RAM.
- Confirms the checkpoint-per-superstep mechanic from [[10-persistence-deep-dive]] with a concrete, inspectable example (3 checkpoints per turn, visible in the SQLite file itself).
- Updated [`_meta/glossary.md`](../../_meta/glossary.md): expanded **Persistence / Checkpointer (LangGraph)** to name the three checkpointer tiers explicitly.

## Self-Test
- Why does `sqlite3.connect(...)` need `check_same_thread=False` specifically for this chatbot's use case, when it wouldn't be needed for a single-threaded script?
- Why does `retrieve_all_threads()` collect thread IDs into a `set` rather than a plain list, given that `checkpointer.list(None)` returns one item per *checkpoint*, not per *thread*?
- If a fresh conversation with 4 user messages exchanged produces how many checkpoints in this graph's SQLite database, and why?

---
