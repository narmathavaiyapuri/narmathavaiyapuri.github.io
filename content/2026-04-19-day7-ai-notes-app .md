Title: Day 7 – AI Notes App with FastAPI, MongoDB & Local LLM  
Date: 2026-04-20  
Category: GenAI  
Tags: GenAI, FastAPI, MongoDB, LLM  
Slug: day7-ai-notes-app  
Status: published  


## Introduction

In this session, I built an AI-powered Notes application by integrating a local Large Language Model with FastAPI and MongoDB.

This project goes beyond basic APIs by combining model inference, backend logic, and persistent storage — similar to how real-world AI systems operate.

The goal was to create a system where users can send prompts, receive AI-generated responses, and store the entire conversation with timestamps.

---

## Architecture

User → FastAPI → LLM (llama.cpp) → MongoDB → Response  

- FastAPI handles incoming requests  
- The prompt is sent to a local LLM (TinyLlama via llama.cpp)  
- The model generates a response  
- The response is stored in MongoDB  
- Final output is returned to the user  

This pipeline reflects a typical AI backend workflow.

---

## Core Features

- Chat with a locally running LLM  
- Store prompts and responses in MongoDB  
- Maintain session-based chat history  
- Track timestamps for each interaction  
- REST API built using FastAPI  
- Easy testing via Swagger UI  

---

## API Endpoints

### POST /chat  
Send a prompt and receive an AI response.  
Also stores the conversation in the database.

### GET /notes  
Returns all saved conversations (latest first).

### GET /notes/{session_id}  
Fetches chat history for a specific session.

### DELETE /notes/{note_id}  
Deletes a specific note.

### GET /stats  
Provides basic usage insights like total notes and sessions.

---

## Running the System

### Start the LLM Server
```bash
llama-server.exe -m "path_to_model.gguf"
```

---

## Running the FastAPI Server

```bash
uvicorn main:app --reload
```

---

### Swagger UI

http://127.0.0.1:8000/docs  

This interface helps test APIs without a frontend.

---

## Database Structure

Each conversation is stored as:

```json
{
  "prompt": "...",
  "response": "...",
  "session_id": "...",
  "timestamp": "..."
}
```

This structure allows efficient storage and retrieval of chat history.

---

## Testing and Debugging

- Swagger UI used for API testing  
- Jupyter Lab used to verify MongoDB data  
- Environment variables managed using `.env`  
- Curl used for direct API calls  

---

## Challenges Faced

- Setting up and running the local LLM  
- Fixing connection issues between FastAPI and the model  
- Handling environment variables in different environments  
- Debugging MongoDB connection errors  
- Ensuring proper request and response formatting  

---

## Conclusion

This project provided practical experience in building a complete AI backend system.

By integrating FastAPI, MongoDB, and a local LLM, I understood how AI applications handle requests, process data, and persist results.

---

## Future Improvements

- Build a frontend chat interface  
- Add real-time streaming responses  
- Implement authentication system  
- Deploy the application to the cloud  

---

## Outcome

Successfully built a functional AI Notes application that can generate, store, and retrieve intelligent conversations — forming a solid foundation for scalable AI applications.
