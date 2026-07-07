# What is Agentic AI? (Characteristics + Components)

**Course:** LangGraph (CampusX) · **Video:** [Video 02](https://youtu.be/GWnSsjT4V68?si=514IYILWNX4CMLgv) · **Watched:** 2026-07-07

## TL;DR
Formalizes what [[01-genai-vs-agentic-ai]] introduced intuitively: Agentic AI is a system that takes a goal and works toward it on its own, with minimal human guidance. Every agentic system can be checked against six characteristics and is architecturally built from five recurring components — this note is the vocabulary the rest of the course builds on.

## Core Concepts

- **Formal definition** — "AI that can take up a task/goal from a user and then work towards completing it on its own with minimal human guidance. It plans, takes action, adapts to changes, and seeks help only when necessary." (Same HR-recruiter-hiring-a-backend-engineer example from [[01-genai-vs-agentic-ai]] is reused here to walk through this — not repeated in this note.)

- **Six characteristics** — the test for "is this system actually agentic?":
  1. **Autonomy** — makes decisions/takes actions to reach a goal without step-by-step human instructions; shows up at multiple levels (execution order, decision-making like shortlisting criteria, tool choice). Because unrestricted autonomy is risky (e.g. an agent could roll out an incorrect offer, show hiring bias, or spend budget on ads unsupervised), it's deliberately *controlled* via: scoped permissions (limit which tools/actions it can use independently), human-in-the-loop checkpoints (approval required before risky steps), override controls (user can stop/pause/redirect anytime), and guardrails/policies (hard rules, e.g. "never schedule interviews on weekends").
  2. **Goal-oriented** — operates with a persistent objective directing all its actions, rather than reacting to isolated prompts. Goals can be independent ("hire a backend engineer") or constrained (remote-only, budget cap, location). Goals live in the agent's memory (conceptually: goal + constraints + status + progress-so-far, e.g. JD drafted / posted / N applicants / interviews scheduled) and can be altered mid-way (e.g. switching from "hire an engineer" to "find a freelancer"), which then reshapes the whole plan.
  3. **Planning** — arguably the most important trait. Any agentic system operates in exactly two steps: **plan**, then **execute** — and this loop is iterative (if a step turns out to be infeasible mid-execution, the agent re-plans). Planning itself is a 3-step process: (a) generate *multiple candidate plans* (planning is treated as a search problem — many paths from an initial state to the goal state), (b) evaluate them on efficiency, tool availability, cost, risk, and alignment with constraints, (c) select the best one — either via human-in-the-loop input or a pre-programmed policy.
  4. **Reasoning** — the cognitive process of interpreting information, drawing conclusions, and making decisions — needed in *both* planning (goal decomposition into sub-steps, tool selection, estimating resources/time/risk) and execution (choosing between options mid-task, deciding when to escalate to a human, handling tool errors/failures by finding an alternate path).
  5. **Adaptability** — modifying plans/strategies/actions in response to unexpected conditions while staying aligned with the goal. Triggers: tool/execution failures (e.g. a calendar API is down, so it asks the human directly instead), external feedback from the environment (e.g. too few job applicants), or the goal itself changing mid-way.
  6. **Context awareness** — retaining and using relevant info across a multi-step, multi-day process: the original goal, progress so far, conversation history, environment state, tool responses, user preferences, and guardrails. Without this, the agent can't function across sessions (asking "which job post?" four days later defeats the purpose). Implemented via **memory** — short-term (current session: recent messages, tool call results) vs. long-term (persists across sessions: goals, preferences, past decisions, guardrails).

- **Five architectural components** (present in nearly every agentic AI application):
  1. **Brain** — the LLM. Does the heavy lifting: interprets the goal, plans, reasons, decides which tool to use, generates/understands natural language for human communication.
  2. **Orchestrator** — executes the plan step by step (sequencing, conditional routing based on a prior step's output, retry logic on failure, looping, delegating a given step to the LLM vs. a human). Described as the agent's "nervous system" / project manager — this is what a framework like LangGraph, CrewAI, or AutoGen actually gives you classes to build.
  3. **Tools** — how the agent acts on the external world: API calls, database writes, sending email. A RAG knowledge base counts as a tool too (retrieving factual/domain-specific info to ground responses). Described as the agent's "hands and legs."
  4. **Memory** — same short-term/long-term split as context awareness above, plus **state tracking** (how much of the plan is done vs. remaining).
  5. **Supervisor** — implements human-in-the-loop: requests approval before high-risk actions (e.g. sending an offer letter, spending on ads), enforces guardrails, and escalates edge cases a guardrail didn't anticipate (e.g. a strong candidate who doesn't meet a stated hard filter).

## How This Connects
- Builds directly on [[01-genai-vs-agentic-ai]] — that note's reactive-vs-proactive distinction is characteristic #1 (autonomy) and #2 (goal-oriented) here, formalized.
- Added to [`_meta/glossary.md`](../../_meta/glossary.md): **Agentic AI (formal definition)**, **Short-term vs. long-term memory (agents)** — memory implementation gets a full dedicated treatment later in this course.

## Self-Test
- An agent re-plans mid-execution because step 4 turned out to be infeasible. Which two characteristics does this demonstrate, and why is planning described as a "loop" rather than a one-shot step?
- Give an example (not from the video) of a guardrail vs. a human-in-the-loop checkpoint — what's the structural difference between the two ways of controlling autonomy?
- Which of the five components would you touch to change *how* a failed tool call gets retried — and which one decides *whether* a human needs to approve the retry?

---
