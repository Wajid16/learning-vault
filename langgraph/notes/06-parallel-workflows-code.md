# Building Parallel Workflows in LangGraph (Structured Output + Reducers)

**Course:** LangGraph (CampusX) · **Video:** [Video 06](https://youtu.be/O6ryuSpqdOw?si=Swr6nV7LJQH31nTj) · **Watched:** 2026-07-07

## TL;DR
Extends [[05-sequential-workflows-code]]'s recipe to fan-out/fan-in graphs via two examples: a non-LLM cricket-stats calculator that exposes a critical gotcha (parallel nodes must return *partial* state updates, not the full state, or LangGraph errors out), and an LLM-based UPSC-essay evaluator that combines parallel LLM calls with **structured output** (Pydantic schemas) and a real **reducer** (`Annotated[list[int], operator.add]`) — turning [[04-langgraph-core-concepts]]'s abstract reducer concept into actual code.

## Core Concepts

- **Building the graph shape is simple** — fan-out is just multiple `add_edge(START, node)` calls from the same source; fan-in is multiple `add_edge(node, next_node)` calls converging on the same destination. The graph-construction code itself barely changes from the sequential case.

- **Gotcha: parallel nodes must return partial state, not the full state** — in the sequential-workflow video, every node returned the entire state object and that worked fine. Doing the same in a *parallel* workflow throws `InvalidUpdateError: At key '...' key can receive only one value per step`. Why: when multiple nodes run concurrently and each returns the whole state object, LangGraph treats that as if every node tried to write every key — including keys it never actually touched — and can't resolve the conflict between the parallel writers. **Fix:** each node should return a plain dict containing *only* the key(s) it actually computed (e.g. `return {"strike_rate": value}`), never the full state. This is safe in sequential workflows too, so the video recommends doing it everywhere going forward, not just in parallel graphs.

- **Structured Output (revisited from the LangChain playlist)** — needed here because three parallel LLM calls each must reliably return two things in the exact same shape every time: a text feedback string and a 0–10 integer score. Free-form prompting risks occasional format drift (e.g. the model writing "seven" instead of `7`), which silently breaks any downstream averaging. Fix: define a schema as a Pydantic class (extends `BaseModel`; each field uses `Field(description="...")` to guide the LLM toward the right value), then call `model.with_structured_output(schema)` to get a model that reliably returns an object matching that schema (`result.score`, `result.feedback`).

- **Reducers in practice** — the UPSC-essay-evaluator example has three parallel nodes (clarity of thought, depth of analysis, language), each meant to append one score into a shared `individual_scores` list. Since they run concurrently and all target the same state key, the default "replace" behavior would silently keep only the last writer's value and lose the other two scores. **Fix:** annotate the field as `Annotated[list[int], operator.add]` in the state's `TypedDict` — `operator.add` (from Python's `operator` module — the functional form of `+`) is the reducer; for lists, `+` concatenates rather than overwrites, so each node's single-item list result gets merged into one combined list instead of clobbering the others. This is the concrete code behind the abstract "each key in the state can have its own reducer" idea from [[04-langgraph-core-concepts]].

- **Worked pattern (UPSC essay evaluator)** — three parallel nodes (`evaluate_language`, `evaluate_analysis`, `evaluate_thought`) each call the *same* structured-output model with a different evaluation prompt, and each returns a partial update: its own feedback string plus `{"individual_scores": [score]}` (merged via the reducer above). A final `final_evaluation` node deliberately uses the **plain** (non-structured-output) model to merge the three feedback strings into one summarized feedback — structured output is skipped here on purpose, since forcing a score out of a pure summarization step risks the model inventing a spurious fourth score — and separately computes the numeric average by hand from `individual_scores`.

## How This Connects
- Directly extends [[05-sequential-workflows-code]]'s four-step recipe (State → Graph → compile → invoke) to fan-out/fan-in shapes.
- Makes concrete the reducer concept from [[04-langgraph-core-concepts]] with real code (`Annotated[list, operator.add]`).
- Added to [`_meta/glossary.md`](../../_meta/glossary.md): **Structured Output (LLM)** — a cross-course concept (from the LangChain playlist, reused here) that will keep recurring anywhere an LLM's output needs to be reliably machine-parseable.

## Self-Test
- Why does returning the entire state object from a node work fine in a sequential workflow but throw `InvalidUpdateError` in a parallel one?
- In the UPSC evaluator, why does the `final_evaluation` node use the plain model instead of the structured-output model, even though every other node in the graph uses structured output?
- What specifically would go wrong with `individual_scores` if its field were declared as plain `list[int]` instead of `Annotated[list[int], operator.add]`?

---
