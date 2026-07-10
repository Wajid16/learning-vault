# Streaming Responses in the LangGraph Chatbot

**Course:** LangGraph (CampusX) · **Video:** [Video 12](https://youtu.be/D1PcZaeQ2eg?si=Fj-D_zcabwVkaOgY) · **Watched:** 2026-07-07

## TL;DR
The chatbot from [[11-streamlit-ui-for-chatbot]] has one more rough edge: for a long response (e.g. a 500-word blog), the UI sits frozen for several seconds and then dumps the entire answer at once. **Streaming** — sending tokens to the UI as soon as they're generated, instead of waiting for the whole response — fixes this, and requires almost no backend change: swap `.invoke()` for `.stream()`, and consume the generator it returns.

## Core Concepts

- **Streaming (definition)** — instead of the LLM generating a full response and returning it all at once, tokens are sent back one at a time as they're produced, giving the familiar ChatGPT-style typewriter effect.

- **Why it matters (five reasons):**
  1. **Perceived speed** — a 5–10 second wait with a blank screen reads as "the app is frozen" to non-technical users, increasing the chance they abandon the app; streaming shows immediate activity even though total generation time is the same.
  2. **Feels like a real conversation** — mimics human back-and-forth, builds trust, keeps the user engaged rather than staring at a spinner.
  3. **Essential for voice/multimodal UIs** — a device like Alexa without streaming would sit in awkward silence for the full generation time before speaking the whole answer at once; streaming lets it start responding immediately.
  4. **Better readability for long structured output like code** — code that appears line-by-line is easier to follow than an entire code block appearing all at once.
  5. **Lets the user interrupt** — if the response is clearly heading somewhere unwanted, the user can stop it mid-generation, saving the remaining tokens (and therefore cost, since LLM providers bill per token).
  - **Bonus use, relevant to future agent videos:** streaming isn't only for the final answer's text — it can also surface step-by-step progress updates for an agent (e.g. "opening BookMyShow" → "selecting movie" → "selecting seat" → "paying") instead of one long silent wait followed by a sudden "done," via a different `stream_mode`.

- **Implementation — backend needs zero changes.** The compiled graph object itself is untouched; only how it's *called* changes:
  - Replace `chatbot.invoke(initial_state, config=CONFIG)` with `chatbot.stream(initial_state, config=CONFIG, stream_mode="messages")`.
  - `.stream()` returns a **Python generator**, not a final value. LangGraph offers multiple `stream_mode` options (`updates`, `values`, `custom`, `messages`) — `"messages"` is the one needed for token-by-token LLM text; the others become relevant later for tool-using agents, where you want to stream *progress* rather than raw tokens.
  - Iterate it: `for message_chunk, metadata in chatbot.stream(...):` — each yielded item is a `(message_chunk, metadata)` pair; `message_chunk.content` holds that piece of text.

- **Streamlit integration** — `st.write_stream(generator)` is a built-in Streamlit component purpose-built to consume a Python generator and render it with the typewriter effect automatically; it also returns the fully assembled final string once done. The frontend pattern becomes: inside `st.chat_message("assistant")`, call `ai_message = st.write_stream(message_chunk.content for message_chunk, metadata in chatbot.stream(...))`, then store `ai_message` into `st.session_state["message_history"]` exactly as the plain-text response was stored in [[11-streamlit-ui-for-chatbot]] — the only thing that changed is *how* the reply is obtained and displayed, not how it's persisted in session state.

## How This Connects
- Directly extends [[11-streamlit-ui-for-chatbot]] — same `chatbot` object, same `CONFIG`/thread ID, same `session_state` history pattern; only the invoke→stream swap and the display call change.
- Added to [`_meta/glossary.md`](../../../_meta/glossary.md): **Streaming (LLM apps)** — a concept that applies well beyond LangGraph and will resurface in any future course touching LLM-facing UIs.

## Self-Test
- Why does implementing streaming require zero changes to the LangGraph backend graph itself?
- What are the two things yielded by each item of `chatbot.stream(..., stream_mode="messages")`, and which one actually holds the text to display?
- Streaming is described as also useful for showing an agent's step-by-step progress (e.g. "selecting seat" → "paying"), not just token-by-token text. What's different about that use case compared to streaming a chat reply?

---
