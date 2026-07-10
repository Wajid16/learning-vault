# Generative AI vs Agentic AI

**Course:** LangGraph (CampusX) · **Video:** [Video 01](https://youtu.be/xdA0pGDiUPE?si=UrPo3FFiKw-JLDGY) · **Watched:** 2026-07-07

## TL;DR
Generative AI creates content; Agentic AI achieves goals. The instructor makes this concrete by solving one HR-hiring problem four times — plain chatbot → RAG chatbot → tool-augmented chatbot → agentic AI — with each version fixing one weakness of the last, until what's left standing is proactive, memory-aware, and self-correcting instead of just reactive.

## Core Concepts

- **Generative AI (definition)** — a class of AI models that create new content (text, image, audio, code, video) resembling human-created data. Mechanically: it learns the *distribution* of the training data (e.g. "what do cats look like in general") so it can sample something new from that distribution — rather than learning an input→output mapping.

- **Traditional AI vs. Generative AI** — traditional AI (classification, regression) is given input+output pairs and learns the *relationship* between them, so it can predict an output for a new input (spam detection, cancer-from-X-ray, stock price). Generative AI is given data and learns the *shape/nature of the data itself*, so it can generate a plausible new sample from that same shape. This is the fundamental split — not "which is smarter" but "pattern-mapping vs. distribution-learning."

- **GenAI application areas** (from the video, not exhaustive) — creative/business writing (blog drafts, formal emails), software development (autocomplete, debugging), customer support (chatbots handling scale that human agents can't), education (doubt-clearing, personalized curricula), design (thumbnails, infographics, ad clips). The common thread: GenAI mimics human creative output convincingly enough to be dropped directly into these workflows.

- **The four-stage HR recruiter example** (the instructor's core teaching device — one running scenario, evolved step by step): Task = hire a backend engineer, broken into: draft JD → post to job platforms → shortlist applicants → schedule interviews → conduct interviews → send offer → onboard.

  1. **Plain LLM chatbot** — helps at every step (drafts the JD, suggests platforms, gives generic shortlisting/interview-question advice, drafts the offer letter), but: advice is *generic* (not specific to this company), it has *no memory* (forgets the JD three days later), and it can't *act* — it can draft an email but not send it, draft a JD but not post it. All of this is on the human to execute manually.

  2. **RAG-based chatbot** — improvement: connect the chatbot to the company's own knowledge base (past JD templates, hiring playbook, internal salary bands, past interview question banks, offer-letter/welcome-email templates). Now its advice is *company-specific* instead of generic. Still reactive (only responds when asked), still no memory across sessions, still can't take actions itself.

  3. **Tool-augmented chatbot** — improvement: integrate tools/APIs (LinkedIn API, resume-parser tool, calendar API, email API, HRMS software). Now it can *act*: post the JD itself, pull and screen resumes itself, check calendar availability and send interview invites itself, send the offer letter itself, trigger onboarding itself. Still reactive though — the human has to prompt every single step ("check applications," "shortlist them," "schedule the interview").

  4. **Agentic AI** — the final improvement is giving it a *goal* instead of step-by-step instructions ("I want to hire a backend engineer" — full stop). From that one goal it plans the entire sequence itself, executes each step, and — critically — *monitors and adapts*: e.g. it notices applications are far below expectation on its own, proposes broadening the JD to full-stack and boosting the LinkedIn post, and only asks for approval rather than waiting to be told there's a problem. The human's role shrinks to giving approvals; the system does the planning, execution, and course-correction.

- **What separates Agentic AI from the earlier stages** — three properties, each mapped to a stage that lacked it: **proactive** (sets its own goal-driven plan, vs. reactive = waits to be told each next step), **context-aware** (has memory of what it already did and why, vs. forgetting between sessions), **adaptable** (notices when a path isn't working and proposes an alternate one, vs. only doing exactly what's asked).

- **Generative AI vs. Agentic AI — the three closing distinctions:**
  1. GenAI's end goal is *producing content*; Agentic AI's end goal is *achieving a goal*, via planning + step-by-step execution.
  2. GenAI is *reactive* (human drives every step); Agentic AI is *proactive/autonomous* (human mostly just approves).
  3. GenAI is a **building block of** Agentic AI, not a separate competing thing — agentic systems use LLMs (a GenAI element) internally to do their planning and reasoning. One memorable framing from the video: *"Generative AI is a capability, Agentic AI is a behavior."*

## How This Connects
- [[../../llm-evals/notes/01-why-llm-evals.md]] — that note's "vibe testing" and eval concepts apply once you're building agentic systems too: an agent that plans and acts autonomously is *harder* to evaluate than a plain chatbot, since failures can compound across planning + tool-use steps, not just one generated answer.
- Added to [`_meta/glossary.md`](../../../_meta/glossary.md): **RAG (Retrieval-Augmented Generation)**, **Reactive vs. Proactive (AI systems)** — both will resurface across the `rag` and `langchain` courses.

## Self-Test
- Why can the RAG-based chatbot still not be called "agentic," even though its advice is now company-specific and clearly better than the plain chatbot's?
- What's the actual difference between the tool-augmented chatbot and the agentic one, given that both can send emails, post jobs, and hit APIs on their own?
- Someone says "Agentic AI is just Generative AI with extra steps." Using the "capability vs. behavior" framing, explain what's wrong with that statement.

---
