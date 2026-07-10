# What Are LLM Evals? Model Evals vs. Application Evals

**Course:** LLM Evals (CampusX) · **Video:** [Video 02](https://youtu.be/cNF_MO82Qew?si=i6YVeBVfFzGDJApu) · **Watched:** 2026-07-03

## TL;DR
An LLM eval is a systematic, repeatable test against clear criteria — not a metric, but the whole testing setup around it. Evals split into two different questions: **model evals** ask "can the model do this in general?", **application evals** ask "does *this product* actually work?" This course is about the second one.

## Core Concepts

- **LLM Eval, properly defined** — three things have to be true, or you're just vibe-testing again ([[01-why-llm-evals.md]]):
  - **Systematic** — planned test cases, not random prompting. E.g. 100 real student doubts for a CampusX course assistant, not 5 questions you thought of on the spot.
  - **Repeatable** — the exact same eval can be re-run after you change the prompt, model, retriever, chunking strategy, or system instructions, so you can tell if the change actually helped or hurt.
  - **Clear criteria** — you've written down what "good" means *before* judging. For a course assistant: correct, simply expressed, grounded in the course content, safe/policy-compliant. No criteria = judging by vibes again, just with more test cases.

- **An eval is a setup, not a score.** It bundles: what's being evaluated, what "good" means, what test cases are used, how outputs are judged, when it runs, and which tool runs it. The score only matters because it answers a real question — can this ship, did prompt v2 beat v1, is the RAG answer grounded, is the agent finishing the task, is latency acceptable, is this safe for real users.

- **Model Evals** — test the underlying model's raw capability, independent of any product built on it: reasoning, knowledge, maths, coding, instruction-following, long-context handling, multimodal understanding, tool-use. Measured via standard benchmarks:

  | Capability | Benchmark(s) | Checks |
  |---|---|---|
  | General knowledge + reasoning | MMLU | Broad subject knowledge/reasoning across domains |
  | Maths | GSM8K | Grade-school math word problems, step-by-step reasoning |
  | Coding | HumanEval, SWE-bench | Code generation, real-world SWE issue solving |
  | Instruction following | IFEval | Following explicit constraints/formatting |
  | Long context | Needle-in-a-Haystack | Finding specific info buried in a long context |
  | Multimodal | MMMU | Reasoning over images, diagrams, charts |

  This is what frontier labs run to compare models against each other — it says nothing about whether a specific product built on the model works.

- **Application Evals** — test the behavior of the whole LLM-*powered application* (the model is just one block inside: UI, input handler, prompt layer, tools/APIs, orchestrator/workflow, guardrails/safety, output parser, context/memory, retrieval system, embedding model, vector DB, monitoring/logging, feedback loop). The question is never "can the model do this?" — it's "does the product work?" For the CampusX assistant: did it answer the student's question correctly, did it use the course material properly, was the answer faithful to the retrieved context, was it clear for a beginner, did it avoid hallucinating policies, did it respond fast enough, did it stay safe?

- **The distinction that matters:** a great model plugged into a broken retrieval step, a bad prompt, or missing guardrails still produces a bad product. Model evals tell you about the engine; application evals tell you about the car. **This course's focus is application evals** — building the product, so that's the harder and more relevant problem.

## How This Connects
- [[01-why-llm-evals.md]] — the multi-dimensional metrics mentioned there (factuality, groundedness, correctness, latency, cost) are exactly what application-eval criteria are made of; this video gives them a home (application evals) and contrasts them against the other kind of eval (model evals).
- Added to [`_meta/glossary.md`](../../../_meta/glossary.md): *Model Evals*, *Application Evals*, *Benchmark (LLM)*.

## Self-Test
- What are the three things that have to be true for something to count as an "LLM eval" rather than vibe testing?
- If a benchmark says a model scores well on MMLU, what does that tell you — and *not* tell you — about your product?
- For a RAG-based support bot, write two application-eval questions that a model eval could never answer.

---
*Note: the instructor referenced a "smartphone" analogy for model vs. application evals right at this point in the video, but it was cut off the bottom of the shared screenshot — worth adding in if you want it captured, otherwise skipping since I don't have the actual explanation.*
