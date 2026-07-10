# Why LangGraph? (LangChain vs. LangGraph)

**Course:** LangGraph (CampusX) · **Video:** [Video 03](https://youtu.be/GWnSsjT4V68?si=yXvQrB18qrhOGZ_g) · **Watched:** 2026-07-07

## TL;DR
LangChain gives you the building blocks for LLM apps (models, prompts, retrievers) and a way to chain them linearly — but the automated-hiring example from [[02-what-is-agentic-ai]] is actually a **workflow**, not an agent, and it's highly *non-linear* (branches, loops, long pauses). Trying to build it in LangChain forces the developer to hand-write "glue code" for everything LangChain wasn't designed for. LangGraph exists to be the orchestration layer for exactly that: non-linear, stateful, long-running, event-driven workflows — built *on top of* LangChain, not a replacement for it.

## Core Concepts

- **Workflow vs. Agent** (from Anthropic's "Building Effective Agents" post) — a **workflow** is a system where LLMs and tools are orchestrated through a *predefined* code path (a fixed flowchart the developer designed); an **agent** is a system where the LLM *dynamically* directs its own process and tool use. Correction/nuance on the automated-hiring example from [[02-what-is-agentic-ai]]: the flowchart built for it here is a **workflow** — static, same order every run, designed by the developer — not an agent, even though it uses LLMs throughout.

- **LangChain recap** — an open-source library that simplifies building LLM-based apps via modular building blocks: **Model** (unified interface across LLM providers), **Prompts** (prompt engineering), **Retrievers** (fetch relevant docs from a vector store for RAG), and **Chains** (LangChain's headline feature — wire components together so one's output auto-becomes the next's input). This is enough to build conversational workflows, multi-step workflows, RAG apps, and basic tool-calling agents — but chains are fundamentally **linear**.

- **Eight things a complex non-linear workflow needs, and how the two libraries compare:**

  1. **Control flow complexity** — the hiring workflow has conditional branches, loops, and jumps (non-linear). LangChain has no built-in construct for these — you write your own Python `while`/`if` around the chains ("glue code"), which hurts maintainability as complexity grows. LangGraph represents the whole workflow as a **graph**: each task is a node (a plain Python function), each transition is an edge, and conditional/looping edges are native constructs — zero glue code.

  2. **State handling** — a complex workflow has many evolving data points (JD text, approved?, posted?, applicant count, shortlist, offer status...) — together called the **state**. LangChain has no mechanism to store/track structured key-value state (only conversational memory); you'd maintain a global dict by hand. LangGraph is **stateful**: you define a state object/dict once, and every node automatically receives it, can read *and* mutate it, and passes the updated version to the next node.

  3. **Event-driven execution** — some steps must *pause* and wait for an external trigger (wait 7 days before checking applications, wait for a candidate to accept/reject an offer) rather than running straight through (sequential execution). LangChain is built only for sequential execution — no native pause/resume. LangGraph supports pausing indefinitely and resuming later via **checkpointing** (state is saved, then reloaded when the trigger arrives).

  4. **Fault tolerance** — long-running workflows (days to months) are prone to small faults (one API down) and big faults (server/container crash). LangChain has none — a failure mid-chain means restarting from step one. LangGraph gives retry logic for small faults and, since every node's execution creates a checkpoint of the state, full **recovery**: resume exactly from the last completed node after a crash.

  5. **Human-in-the-loop** — some steps need a human decision (approve the JD, approve posting) that may take hours or days. LangChain can take synchronous input mid-chain, but can't pause a running chain indefinitely without tying up the process/resources or manually splitting the chain and hand-passing state. LangGraph treats this as a first-class feature: pause indefinitely (via the same checkpointing mechanism as #3/#4), resume exactly where it left off once input arrives — like a video game save state.

  6. **Nested workflows (subgraphs)** — a single node can itself *be* a whole other graph. Two big uses: (a) **multi-agent systems** — e.g. a self-driving car's sensor agent, driving agent, entertainment agent, and a coordinating "CEO" agent, each a subgraph; (b) **reusability** — build one small graph (e.g. "get approval") once, reuse it as a node everywhere approval is needed, the same way you'd reuse a function. Not possible in LangChain at all.

  7. **Observability** — being able to monitor/debug/understand what a workflow did at runtime (critical in production for auditing bad decisions, e.g. an agent overspending on ads unsupervised). LangSmith integrates with LangChain, but only tracks LangChain-native calls — it's blind to your hand-written glue code, so a complex LangChain workflow gets only **partial** observability. Because LangGraph has zero glue code (everything is graph-native), LangSmith gets a complete node-by-node, state-by-state timeline — full observability.

- **Formal definition (closing the loop)** — "LangGraph is an orchestration framework that enables you to build stateful, multistep, and event-driven workflows using LLMs. It's ideal for designing both single-agent and multi-agent agentic AI applications." Mental model: **a flowchart engine for LLMs** — you define steps as nodes, connections as edges, and LangGraph handles state management, conditional branching, looping, pausing/resuming, and fault recovery for you.

- **When to use which** — LangChain: simple *linear* workflows (prompt chains, summarizers, basic RAG). LangGraph: complex *non-linear* workflows — conditionals, loops, human-in-the-loop, multi-agent coordination, async event-driven execution.

- **LangGraph is not a LangChain replacement** — it's built *on top of* LangChain. LangChain still supplies the components (`ChatOpenAI`, prompt templates, retrievers, document loaders, text splitters, tools); LangGraph supplies the orchestration layer that connects them for anything more complex than a straight chain. Real projects going forward use both together.

## How This Connects
- Builds on [[02-what-is-agentic-ai]] — reuses that video's HR-hiring scenario, but reclassifies it as a *workflow*, not an agent, which sharpens the workflow-vs-agent distinction from Anthropic's blog.
- Added to [`_meta/glossary.md`](../../../_meta/glossary.md): **Workflow vs. Agent (Anthropic's distinction)**, **Checkpointing (LangGraph)** — both are framework-agnostic ideas that will resurface once `langchain` notes exist.

## Self-Test
- The automated-hiring flowchart uses LLMs at every step, yet the video insists it's not an "agent." What's the specific criterion that makes it a workflow instead?
- Why does "stateful execution" turn out to be the mechanism underlying *three* separate challenges (state handling, event-driven execution, fault tolerance) rather than being a separate fourth thing?
- Your team already has a working LangChain RAG chatbot and now wants to add a step where a human can approve/reject an answer before it's sent, with approval sometimes taking a day. Which of the 8 points does this hit, and what would migrating to LangGraph actually buy you here?

---
