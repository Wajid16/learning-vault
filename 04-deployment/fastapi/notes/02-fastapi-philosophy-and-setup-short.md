# FastAPI Philosophy & Setup — Quick Recall

**Course:** FastAPI (CampusX) · **Video:** [FastAPI Philosophy | How to setup FastAPI | Installation and Code Demo | Video 2 | CampusX](https://youtu.be/lXx-_1r0Uss?si=yKlIm7jmcRjvt28t) · **Date:** July 10, 2026
→ Deep-dive: [02-fastapi-philosophy-and-setup.md](02-fastapi-philosophy-and-setup.md)

---

## TL;DR

FastAPI is a modern Python framework built on Starlet (ASGI web core) and Pydantic (data validation). Its core philosophy focuses on run-time speed (non-blocking ASGI concurrency) and code-time speed (auto-generated docs and low boilerplate).

---

## Key Points

* **Under the Hood** — FastAPI = Starlet (ASGI web framework) + Pydantic (strict data validation based on Python type hints).
* **Asynchronous Concurrency** — Uses **ASGI** instead of Flask's blocking **WSGI**. This allows non-blocking request handling (like a waiter taking other tables' orders while the first order cooks).
* **Uvicorn ASGI Server** — A high-performance ASGI server that executes FastAPI applications, running via `uvicorn main:app --reload`.
* **Automatic Docs** — Instantly generates interactive Swagger UI documentation at `/docs` (and ReDoc at `/redoc`), removing the need for Postman to test endpoints.
* **Auto-reload (`--reload`)** — A developmental flag that watches files for changes and restarts the Uvicorn server automatically.

---

## Terms Introduced

| Term | Definition (one line) |
|---|---|
| **ASGI** | Asynchronous Server Gateway Interface: non-blocking interface standard for Python async web applications. |
| **WSGI** | Web Server Gateway Interface: synchronous, blocking legacy standard for Python web applications (Flask, Django). |
| **Starlet** | A lightweight ASGI toolkit/framework that handles FastAPI's routing and web request/response handling. |
| **Pydantic** | A data validation library that checks if the incoming data matches the declared Python type hints. |
| **Uvicorn** | A lightning-fast ASGI HTTP server implementation for Python. |

---

## Self-Test

- What makes FastAPI faster to run than Flask when dealing with many concurrent request connections?
- How do you access the interactive OpenAPI/Swagger testing playground on a running FastAPI local server?
- Write down the command to start a FastAPI server using Uvicorn if the file is called `api.py` and the FastAPI instance is called `api_instance`.

---
<!-- Short note. Full coverage: [long note](02-fastapi-philosophy-and-setup.md) -->
