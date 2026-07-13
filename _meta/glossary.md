# Glossary

Shared concepts that show up across more than one course. Defined once here; individual notes link back instead of re-explaining.

Format: `**Term** — definition. First seen in: [course/note](link).`

**Vibe testing** — casually trying an LLM app on a handful of prompts and judging by feel. Informal, subjective, not repeatable; only holds up at personal-project scale. First seen in: [llm-evals/notes/01-why-llm-evals.md](../03-ai-engineer/llm-evals/notes/01-why-llm-evals.md).

**Deterministic vs. probabilistic systems** — traditional software gives the same output for the same input every time (testable with fixed pass/fail cases); LLMs can give different outputs for the same input, so evaluation has to work differently (statistical/aggregate, not one-shot pass/fail). First seen in: [llm-evals/notes/01-why-llm-evals.md](../03-ai-engineer/llm-evals/notes/01-why-llm-evals.md).

**Groundedness / faithfulness (RAG)** — whether a generated answer actually stays tied to the retrieved context, rather than hallucinating something not supported by it. One of several axes (alongside factuality, relevance, latency, cost) used to judge a RAG app, since no single correctness check is enough. First seen in: [llm-evals/notes/01-why-llm-evals.md](../03-ai-engineer/llm-evals/notes/01-why-llm-evals.md).

**Model Evals** — evaluating the raw capability of a foundation model itself (reasoning, knowledge, maths, coding, instruction-following, long-context, multimodal, tool-use), independent of any product built on top of it. First seen in: [llm-evals/notes/02-model-vs-application-evals.md](../03-ai-engineer/llm-evals/notes/02-model-vs-application-evals.md).

**Application Evals** — evaluating the behavior of an entire LLM-powered application (or a component within it) — does the product actually work, not just "can the model do this." First seen in: [llm-evals/notes/02-model-vs-application-evals.md](../03-ai-engineer/llm-evals/notes/02-model-vs-application-evals.md).

**Benchmark (LLM)** — a standardized test set used to score a model capability, e.g. MMLU (knowledge/reasoning), GSM8K (maths), HumanEval/SWE-bench (coding), IFEval (instruction-following), Needle-in-a-Haystack (long context), MMMU (multimodal). Used for model evals, not application evals. First seen in: [llm-evals/notes/02-model-vs-application-evals.md](../03-ai-engineer/llm-evals/notes/02-model-vs-application-evals.md).

**Eval method (automated / human / LLM-as-judge)** — the three ways an output can be scored against expected results: a script/code check (automated), a person reviewing it (human), or another LLM scoring it (LLM-as-judge). Choice depends on how objectively checkable the task is. First seen in: [llm-evals/notes/03-complete-eval-workflow.md](../03-ai-engineer/llm-evals/notes/03-complete-eval-workflow.md).

**Failure Points (Component / Workflow / Application)** — the three levels of granularity a failure can occur at: a single component (retriever, prompt, guardrails...), a workflow chaining components together (RAG workflow, agent workflow...), or the entire application end-to-end. First seen in: [llm-evals/notes/04-failure-points-and-risk-categories.md](../03-ai-engineer/llm-evals/notes/04-failure-points-and-risk-categories.md).

**Risk Categories (Application quality / Safety / Operational)** — the three kinds of thing that can go wrong in an LLM app, independent of where: quality (is the answer good?), safety (could it cause harm?), operational (is it fast/cheap/reliable enough to run?). First seen in: [llm-evals/notes/04-failure-points-and-risk-categories.md](../03-ai-engineer/llm-evals/notes/04-failure-points-and-risk-categories.md).

**RAG (Retrieval-Augmented Generation)** — connecting an LLM to an external knowledge base (documents, past records, templates) so its answers are grounded in that specific data instead of generic training knowledge. First seen in: [langgraph/notes/01-genai-vs-agentic-ai.md](../03-ai-engineer/langgraph/notes/01-genai-vs-agentic-ai.md).

**Reactive vs. Proactive (AI systems)** — reactive means the system only responds when a human explicitly prompts each step; proactive means it plans and initiates the next step itself once given a goal. The reactive→proactive shift is the key marker separating plain/RAG/tool-augmented chatbots from agentic AI. First seen in: [langgraph/notes/01-genai-vs-agentic-ai.md](../03-ai-engineer/langgraph/notes/01-genai-vs-agentic-ai.md).

**Agentic AI (formal definition)** — AI that takes a goal from a user and works toward completing it on its own with minimal human guidance: it plans, takes action, adapts to changes, and seeks help only when necessary. Checked against six characteristics (autonomy, goal-oriented, planning, reasoning, adaptability, context awareness). First seen in: [langgraph/notes/02-what-is-agentic-ai.md](../03-ai-engineer/langgraph/notes/02-what-is-agentic-ai.md).

**Short-term vs. long-term memory (agents)** — short-term memory holds current-session info (recent messages, tool call results); long-term memory persists across sessions (goals, user preferences, past decisions, guardrails). Together they implement an agent's context awareness. First seen in: [langgraph/notes/02-what-is-agentic-ai.md](../03-ai-engineer/langgraph/notes/02-what-is-agentic-ai.md).

**Workflow vs. Agent (Anthropic's distinction)** — a workflow orchestrates LLMs/tools through a predefined, developer-designed code path (static, same order every run); an agent is a system where the LLM dynamically directs its own process and tool use. Many "agentic-looking" systems (e.g. a flowchart-driven hiring pipeline) are actually workflows, not agents. First seen in: [langgraph/notes/03-langchain-vs-langgraph.md](../03-ai-engineer/langgraph/notes/03-langchain-vs-langgraph.md).

**Checkpointing (LangGraph)** — saving a snapshot of a workflow's state after each node's execution, so the workflow can pause indefinitely (for an external trigger or human input) or recover after a crash by resuming from the last saved node instead of restarting from scratch. First seen in: [langgraph/notes/03-langchain-vs-langgraph.md](../03-ai-engineer/langgraph/notes/03-langchain-vs-langgraph.md).

**LLM Workflow patterns** — five recurring shapes LLM-based workflows take: prompt chaining (sequential LLM calls), routing (an LLM classifies/dispatches to a handler), parallelization (independent subtasks run concurrently, then aggregated), orchestrator-workers (like parallelization, but an orchestrator LLM decides subtask nature dynamically per input), and evaluator-optimizer (generator + evaluator LLMs loop until output passes criteria). First seen in: [langgraph/notes/04-langgraph-core-concepts.md](../03-ai-engineer/langgraph/notes/04-langgraph-core-concepts.md).

**Reducer (state update policy)** — defines how a node's update to a given state key is applied: replace (default), add/append, or merge. Getting this wrong silently breaks things — e.g. a chatbot's message history needs "append," not "replace," or earlier context is lost. First seen in: [langgraph/notes/04-langgraph-core-concepts.md](../03-ai-engineer/langgraph/notes/04-langgraph-core-concepts.md).

**Structured Output (LLM)** — constraining an LLM's response to match a predefined schema (e.g. a Pydantic model) instead of relying on free-form text, so downstream code can reliably parse fields (like a numeric score) without occasional format drift breaking things. First seen in: [langgraph/notes/06-parallel-workflows-code.md](../03-ai-engineer/langgraph/notes/06-parallel-workflows-code.md) (originally taught in the LangChain playlist).

**Conditional Workflow (routing function)** — a workflow shape where multiple candidate next-nodes fan out from one source, but a routing function picks exactly one to execute per run based on a condition — the graph equivalent of if/elif/else. Differs from a parallel workflow, where all the fanned-out nodes execute simultaneously. First seen in: [langgraph/notes/07-conditional-workflows-code.md](../03-ai-engineer/langgraph/notes/07-conditional-workflows-code.md).

**Message types (BaseMessage hierarchy)** — `SystemMessage` (sets an LLM's role), `HumanMessage` (user input), `AIMessage` (model output), `ToolMessage` (a tool call's result) all inherit from a shared `BaseMessage` type. A state field typed `list[BaseMessage]` can hold any mix of these. First seen in: [langgraph/notes/09-chatbot-memory-bug.md](../03-ai-engineer/langgraph/notes/09-chatbot-memory-bug.md) (originally taught in the LangChain playlist).

**Persistence / Checkpointer (LangGraph)** — saving a graph's state (via a "checkpointer" object) so it survives past a single `invoke()` call and can be reloaded on the next one. A checkpoint is saved once per superstep (see [[04-langgraph-core-concepts]]), not just at the end, and each is tagged with a "thread" (one ongoing conversation/session, via `thread_id`) so different runs don't mix. Three tiers: `InMemorySaver` (RAM, wiped on restart — demos only), `SqliteSaver` (file-based DB — prototyping), a Postgres-backed saver (production). Without persistence, every `invoke()` starts from a blank state — which looks like the app "forgetting" everything between turns. This one mechanism underlies four features: chatbot short-term memory, fault tolerance (resume after a crash via `invoke(None, ...)`), human-in-the-loop (deliberate pause/resume), and time travel. First seen in: [langgraph/notes/09-chatbot-memory-bug.md](../03-ai-engineer/langgraph/notes/09-chatbot-memory-bug.md), deep dive in [langgraph/notes/10-persistence-deep-dive.md](../03-ai-engineer/langgraph/notes/10-persistence-deep-dive.md), durable storage in [langgraph/notes/14-sqlite-persistent-storage.md](../03-ai-engineer/langgraph/notes/14-sqlite-persistent-storage.md).

**Time Travel (LangGraph)** — rewinding to a specific past checkpoint (by `checkpoint_id`) and replaying execution forward from there, optionally editing the state first via `update_state`. Useful for debugging a complex workflow; each replay creates a new branch in the checkpoint history rather than overwriting the original. First seen in: [langgraph/notes/10-persistence-deep-dive.md](../03-ai-engineer/langgraph/notes/10-persistence-deep-dive.md).

**Streamlit rerun model + `session_state`** — Streamlit re-executes the entire script top-to-bottom on every user interaction, so any plain variable resets each time; only `st.session_state` (a dict that survives reruns, cleared only on manual page refresh) can hold state like conversation history across turns. First seen in: [langgraph/notes/11-streamlit-ui-for-chatbot.md](../03-ai-engineer/langgraph/notes/11-streamlit-ui-for-chatbot.md).

**Streaming (LLM apps)** — sending an LLM's output token-by-token as it's generated instead of waiting for the full response, giving a typewriter effect. Improves perceived speed, feels more conversational, is essential for voice UIs, reads better for long structured output like code, lets a user interrupt (saving tokens/cost), and can also surface an agent's step-by-step progress rather than just chat text. In LangGraph: `graph.stream(state, config, stream_mode="messages")` returns a generator of `(message_chunk, metadata)` pairs. First seen in: [langgraph/notes/12-streaming-chatbot-responses.md](../03-ai-engineer/langgraph/notes/12-streaming-chatbot-responses.md).

**Containerization** — packaging an application together with everything it needs to run (code, runtime, libraries, config) into a single portable, isolated unit called a container, so it behaves identically across dev/test/prod machines instead of breaking on environment differences (OS, library versions). Lighter weight than a VM since a container doesn't carry a full guest OS. First seen in: [docker/notes/01-docker-fundamentals.md](../04-deployment/docker/notes/01-docker-fundamentals.md).

**Context (LLM)** — everything an AI can see when generating a response: conversation history, external documents, code, schemas, whatever's fed in. In simple chat it's just the conversation so far; in real professional work it's scattered across many systems (tickets, codebase, database schema, docs, chat threads) rather than sitting in one place — that scattering is the core problem MCP (Model *Context* Protocol) is named after. First seen in: [mcp/notes/02-the-why-context-and-integration-problem.md](../03-ai-engineer/mcp/notes/02-the-why-context-and-integration-problem.md).

**Function Calling / Tool Calling** — letting an LLM invoke a predefined external function (given a name, description, and arguments) instead of only generating text, so it can complete a task (fetch a file, query a database, hit an API) rather than just talk about it. Introduced by OpenAI, mid-2023. At scale it creates an N×M integration problem — N AI clients × M services requires N×M hand-written functions, each with its own auth, data-format handling, and error handling. First seen in: [mcp/notes/02-the-why-context-and-integration-problem.md](../03-ai-engineer/mcp/notes/02-the-why-context-and-integration-problem.md).

**MCP (Model Context Protocol)** — a standardized client-server protocol (from Anthropic) connecting an AI chatbot (the "client": Claude, ChatGPT, Cursor, Perplexity...) to external services (the "server": GitHub, Google Drive, Slack...). Unlike plain function/tool calling, the **server** does all the heavy lifting — business logic, auth, rate limiting, data-format translation, error handling — so the client just connects and speaks the shared protocol, no custom integration code. Turns the N×M integration problem into N+M, and shifts even that N+M work onto service providers rather than every AI-client builder repeating it. First seen in: [mcp/notes/02-the-why-context-and-integration-problem.md](../03-ai-engineer/mcp/notes/02-the-why-context-and-integration-problem.md).

**API (Application Programming Interface)** — a standardized software connector that allows two different applications to communicate using a defined set of rules, protocols, and data formats. First seen in: [fastapi/notes/01-what-is-an-api.md](../04-deployment/fastapi/notes/01-what-is-an-api.md).

**ASGI (Asynchronous Server Gateway Interface)** — a modern standard interface for asynchronous Python web applications and servers, allowing concurrent and non-blocking request handling. First seen in: [fastapi/notes/02-fastapi-philosophy-and-setup.md](../04-deployment/fastapi/notes/02-fastapi-philosophy-and-setup.md).

**WSGI (Web Server Gateway Interface)** — a legacy standard interface for synchronous Python web applications, processing requests in a blocking, one-at-a-time manner. First seen in: [fastapi/notes/02-fastapi-philosophy-and-setup.md](../04-deployment/fastapi/notes/02-fastapi-philosophy-and-setup.md).

**Uvicorn** — a lightning-fast ASGI web server implementation used to run asynchronous Python applications (like FastAPI). First seen in: [fastapi/notes/02-fastapi-philosophy-and-setup.md](../04-deployment/fastapi/notes/02-fastapi-philosophy-and-setup.md).

**CRUD (Create, Read, Update, Delete)** — the four fundamental actions representing data storage interactions in persistent dynamic systems. First seen in: [fastapi/notes/03-http-methods-and-project-setup.md](../04-deployment/fastapi/notes/03-http-methods-and-project-setup.md).

**HTTP Methods** — standardized request verbs (e.g., GET, POST, PUT, DELETE) used in the HTTP protocol to inform a web server of the action a client wants to perform. First seen in: [fastapi/notes/03-http-methods-and-project-setup.md](../04-deployment/fastapi/notes/03-http-methods-and-project-setup.md).

**Path Parameter** — dynamic segment of an API endpoint path (URL) used to target and uniquely identify a specific resource. First seen in: [fastapi/notes/04-path-and-query-parameters.md](../04-deployment/fastapi/notes/04-path-and-query-parameters.md).

**Query Parameter** — optional key-value pair appended to the end of a URL after a question mark (`?`) to sort, filter, search, or paginate a list of resources. First seen in: [fastapi/notes/04-path-and-query-parameters.md](../04-deployment/fastapi/notes/04-path-and-query-parameters.md).

**HTTP Status Code** — standard 3-digit code returned by the server (e.g., 200, 400, 404, 500) indicating the execution result of an HTTP request. First seen in: [fastapi/notes/04-path-and-query-parameters.md](../04-deployment/fastapi/notes/04-path-and-query-parameters.md).

**Dynamic Typing** — A programming language feature where variable data types are evaluated and assigned at runtime based on their value, rather than compile time. First seen in: [python/notes/01-python-fundamentals.md](../00-prerequisites/python/notes/01-python-fundamentals.md).

**Dynamic Binding** — The ability of a variable name to reference objects of different data types at different points during program execution. First seen in: [python/notes/01-python-fundamentals.md](../00-prerequisites/python/notes/01-python-fundamentals.md).

**Type Conversion** — The process of converting a value from one data type to another, either automatically by the interpreter (implicit) or manually by the programmer (explicit casting). First seen in: [python/notes/01-python-fundamentals.md](../00-prerequisites/python/notes/01-python-fundamentals.md).

**Floor Division (`//`)** — A division operation that truncates the decimal part of the result, returning the floor integer. First seen in: [python/notes/02-operators-if-else-loops.md](../00-prerequisites/python/notes/02-operators-if-else-loops.md).

**Membership Operators** — Optimized symbols (`in` / `not in`) used to verify containment of a value inside an iterable structure. First seen in: [python/notes/02-operators-if-else-loops.md](../00-prerequisites/python/notes/02-operators-if-else-loops.md).

**Module** — A Python file containing functions, variables, and classes designed for import and code reuse across different scripts. First seen in: [python/notes/02-operators-if-else-loops.md](../00-prerequisites/python/notes/02-operators-if-else-loops.md).

**while-else loop** — A Python-specific loop construct whose `else` block executes only when the loop terminates naturally without hitting a `break`. First seen in: [python/notes/02-operators-if-else-loops.md](../00-prerequisites/python/notes/02-operators-if-else-loops.md).

**Immutability** — A memory management constraint preventing in-place modifications to an object (e.g. Python strings) after creation. First seen in: [python/notes/03-python-strings.md](../00-prerequisites/python/notes/03-python-strings.md).

**Lexicographical Comparison** — The alphabetical comparison of strings based on the numeric Unicode values of their characters. First seen in: [python/notes/03-python-strings.md](../00-prerequisites/python/notes/03-python-strings.md).

**Short-Circuit Evaluation** — A logical operator behavior where evaluation stops as soon as the overall truth value is determined. First seen in: [python/notes/03-python-strings.md](../00-prerequisites/python/notes/03-python-strings.md).

**Referential Array** — A memory layout model that stores pointers/addresses contiguously in a list container while the actual objects are stored dynamically elsewhere in memory. First seen in: [python/notes/04-python-lists.md](../00-prerequisites/python/notes/04-python-lists.md).

**List Comprehension** — An optimized Python builder syntax that generates list objects from iterables in a single line. First seen in: [python/notes/04-python-lists.md](../00-prerequisites/python/notes/04-python-lists.md).

**Shallow Copy** — A copy operation that constructs a new container but references the same inner child elements as the original. First seen in: [python/notes/04-python-lists.md](../00-prerequisites/python/notes/04-python-lists.md).



