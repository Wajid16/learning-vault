# Giving the LangGraph Chatbot a UI (Streamlit)

**Course:** LangGraph (CampusX) · **Video:** [Video 11](https://youtu.be/voZAgDmO-rk?si=R1MQawOakH3LUPmx) · **Watched:** 2026-07-07

## TL;DR
Fixes the last obvious gap in the chatbot from [[09-chatbot-memory-bug]]/[[10-persistence-deep-dive]]: no UI, just a Jupyter loop. The chatbot is split into a **backend** (the LangGraph workflow, unchanged) and a **frontend** (a Streamlit web page). Getting there means learning Streamlit's two chat components and — the actual gotcha — its rerun model, which silently wipes conversation history unless you deliberately store it in `st.session_state` instead of a plain variable.

## Core Concepts

- **Backend/frontend split** — the exact same LangGraph code from earlier videos (state, nodes, `chatbot.compile(checkpointer=...)`) becomes `langgraph_backend.py`, untouched. A new `streamlit_frontend.py` imports the compiled `chatbot` graph object directly (`from langgraph_backend import chatbot`) and owns only the UI — no HTTP layer, just a Python import, since both files run in the same process here.

- **Two Streamlit chat components:**
  - `st.chat_message(role)` — renders one message bubble, with an icon determined by `role` (`"user"` vs. `"assistant"`); `st.text(...)` inside it renders the content.
  - `st.chat_input(placeholder)` — the input box pinned to the bottom of the page; returns the typed string once the user presses enter (or `None` otherwise).

- **Streamlit's rerun model (the actual gotcha)** — Streamlit re-executes the *entire script top-to-bottom* every time the user interacts with the page (e.g. submits `chat_input`). A naive approach — keep conversation history in a plain Python list defined near the top of the script — breaks immediately: that list gets reinitialized to empty on every single rerun, so only the most recent exchange ever displays; everything earlier vanishes. This mirrors the exact shape of the bug in [[09-chatbot-memory-bug]] (state reset between invocations) but at the UI layer instead of the graph layer.

- **Fix: `st.session_state`** — a dict-like object that, unlike a plain variable, *persists across reruns* — it's only cleared on a manual page refresh, not on every interaction. The working pattern: 
  1. `if "message_history" not in st.session_state: st.session_state["message_history"] = []` (initialize once).
  2. At the top of the script, loop over `st.session_state["message_history"]` and re-render every past message via `st.chat_message(...)`.
  3. When new input arrives via `chat_input`, append the user's `{"role": "user", "content": ...}` dict into `st.session_state["message_history"]` *before* displaying it, then do the same for the assistant's reply.
  - Built first as a "copycat" bot (the assistant just echoes the user's own input) specifically to isolate and debug the Streamlit mechanics before wiring in the real LLM — same staged-complexity approach used throughout this course.

- **Wiring in the real LangGraph backend** — once the copycat version works, only the assistant-reply step changes: wrap the user's text in `HumanMessage(content=user_input)`, call `chatbot.invoke({"messages": [HumanMessage(...)]}, config=CONFIG)`, and extract the reply via `response["messages"][-1].content`. `CONFIG` (`{"configurable": {"thread_id": "1"}}`, from [[10-persistence-deep-dive]]) is defined once at the top of the frontend file — forgetting to pass it to `.invoke()` was a bug the video hit live, since the backend's checkpointer requires a thread ID on every call, UI or not.

## How This Connects
- Directly builds on [[09-chatbot-memory-bug]] and [[10-persistence-deep-dive]] — the same `chatbot` graph object and `CONFIG`/thread ID pattern are reused verbatim, just called from a Streamlit script instead of a Jupyter loop.
- The Streamlit rerun/session_state gotcha is structurally the same lesson as the invoke-resets-state bug from [[09-chatbot-memory-bug]]: anything not deliberately persisted gets wiped on the next execution cycle, whether that cycle is a LangGraph `.invoke()` or a Streamlit script rerun.
- Added to [`_meta/glossary.md`](../../../_meta/glossary.md): **Streamlit rerun model + `session_state`** — likely to resurface as this chatbot arc keeps adding UI-facing features (tools, human-in-the-loop approval, etc.).

## Self-Test
- Why does storing conversation history in a plain Python list at the top of a Streamlit script fail, when the exact same list-of-dicts pattern would work fine in a normal long-running program?
- What's the one line that was missing when the real LangGraph backend was first wired into the UI, and why did the checkpointer specifically require it?
- The video builds a "copycat" chatbot before the real one. What specifically does that intermediate step isolate and de-risk?

---
