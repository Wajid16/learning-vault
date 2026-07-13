# What is an API? | Introduction to APIs | FAST API for Machine Learning | CampusX

> 🎥 [What is an API? | Introduction to APIs](https://youtu.be/WJKsPchji0Q?si=9Pp3bj7lVKvGUT1a) · 📅 July 10, 2026 · 📚 FastAPI (CampusX)
> Quick Recall: [FastAPI — Quick Recall](quick-recall.md#01-what-is-an-api)

---

## TL;DR

This video introduces the FastAPI course curriculum and explains the fundamental concept of APIs (Application Programming Interfaces). It contrasts modern decoupled API-driven architectures with legacy monolithic architectures, detailing why APIs are essential for serving machine learning models to web, mobile, and third-party clients.

---

## Course Curriculum & Roadmap

The course is divided into three distinct phases to take a learner from FastAPI basics to production-ready ML deployments:

| Phase | Title | Focus / Topics Covered |
|---|---|---|
| **Part 1** | **FastAPI Fundamentals** | FastAPI as a framework, routing, HTTP protocols, requests/responses, path/query parameters, status codes, and JSON data exchange (learned via a mini-project). |
| **Part 2** | **FastAPI + Machine Learning** | Integrating pre-trained ML models into a FastAPI backend. Building prediction endpoints and connecting them to a user-facing website/frontend. |
| **Part 3** | **Deployment & Production** | Writing production-grade code, containerizing the FastAPI application using Docker, and deploying to cloud infrastructure (specifically AWS). |

* **Playlist duration:** ~15 videos.
* **Timeline goal:** Completed in 21–25 days.

---

## What is an API?

### Definition
An **API (Application Programming Interface)** is a software mechanism that enables two distinct software components (such as a frontend client and a backend server) to communicate with each other using a defined set of rules, protocols, and data formats.

In simple terms, an API acts as a **connector** that bridges different software applications, allowing them to exchange data and trigger actions without needing direct access to each other's internal codebase or databases.

### The Restaurant Analogy (Mental Model)
A classic way to visualize how an API works is to think of a dining experience at a restaurant:

* **The Customer (Frontend / Client):** Sits at the table and decides what they want. They cannot go directly into the kitchen to cook or grab food.
* **The Kitchen & Chef (Backend / Server):** Contains the raw ingredients, recipes, and logic to cook the food. It is hidden away from the customer.
* **The Waiter (API):** Acts as the intermediary. The customer places an order with the waiter. The waiter takes the request to the kitchen, the chef prepares the food (executes backend logic), and the waiter delivers the finished dish back to the customer's table in a structured presentation (data format like JSON).
* **The Menu Card (Protocol / Rules):** Dictates what the customer is allowed to order, how much it costs, and what they can expect. This is the API documentation / endpoints definition.
* **Plates & Food Presentation (Data Format):** The specific way the food is served to the customer. In software, this is represented by structured data formats, usually JSON (JavaScript Object Notation).

---

## The Need for APIs: Monolithic vs. Decoupled Architecture

To appreciate why APIs exist, we must look at how software was built before they became dominant.

### Monolithic Architecture (Pre-API Era)
In a monolith, the entire application—both the user interface (frontend) and the business logic/database access (backend)—is packaged together in a single codebase, deployed as a single unit, and run on a single directory.

```
+------------------------------------------+
|          MONOLITHIC APPLICATION          |
|                                          |
|  [ Frontend UI ] <--> [ Backend Logic ]  |
|                               |          |
|                               v          |
|                         [ Database ]     |
+------------------------------------------+
```

* **How it communicates:** Since the code is in the same runtime/directory, they communicate directly via internal function calls.
* **The Problems:**
  1. **Tight Coupling:** If a bug occurs in the backend or if it crashes under heavy load, the entire website goes down. Updating a minor frontend color requires redeploying the entire backend system.
  2. **No External Integration:** External applications cannot access any of the internal functions or databases. Exposing database credentials directly to the public internet is a major security vulnerability.
  3. **Code Duplication (Multi-client support):** If you want to expand from a web app to have an Android app and an iOS app, a monolithic architecture forces you to rewrite the backend logic separately for each client, leading to massive code duplication and maintenance nightmares.

### Decoupled API-Driven Architecture
In modern architecture, the frontend client and the backend server are completely independent software entities. They communicate strictly over the network using HTTP protocols and exchange data using JSON.

```
+--------------+
|   Web UI     | -----\
+--------------+       \
+--------------+        v      +-------------+      +--------------+
| Android App  | ------------> |  API Layer  | ===> | Backend/DB   |
+--------------+        ^      +-------------+      +--------------+
+--------------+       /
|   iOS App    | -----/
+--------------+
```

* **Benefits:**
  * **Loose Coupling:** The backend doesn't care how the frontend is built (React, Swift, Kotlin), and the frontend doesn't care what language the backend uses (Python, Java, Go). As long as the API contract is maintained, both can evolve independently.
  * **Reusability:** A single backend API can serve multiple clients (web browser, Android app, iOS app, and smart TV apps) simultaneously, eliminating duplicate backend work.
  * **Secure Integration:** External third-party apps can hit public API endpoints without ever seeing the database or internal code.

---

## APIs in the Machine Learning Ecosystem

In machine learning, model training and building is typically done in Python-centric environments (like Jupyter Notebooks). Once a model is finalized and achieves good accuracy, we need to make it accessible to real-world applications.

```
                                  +-----------------------+
                                  |     BACKEND API       |
+------------+     HTTP (JSON)    |                       |
|  Frontend  | -----------------> | [FastAPI Controller]  |
| (Web/App)  | <----------------- |           |           |
+------------+     HTTP (JSON)    |           v           |
                                  |    [ML Model (run)]   |
                                  +-----------------------+
```

1. **The Role of FastAPI:** We build a web server wrapper using FastAPI that loads the serialized model (e.g., a `.pkl` or `.h5` file).
2. **Exposing Endpoints:** FastAPI exposes an endpoint (e.g., `/predict`).
3. **Serving Predictions:** 
   * The client application sends input features in JSON format to the API endpoint.
   * FastAPI parses the JSON, passes the values to the Python ML model, and runs the prediction.
   * The prediction output is packed back into JSON format and returned to the client.
4. **Third-Party Access:** When OpenAI released ChatGPT, they exposed it via an API. Companies like Zomato, Swiggy, and Amazon did not need to download the massive GPT weights or access OpenAI's internal database; they simply send user queries to the OpenAI API endpoint and receive the text response back via JSON.

### Conceptual Code Example (Client-Server Request)
Here is how a frontend client in Python would send features to an ML API endpoint to get a prediction:

```python
import requests

# 1. Define the API endpoint URL (hosted backend)
api_url = "https://api.my-ml-service.com/predict"

# 2. Package the feature inputs into a JSON payload
payload = {
    "age": 28,
    "income": 75000,
    "credit_score": 720
}

# 3. Send a POST request to the API with the JSON data
response = requests.post(api_url, json=payload)

# 4. Parse the JSON response returned by the API
if response.status_code == 200:
    prediction = response.json()
    print(f"Prediction: {prediction['result']}") # e.g., "Approved"
else:
    print(f"Error: API returned status code {response.status_code}")
```

**Interview / exam angle:**
*Question:* "Why can't we just deploy an ML model directly inside a mobile app or a web browser instead of wrapping it in an API?"
*Answer:* ML models (especially Deep Learning and LLMs) are computationally heavy, require specific hardware (GPUs), and are written in Python. Mobile devices or web browsers (running JavaScript) don't have the memory/hardware or the runtime support. Wrapping the model in an API allows it to run on a powerful cloud server while lightweight clients just send requests and receive predictions.

---

## Added Context

* **JSON (JavaScript Object Notation):** The default data format for APIs today. It is lightweight, text-based, and human-readable, consisting of key-value pairs.
* **REST APIs:** Most APIs built with FastAPI follow REST (Representational State Transfer) architecture principles, communicating over HTTP standard methods (GET, POST, PUT, DELETE).

---

## Quick Recap

| Concept | One-liner |
|---|---|
| **API** | An intermediary connector that lets two software components securely talk to each other over HTTP. |
| **Monolith** | An application structure where the frontend and backend are tightly coupled in a single codebase. |
| **Decoupled Architecture** | Splitting frontend and backend into separate entities that communicate via APIs. |
| **FastAPI** | A high-performance Python framework used to build robust, scalable APIs, particularly popular for serving ML models. |

---

## Practice Check

1. Explain the difference between Monolithic and Decoupled architectures. What is the main risk of using a Monolithic architecture as a company scales its user base across web and mobile platforms?
2. In the restaurant analogy of an API, what do the *Chef*, the *Waiter*, and the *Menu* represent in software terms?
3. Suppose you build a churn prediction model in Python. Walk through the step-by-step flow of how an iOS app written in Swift displays a "Churn Risk Score" to a customer using your model.
4. Why is FastAPI highly favored in the AI/ML industry compared to older frameworks like Flask or Django? (Think about language integration and performance).

---
<!-- Long note complete. Companion: [01-what-is-an-api-short.md](01-what-is-an-api-short.md) -->
