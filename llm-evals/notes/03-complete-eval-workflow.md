# How to Evaluate LLM Applications: The Complete Workflow

**Course:** LLM Evals (CampusX) · **Video:** [Video 03](https://youtu.be/Pv4mkG2K_s8?si=ypbvoQ8WsrXDkS0v) · **Watched:** 2026-07-03

## TL;DR
Evaluating an LLM application is a repeating loop, not a one-off check: define what you're building and what "good" means, build a dataset, run it through the system, score it, dig into *why* it scored that way, improve, and re-run — then keep going even after deploy, because production failures feed straight back into the dataset that started the whole loop.

## Core Concepts

The instructor walks the whole thing through a running example: an **email classifier** — an LLM wrapped in a system/workflow (orchestration around the model, not the raw model) that takes an email in and produces a classification out.

**The workflow, step by step:**

1. **Define Task & Target** — what is the system supposed to do, and what target are you aiming for? (E.g., classify incoming emails; target ~90% accuracy.)
2. **Define a Success Criteria** — pick the metric that actually represents "good" for this task. For a classifier, that's accuracy.
3. **Build a Dataset** — a set of real, representative inputs with known-correct expected outputs (e.g., a batch of emails with their correct category labels).
4. **Define an eval method** — decide *how* outputs get judged. Three options: **automated** (a script/code checks the output, e.g. exact match), **human** (a person reviews it), or **LLM** (an LLM-as-judge scores it). Which one you pick depends on how checkable the task is — a classification label is easy to check automatically; something like tone or helpfulness usually isn't.
5. **Run the model** — push the dataset through the system: `dataset → system → answers`. This produces the actual outputs to be judged, not the model in isolation ([[02-model-vs-application-evals.md]] — this is an application eval, the model is one piece of the system).
6. **Evaluate the results** — score the answers against the expected outputs using the eval method from step 4. In the example: a Python script computing accuracy, landing at 80% — short of the 90% target.
7. **Analyze the results** — don't stop at the number. Look at *which* cases failed and why, to find a fixable pattern rather than guessing.
8. **Improve the model** — act on that analysis (better prompt, better retrieval, different model, tweaked system instructions, etc.), then loop back to step 5 and re-run the same eval. This inner loop (Run → Evaluate → Analyze → Improve → Run again) repeats until the success criteria from step 2 is actually met.
9. **Deploy & Monitor** — once the loop above clears the bar, ship it — but keep watching it in production, because a passing eval score is not a guarantee.
10. **Production Failures → back into the dataset.** Real failures that show up in production don't just get patched and forgotten — they get added back into the dataset from step 3. The eval set keeps growing to cover cases you didn't think of originally, so the whole cycle starts again with a stronger dataset.

**Two loops, not one:** an inner iteration loop (steps 5→8) for improving *before* shipping, and an outer production loop (steps 9→10→3) for catching what the eval dataset missed and folding it back in. This is what makes the eval "repeatable" in the sense from [[01-why-llm-evals.md]] — not run-once-and-forget, but a living process that gets stricter over time.

## How This Connects
- [[01-why-llm-evals.md]] — "systematic, repeatable, clear criteria" is exactly steps 1–4 of this workflow, made concrete.
- [[02-model-vs-application-evals.md]] — "Run the model" here means running the whole system (dataset → system → answers), not a standalone model benchmark; this is squarely an application eval.
- Added to [`_meta/glossary.md`](../../_meta/glossary.md): *Eval method (automated / human / LLM-as-judge)*.

## Self-Test
- Name the 8 steps of the workflow in order, from "Define Task & Target" to "Production Failures."
- Why does the workflow loop back from "Improve the model" to "Run the model" instead of just moving on to Deploy?
- Where do production failures go, and why does that matter for the eval dataset over time?
- For the email classifier example: what's the success criteria, what eval method fits it, and why?
