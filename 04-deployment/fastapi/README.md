# FastAPI

Notes from the **FastAPI for Machine Learning** course by CampusX (Nitish Singh). FastAPI is the industry-standard framework for wrapping, serving, and deploying machine learning models into scalable and robust production APIs.

See [`_meta/workflow.md`](../../_meta/workflow.md) for how notes get made.

## Notes

| # | Note | Companion Card | Video |
|---|---|---|---|
| 01 | [What is an API?](notes/01-what-is-an-api.md) | [01-short](notes/01-what-is-an-api-short.md) | [link](https://youtu.be/WJKsPchji0Q?si=9Pp3bj7lVKvGUT1a) |

---

## Course Outline & Topic Progress

This outline is tracked dynamically as topics are introduced and covered in the course videos.

### Part 1: FastAPI Fundamentals (🟡 In Progress)
- [x] **What is an API?** — core concepts, HTTP, JSON, monolithic vs. decoupled architectures.
- [ ] **FastAPI Setup & Installation** — setting up the environment, installing dependencies.
- [ ] **Our First API** — building and running a basic FastAPI app.
- [ ] **Routing & HTTP Methods** — GET, POST, PUT, DELETE requests.
- [ ] **Parameters & Request Bodies** — path parameters, query parameters, and Pydantic models.
- [ ] **Responses & Status Codes** — returning custom headers, status codes, and JSON payloads.

### Part 2: FastAPI + Machine Learning (⚪ Not Started)
- [ ] **ML Model Serialization** — loading serialized model binaries (`.pkl`, `.h5`) in Python.
- [ ] **Exposing ML Endpoints** — wrapping pre-trained model predictions in a POST handler.
- [ ] **Frontend Integration** — connecting the backend FastAPI prediction service with a web user interface.

### Part 3: Deployment & Production (⚪ Not Started)
- [ ] **Production Code Quality** — directory structures, configurations, and logging.
- [ ] **Containerization with Docker** — writing Dockerfiles and packaging dependencies.
- [ ] **Cloud Deployment** — hosting Dockerized FastAPI services on AWS.
