# Glossary

Shared concepts that show up across more than one course. Defined once here; individual notes link back instead of re-explaining.

Format: `**Term** — definition. First seen in: [course/note](link).`

**Vibe testing** — casually trying an LLM app on a handful of prompts and judging by feel. Informal, subjective, not repeatable; only holds up at personal-project scale. First seen in: [llm-evals/notes/01-why-llm-evals.md](../llm-evals/notes/01-why-llm-evals.md).

**Deterministic vs. probabilistic systems** — traditional software gives the same output for the same input every time (testable with fixed pass/fail cases); LLMs can give different outputs for the same input, so evaluation has to work differently (statistical/aggregate, not one-shot pass/fail). First seen in: [llm-evals/notes/01-why-llm-evals.md](../llm-evals/notes/01-why-llm-evals.md).

**Groundedness / faithfulness (RAG)** — whether a generated answer actually stays tied to the retrieved context, rather than hallucinating something not supported by it. One of several axes (alongside factuality, relevance, latency, cost) used to judge a RAG app, since no single correctness check is enough. First seen in: [llm-evals/notes/01-why-llm-evals.md](../llm-evals/notes/01-why-llm-evals.md).
