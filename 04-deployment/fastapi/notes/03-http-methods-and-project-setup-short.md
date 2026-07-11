# HTTP Methods & Project Setup — Quick Recall

**Course:** FastAPI (CampusX) · **Video:** [HTTP Methods in FastAPI | Video 3 | CampusX](https://youtu.be/O8KrViWNhOM?si=_zCr-cRvXY8YP2cG) · **Date:** July 11, 2026
→ Deep-dive: [03-http-methods-and-project-setup.md](03-http-methods-and-project-setup.md)

---

## TL;DR

This video introduces our main project—a Patient Management System API. It covers mapping CRUD operations to HTTP methods (GET, POST, PUT, DELETE) and implements a `/view` GET endpoint to load and return mock data from `patients.json`.

---

## Key Points

* **CRUD Model** — The four essential interactions in dynamic software: Create (POST), Retrieve (GET), Update (PUT), Delete (DELETE).
* **HTTP Methods** — Verbs included in request headers to indicate the desired operation to the server.
* **Mock Database** — A local file `patients.json` is used as a mock database storing structured patient profiles (name, city, age, gender, height, weight, BMI).
* **JSON Helper** — Python's `json.load()` parses the text file, which FastAPI automatically serializes into an HTTP JSON response.
* **GET `/view` Route** — Endpoint that reads the list of patients and outputs it dynamically to clients.

---

## Terms Introduced

| Term | Definition (one line) |
|---|---|
| **CRUD** | Create, Read, Update, Delete: the four core operations of persistent storage. |
| **HTTP Methods** | Standard request verbs (GET, POST, PUT, DELETE) indicating client intent to the server. |
| **GET Request** | An HTTP method used to fetch data safely without modifying server state. |
| **POST Request** | An HTTP method used to submit data to the server to create new resources. |

---

## Self-Test

- Which HTTP method maps to the "Create" operation in CRUD?
- Why is it considered unsafe to write to a single JSON file directly in a high-concurrency production backend?
- What are the steps to display all patient data using our new `/view` endpoint on Swagger UI (`/docs`)?

---
<!-- Short note. Full coverage: [long note](03-http-methods-and-project-setup.md) -->
