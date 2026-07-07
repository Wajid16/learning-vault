# Glossary

Shared concepts that show up across more than one course. Defined once here; individual notes link back instead of re-explaining.

Format: `**Term** — definition. First seen in: [course/note](link).`

**Vibe testing** — casually trying an LLM app on a handful of prompts and judging by feel. Informal, subjective, not repeatable; only holds up at personal-project scale. First seen in: [llm-evals/notes/01-why-llm-evals.md](../llm-evals/notes/01-why-llm-evals.md).

**Deterministic vs. probabilistic systems** — traditional software gives the same output for the same input every time (testable with fixed pass/fail cases); LLMs can give different outputs for the same input, so evaluation has to work differently (statistical/aggregate, not one-shot pass/fail). First seen in: [llm-evals/notes/01-why-llm-evals.md](../llm-evals/notes/01-why-llm-evals.md).

**Groundedness / faithfulness (RAG)** — whether a generated answer actually stays tied to the retrieved context, rather than hallucinating something not supported by it. One of several axes (alongside factuality, relevance, latency, cost) used to judge a RAG app, since no single correctness check is enough. First seen in: [llm-evals/notes/01-why-llm-evals.md](../llm-evals/notes/01-why-llm-evals.md).

**Model Evals** — evaluating the raw capability of a foundation model itself (reasoning, knowledge, maths, coding, instruction-following, long-context, multimodal, tool-use), independent of any product built on top of it. First seen in: [llm-evals/notes/02-model-vs-application-evals.md](../llm-evals/notes/02-model-vs-application-evals.md).

**Application Evals** — evaluating the behavior of an entire LLM-powered application (or a component within it) — does the product actually work, not just "can the model do this." First seen in: [llm-evals/notes/02-model-vs-application-evals.md](../llm-evals/notes/02-model-vs-application-evals.md).

**Benchmark (LLM)** — a standardized test set used to score a model capability, e.g. MMLU (knowledge/reasoning), GSM8K (maths), HumanEval/SWE-bench (coding), IFEval (instruction-following), Needle-in-a-Haystack (long context), MMMU (multimodal). Used for model evals, not application evals. First seen in: [llm-evals/notes/02-model-vs-application-evals.md](../llm-evals/notes/02-model-vs-application-evals.md).

**Eval method (automated / human / LLM-as-judge)** — the three ways an output can be scored against expected results: a script/code check (automated), a person reviewing it (human), or another LLM scoring it (LLM-as-judge). Choice depends on how objectively checkable the task is. First seen in: [llm-evals/notes/03-complete-eval-workflow.md](../llm-evals/notes/03-complete-eval-workflow.md).

**Failure Points (Component / Workflow / Application)** — the three levels of granularity a failure can occur at: a single component (retriever, prompt, guardrails...), a workflow chaining components together (RAG workflow, agent workflow...), or the entire application end-to-end. First seen in: [llm-evals/notes/04-failure-points-and-risk-categories.md](../llm-evals/notes/04-failure-points-and-risk-categories.md).

**Risk Categories (Application quality / Safety / Operational)** — the three kinds of thing that can go wrong in an LLM app, independent of where: quality (is the answer good?), safety (could it cause harm?), operational (is it fast/cheap/reliable enough to run?). First seen in: [llm-evals/notes/04-failure-points-and-risk-categories.md](../llm-evals/notes/04-failure-points-and-risk-categories.md).

**RAG (Retrieval-Augmented Generation)** — connecting an LLM to an external knowledge base (documents, past records, templates) so its answers are grounded in that specific data instead of generic training knowledge. First seen in: [langgraph/notes/01-genai-vs-agentic-ai.md](../langgraph/notes/01-genai-vs-agentic-ai.md).

**Reactive vs. Proactive (AI systems)** — reactive means the system only responds when a human explicitly prompts each step; proactive means it plans and initiates the next step itself once given a goal. The reactive→proactive shift is the key marker separating plain/RAG/tool-augmented chatbots from agentic AI. First seen in: [langgraph/notes/01-genai-vs-agentic-ai.md](../langgraph/notes/01-genai-vs-agentic-ai.md).

**Agentic AI (formal definition)** — AI that takes a goal from a user and works toward completing it on its own with minimal human guidance: it plans, takes action, adapts to changes, and seeks help only when necessary. Checked against six characteristics (autonomy, goal-oriented, planning, reasoning, adaptability, context awareness). First seen in: [langgraph/notes/02-what-is-agentic-ai.md](../langgraph/notes/02-what-is-agentic-ai.md).

**Short-term vs. long-term memory (agents)** — short-term memory holds current-session info (recent messages, tool call results); long-term memory persists across sessions (goals, user preferences, past decisions, guardrails). Together they implement an agent's context awareness. First seen in: [langgraph/notes/02-what-is-agentic-ai.md](../langgraph/notes/02-what-is-agentic-ai.md).

**Workflow vs. Agent (Anthropic's distinction)** — a workflow orchestrates LLMs/tools through a predefined, developer-designed code path (static, same order every run); an agent is a system where the LLM dynamically directs its own process and tool use. Many "agentic-looking" systems (e.g. a flowchart-driven hiring pipeline) are actually workflows, not agents. First seen in: [langgraph/notes/03-langchain-vs-langgraph.md](../langgraph/notes/03-langchain-vs-langgraph.md).

**Checkpointing (LangGraph)** — saving a snapshot of a workflow's state after each node's execution, so the workflow can pause indefinitely (for an external trigger or human input) or recover after a crash by resuming from the last saved node instead of restarting from scratch. First seen in: [langgraph/notes/03-langchain-vs-langgraph.md](../langgraph/notes/03-langchain-vs-langgraph.md).

**LLM Workflow patterns** — five recurring shapes LLM-based workflows take: prompt chaining (sequential LLM calls), routing (an LLM classifies/dispatches to a handler), parallelization (independent subtasks run concurrently, then aggregated), orchestrator-workers (like parallelization, but an orchestrator LLM decides subtask nature dynamically per input), and evaluator-optimizer (generator + evaluator LLMs loop until output passes criteria). First seen in: [langgraph/notes/04-langgraph-core-concepts.md](../langgraph/notes/04-langgraph-core-concepts.md).

**Reducer (state update policy)** — defines how a node's update to a given state key is applied: replace (default), add/append, or merge. Getting this wrong silently breaks things — e.g. a chatbot's message history needs "append," not "replace," or earlier context is lost. First seen in: [langgraph/notes/04-langgraph-core-concepts.md](../langgraph/notes/04-langgraph-core-concepts.md).

**Structured Output (LLM)** — constraining an LLM's response to match a predefined schema (e.g. a Pydantic model) instead of relying on free-form text, so downstream code can reliably parse fields (like a numeric score) without occasional format drift breaking things. First seen in: [langgraph/notes/06-parallel-workflows-code.md](../langgraph/notes/06-parallel-workflows-code.md) (originally taught in the LangChain playlist).

**Conditional Workflow (routing function)** — a workflow shape where multiple candidate next-nodes fan out from one source, but a routing function picks exactly one to execute per run based on a condition — the graph equivalent of if/elif/else. Differs from a parallel workflow, where all the fanned-out nodes execute simultaneously. First seen in: [langgraph/notes/07-conditional-workflows-code.md](../langgraph/notes/07-conditional-workflows-code.md).

**Message types (BaseMessage hierarchy)** — `SystemMessage` (sets an LLM's role), `HumanMessage` (user input), `AIMessage` (model output), `ToolMessage` (a tool call's result) all inherit from a shared `BaseMessage` type. A state field typed `list[BaseMessage]` can hold any mix of these. First seen in: [langgraph/notes/09-chatbot-memory-bug.md](../langgraph/notes/09-chatbot-memory-bug.md) (originally taught in the LangChain playlist).

**Persistence / Checkpointer (LangGraph)** — saving a graph's state (via a "checkpointer" object, e.g. `InMemorySaver` or a Postgres/Redis-backed one) so it survives past a single `invoke()` call and can be reloaded on the next one. A checkpoint is saved once per superstep (see [[04-langgraph-core-concepts]]), not just at the end, and each is tagged with a "thread" (one ongoing conversation/session, via `thread_id`) so different runs don't mix. Without it, every `invoke()` starts from a blank state — which looks like the app "forgetting" everything between turns. This one mechanism underlies four features: chatbot short-term memory, fault tolerance (resume after a crash via `invoke(None, ...)`), human-in-the-loop (deliberate pause/resume), and time travel. First seen in: [langgraph/notes/09-chatbot-memory-bug.md](../langgraph/notes/09-chatbot-memory-bug.md), deep dive in [langgraph/notes/10-persistence-deep-dive.md](../langgraph/notes/10-persistence-deep-dive.md).

**Time Travel (LangGraph)** — rewinding to a specific past checkpoint (by `checkpoint_id`) and replaying execution forward from there, optionally editing the state first via `update_state`. Useful for debugging a complex workflow; each replay creates a new branch in the checkpoint history rather than overwriting the original. First seen in: [langgraph/notes/10-persistence-deep-dive.md](../langgraph/notes/10-persistence-deep-dive.md).
