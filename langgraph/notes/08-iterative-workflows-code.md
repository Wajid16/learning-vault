# Building Iterative (Looping) Workflows in LangGraph

**Course:** LangGraph (CampusX) · **Video:** [Video 08](https://youtu.be/7CbSqrovcsE?si=53Yw8nhYPJOgSc7Q) · **Watched:** 2026-07-07

## TL;DR
The fourth and final basic workflow shape, alongside sequential ([[05-sequential-workflows-code]]), parallel ([[06-parallel-workflows-code]]), and conditional ([[07-conditional-workflows-code]]): an **iterative/looping workflow** cycles between two nodes to progressively improve something, until a condition is met or a safety cap is hit. Demonstrated via a three-LLM tweet generator (generate → evaluate → optimize → back to evaluate) — and the mechanism turns out to be nothing new: a loop is just a conditional edge going one way plus a normal edge going back.

## Core Concepts

- **Iterative workflow** — runs a generate/evaluate cycle repeatedly to improve an output, rather than accepting the first attempt. Useful anywhere a single LLM pass is unreliable at hitting a quality bar (e.g. the video's motivating case: auto-generating social posts that are actually funny/original on the first try, which base LLMs are often not).

- **Three-LLM structure (generator / evaluator / optimizer)** — in an ideal build, each is a *different* model chosen for its specific strength: a strong writer model for generation, a strict/reliable model for evaluation, a model good at revising given feedback for optimization. The video uses the same family of models for all three (as a demo), but flags this as the first place to specialize when hardening a real project.

- **The workflow (tweet generator)**: `generate` (system+human message prompt describing tone/format rules → generator LLM → tweet) → `evaluate` (structured-output evaluator LLM scores the tweet against an explicit criteria prompt, returning `evaluation: Literal["approved", "needs_improvement"]` plus a `feedback` string) → **[conditional edge]** → either `END` (if approved) or `optimize` (rewrites the tweet using the original tweet + the evaluator's feedback, then loops back to `evaluate`).

- **A loop is just edge manipulation** — there is no separate "loop" construct in LangGraph. You get a loop by combining: (1) a conditional edge from `evaluate` that can route back to `optimize`, and (2) a plain `add_edge(optimize, evaluate)` sending control back to the evaluation step. That's the entire mechanism — "creating loops in LangGraph is just manipulating edges."

- **Guarding against infinite loops** — since an evaluator could reject indefinitely (criteria too strict, model not capable enough), the state carries an `iteration` counter and a `max_iteration` cap. The routing function checks *both* conditions before deciding: `if evaluation == "approved" or iteration >= max_iteration: return "approved"` (→ `END`) `else: return "needs_improvement"` (→ `optimize`) — the iteration cap is what guarantees termination even if quality is never reached.

- **Structured output reused for the evaluator** ([[06-parallel-workflows-code]]) — a Pydantic schema with an `evaluation: Literal["approved", "needs_improvement"]` field and a `feedback: str` field, so the routing function always gets a reliably-parseable decision instead of free-form text.

- **Reducers reused outside a parallel context** ([[04-langgraph-core-concepts]], [[06-parallel-workflows-code]]) — to keep a full history of every attempt (not just the latest), the state adds `tweet_history` and `feedback_history` as `Annotated[list[str], operator.add]`. Two *different* nodes (`generate` and `optimize`) both write into `tweet_history` across multiple passes through the loop — the reducer's job here isn't merging concurrent parallel writes, but accumulating sequential writes across loop iterations, showing reducers are a general "how do repeated writes to this key combine" mechanism, not just a parallel-workflow tool.

## How This Connects
- Completes the set of four basic workflow shapes with [[05-sequential-workflows-code]], [[06-parallel-workflows-code]], and [[07-conditional-workflows-code]] — real LangGraph applications combine all four.
- Reuses Structured Output and the `Annotated[list, operator.add]` reducer pattern from [[06-parallel-workflows-code]], applied in a new context (sequential loop accumulation rather than parallel merging).
- Flagged as a workflow this course will revisit once tools and human-in-the-loop are covered — right now the loop ends at `END`, but a real deployment would insert a human-approval step before actually posting.
- No new glossary terms — this video applies concepts already captured (structured output, reducers, conditional edges) to a new shape (loops).

## Self-Test
- What are the two edges that together make a loop in LangGraph, and why isn't a loop a separate construct?
- Why does the routing function check `iteration >= max_iteration` in addition to `evaluation == "approved"`, rather than relying on the evaluator alone to end the loop?
- `tweet_history` uses the same `Annotated[list[str], operator.add]` reducer as the parallel-workflow example in [[06-parallel-workflows-code]] — but the reason it's needed is different here. What's actually being merged in each case?

---
