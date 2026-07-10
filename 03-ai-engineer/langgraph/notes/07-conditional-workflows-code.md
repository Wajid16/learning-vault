# Building Conditional Workflows in LangGraph

**Course:** LangGraph (CampusX) · **Video:** [Video 07](https://youtu.be/I-dvZqTz-Wc?si=F1yG8DJU5fyNBcxu) · **Watched:** 2026-07-07

## TL;DR
A third workflow shape, alongside [[05-sequential-workflows-code]] and [[06-parallel-workflows-code]]: a **conditional workflow** looks like branching (multiple candidate next-nodes off one source), but unlike a parallel workflow, only *one* branch actually runs per execution — the graph-equivalent of `if/elif/else`. Demonstrated via a quadratic-equation solver (routes on the sign of the discriminant) and an LLM-based customer-review handler (routes on sentiment, then diagnoses negative reviews before replying).

## Core Concepts

- **Conditional vs. Parallel workflow** — in a parallel workflow ([[06-parallel-workflows-code]]), two or more nodes fan out from one source and *all* execute, deliberately, at the same time. In a conditional workflow, two or more nodes are *candidates* for what runs next off one source, but a condition picks exactly one of them at runtime — the others never execute in that run. LangGraph's graph visualization renders conditional edges as **dotted lines** (vs. solid for ordinary edges) precisely because only one is actually traversed per execution.

- **Building a conditional edge** — write a separate **routing function** (not a graph node itself) that takes the state and returns a string naming which node to go to next — often type-hinted as `Literal["node_a", "node_b", ...]` for clarity. Then wire it in with `graph.add_conditional_edges(source_node, routing_function)` instead of `graph.add_edge`. At runtime LangGraph calls the routing function and sends execution to whichever node name it returned. Each candidate destination node still needs its own ordinary edge onward (e.g. to `END`) — the conditional edge only decides which one is entered, not what happens after.

- **Worked example 1 — quadratic equation solver (non-LLM)** — `show_equation` → `calculate_discriminant` → **[routing function checks the discriminant's sign]** → exactly one of `real_roots` (discriminant > 0) / `repeated_root` (= 0) / `no_real_roots` (< 0) → `END`. The routing function is just `if state["discriminant"] > 0: return "real_roots"` / `elif ... == 0: ...` / `else: ...` — structurally identical to `if/elif/else`.

- **Worked example 2 — LLM customer-review handler** — `find_sentiment` (structured output: `Literal["positive", "negative"]`) → **[routing function checks sentiment]** → either:
  - **positive path:** `positive_response` (a plain, non-structured LLM call that writes a warm thank-you reply) → `END`; or
  - **negative path:** `run_diagnosis` (a *second* structured-output call extracting `issue_type` / `tone` / `urgency` from the review, stored as a nested dict in state) → `negative_response` (a plain LLM call that uses those three diagnosis fields to write a specific, empathetic reply, e.g. referencing "high urgency" and a "frustrated" tone) → `END`.
  - The two-step negative path (diagnose, *then* respond) is the deliberate design choice — it's what makes the negative reply noticeably more targeted than a generic apology would be.

- **This example is the first to combine three previously separate techniques in one graph:** conditional routing, structured output ([[06-parallel-workflows-code]]) used *twice* with two different Pydantic schemas (sentiment schema, then a diagnosis schema), and a state field holding a **nested dict** (`diagnosis: dict`) rather than a flat scalar value.

- **Note for later** — there's a second, more advanced way to build conditional routing using a `Command` object, planned for a future video on dynamic workflows; `add_conditional_edges` (covered here) is the simpler, first approach.

## How This Connects
- Completes the trio of basic workflow shapes with [[05-sequential-workflows-code]] (sequential) and [[06-parallel-workflows-code]] (parallel) — real workflows combine all three.
- Reuses Structured Output from [[06-parallel-workflows-code]], applied twice in a single graph for two different extraction tasks.
- Added to [`_meta/glossary.md`](../../../_meta/glossary.md): **Conditional Workflow (routing function)**.

## Self-Test
- What's the actual difference between a parallel workflow and a conditional workflow, given that both look like a fan-out of multiple candidate nodes from one source?
- In the review-handling example, why does the negative path route through an extra `run_diagnosis` node instead of generating the reply directly off the sentiment result alone?
- What does the routing function passed to `add_conditional_edges` actually return, and how does that differ from what a normal node function returns?

---
