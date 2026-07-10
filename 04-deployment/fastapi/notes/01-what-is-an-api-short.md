# What is an API? — Quick Recall

**Course:** FastAPI (CampusX) · **Video:** [What is an API? | Introduction to APIs | FAST API for Machine Learning | CampusX](https://youtu.be/WJKsPchji0Q?si=9Pp3bj7lVKvGUT1a) · **Date:** July 10, 2026
→ Deep-dive: [01-what-is-an-api.md](01-what-is-an-api.md)

---

## TL;DR

This video introduces APIs as connectors that bridge software applications (like frontend and backend), detailing why decoupled architectures are preferred over monoliths for scalability, multi-client support, and serving machine learning models.

---

## Key Points

* **API (Application Programming Interface)** — A software connection mechanism communicating via standard protocols (HTTP) and structured formats (JSON).
* **Decoupled Architecture** — Splitting frontend and backend into independent apps to enable separate deployments, code reusability, and multi-client (web, iOS, Android) support.
* **Monolithic Architecture** — A single, tightly-coupled codebase where frontend and backend share runtime, presenting scalability and reliability risks.
* **APIs in ML/AI** — Essential for wrapping computationally heavy Python models running on server hardware, allowing lightweight client devices to make predictions via JSON requests.
* **FastAPI Standard** — A high-performance Python framework widely adopted by industry (9/10 companies in ML) to serve robust and scalable ML prediction APIs.

---

## Terms Introduced

| Term | Definition (one line) |
|---|---|
| **API** | Software connector enabling secure communication between components using defined protocols. |
| **Monolith** | Architecture pattern where frontend and backend are tightly coupled inside a single directory. |
| **Decoupling** | Structuring apps independently so they communicate strictly over the network (e.g. HTTP/JSON). |
| **JSON** | JavaScript Object Notation: a text-based, human-readable data format used for API payload exchange. |

---

## Self-Test

- Explain why wrapping an ML model in an API is better than packaging the model file directly within a frontend client app.
- What is the difference between a Monolith and a Decoupled architecture regarding their failure boundaries (loose vs. tight coupling)?
- In the restaurant analogy of APIs, what software components map to the *Customer*, *Waiter*, *Chef*, *Menu*, and *Plate*?

---
<!-- Short note. Full coverage: [long note](01-what-is-an-api.md) -->
