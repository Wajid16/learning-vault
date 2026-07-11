# Path & Query Parameters in FastAPI

> 🎥 [https://youtu.be/VVVKEfhXCQ4?si=m-mil49kVLkVygtx](https://youtu.be/VVVKEfhXCQ4?si=m-mil49kVLkVygtx) · 📅 July 11, 2026 · 📚 FastAPI (CampusX)
> Short note: [04-path-and-query-parameters-short.md](04-path-and-query-parameters-short.md)

---

## TL;DR

This video covers the two key ways parameters are passed to API endpoints: **Path Parameters** and **Query Parameters**. It also details **HTTP Status Codes** and explains how to raise proper error states using FastAPI's `HTTPException` class. We implement endpoints to view a specific patient profile by ID and sort the patient directory dynamically, utilizing validation helpers (`Path` and `Query`) to enrich the Swagger UI.

---

## Path Parameters

### Definition
**Path Parameters** are dynamic segments of a URL path that are used to identify a specific, unique resource on the server.

* **URL Pattern:** `/patient/{patient_id}`
* **Concrete Call:** `/patient/P001` or `/patient/P002`

Here, `P001` or `P002` are dynamic values processed by the backend to fetch the matching record.

### Key Characteristics:
* **Scope:** Typically used to target a single, specific resource.
* **Obligation:** Path parameters are **required** by design. A request to `/patient/` without an ID will result in a 404 Not Found error (unless a separate root handler is defined).
* **Common Use Cases:** Read a single profile, Update a single profile (PUT), or Delete a single profile (DELETE).

### FastAPI's `Path` Class
FastAPI provides the `Path` function to enrich path parameters with documentation and validation rules:
* Mark as required using `...` (Ellipsis).
* Add descriptions and examples that render directly in the Swagger interactive UI (`/docs`).
* Add constraints: `gt` (greater than), `ge` (greater than or equal to), `lt` (less than), `le` (less than or equal to), `min_length`, `max_length`, or a regex pattern.

---

## HTTP Status Codes & Error Handling

An API should not only return the correct data, it must also communicate the status of the request using standard **HTTP Status Codes**.

### Classification of Status Codes:
* **2xx (Success):** The request was successfully received and accepted (e.g., `200 OK`, `201 Created`, `204 No Content`).
* **3xx (Redirection):** Further action is needed to complete the request.
* **4xx (Client Error):** The client sent a request containing errors (e.g., `400 Bad Request` for invalid inputs, `401 Unauthorized`, `403 Forbidden`, `404 Not Found` for missing resources).
* **5xx (Server Error):** The server failed to fulfill an apparently valid request (e.g., `500 Internal Server Error`).

### The HTTP Error Naming Antipattern
A common beginner mistake is returning a generic successful status code (`200 OK`) containing a JSON response payload representing an error:
```json
// Antipattern: HTTP Status is 200 OK, but body says error
{ "error": "Patient not found" }
```
**Why this is bad:** Client frameworks (like React, iOS SDKs, or API gateways) monitor HTTP status codes to determine success or failure. If you return 200, client error catch blocks will not trigger, masking errors.

### Correct Approach: `HTTPException`
In FastAPI, we interrupt execution and return a proper HTTP status code (like `404 Not Found`) by raising an `HTTPException`:
```python
from fastapi import HTTPException
raise HTTPException(status_code=404, detail="Patient not found")
```

---

## Query Parameters

### Definition
**Query Parameters** are optional key-value pairs appended to the end of the URL to filter, sort, search, or paginate a list of resources without changing the endpoint path itself.

* **URL Pattern:** `/sort?sort_by=bmi&order=descending`
* **Syntax:** 
  * Starts with a question mark (`?`) following the path.
  * Formatted as `key=value` pairs.
  * Separated by an ampersand (`&`) if multiple parameters are passed.

### Key Characteristics:
* **Scope:** Used to modify, sort, or filter arrays/lists of resources.
* **Obligation:** By default, query parameters are **optional**. If a client does not send them, the server uses fallback default values.
* **Common Use Cases:** Filtering a product catalog by category, sorting results, searching text, or paginating lists (`page=2&limit=20`).

### FastAPI's `Query` Class
FastAPI provides the `Query` function to configure query parameters:
* Set default values (e.g., `order: str = Query("ascending")`).
* Mark as required using `...` (Ellipsis) (e.g., `sort_by: str = Query(...)`).
* Document description and examples for Swagger UI.
* Apply min/max value validation constraints.

---

## Code Demo: View Specific Patient & Sorting List

This is the updated code inside `main.py`, demonstrating path parameter extraction, query parameter handling, input checks, and error responses.

```python
import json
from fastapi import FastAPI, Path, Query, HTTPException

app = FastAPI()

# Helper Function: Loads patient record database
def load_data():
    with open("patients.json", "r") as f:
        return json.load(f)

# --- Path Parameter Demo: View Specific Patient ---
@app.get("/patient/{patient_id}")
def view_patient(
    # Path parameter: validated to be a string, documented with description and example
    patient_id: str = Path(..., description="ID of the patient to retrieve", example="P001")
):
    data = load_data()
    
    # Check if key exists in the database dictionary
    if patient_id in data:
        # Return the dictionary representing the patient
        return data[patient_id]
    
    # If not found, raise a proper HTTP 404 client error
    raise HTTPException(status_code=404, detail="Patient not found")


# --- Query Parameter Demo: Sort Patients ---
@app.get("/sort")
def sort_patients(
    # Query parameters:
    # 1. sort_by (Required, indicated by Ellipsis)
    sort_by: str = Query(..., description="Field to sort by: height, weight, or bmi"),
    # 2. order (Optional, defaults to 'ascending')
    order: str = Query("ascending", description="Sorting direction: ascending or descending")
):
    # Validation list: ensure client requests fields that exist
    valid_fields = ["height", "weight", "bmi"]
    if sort_by not in valid_fields:
        # Raise HTTP 400 Bad Request
        raise HTTPException(
            status_code=400, 
            detail=f"Invalid field. Select from: {valid_fields}"
        )
        
    # Ensure sorting order is valid
    if order not in ["ascending", "descending"]:
        raise HTTPException(
            status_code=400, 
            detail="Invalid order. Select between: 'ascending' or 'descending'"
        )

    data = load_data()
    
    # Convert dictionary values to a list of patient dictionaries
    patient_list = list(data.values())
    
    # Convert 'order' string into a python boolean flag for sorted()
    is_reverse = True if order == "descending" else False
    
    # Sort the list using key extraction
    sorted_data = sorted(patient_list, key=lambda x: x[sort_by], reverse=is_reverse)
    
    return sorted_data
```

### Running and Verifying Endpoints
Start the server: `uvicorn main:app --reload`

1. **Path Parameter Check:**
   * GET `http://127.0.0.1:8000/patient/P002` successfully returns Priya Patel's profile.
   * GET `http://127.0.0.1:8000/patient/P007` correctly returns a `404 Not Found` response with `{"detail": "Patient not found"}`.
2. **Query Parameter Check:**
   * GET `http://127.0.0.1:8000/sort?sort_by=weight&order=descending` returns the list sorted from heaviest to lightest patient.
   * GET `http://127.0.0.1:8000/sort?sort_by=age` throws a `400 Bad Request` because sorting by `age` is blocked by our validation check.
   * GET `http://127.0.0.1:8000/sort?sort_by=weight` works without sending `order` because it falls back to the default value `"ascending"`.

---

## Added Context

* **FastAPI Automated Parameter Matching:** FastAPI is smart enough to distinguish between path and query parameters automatically. If a function argument is declared in the route path (e.g., `{patient_id}`), FastAPI treats it as a path parameter. If the argument is NOT in the path (e.g., `sort_by`), it is automatically treated as a query parameter.
* **REST API Path vs. Query Parameters Guideline:**
  * Use **Path Parameters** when you want to identify a **specific resource** (e.g., `/users/123/posts/45`).
  * Use **Query Parameters** when you want to **filter, sort, or paginate** resources (e.g., `/posts?author=nitish&sort=date`).

---

## Quick Recap

| Aspect | Path Parameters | Query Parameters |
|---|---|---|
| **Syntax** | Part of URL path: `/resource/{id}` | Appended at the end: `?key=value` |
| **Obligation** | Always required. | Optional by default (can specify defaults). |
| **Role** | Identifies a specific unique resource. | Filters, sorts, searches, or paginates a resource array. |
| **Validation** | Annotated with `Path()`. | Annotated with `Query()`. |

---

## Practice Check

1. Explain what happens if a user navigates to `http://127.0.0.1:8000/patient/` (without an ID segment). What HTTP Status code does FastAPI return by default, and why?
2. Implement a validation constraint on the `/patient/{patient_id}` path parameter using regex inside `Path()` to ensure that only patient IDs starting with 'P' followed by three digits (e.g., `P001`, `P999`) are processed. Test this constraint.
3. Add a new query parameter to the `/view` endpoint called `gender` that defaults to `None`. If a gender is provided (e.g., `?gender=Female`), filter and return only patients matching that gender.
4. What is the difference between an HTTP 400 status code and an HTTP 500 status code? In what scenario would you raise a 400 versus a 500 in an ML deployment context?

---
<!-- Long note complete. Companion: [04-path-and-query-parameters-short.md](04-path-and-query-parameters-short.md) -->
