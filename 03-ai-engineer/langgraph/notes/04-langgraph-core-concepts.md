# LangGraph Core Concepts: Workflows, Graphs, State, Reducers

**Course:** LangGraph (CampusX) · **Video:** [Video 04](https://youtu.be/D5KhiCDM9XQ?si=q6layJjYBw20-v5k) · **Watched:** 2026-07-07

## TL;DR
The vocabulary from [[03-langchain-vs-langgraph]] made concrete: five recurring shapes that LLM workflows take, and the four building blocks LangGraph gives you to construct any of them — graphs/nodes/edges, state, reducers — plus how execution actually runs under the hood (Google Pregel–style rounds called "supersteps").

## Core Concepts

- **LLM Workflow** — a series of tasks executed in order to achieve a goal, where several of those tasks depend on an LLM (prompting, reasoning, tool calling, memory access, decision-making). Workflows can be linear, parallel, branched, or looped — the automated-hiring example from earlier notes is one instance; every application has its own, but certain *shapes* recur constantly:

  1. **Prompt Chaining** — multiple LLM calls in sequence, each one's output feeding the next (e.g. topic → outline → detailed report), often with a validation check gating a step (e.g. reject if report exceeds a word limit).
  2. **Routing** — one LLM call acts purely as a classifier/dispatcher, deciding *which* downstream handler should take a query (e.g. a support bot routing a query to a refund-LLM, a technical-LLM, or a sales-LLM based on its content).
  3. **Parallelization** — a task is split into independent subtasks that run *simultaneously*, then an aggregator merges the results into one decision (e.g. content moderation checking community-guidelines, misinformation, and explicit-content in parallel, then combining into publish/flag).
  4. **Orchestrator–Workers** — looks like parallelization, but the subtasks' *nature* isn't known in advance — an orchestrator LLM decides dynamically, per input, what each worker should do (e.g. a research assistant deciding at runtime whether to search Google Scholar or Google News, depending on whether the query is a scientific term or a current event).
  5. **Evaluator–Optimizer** — for tasks that can't be nailed in one shot (drafting an email, blog, poem): a generator LLM produces a solution, an evaluator LLM checks it against explicit criteria and either accepts it or rejects it with feedback, looping back to the generator until accepted.

- **Graphs, Nodes, Edges** — LangGraph's core mechanism: represent *any* LLM workflow as a graph. Each **node** is one task in the workflow — and under the hood a node is nothing more than a plain Python function. Each **edge** defines control flow: which node runs next after a given node finishes. Edges can be sequential, parallel (fan-out to multiple nodes at once), conditional (branch one way or another based on a check), or looping (send flow back to an earlier node). Worked example: a UPSC-essay-practice site (generate topic → collect essay → evaluate on 3 criteria → aggregate score → congratulate, or give feedback and loop back to let the student retry) maps directly onto a graph — every box in a hand-drawn flowchart becomes a node, every arrow becomes an edge.

- **State** — the shared, mutable memory that flows through a workflow's execution, holding every data point the workflow needs to run and evolving as execution proceeds (e.g. essay text, per-criterion scores, final score). In code it's a `TypedDict` (or a Pydantic object) defined up front, before the graph itself. Every node receives the *entire* current state as input, can read and mutate any field in it, and passes the updated state on to the next node via the edge — this is what makes LangGraph's execution **stateful** (as established in [[03-langchain-vs-langgraph]]).

- **Reducers** — define *how* an update to a given state key is applied when a node writes to it: **replace** (default — new value overwrites old), **add/append**, or **merge**. The distinction matters a lot: overwriting is fine for a running numeric score, but it silently breaks a chatbot's `messages` key — if each new message *replaces* the last instead of being *appended*, the LLM loses all earlier conversation history and can't answer something like "what's my name?" after the message containing the name has been overwritten. Each key in the state can have its own reducer; parallel workflows especially need explicit reducers to merge concurrent writes correctly.

- **Execution model (Pregel-inspired)** — LangGraph's runtime is modeled on Google's Pregel, a large-scale graph-processing system. Three phases:
  1. **Graph definition** — define nodes, edges, and the state (`TypedDict`).
  2. **Compile** — validates the graph's structure (e.g. catches an "orphan node" with no connecting edge) before anything runs.
  3. **Execution (invoke)** — the initial state is passed to the first node, which *activates* (its Python function runs), partially updates the state, then passes the updated state to the next node(s) via edges — this hand-off is called **message passing**. Execution stops once there's no active node and no message being passed along any edge. A single round of this is called a **superstep** rather than just "step" — because when an edge fans out to multiple parallel nodes, one round can contain more than one node executing at the same time.

## How This Connects
- Makes concrete the abstractions introduced in [[03-langchain-vs-langgraph]]: "stateful" now has a precise mechanism (state + reducers), and "graph-based orchestration" now has a precise execution model (nodes/edges + supersteps).
- Added to [`_meta/glossary.md`](../../../_meta/glossary.md): **LLM Workflow patterns (prompt chaining, routing, parallelization, orchestrator-workers, evaluator-optimizer)**, **Reducer (state update policy)** — both are framework-agnostic ideas likely to resurface in `langchain`/`rag`.

## Self-Test
- A workflow node writes to a `documents_found` key that should accumulate results from three parallel search nodes. What goes wrong if that key uses the default reducer instead of an "add" reducer?
- What's the actual difference between the Parallelization pattern and the Orchestrator-Workers pattern, given that both run subtasks concurrently and aggregate results?
- Why does LangGraph call a round of execution a "superstep" instead of a "step," and under what condition would a superstep contain only a single node?

---
