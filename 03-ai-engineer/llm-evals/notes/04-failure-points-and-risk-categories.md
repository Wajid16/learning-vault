# Why Your AI Application Needs Multiple Eval Pipelines

**Course:** LLM Evals (CampusX) · **Video:** [Video 04](https://youtu.be/DcZ-XCk-O_M?si=ehsCxFz4L9Y0DznO) · **Watched:** 2026-07-04

## TL;DR
Failures in an LLM application happen at different levels (a component, a workflow, or the whole app) and take different forms (bad quality, unsafe, or operationally broken). A single end-to-end eval collapses all of that into one pass/fail number — it can't tell you *where* or *what kind* of thing broke. That's the actual reason you need multiple, targeted eval pipelines instead of one.

## Core Concepts

**Failure Points/Target — *where* a failure can happen:**
- **Component** — a single piece of the system: prompt, retriever, reranker, query rewriter, embedding model, vector database, output parser, tool selector, memory, guardrails.
- **Workflow** — a chain of components working together for a specific job: RAG workflow, agent workflow, multi-turn conversation workflow, structured-output workflow, document-extraction workflow.
- **Entire Application** — the whole product, end-to-end.

These three map directly onto the LLM Application diagram from [[02-model-vs-application-evals.md]]: a component eval checks one block (say, just the retrieval system) in isolation; a workflow eval checks several blocks chained together (retrieval + embedding + reranker = the RAG workflow); an application eval checks the whole diagram at once.

**Risk Categories — *what kind* of failure it is, regardless of where it happens:**
- **Application quality** — "Is the answer any good?" Correct, relevant, complete, follows instructions. This is the core "does it work" question — the reason the product exists.
- **Safety** — "Could the answer cause harm?" Toxic/dangerous content, bias against groups, leaking private data, getting tricked into breaking its own rules. Not about whether the answer is *good* — a factually correct, well-written answer can still be unsafe.
- **Operational** — "Is it fast, cheap, and reliable enough to run?" Latency, cost, not crashing under real traffic. Not about what the answer says at all — about whether the system producing it is practical to operate at scale.

Instructor's own dividing line, worth keeping verbatim: *quality is about the content of the answer, safety is about the harm the answer could do, and operational is about the system producing it.*

**The full criteria checklist** (concrete list to pull from when defining success criteria for any project — ties directly to [[03-complete-eval-workflow.md]] step 2, "Define a Success Criteria"):

- *Application quality* — breaks down by what the app actually does:
  - Core generation (any LLM app): correctness/accuracy, relevance, completeness, instruction following.
  - RAG-specific: context relevance, retrieval recall, groundedness/faithfulness, citation accuracy.
  - Agent/tool-use: tool selection, parameter correctness, task completion, error recovery.
  - Multi-turn conversation: context retention/memory, clarification behavior.
- *Safety*: toxicity, harmful content, bias/fairness, PII leakage, prompt injection/jailbreak resistance.
- *Operational*: end-to-end latency, cost per request, token efficiency, error/failure rate, latency under load.

**Why "multiple pipelines," not one:** one blended end-to-end eval can only tell you pass or fail overall. If it fails, you don't know whether it's a quality, safety, or operational problem, or which component/workflow caused it. Separate pipelines built around each failure point × risk category combination are what actually let you localize a failure instead of just detecting that *something* is wrong.

## How This Connects
- [[01-why-llm-evals.md]] — the "multi-dimensional metrics" mentioned there (factuality, groundedness, correctness, latency, cost) are specific entries in this taxonomy: correctness/groundedness sit under Application quality, latency/cost sit under Operational.
- [[02-model-vs-application-evals.md]] — the application-eval example questions there (faithful to context, avoid hallucinating policies, respond quickly, stay safe) each land in one of these three risk categories; the LLM Application diagram's blocks are the "Component" failure points.
- [[03-complete-eval-workflow.md]] — this taxonomy is exactly what you'd choose from at the "Define a Success Criteria" step, before building the dataset.
- Added to [`_meta/glossary.md`](../../../_meta/glossary.md): *Failure Points (Component/Workflow/Application)*, *Risk Categories (Application quality/Safety/Operational)*.

## Self-Test
- What's the difference between a "component" failure and a "workflow" failure? Give an example of each in a RAG app.
- An answer is factually correct but explains how to pick a lock. Which risk category does that fail under, and why isn't it a quality problem?
- Why doesn't one end-to-end eval pipeline cover an LLM application well enough?
- Name two criteria specific to agent/tool-use quality that wouldn't apply to a plain Q&A bot.
