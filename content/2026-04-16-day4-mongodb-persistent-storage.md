Title: "Day 4 – MongoDB Connection & Persistent Storage"
Date: 2026-04-16
Category: GenAI
Tags: [GenAI, MongoDB, Backend]
Slug: day4-mongodb-persistent-storage
Status: published


## Introduction

In AI systems, data should not be lost after execution. Persistent storage helps store data permanently.

### Use

- Store user inputs  
- Save AI responses  
- Maintain history  

On Day 4, I connected my Python application to MongoDB to build a persistent backend system.


## Understanding Persistent Storage

Persistent storage means saving data permanently in a database.

### Use

- Prevent data loss  
- Enable data reuse  
- Support long-term storage  

### Types

- **Stateless** → No memory  
- **Stateful** → Stores memory  

---

## MongoDB Overview

MongoDB is a NoSQL database that stores data as JSON-like documents.

### Use

- Store flexible data  
- Handle scalable applications  

### Structure

- Database  
- Collection  
- Document  

## Connecting Python to MongoDB
This step connects Python application with MongoDB.

### Use
- Insert data  
- Retrieve data  
- Build backend systems  
### Code

```python
from pymongo import MongoClient
from dotenv import load_dotenv
import os
import certifi

load_dotenv()

MONGO_URI = os.getenv("MONGO_URI")
DB_NAME = os.getenv("DB_NAME")

client = MongoClient(MONGO_URI, tls=True, tlsCAFile=certifi.where())

try:
    client.admin.command("ping")
    print("MongoDB Connected ✅")
except Exception as e:
    print("Connection Error ❌", e)

db = client[DB_NAME]
collection = db["ai_outputs"]
```

## Environment Variables

Environment variables store sensitive data securely.

### Use
- Protect credentials  
- Avoid exposing secrets  

### Code

```env
MONGO_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/ai_pipeline?retryWrites=true&w=majority
DB_NAME=ai_pipeline

```
## Inserting Data

Inserting data means storing new data into MongoDB.

### Use
- Save AI responses  
- Store user queries  

### Code

```python
from datetime import datetime, UTC

data = {
    "prompt": "What is AI?",
    "response": "AI is intelligence demonstrated by machines.",
    "timestamp": datetime.now(UTC)
}

result = collection.insert_one(data)
print("Inserted ID:", result.inserted_id)

```

## Retrieving Data

Retrieving data means fetching stored information.

### Use
- Access stored responses  
- View history  

### Types

#### Fetch all
```python
for doc in collection.find():
    print(doc)

```
### Fetch one
```python
result = collection.find_one({"prompt": "What is AI?"})
print(result)
```

## Saving AI Output
Saving AI output means storing prompt and response together.
### Use
- Maintain conversation history  
- Enable memory-based AI  
### Code

```python
def save_ai_output(prompt, response):
    from datetime import datetime, UTC

    data = {
        "prompt": prompt,
        "response": response,
        "timestamp": datetime.now(UTC)
    }

    collection.insert_one(data)
```

## System Flow

System flow shows how data moves in the application.

### Use
- Understand pipeline  
- Debug easily  

### Flow Diagram

![System Flow](images/system-flow.png)

-User input
-Python processes
-AI generates response
-Data stored in MongoDB
-Data retrieved when needed 

---

### Summary
Today, I learned how to connect Python with MongoDB and implement persistent storage.

### Key Learning
- Database integration  
- Data storage and retrieval  
- Building stateful AI systems  

This is an important step toward building real-world AI applications.