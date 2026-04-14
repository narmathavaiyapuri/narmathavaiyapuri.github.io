Title: Day 2 – Building APIs with FastAPI
Date: 2026-04-14
Category: GenAI
Tags: GenAI, FastAPI, APIs
Slug: day2-fastapi-get-post-api
Status: published

## Introduction

In Generative AI systems, models do not work in isolation. They rely on APIs to receive input, process data, and return responses.

To understand how backend systems work in AI applications, I built my first API using FastAPI.

In this session, I focused on:

- Creating API endpoints  
- Handling data using GET and POST requests  
- Validating input using Pydantic  
- Testing APIs using Swagger UI  

These concepts form the foundation of backend development for AI systems.

---

## 1. Setting Up FastAPI

### Installation

To begin, I installed the required packages:

### Command

pip install fastapi uvicorn

- FastAPI → framework to build APIs  
- Uvicorn → ASGI server to run the application  

### Role in GenAI

APIs act as the bridge between users and AI models. They handle incoming requests and send back model responses.

---

## 2. Creating the FastAPI Application

### Basic Setup
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello, GenAI World!"}
```
### Explanation

- FastAPI() initializes the application  
- @app.get("/") defines a GET endpoint  
- The function returns a JSON response  

### Role in GenAI

This is similar to how AI services expose endpoints to interact with models.

---

## 3. GET Endpoint – Retrieving Data

### Example
```python
@app.get("/items")
def get_items():
    return {
        "items": [
            {"id": 1, "name": "AI Agent"},
            {"id": 2, "name": "Chatbot"}
        ]
    }
```
### Purpose

- Retrieves data from the server  
- Returns structured JSON response  

### Role in GenAI

Used to fetch:
- stored responses  
- model outputs  
- system data  

---

## 4. POST Endpoint – Sending Data

### Request Flow

Send → Validate → Process → Respond

### Pydantic Model

from pydantic import BaseModel
```python
class Item(BaseModel):
    name: str
    price: float
    is_available: bool
```
This model defines the structure of the incoming data.

### POST Endpoint Example
```python
@app.post("/items")
def create_item(item: Item):
    return {
        "message": "Item received",
        "item": item
    }
```
### Purpose

- Receives user input  
- Validates data  
- Processes request  
- Returns response  

### Role in GenAI

POST requests are used to:
- send prompts  
- submit user input  
- interact with AI models  

---

## 5. Running the Server

### Command

uvicorn main:app --reload

### Explanation

- Runs the FastAPI application  
- Makes the API accessible in the browser  
- --reload enables auto-restart on changes  

### ASGI Server

ASGI (Asynchronous Server Gateway Interface) allows handling multiple requests efficiently, making it suitable for modern applications.

---

## 6. Testing APIs with Swagger

### What is Swagger?

Swagger is a tool that allows testing APIs directly from the browser without building a frontend.

### Features

- View all API endpoints  
- Test GET and POST requests  
- Send JSON input  
- View responses instantly  

### Swagger UI

Accessible at:

http://127.0.0.1:8000/docs

### Example Request
```python
{
  "name": "AI Tool",
  "price": 100,
  "is_available": true
}
```
### Types of Swagger

- Swagger UI → Interactive API testing interface  
- OpenAPI Specification → API structure in JSON format  
- ReDoc → Clean API documentation view  

---

## Final Thoughts

Building APIs is a key step in developing AI-powered applications.

- GET endpoints → retrieve data  
- POST endpoints → send and process data  
- Pydantic → ensures data validation  
- Swagger → simplifies API testing  

These components form the backbone of how AI systems interact with users and external services.