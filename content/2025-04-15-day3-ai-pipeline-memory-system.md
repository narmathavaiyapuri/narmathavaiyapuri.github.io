Title: Day 3 – Building an End-to-End AI Pipeline  
Date: 2025-04-15  
Category: GenAI  
Tags: GenAI, AI Pipeline, llama.cpp, MongoDB  
Slug: day3-ai-pipeline-memory-system  
Status: published  

## Introduction

In real-world AI systems, models alone are not enough. They need memory, structured outputs, and backend logic to work effectively.

To understand this, I built a simple end-to-end AI pipeline using a local model (llama.cpp) and MongoDB.

In this session, I focused on:

- Running a local AI model  
- Structuring AI responses  
- Storing and retrieving data  
- Building a stateful AI system  

---

## 1. Understanding the AI Pipeline

### Flow

User → FastAPI → AI (llama.cpp) → Decision → MongoDB → Response  

This pipeline shows how AI systems process input, use memory, and return meaningful responses.

---

## 2. Running a Local AI Model

I used llama.cpp with a GGUF model to run the AI locally.

- Temperature → controls creativity  
- Top-p → controls randomness  
- Max tokens → controls response length  

This allows better control, privacy, and offline capability. It also reduces dependency on external APIs.

### Example

User says:

"Remember that I like AI"

→ Prompt is sent to the AI (llama.cpp)  
→ AI understands the intent  
→ AI responds with structured output:

{
  "action": "store",
  "data": "User likes AI"
}

---

## 3. Structuring AI Output
```
TOP:
Response for user

BOTTOM_JSON:
{
  "action": "store" | "retrieve" | "none",
  "data": "..."
}
```

This helps the system understand and act on AI responses. Structured output ensures reliable communication between the AI and the backend.

---

## 4. MongoDB as a Memory System

MongoDB is used to store and retrieve user data, enabling memory and personalization. This allows the system to persist user data and reuse it across multiple interactions.

## Example 
```

{
  "text": "User likes AI",
  "date": "2025-04-15"
}
```

### How it works for example:

Later, the user asks:

"What do I like?"

→ We search in MongoDB  
→ Answer: "You like AI"

---

## 5. Building Stateful AI

- Store user inputs  
- Retrieve memory  
- Use it in responses  

This makes the system more intelligent by remembering past interactions and improving response quality over time.

---

## 6. AI Decision Making

- store → save data  
- retrieve → fetch data  
- none → normal response  

This approach enables the AI to act like an agent that can decide what action to take based on the user input.

---

## 7. Pipeline Execution Logic

1. Receive user input through FastAPI  
2. Retrieve memory from MongoDB  
3. Send the prompt to the AI model  
4. Generate a structured response  
5. Parse the JSON output  
6. Execute the required action  
7. Return the final response  

This step-by-step execution ensures that the system behaves consistently and can scale for real-world applications.

---

## Real-World Use Case

This type of AI pipeline can be used in chatbots, virtual assistants, and recommendation systems where memory and decision-making are important.

---

## Final Thoughts

This project helped me understand how AI models, backend systems, and databases work together to build real-world applications.

By combining llama.cpp, MongoDB, and structured outputs, I built a simple system that can respond, remember, and take actions.