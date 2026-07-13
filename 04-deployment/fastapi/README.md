# FastAPI

Notes from the **FastAPI for Machine Learning** course by CampusX (Nitish Singh). FastAPI is the industry-standard framework for wrapping, serving, and deploying machine learning models into scalable and robust production APIs.

See [`_meta/workflow.md`](../../_meta/workflow.md) for how notes get made.

## Notes

| # | Note | Companion Card | Video |
|---|---|---|---|
| 01 | [What is an API?](notes/01-what-is-an-api.md) | [01-short](notes/quick-recall.md#01-what-is-an-api) | [link](https://youtu.be/WJKsPchji0Q?si=9Pp3bj7lVKvGUT1a) |
| 02 | [FastAPI Philosophy & Setup](notes/02-fastapi-philosophy-and-setup.md) | [02-short](notes/quick-recall.md#02-fastapi-philosophy-setup) | [link](https://youtu.be/lXx-_1r0Uss?si=yKlIm7jmcRjvt28t) |
| 03 | [HTTP Methods & Project Setup](notes/03-http-methods-and-project-setup.md) | [03-short](notes/quick-recall.md#03-http-methods-project-setup) | [link](https://youtu.be/O8KrViWNhOM?si=_zCr-cRvXY8YP2cG) |
| 04 | [Path & Query Parameters](notes/04-path-and-query-parameters.md) | [04-short](notes/quick-recall.md#04-path-query-parameters) | [link](https://youtu.be/VVVKEfhXCQ4?si=m-mil49kVLkVygtx) |

---

## Course Outline & Topic Progress

This outline is tracked dynamically as topics are introduced and covered in the course videos.

### Part 1: FastAPI Fundamentals (🟡 In Progress)
- [x] **What is an API?** — core concepts, HTTP, JSON, monolithic vs. decoupled architectures.
- [x] **FastAPI Setup & Installation** — setting up the environment, installing dependencies.
- [x] **Our First API** — building and running a basic FastAPI app.
- [x] **Routing & HTTP Methods** — GET, POST, PUT, DELETE requests.
- [x] **Parameters & Request Bodies** — path parameters, query parameters, and Pydantic models.
- [x] **Responses & Status Codes** — returning custom headers, status codes, and JSON payloads.

### Part 2: FastAPI + Machine Learning (⚪ Not Started)
- [ ] **ML Model Serialization** — loading serialized model binaries (`.pkl`, `.h5`) in Python.
- [ ] **Exposing ML Endpoints** — wrapping pre-trained model predictions in a POST handler.
- [ ] **Frontend Integration** — connecting the backend FastAPI prediction service with a web user interface.

### Part 3: Deployment & Production (⚪ Not Started)
- [ ] **Production Code Quality** — directory structures, configurations, and logging.
- [ ] **Containerization with Docker** — writing Dockerfiles and packaging dependencies.
- [ ] **Cloud Deployment** — hosting Dockerized FastAPI services on AWS.
