# Path & Query Parameters — Quick Recall

**Course:** FastAPI (CampusX) · **Video:** [Path & Query Params in FastAPI | Video 4 | CampusX](https://youtu.be/VVVKEfhXCQ4?si=m-mil49kVLkVygtx) · **Date:** July 11, 2026
→ Deep-dive: [04-path-and-query-parameters.md](04-path-and-query-parameters.md)

---

## TL;DR

This video covers passing inputs to endpoints using Path Parameters (identifying unique resources) and Query Parameters (filtering/sorting lists), alongside proper error handling using `HTTPException`.

---

## Key Points

* **Path Parameters** — Dynamic, required parts of the URL path (e.g., `/patient/{patient_id}`) used to identify individual resources.
* **Query Parameters** — Optional key-value pairs appended at the end of the URL (e.g., `?sort_by=bmi&order=descending`), separated by `&`, used to filter, sort, or paginate.
* **Validation Helpers** — `Path()` and `Query()` functions let you declare default values, validation constraints, descriptions, and examples for the interactive docs.
* **HTTP Status Codes** — Standardized 3-digit identifiers (e.g., 200 OK, 400 Bad Request, 404 Not Found) returned by the server.
* **`HTTPException`** — Used to return client errors gracefully (e.g., raising 404 when a resource does not exist instead of returning a success code with an error message).

---

## Terms Introduced

| Term | Definition (one line) |
|---|---|
| **Path Parameter** | Dynamic segments of a URL path used to locate a specific resource. |
| **Query Parameter** | Key-value pairs appended to the URL after `?` to refine search/sorting. |
| **HTTP Status Code** | 3-digit number sent by the server indicating the result of the HTTP request. |
| **HTTPException** | A FastAPI exception class that returns custom HTTP error codes and detail strings. |

---

## Self-Test

- When would you use a Path Parameter versus a Query Parameter in API design?
- Write the python statement to raise an HTTP 400 Bad Request error with the message "Invalid credentials".
- How does Uvicorn know whether a function argument is a path parameter or a query parameter in FastAPI?

---
<!-- Short note. Full coverage: [long note](04-path-and-query-parameters.md) -->
