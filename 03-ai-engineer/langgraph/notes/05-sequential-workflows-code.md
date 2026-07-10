# Building Sequential Workflows in LangGraph (First Code)

**Course:** LangGraph (CampusX) · **Video:** [Video 05](https://youtu.be/bAWujyAl1Kk?si=Xb_V96c9V8p0qd27) · **Watched:** 2026-07-07

## TL;DR
First hands-on video. The same four-step recipe — define State, define Graph (nodes + edges), compile, invoke — builds three increasingly rich examples: a non-LLM BMI calculator, a bare single-LLM-call workflow, and a prompt-chaining blog generator. The last one is the concrete payoff of everything [[04-langgraph-core-concepts]] and [[03-langchain-vs-langgraph]] argued abstractly: because state persists and accumulates, the final output exposes *every* intermediate node's result (title, outline, *and* content), not just the last step's.

## Core Concepts

- **Setup** — `pip install langgraph langchain langchain-openai python-dotenv`, API keys in a `.env` file loaded via `load_dotenv()`. Work happens in a **Jupyter notebook** specifically, not a plain `.py` file — LangGraph's graph-visualization helper only renders inline in a notebook.

- **The four-step recipe every LangGraph workflow follows:**
  1. **Define State** — a class inheriting `TypedDict`, one field per piece of data the workflow needs, each annotated with its type (e.g. `weight: float`).
  2. **Define Graph** — `StateGraph(YourState)` creates the graph object; `graph.add_node("name", function)` registers each task (every node is, under the hood, just a plain Python function that receives the current state as input and returns a state — often only a partial update); `graph.add_edge(from, to)` wires nodes together, using the special `START` and `END` markers for entry/exit.
  3. **Compile** — `graph.compile()` validates the structure (e.g. catches a node with no connecting edge) and returns a runnable workflow object.
  4. **Invoke** — `workflow.invoke(initial_state)` runs the graph end-to-end and returns the final state.

- **Non-LLM example (BMI calculator)** — deliberately has zero LLM involvement so the LangGraph syntax itself is the whole focus. One node, `calculate_bmi`, reads `weight`/`height` from state and writes `bmi` back. Extended to a second sequential node, `label_bmi`, which reads the computed `bmi` and writes a `category` (underweight/normal/overweight/obese) — showing how cheaply a sequential chain extends: one new node function + one new edge, nothing else changes.

- **Simplest LLM workflow** — a single node (`llm_qa`) that pulls a `question` out of state, builds a prompt, calls `model.invoke(prompt)` (`model = ChatOpenAI(...)` from `langchain_openai`), pulls out `.content`, and writes it to state as `answer`. This is the concrete instance of "LangChain supplies the components, LangGraph supplies the orchestration" from [[03-langchain-vs-langgraph]] — and the video is explicit that this example is **overkill on purpose**: one LLM call doesn't need a graph at all (it's one line of plain LangChain). LangGraph's actual value only shows up once a workflow has more than one step.

- **Prompt Chaining example (topic → outline → blog)** — two LLM-calling nodes in sequence: `create_outline` (title from state → LLM call → outline written back to state) then `create_blog` (title *and* outline read from state → LLM call → content written back to state). This is the practical payoff of **state**: the final state exposes `title`, `outline`, and `content` all together — a plain LangChain chain would only surface the *last* step's output, discarding the outline. That's exactly the state-handling limitation [[03-langchain-vs-langgraph]] raised in the abstract, now demonstrated as working code.

## How This Connects
- Turns the abstractions from [[04-langgraph-core-concepts]] (state, nodes, edges) into the concrete code pattern used for the rest of the course.
- Directly demonstrates the state-handling advantage argued for in [[03-langchain-vs-langgraph]] — the prompt-chaining example is a working instance of the exact problem that motivated LangGraph over plain LangChain chains.
- No new glossary terms this time — this video is applied practice of vocabulary already captured in notes 02–04.

## Self-Test
- Why does the video deliberately build a non-LLM BMI-calculator workflow before touching any LLM code?
- In the prompt-chaining example, what specifically would you lose if you'd built the same topic→outline→blog pipeline as a plain LangChain chain instead of a LangGraph graph?
- Walk through the four steps every LangGraph workflow goes through, from an empty notebook to a runnable result — what does each of `StateGraph`, `add_node`, `compile`, and `invoke` actually do?

---
