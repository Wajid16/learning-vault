# Why LLM Evals?

**Course:** LLM Evals (CampusX) · **Video:** [Video 01](https://youtu.be/6W92_t9FveA?si=XOZO1XTmHdykl988) · **Watched:** 2026-07-03

## TL;DR
An AI engineer builds products on top of foundation models (LLMs) rather than training them from scratch — and the skill that separates a working product from a demo is *evaluation*: knowing, systematically, whether the app actually works, instead of guessing from a handful of prompts.

## Core Concepts

- **AI engineer** — someone who builds applications/products on top of existing foundation models (as opposed to an ML engineer/researcher who builds or trains the models themselves).

- **Vibe testing** — trying an LLM app on 5–10 prompts, the answers "look fine," so you conclude it works. It's informal, subjective, and not repeatable — two people (or the same person on two days) can get different impressions from the same app. It only holds up at personal-project scale; it falls apart the moment real users hit the app with inputs you didn't anticipate. The video walks through real cases of production LLM apps that broke despite looking fine in casual testing — the common thread was skipping real evaluation.

- **Why evals are harder than traditional software testing** — two structural differences:
  1. **Deterministic vs. probabilistic.** Traditional software is deterministic: a given input always produces the same output (`2 + 2` is always `4`), so a test either passes or fails, permanently. An LLM is probabilistic: the *same* input can produce different outputs across calls. That also means a prompt/system that scores well on your test set can still be overfit to it — looking correct on the cases you checked without actually generalizing.
  2. **Single correctness check vs. multi-dimensional metrics.** Software testing checks one thing: is the output correct? An LLM app (e.g. a RAG system) has to be judged on several axes at once — factual accuracy, whether the answer stays grounded in the retrieved context (vs. hallucinating), answer relevance/correctness, latency, and cost — and which of these matter, and how much, changes per application. That's what makes "is it correct?" the wrong question to even ask by itself.

## How This Connects
- First note in the vault — nothing to link to yet.
- Added to [`_meta/glossary.md`](../../_meta/glossary.md): *vibe testing*, *deterministic vs. probabilistic systems*, *groundedness*. Future notes (RAG, ML) should link back here instead of re-explaining.

## Self-Test
- Why can't you "unit test" an LLM app the same way you'd unit test a normal function?
- What's wrong with "I tried 8 prompts and they all looked right, so it works"?
- Name two evaluation dimensions a RAG app needs beyond plain correctness, and why correctness alone isn't enough.

---
*Note: raw notes had a couple of metric names that came through garbled from the video audio ("tunality", "groundility") — captured here as the closest sensible RAG-eval concepts (faithfulness/groundedness). Worth a quick double-check against the video if exact terminology matters later.*
