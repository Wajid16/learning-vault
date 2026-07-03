# Glossary

Shared concepts that show up across more than one course. Defined once here; individual notes link back instead of re-explaining.

Format: `**Term** — definition. First seen in: [course/note](link).`

**Vibe testing** — casually trying an LLM app on a handful of prompts and judging by feel. Informal, subjective, not repeatable; only holds up at personal-project scale. First seen in: [llm-evals/notes/01-why-llm-evals.md](../llm-evals/notes/01-why-llm-evals.md).

**Deterministic vs. probabilistic systems** — traditional software gives the same output for the same input every time (testable with fixed pass/fail cases); LLMs can give different outputs for the same input, so evaluation has to work differently (statistical/aggregate, not one-shot pass/fail). First seen in: [llm-evals/notes/01-why-llm-evals.md](../llm-evals/notes/01-why-llm-evals.md).

**Groundedness / faithfulness (RAG)** — whether a generated answer actually stays tied to the retrieved context, rather than hallucinating something not supported by it. One of several axes (alongside factuality, relevance, latency, cost) used to judge a RAG app, since no single correctness check is enough. First seen in: [llm-evals/notes/01-why-llm-evals.md](../llm-evals/notes/01-why-llm-evals.md).

**Model Evals** — evaluating the raw capability of a foundation model itself (reasoning, knowledge, maths, coding, instruction-following, long-context, multimodal, tool-use), independent of any product built on top of it. First seen in: [llm-evals/notes/02-model-vs-application-evals.md](../llm-evals/notes/02-model-vs-application-evals.md).

**Application Evals** — evaluating the behavior of an entire LLM-powered application (or a component within it) — does the product actually work, not just "can the model do this." First seen in: [llm-evals/notes/02-model-vs-application-evals.md](../llm-evals/notes/02-model-vs-application-evals.md).

**Benchmark (LLM)** — a standardized test set used to score a model capability, e.g. MMLU (knowledge/reasoning), GSM8K (maths), HumanEval/SWE-bench (coding), IFEval (instruction-following), Needle-in-a-Haystack (long context), MMMU (multimodal). Used for model evals, not application evals. First seen in: [llm-evals/notes/02-model-vs-application-evals.md](../llm-evals/notes/02-model-vs-application-evals.md).
