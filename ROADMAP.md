# AI Engineer Roadmap (CampusX — Nitish Singh)

> **How this file works:** Agent checks items off as they are covered in session notes. Each checked item links to the note where it was covered. The roadmap is updated after every session.
>
> Last updated after: **Python — Session 01**

---

## Phase 0 — Python Foundations

**Course:** [Python Core](python/) · **Status:** 🟡 In Progress · **Notes:** 1

### Python Core Fundamentals
- [x] Python syntax, indentation, code style (PEP8) — partial ([01-python-basics-i.md](python/notes/session-01-python-basics-i.md))
- [x] Variables, data types, type casting ([01-python-basics-i.md](python/notes/session-01-python-basics-i.md))
- [x] Input/output, comments — `print()` & `input()` done, docstrings pending ([01-python-basics-i.md](python/notes/session-01-python-basics-i.md))
- [ ] Control flow: if/else, loops (for, while)
- [ ] Functions, arguments, return values
- [ ] Lambda functions
- [ ] List / dict / set comprehensions

### Built-in Data Structures
- [ ] Lists
- [ ] Tuples
- [ ] Sets
- [ ] Dictionaries
- [ ] Strings (immutability, slicing, formatting)

### Pythonic Thinking
- [ ] Iterators and generators
- [ ] zip, enumerate, map, filter, reduce
- [ ] Shallow vs deep copy
- [ ] Mutability vs immutability
- [ ] *args and **kwargs

### Object-Oriented Programming (OOP)
- [ ] Classes and objects
- [ ] Constructors (`__init__`)
- [ ] Instance vs class variables
- [ ] Methods and dunder methods
- [ ] Inheritance and method overriding
- [ ] Polymorphism
- [ ] Encapsulation & abstraction
- [ ] Dataclasses (`@dataclass`)

### Error Handling & Debugging
- [ ] Exceptions (try/except/finally)
- [ ] Custom exceptions
- [ ] Common runtime errors

### Modules, Packages & Environments
- [ ] Import system (import, from, as)
- [ ] Creating modules and packages
- [ ] Virtual environments (venv, conda)
- [ ] Dependency management (pip, requirements.txt, poetry)
- [ ] Understanding `__main__`

### File Handling & Serialization
- [ ] Reading/writing text files
- [ ] CSV, JSON handling
- [ ] Pickle (pros & cons)
- [ ] Working with directories (os, pathlib)
- [ ] Logging to files

### Numerical Computing — NumPy
- [ ] Arrays, shapes, dtypes
- [ ] Broadcasting
- [ ] Vectorized operations
- [ ] Linear algebra basics
- [ ] Random sampling

### Data Analysis — Pandas
- [ ] Series and DataFrames
- [ ] Indexing & filtering
- [ ] GroupBy & aggregation
- [ ] Missing values handling
- [ ] Merging & joining
- [ ] Time-series basics

### Data Visualization
- [ ] Matplotlib
- [ ] Seaborn
- [ ] Plot types for EDA

### Standard Library (High-ROI Parts)
- [ ] os, sys
- [ ] pathlib
- [ ] datetime, time
- [ ] math, random
- [ ] logging

### Async & Parallel Python
- [ ] Multithreading vs multiprocessing
- [ ] async / await
- [ ] Async I/O basics
- [ ] When to use each

### Production-Ready Mindset
- [ ] Writing clean, readable code
- [ ] Modular design
- [ ] Logging & monitoring mindset
- [ ] Reading other people's code

### Extra topics (covered in videos, not in original syllabus)
- [x] Why Python? (design philosophy, batteries included) ([01-python-basics-i.md](python/notes/session-01-python-basics-i.md))
- [x] Keywords & Identifiers ([01-python-basics-i.md](python/notes/session-01-python-basics-i.md))
- [x] Literals — numeric, float, complex, string, boolean, None ([01-python-basics-i.md](python/notes/session-01-python-basics-i.md))
- [x] Dynamic typing & dynamic binding ([01-python-basics-i.md](python/notes/session-01-python-basics-i.md))
- [x] `type()` function ([01-python-basics-i.md](python/notes/session-01-python-basics-i.md))
<!-- agent appends anything covered that isn't above -->

---

## Phase 1 — Mathematics for ML

**Status:** ⚪ Not Started

### Linear Algebra
- [ ] Scalars, vectors, matrices, tensors
- [ ] Matrix operations (addition, multiplication, transpose)
- [ ] Dot product and its geometric meaning
- [ ] Eigenvalues and eigenvectors
- [ ] SVD (Singular Value Decomposition)
- [ ] Norms (L1, L2)

### Calculus
- [ ] Derivatives and partial derivatives
- [ ] Chain rule
- [ ] Gradient and gradient descent intuition
- [ ] Jacobian and Hessian (conceptual)

### Probability & Statistics
- [ ] Random variables, distributions
- [ ] Conditional probability, Bayes' theorem
- [ ] Expectation, variance, covariance
- [ ] Maximum likelihood estimation (MLE)
- [ ] Common distributions (Normal, Bernoulli, Binomial, Poisson)
- [ ] Central Limit Theorem
- [ ] Hypothesis testing basics

---

## Phase 2 — Machine Learning

**Status:** ⚪ Not Started

### ML Foundations
- [ ] What is ML? Types (supervised, unsupervised, reinforcement)
- [ ] The ML workflow: data → features → model → eval → deploy
- [ ] Bias-variance tradeoff
- [ ] Overfitting vs underfitting
- [ ] Train / validation / test split
- [ ] Cross-validation

### Supervised Learning — Regression
- [ ] Linear Regression (OLS, gradient descent)
- [ ] Polynomial Regression
- [ ] Regularization (Ridge, Lasso, ElasticNet)
- [ ] Evaluation: MSE, RMSE, MAE, R²

### Supervised Learning — Classification
- [ ] Logistic Regression
- [ ] Decision Trees
- [ ] Random Forests & Bagging
- [ ] Gradient Boosting (XGBoost, LightGBM)
- [ ] Support Vector Machines (SVM)
- [ ] K-Nearest Neighbours (KNN)
- [ ] Naïve Bayes
- [ ] Evaluation: accuracy, precision, recall, F1, ROC-AUC, confusion matrix

### Unsupervised Learning
- [ ] K-Means Clustering
- [ ] DBSCAN
- [ ] Hierarchical Clustering
- [ ] PCA (Principal Component Analysis)
- [ ] t-SNE / UMAP (dimensionality reduction for visualization)

### Feature Engineering
- [ ] Feature scaling (StandardScaler, MinMaxScaler)
- [ ] Encoding (one-hot, label, target encoding)
- [ ] Handling missing values
- [ ] Feature selection (correlation, mutual information, RFE)

### Model Selection & Pipelines
- [ ] Hyperparameter tuning (GridSearchCV, RandomizedSearchCV, Optuna)
- [ ] scikit-learn Pipelines
- [ ] Saving and loading models (joblib, pickle)

---

## Phase 3 — Deep Learning & NLP

**Status:** ⚪ Not Started

### Neural Network Fundamentals
- [ ] Perceptron and multi-layer perceptron (MLP)
- [ ] Activation functions (ReLU, sigmoid, tanh, softmax)
- [ ] Backpropagation and chain rule in context
- [ ] Optimizers (SGD, Adam, AdamW)
- [ ] Loss functions (cross-entropy, MSE)
- [ ] Batch normalization, dropout
- [ ] PyTorch basics (tensors, autograd, nn.Module)

### CNNs (Computer Vision)
- [ ] Convolution, pooling, stride, padding
- [ ] Classic architectures (LeNet, AlexNet, ResNet, VGG — conceptual)
- [ ] Transfer learning with pretrained CNNs

### RNNs & Sequence Models
- [ ] Vanilla RNN and its vanishing gradient problem
- [ ] LSTM and GRU
- [ ] Seq2Seq architecture

### Transformers & Attention
- [ ] Self-attention mechanism
- [ ] Multi-head attention
- [ ] Positional encoding
- [ ] Transformer architecture (encoder, decoder, encoder-decoder)
- [ ] BERT (encoder-only) and GPT (decoder-only) distinction

### NLP Essentials
- [ ] Tokenization (BPE, WordPiece, SentencePiece)
- [ ] Word embeddings (Word2Vec, GloVe — conceptual)
- [ ] Sentence embeddings (SBERT)
- [ ] Fine-tuning pretrained models (Hugging Face)
- [ ] Named Entity Recognition, text classification tasks

---

## Phase 4 — Tooling & Infrastructure

### FastAPI
**Course:** [FastAPI](fastapi/) · **Status:** ⚪ Not Started · **Notes:** 0

- [ ] Path operations, request/response models
- [ ] Dependency injection
- [ ] Pydantic integration for validation
- [ ] Background tasks
- [ ] Async endpoints
- [ ] OpenAPI/Swagger auto-docs
- [ ] Authentication (OAuth2, JWT basics)

### Docker
**Course:** [Docker](docker/) · **Status:** 🟡 In Progress · **Notes:** 1

- [ ] What is containerization? Why Docker?
- [ ] Dockerfile: FROM, RUN, COPY, CMD, ENTRYPOINT
- [ ] Building and running images/containers
- [ ] docker-compose for multi-service apps
- [ ] Volumes and bind mounts
- [ ] Networking between containers
- [ ] Pushing to Docker Hub / container registry
- [ ] Docker in an AI app deployment context

### Pydantic
**Course:** [Pydantic](pydantic/) · **Status:** ⚪ Not Started · **Notes:** 0

- [ ] BaseModel, field types, validation
- [ ] Validators (field_validator, model_validator)
- [ ] Nested models
- [ ] Config and settings management (BaseSettings)
- [ ] Serialization (model_dump, model_dump_json)
- [ ] Pydantic v2 vs v1 differences

---

## Phase 5 — LLM Ecosystem

### LangChain
**Course:** [LangChain](langchain/) · **Status:** ⚪ Not Started · **Notes:** 0

- [ ] LCEL (LangChain Expression Language) chains
- [ ] Chat models and prompts
- [ ] Output parsers
- [ ] Memory (ConversationBufferMemory, etc.)
- [ ] Tools and Agents (ReAct pattern)
- [ ] Document loaders and text splitters
- [ ] Embeddings and vector stores
- [ ] Retrieval chains

### RAG (Retrieval-Augmented Generation)
**Course:** [RAG](rag/) · **Status:** ⚪ Not Started · **Notes:** 0

- [ ] Why RAG? The hallucination and stale-knowledge problem
- [ ] Chunking strategies (fixed, semantic, recursive)
- [ ] Embedding models (OpenAI, open-source)
- [ ] Vector databases (FAISS, Chroma, Pinecone, Qdrant)
- [ ] Retrieval strategies (similarity, MMR, hybrid)
- [ ] Reranking
- [ ] Advanced RAG patterns (HyDE, FLARE, self-RAG)
- [ ] Evaluation: faithfulness, relevance, groundedness

---

## Phase 6 — Agentic AI

### LangGraph
**Course:** [LangGraph](langgraph/) · **Status:** 🟡 In Progress · **Notes:** 14

- [x] GenAI vs Agentic AI ([01](langgraph/notes/01-genai-vs-agentic-ai.md))
- [x] What is Agentic AI? Characteristics & components ([02](langgraph/notes/02-what-is-agentic-ai.md))
- [x] Why LangGraph? LangChain vs LangGraph ([03](langgraph/notes/03-langchain-vs-langgraph.md))
- [x] Core concepts: graphs, nodes, edges, state, reducers ([04](langgraph/notes/04-langgraph-core-concepts.md))
- [x] Sequential workflows (first code) ([05](langgraph/notes/05-sequential-workflows-code.md))
- [x] Parallel workflows (structured output + reducers) ([06](langgraph/notes/06-parallel-workflows-code.md))
- [x] Conditional workflows ([07](langgraph/notes/07-conditional-workflows-code.md))
- [x] Iterative (looping) workflows ([08](langgraph/notes/08-iterative-workflows-code.md))
- [x] Chatbot + memory bug ([09](langgraph/notes/09-chatbot-memory-bug.md))
- [x] Persistence deep dive (checkpointers, threads) ([10](langgraph/notes/10-persistence-deep-dive.md))
- [x] Streamlit UI for chatbot ([11](langgraph/notes/11-streamlit-ui-for-chatbot.md))
- [x] Streaming responses ([12](langgraph/notes/12-streaming-chatbot-responses.md))
- [x] Resume chat feature ([13](langgraph/notes/13-resume-chat-feature.md))
- [x] SQLite persistent storage ([14](langgraph/notes/14-sqlite-persistent-storage.md))
- [ ] Human-in-the-loop (interrupt, approve/reject)
- [ ] Multi-agent systems (supervisor pattern)
- [ ] Tool calling in LangGraph
- [ ] Long-term memory (external stores)
- [ ] Deployment (LangGraph Platform / LangServe)

### MCP (Model Context Protocol)
**Course:** [MCP](mcp/) · **Status:** 🟡 In Progress · **Notes:** 2

- [x] What is MCP? The context & integration problem ([mcp/notes/02...](mcp/notes/))
- [ ] MCP architecture (client, server, protocol)
- [ ] Building an MCP server
- [ ] Connecting MCP to LangGraph / LangChain agents
- [ ] Authentication and security in MCP
- [ ] MCP vs function calling — when to use each

---

## Phase 7 — Evaluation & Production

### LLM Evals
**Course:** [LLM Evals](llm-evals/) · **Status:** 🟡 In Progress · **Notes:** 4

- [x] Why LLM evals? ([llm-evals/notes/01...](llm-evals/notes/))
- [x] Model evals vs application evals ([llm-evals/notes/02...](llm-evals/notes/))
- [x] Complete eval workflow ([llm-evals/notes/03...](llm-evals/notes/))
- [x] Failure points and risk categories ([llm-evals/notes/04...](llm-evals/notes/))
- [ ] Eval frameworks (RAGAS, DeepEval, LangSmith)
- [ ] LLM-as-judge: prompting strategy and calibration
- [ ] Building eval datasets
- [ ] Regression testing for LLM apps

---

## Phase 8 — Automation

### n8n
**Course:** [n8n](n8n/) · **Status:** ⚪ Not Started · **Notes:** 0

- [ ] What is n8n? No-code/low-code workflow automation
- [ ] Core concepts: workflows, nodes, triggers
- [ ] Connecting AI APIs in n8n
- [ ] Building AI agents with n8n
- [ ] Self-hosting n8n

---

## Courses Outside the Main Roadmap

### Non-technical
| Course | Status | Notes |
|---|---|---|
| [Scientific Writing](non-technical/scientific-writing/) | 🟡 In Progress | 5 |
| [IELTS](non-technical/ielts/) | ⚪ Not started | 0 |
| [English](non-technical/english/) | 🟡 In Progress | 2 |
| [Freelancing](non-technical/freelancing/) | ⚪ Not started | 0 |
