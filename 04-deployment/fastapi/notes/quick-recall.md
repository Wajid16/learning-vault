# FastAPI — Quick Recall

This file contains the short quick-recall cards for all FastAPI course videos. Use this file for rapid review and active recall.

---

## 01. What is an API?

**Video:** [What is an API? | Introduction to APIs | FAST API for Machine Learning | CampusX](https://youtu.be/WJKsPchji0Q?si=9Pp3bj7lVKvGUT1a) · **Date:** July 10, 2026
→ Deep-dive: [01-what-is-an-api.md](01-what-is-an-api.md)

### TL;DR
This video introduces APIs as connectors that bridge software applications (like frontend and backend), detailing why decoupled architectures are preferred over monoliths for scalability, multi-client support, and serving machine learning models.

### Key Points
* **API (Application Programming Interface)** — A software connection mechanism communicating via standard protocols (HTTP) and structured formats (JSON).
* **Decoupled Architecture** — Splitting frontend and backend into independent apps to enable separate deployments, code reusability, and multi-client (web, iOS, Android) support.
* **Monolithic Architecture** — A single, tightly-coupled codebase where frontend and backend share runtime, presenting scalability and reliability risks.
* **APIs in ML/AI** — Essential for wrapping computationally heavy Python models running on server hardware, allowing lightweight client devices to make predictions via JSON requests.
* **FastAPI Standard** — A high-performance Python framework widely adopted by industry (9/10 companies in ML) to serve robust and scalable ML prediction APIs.

### Terms Introduced
| Term | Definition (one line) |
|---|---|
| **API** | Secure software connector enabling communication between components using defined protocols. |
| **Monolith** | Architecture pattern where frontend and backend are tightly coupled inside a single runtime. |
| **Decoupling** | Structuring apps independently so they communicate strictly over the network (e.g. HTTP/JSON). |
| **JSON** | JavaScript Object Notation: a text-based, human-readable data format used for API payload exchange. |

### Self-Test
- Explain why wrapping an ML model in an API is better than packaging the model file directly within a frontend client app.
- What is the difference between a Monolith and a Decoupled architecture regarding their failure boundaries (loose vs. tight coupling)?
- In the restaurant analogy of APIs, what software components map to the *Customer*, *Waiter*, *Chef*, *Menu*, and *Plate*?

---

## 02. FastAPI Philosophy & Setup

**Video:** [FastAPI Philosophy | How to setup FastAPI | Installation and Code Demo | Video 2 | CampusX](https://youtu.be/lXx-_1r0Uss?si=yKlIm7jmcRjvt28t) · **Date:** July 10, 2026
→ Deep-dive: [02-fastapi-philosophy-and-setup.md](02-fastapi-philosophy-and-setup.md)

### TL;DR
FastAPI is a modern Python framework built on Starlette (ASGI web core) and Pydantic (data validation). Its core philosophy focuses on run-time speed (non-blocking ASGI concurrency) and code-time speed (auto-generated docs and low boilerplate).

### Key Points
* **Under the Hood** — FastAPI = Starlet (ASGI web framework) + Pydantic (strict data validation based on Python type hints).
* **Asynchronous Concurrency** — Uses **ASGI** instead of Flask's blocking **WSGI**. This allows non-blocking request handling (like a waiter taking other tables' orders while the first order cooks).
* **Uvicorn ASGI Server** — A high-performance ASGI server that executes FastAPI applications, running via `uvicorn main:app --reload`.
* **Automatic Docs** — Instantly generates interactive Swagger UI documentation at `/docs` (and ReDoc at `/redoc`), removing the need for Postman to test endpoints.
* **Auto-reload (`--reload`)** — A developmental flag that watches files for changes and restarts the Uvicorn server automatically.

### Terms Introduced
| Term | Definition (one line) |
|---|---|
| **ASGI** | Asynchronous Server Gateway Interface: non-blocking interface standard for Python async web applications. |
| **WSGI** | Web Server Gateway Interface: synchronous, blocking legacy standard for Python web applications (Flask, Django). |
| **Starlet** | A lightweight ASGI toolkit/framework that handles FastAPI's routing and web request/response handling. |
| **Pydantic** | A data validation library that checks if the incoming data matches the declared Python type hints. |
| **Uvicorn** | A lightning-fast ASGI HTTP server implementation for Python. |

### Self-Test
- What makes FastAPI faster to run than Flask when dealing with many concurrent request connections?
- How do you access the interactive OpenAPI/Swagger testing playground on a running FastAPI local server?
- Write down the command to start a FastAPI server using Uvicorn if the file is called `api.py` and the FastAPI instance is called `api_instance`.

---

## 03. HTTP Methods & Project Setup

**Video:** [HTTP Methods in FastAPI | Video 3 | CampusX](https://youtu.be/O8KrViWNhOM?si=_zCr-cRvXY8YP2cG) · **Date:** July 11, 2026
→ Deep-dive: [03-http-methods-and-project-setup.md](03-http-methods-and-project-setup.md)

### TL;DR
This video introduces our main project—a Patient Management System API. It covers mapping CRUD operations to HTTP methods (GET, POST, PUT, DELETE) and implements a `/view` GET endpoint to load and return mock data from `patients.json`.

### Key Points
* **CRUD Model** — The four essential interactions in dynamic software: Create (POST), Retrieve (GET), Update (PUT), Delete (DELETE).
* **HTTP Methods** — Verbs included in request headers to indicate the desired operation to the server.
* **Mock Database** — A local file `patients.json` is used as a mock database storing structured patient profiles (name, city, age, gender, height, weight, BMI).
* **JSON Helper** — Python's `json.load()` parses the text file, which FastAPI automatically serializes into an HTTP JSON response.
* **GET `/view` Route** — Endpoint that reads the list of patients and outputs it dynamically to clients.

### Terms Introduced
| Term | Definition (one line) |
|---|---|
| **CRUD** | Create, Read, Update, Delete: the four core operations of persistent storage. |
| **HTTP Methods** | Standard request verbs (GET, POST, PUT, DELETE) indicating client intent to the server. |
| **GET Request** | An HTTP method used to fetch data safely without modifying server state. |
| **POST Request** | An HTTP method used to submit data to the server to create new resources. |

### Self-Test
- Which HTTP method maps to the "Create" operation in CRUD?
- Why is it considered unsafe to write to a single JSON file directly in a high-concurrency production backend?
- What are the steps to display all patient data using our new `/view` endpoint on Swagger UI (`/docs`)?

---

## 04. Path & Query Parameters

**Video:** [Path & Query Params in FastAPI | Video 4 | CampusX](https://youtu.be/VVVKEfhXCQ4?si=m-mil49kVLkVygtx) · **Date:** July 11, 2026
→ Deep-dive: [04-path-and-query-parameters.md](04-path-and-query-parameters.md)

### TL;DR
This video covers passing inputs to endpoints using Path Parameters (identifying unique resources) and Query Parameters (filtering/sorting lists), alongside proper error handling using `HTTPException`.

### Key Points
* **Path Parameters** — Dynamic, required parts of the URL path (e.g., `/patient/{patient_id}`) used to identify individual resources.
* **Query Parameters** — Optional key-value pairs appended at the end of the URL (e.g., `?sort_by=bmi&order=descending`), separated by `&`, used to filter, sort, or paginate.
* **Validation Helpers** — `Path()` and `Query()` functions let you declare default values, validation constraints, descriptions, and examples for the interactive docs.
* **HTTP Status Codes** — Standardized 3-digit identifiers (e.g., 200 OK, 400 Bad Request, 404 Not Found) returned by the server.
* **`HTTPException`** — Used to return client errors gracefully (e.g., raising 404 when a resource does not exist instead of returning a success code with an error message).

### Terms Introduced
| Term | Definition (one line) |
|---|---|
| **Path Parameter** | Dynamic segments of a URL path used to locate a specific resource. |
| **Query Parameter** | Key-value pairs appended to the URL after `?` to refine search/sorting. |
| **HTTP Status Code** | 3-digit number sent by the server indicating the result of the HTTP request. |
| **HTTPException** | A FastAPI exception class that returns custom HTTP error codes and detail strings. |

### Self-Test
- When would you use a Path Parameter versus a Query Parameter in API design?
- Write the python statement to raise an HTTP 400 Bad Request error with the message "Invalid credentials".
- How does Uvicorn know whether a function argument is a path parameter or a query parameter in FastAPI?
