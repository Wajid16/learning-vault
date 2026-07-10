# A Chatbot in LangGraph — and Why It Forgets Everything

**Course:** LangGraph (CampusX) · **Video:** [Video 09](https://youtu.be/51Ve2tE3Zns?si=zm34eMFy1NKl5Tug) · **Watched:** 2026-07-07

## TL;DR
Kicks off a new multi-video arc: building one increasingly capable chatbot (plain chat → RAG → tools → UI → LangSmith → memory → persistence → human-in-the-loop → retry/fault-tolerance), reusing it as the running example for every remaining "advanced LangGraph" topic. Today's chatbot is the simplest possible LangGraph app — a single node — but it exposes a deliberate bug: it forgets everything between messages, because every `invoke()` call starts from a blank state. The fix, **persistence**, is introduced just enough to make the bot work, with the full mechanics (checkpointers, threads) explicitly deferred to a dedicated video next.

## Core Concepts

- **The chatbot as a workflow** — the simplest LangGraph shape possible: one node, `chat_node`, which pulls the message list from state, sends it to an LLM, and appends the response. `START → chat_node → END`. The "chatting" feel comes entirely from an *external* Python `while True` loop that keeps calling `.invoke()` on this one-node graph until the user types exit/quit/bye — the graph itself has no built-in notion of an ongoing conversation.

- **State uses `BaseMessage`, not plain strings** — `messages: Annotated[list[BaseMessage], add_messages]`. `BaseMessage` is the parent type of `HumanMessage`/`AIMessage`/`SystemMessage`/`ToolMessage` (from the LangChain playlist) — using it as the list's type lets the state hold any mix of message roles, not just raw text.

- **`add_messages` instead of `operator.add`** — LangGraph ships a purpose-built reducer, `from langgraph.graph.message import add_messages`, for exactly this situation (appending to a list of message objects). It behaves like `operator.add` but is more optimized for `BaseMessage` objects specifically — the recommended reducer whenever a state field accumulates messages.

- **The bug, deliberately surfaced** — after wiring up a `while` loop that calls `chatbot.invoke()` once per user turn, the bot correctly answers a first question but then fails something as simple as "what's my name?" right after being told it, or continuing a multi-step calculation. The reducer *does* correctly append messages **within one `invoke()` call** — but each new `invoke()` call starts from a completely fresh, empty state. When the graph execution reaches `END`, everything accumulated in that state is discarded; the next `invoke()` from the loop has no memory of it. So a chatbot that looks like it's "forgetting" is actually just being re-invoked from scratch every single turn.

- **Persistence (introduced here, explained fully next video)** — instead of discarding state at `END`, save it somewhere so the *next* `invoke()` can reload it rather than starting over. Two storage choices: a database (for production — survives restarts, works across sessions days apart) or in-memory/RAM (fine for a quick demo, but lost the moment the program restarts). Minimal code to wire it up:
  1. `from langgraph.checkpoint.memory import MemorySaver` — create a **checkpointer** object.
  2. `graph.compile(checkpointer=checkpointer)` — tell the graph to persist state via that checkpointer.
  3. Define a **thread** — one thread = one ongoing conversation/user session, identified by a `thread_id` string (so the same chatbot can hold independent, non-mixing conversations with different users at once).
  4. On every `.invoke()`, pass `config={"configurable": {"thread_id": ...}}` alongside the message — this tells LangGraph which conversation's saved state to reload before running the graph.
  5. `chatbot.get_state(config)` inspects the full accumulated conversation history for a given thread at any point.
- With this wired in, the bot correctly recalls the user's name and correctly continues a multi-step calculation across separate `invoke()` calls in the same thread — but restarting the program wipes it, since `MemorySaver` only lives in RAM.

## How This Connects
- Opens a new arc that will run across many future videos, each adding one feature to this same chatbot; earlier notes on structured output ([[06-parallel-workflows-code]]) and reducers ([[04-langgraph-core-concepts]], [[08-iterative-workflows-code]]) are the foundation this builds on.
- Persistence/checkpointers are explicitly flagged by the instructor as needing a dedicated deep-dive — expect a future note in this vault once that video lands, to link back to.
- Added to [`_meta/glossary.md`](../../../_meta/glossary.md): **Message types (BaseMessage hierarchy)**, **Persistence / Checkpointer (LangGraph)** — both are concepts this course will keep building on.

## Self-Test
- Why does the chatbot correctly remember context *within* a single `invoke()` call but forget it *between* calls, even though the same reducer (`add_messages`) is used in both cases?
- What's the difference between a "thread" and a "checkpointer" in LangGraph's persistence model?
- If this chatbot used a database-backed checkpointer instead of `MemorySaver`, what specifically would change about its behavior after the program restarts?

---
