# HTTP Methods & Project Setup in FastAPI

> 🎥 [HTTP Methods in FastAPI](https://youtu.be/O8KrViWNhOM?si=_zCr-cRvXY8YP2cG) · 📅 July 11, 2026 · 📚 FastAPI (CampusX)
> Quick Recall: [FastAPI — Quick Recall](quick-recall.md#03-http-methods-project-setup)

---

## TL;DR

This video introduces our main hands-on project—a Patient Management System API. It covers the fundamentals of HTTP methods (GET, POST, PUT, DELETE) and how they map to CRUD operations. In the coding demo, we establish a mock JSON file database (`patients.json`), write a data loading helper function, and implement a `/view` GET endpoint to retrieve all patient records.

---

## Project Overview: Patient Management System

We are developing a **Patient Management System API** designed to digitize the traditional, paper-based prescription flows in clinics. 

### The Problem Statement
In traditional clinics, doctors write remarks, vitals, and medication on paper prescription pads. These documents are given to patients, who must store them in paper files over the years. This manual process is prone to loss, damage, and misplacement for both patients and doctors.

### The Solution
A digital platform where doctors can manage patient records.
* **Patient Profile Fields:** Name, City, Age, Gender, Height, Weight, and BMI.
* **Storage Solution:** In a real production system, this data would go to a database (like PostgreSQL or MongoDB). For this course's fundamental phase, we will mock a database using a local `patients.json` file.
* **Developer Division of Labor:** As backend developers, our sole responsibility is to build the API endpoints. Frontend developers will build the mobile or web app interfaces that consume these endpoints.

---

## HTTP Methods & CRUD Operations

To understand how web interfaces connect with backend servers, we need to look at how data operations map to HTTP protocols.

### Static vs. Dynamic Software
* **Static Software:** One-way communication where the user only receives information without interacting or editing (e.g., a standard desktop clock, calendar).
* **Dynamic Software:** Two-way communication where users actively modify data and trigger state changes (e.g., Microsoft Excel, Word).

### CRUD: The 4 Interactions
In any dynamic software (and dynamic website), a user can perform exactly **four** types of data interactions, known as **CRUD**:

1. **C - Create:** Add new resources (e.g., writing a new row in Excel, publishing a new post on Instagram, ordering on Zomato).
2. **R - Retrieve / Read:** View existing data (e.g., scrolling a feed, viewing your profile, checking order history).
3. **U - Update:** Modify existing resources (e.g., editing an Excel cell, modifying a comment, updating your shipping address).
4. **D - Delete:** Remove existing resources (e.g., deleting a post, removing an address).

### Mapping CRUD to HTTP Methods
Websites communicate via the HTTP protocol. When a client performs a CRUD action, they must notify the server of their intent by sending a specific verb in the HTTP request header. These verbs are called **HTTP Methods**:

| CRUD Operation | HTTP Method | Action | Example in Web Apps |
|---|---|---|---|
| **Create** | **POST** | Sends data to the server to create a new resource. | Submitting a registration form, logging in. |
| **Retrieve** | **GET** | Requests data from the server. Does not modify server state. | Loading a search results page, opening a profile page. |
| **Update** | **PUT** | Replaces or updates an existing resource on the server. | Editing profile details, changing a password. |
| **Delete** | **DELETE** | Removes a resource from the server. | Clicking "Delete Post" or "Remove Account". |

---

## Coding Implementation: Project Setup & Retrieval

Here is the step-by-step setup and code to start the Patient Management System.

### 1. The Database Mock (`patients.json`)
Create this file in your root folder. It contains a JSON list of pre-configured patient dicts:

```json
[
  {
    "id": 1,
    "name": "Rohan Sharma",
    "city": "Delhi",
    "age": 29,
    "gender": "Male",
    "height": 1.75,
    "weight": 70,
    "bmi": 22.86
  },
  {
    "id": 2,
    "name": "Priya Patel",
    "city": "Mumbai",
    "age": 34,
    "gender": "Female",
    "height": 1.62,
    "weight": 55,
    "bmi": 20.95
  },
  {
    "id": 3,
    "name": "Amit Kumar",
    "city": "Bangalore",
    "age": 42,
    "gender": "Male",
    "height": 1.80,
    "weight": 85,
    "bmi": 26.23
  },
  {
    "id": 4,
    "name": "Sneha Reddy",
    "city": "Hyderabad",
    "age": 27,
    "gender": "Female",
    "height": 1.65,
    "weight": 60,
    "bmi": 22.04
  },
  {
    "id": 5,
    "name": "Vikram Singh",
    "city": "Jaipur",
    "age": 31,
    "gender": "Male",
    "height": 1.78,
    "weight": 78,
    "bmi": 24.62
  }
]
```

### 2. The Main Application Code (`main.py`)
We import the `json` library, implement a helper function to read `patients.json`, and set up routes to display metadata and return the list.

```python
import json
from fastapi import FastAPI

app = FastAPI()

# Helper Function: Loads records from the JSON file
def load_data():
    # Opened in read-only mode ('r')
    with open("patients.json", "r") as f:
        # Load and parse JSON into a Python list of dictionaries
        return json.load(f)

# 1. Updated Home Route
@app.get("/")
def home():
    return {"message": "Patient Management System API"}

# 2. Updated About Route
@app.get("/about")
def about():
    return {
        "message": "A fully functional API to manage your patient records"
    }

# 3. New Route: View all patients
# Maps to GET because it is a RETRIEVE operation
@app.get("/view")
def view_all_patients():
    # Call the helper to fetch parsed JSON data
    patients_data = load_data()
    # FastAPI automatically serializes this list to a JSON HTTP response
    return patients_data
```

### 3. Running & Verifying the API
Run the Uvicorn command:
```bash
uvicorn main:app --reload
```

#### Verifying via URLs:
* `http://127.0.0.1:8000/view` displays the list of 5 patients in JSON format inside the browser.
* `http://127.0.0.1:8000/docs` reveals three active endpoints. Under the `/view` endpoint description, clicking **Try it out** and **Execute** prints the list of patients, HTTP 200 success code, latency, and response headers.

---

## Added Context

* **Database vs. File I/O:** Reading from a JSON file directly via `open()` is fine for local training but unsuitable for production. In real-world applications, concurrent writes to a JSON file will result in data corruption. We will transition to relational databases later in the roadmap.
* **REST API Naming Convention:** While Nitish naming the endpoint `/view` is descriptive for learning, standard REST APIs typically use pluralized nouns representing the resource, e.g., `@app.get("/patients")` instead of `/view`.

---

## Quick Recap

| Term | Action | Mapping |
|---|---|---|
| **CRUD** | Four fundamental data interactions. | Create, Retrieve, Update, Delete. |
| **GET** | Retrieve resource. | Safe operation; does not alter server state. |
| **POST** | Create resource. | Sends data in request body. |
| **`/view`** | GET Endpoint in demo. | Loads `patients.json` and outputs it as JSON. |

---

## Practice Check

1. Why are GET requests considered "safe" and POST requests "unsafe"? (Think about what happens to the server database state when they run).
2. Write a Python script using the `requests` library that makes a GET request to your local `/view` endpoint and prints the names of all Male patients.
3. If a patient changes their address, which HTTP method should the client use to notify the server? Why?
4. In our `load_data()` helper, what exception could be thrown if the `patients.json` file is deleted or corrupt? Write a try-except block to handle it gracefully inside the helper.

---
<!-- Long note complete. Companion: [03-http-methods-and-project-setup-short.md](03-http-methods-and-project-setup-short.md) -->
