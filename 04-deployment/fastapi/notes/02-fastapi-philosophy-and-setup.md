# FastAPI Philosophy, Installation, & Hello World

> 🎥 [FastAPI Philosophy | How to setup FastAPI | Installation and Code Demo](https://youtu.be/lXx-_1r0Uss?si=yKlIm7jmcRjvt28t) · 📅 July 10, 2026 · 📚 FastAPI (CampusX)
> Quick Recall: [FastAPI — Quick Recall](quick-recall.md#02-fastapi-philosophy-setup)

---

## TL;DR

This video covers the core philosophy of FastAPI—focusing on its two main pillars: "Fast to run" (powered by ASGI, Uvicorn, and Python's `async/await`) and "Fast to code" (powered by Pydantic validation and auto-generated interactive Swagger docs). It walks through installing FastAPI inside a virtual environment and writing, running, and testing a basic multi-route Hello World application.

---

## What is FastAPI?

**FastAPI** is a modern, high-performance web framework for building APIs with Python. Under the hood, FastAPI is not built from scratch; it stands on the shoulders of two extremely powerful, specialized Python libraries:

1. **Starlet:** A lightweight ASGI framework/toolkit. Starlet manages the core web aspects: how the API listens for HTTP requests, performs routing, and returns HTTP responses.
2. **Pydantic:** A data validation and settings management library. Pydantic enforces Python type hints, ensuring the incoming and outgoing data format matches expectations.

By combining these two libraries, FastAPI achieves raw speed (from Starlet) and strict data safety with minimal developer overhead (from Pydantic).

---

## The Two Pillars of FastAPI's Philosophy

FastAPI was created because older frameworks like Flask and Django had performance bottlenecks and required significant boilerplate code. Its name reflects two core goals:

### Pillar 1: Fast to Run (High Performance & Concurrency)
FastAPI matches the speed of NodeJS and Go backends, which historically outperformed Python. This speed is achieved through three architectural differences:

#### 1. ASGI vs. WSGI
* **WSGI (Web Server Gateway Interface):** Used by Flask and Django. It is **synchronous and blocking**. When a client makes a request, a server thread processes it. If the code waits for a database query or an ML model prediction, that thread is blocked and cannot serve anyone else.
* **ASGI (Asynchronous Server Gateway Interface):** Used by FastAPI. It is **asynchronous and non-blocking**. It allows multiple concurrent requests to be handled on a single thread.

#### 2. The Waiter Analogy (Concurrency vs. Blocking)
* **Flask (WSGI):** A waiter takes a customer's order, goes to the kitchen, and stands there waiting for the chef to cook the food. The waiter cannot take orders from other customers until this food is served. This results in idle waiting and slow service.
* **FastAPI (ASGI):** A waiter takes an order, submits it to the kitchen, and immediately goes to take orders from other tables. When the first order is ready, the chef alerts the waiter, who then serves it. This non-blocking execution maximizes resource usage.

#### 3. High-Performance ASGI Servers (Uvicorn)
While Flask uses Gunicorn or Werkzeug (synchronous WSGI servers), FastAPI uses **Uvicorn**—a lightning-fast ASGI server implementation. Uvicorn handles concurrent network requests asynchronously.

#### 4. Python Async/Await Support
FastAPI natively supports Python's `async` and `await` keywords, letting developers write code that voluntarily yields execution during long I/O operations (like waiting for database replies or calling model predictions), freeing the server to handle other traffic.

---

### Pillar 2: Fast to Code (Developer Efficiency)
FastAPI minimizes the boilerplate code a developer must write to get a secure, production-grade API up and running.

#### 1. Automatic Input Validation & Type Enforcement
Python is dynamically typed, meaning variables can change types at runtime, which can cause bugs in production. FastAPI uses Pydantic to enforce data types based on standard Python type hints. If a route expects an `int` and gets a `str`, FastAPI automatically blocks the request and returns a clear validation error without the developer writing validation checks.

#### 2. Auto-generated Interactive Documentation
Writing API documentation (like OpenAPI/Swagger files) is tedious but necessary. FastAPI automatically generates interactive documentation as you write code:
* **Swagger UI (accessible at `/docs`):** An interactive, visual page where you can see all available endpoints, their expected input/output schemas, and test them live.
* **ReDoc (accessible at `/redoc`):** A clean, structural alternative documentation page.

This interactive capability means developers do not need tools like Postman to test their API endpoints during development.

#### 3. Modern Integrations
FastAPI integrates seamlessly with modern engineering tools:
* Machine Learning: scikit-learn, TensorFlow, PyTorch.
* Databases: SQLAlchemy, SQLModel, PostgreSQL.
* Security: OAuth2, JWT tokens.
* DevOps: Built-in support for Docker containerization and Kubernetes scaling.

---

## Installation & Environment Setup

Setting up a clean Python environment is the first step in any FastAPI project.

### 1. Create a Project Folder & Virtual Environment
Isolating dependencies ensures other python projects on your machine don't conflict with your FastAPI requirements.

```bash
# 1. Create and enter the directory (done on your local machine)
mkdir fastapi-tutorials
cd fastapi-tutorials

# 2. Create the virtual environment
python -m venv myenv

# 3. Activate the virtual environment (Windows)
myenv\Scripts\activate
```

### 2. Install FastAPI and its ASGI Server
To run FastAPI, we install it along with `uvicorn` and `pydantic`. Since Starlet is a dependency of FastAPI, it installs automatically.

```bash
pip install fastapi uvicorn pydantic
```

---

## Hello World Code Demo

Here is a minimal, complete FastAPI application containing two endpoints (`/` and `/about`).

### 1. The Code (`main.py`)

```python
# Import the main FastAPI class
from fastapi import FastAPI

# Create an instance of the FastAPI class
# This 'app' object represents the web application
app = FastAPI()

# Define the Home Route ("/")
# The @app.get decorator tells FastAPI to listen for GET requests at the root URL
@app.get("/")
def hello():
    # Returning a Python dictionary. 
    # FastAPI automatically serializes this into a JSON string for the client.
    return {"message": "Hello World"}

# Define the About Route ("/about")
@app.get("/about")
def about():
    return {
        "message": "CampusX is an education platform where you can learn AI"
    }
```

### 2. Running the Application
To start the Uvicorn web server, run the following command in your terminal (with the virtual environment active):

```bash
uvicorn main:app --reload
```

#### Breaking Down the Command:
* `uvicorn`: Invokes the ASGI server.
* `main`: The name of the Python file containing your code (`main.py`).
* `:app`: Specifies the variable name of the `FastAPI` instance inside `main.py` (`app = FastAPI()`).
* `--reload`: Enables **auto-reload mode**. The server monitors your project files and automatically restarts when code changes are saved, removing the need to restart the server manually during development.

---

## Interactive Documentation `/docs`

Once the server is running (usually at `http://127.0.0.1:8000`), you can access the interactive Swagger UI by appending `/docs` to the URL.

```
URL: http://127.0.0.1:8000/docs
```

### Key Features of Swagger UI:
1. **Interactive Endpoint List:** Shows all endpoints (`/`, `/about`), their HTTP methods (GET), and parameter descriptions.
2. **"Try it out" Mode:** Clicking "Try it out" enables editing parameters.
3. **"Execute" Button:** Sends a live request to the local Uvicorn server and displays the returned JSON response, response headers, and latency.

This built-in playground speeds up frontend-backend alignment and API debugging.

---

## Added Context

* **ASGI Server Alternatives:** While Uvicorn is the most popular, other ASGI servers include **Hypercorn** (supports HTTP/2 and WebSockets well) and **Daphne** (originally built for Django Channels).
* **Automatic JSON Serialization:** In older frameworks like Flask, developers often had to import `jsonify` and wrap responses (e.g., `return jsonify(message="Hello")`). FastAPI handles this conversion implicitly for python dicts, lists, strings, integers, and Pydantic models.

---

## Quick Recap

| Concept | One-liner |
|---|---|
| **Starlet** | The underlying ASGI web framework handling routing and HTTP requests/responses in FastAPI. |
| **Pydantic** | The validation library used by FastAPI to enforce types and validate schemas. |
| **Uvicorn** | The lightning-fast ASGI server that runs the FastAPI application code. |
| **`--reload`** | A development flag that restarts the server automatically when code edits are saved. |
| **`/docs`** | The automatically generated Swagger UI page for interactive API documentation and testing. |

---

## Practice Check

1. Explain the difference between WSGI and ASGI. How does ASGI allow FastAPI to handle more concurrent requests than Flask on a single thread?
2. Why is Gunicorn considered a WSGI server and Uvicorn an ASGI server? Can they be used together?
3. Modify the Hello World code to add a third GET route at `/contact` that returns a dictionary containing a contact email and phone number. Test it in the `/docs` UI.
4. What happens under the hood when a client sends a GET request to `http://127.0.0.1:8000/about`? Trace the lifecycle of the request through Uvicorn, ASGI, Starlet, your Python code, and back to the client.

---
<!-- Long note complete. Companion: [02-fastapi-philosophy-and-setup-short.md](02-fastapi-philosophy-and-setup-short.md) -->
