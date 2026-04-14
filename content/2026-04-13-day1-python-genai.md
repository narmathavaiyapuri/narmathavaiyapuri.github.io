Title: Day 1 – Python Foundations for GenAI
Date: 2026-04-13
Category: GenAI
Tags: GenAI, Python, LLM
Slug: day1-python-foundations-genai
Status: published

## Introduction

In Generative AI (GenAI), building models is only one part of the process. The real foundation lies in how we handle and structure data before it reaches the model.

To get started, I focused on three essential Python concepts:

- Variables  
- Lists  
- Dictionaries  

These form the backbone of how data flows in AI systems.

---

## 1. Variables – Storing Data

### What are Variables?

Variables are used to store values that can be reused and modified throughout a program.

### Common Data Types

- int → whole numbers  
- float → decimal values  
- string → text data  
- boolean → True or False  

```python
age = 21
price = 99.99
name = "Arun"
is_active = True
```

### Role in GenAI

In AI applications, variables are used to store:
- user prompts  
- model settings  
- outputs and responses  

```python
prompt = "Explain Artificial Intelligence in simple terms"
temperature = 0.7

print(prompt)
print(temperature)
```

Variables help manage dynamic data in AI workflows.

---

## 2. Lists – Managing Collections

### What are Lists?

Lists are ordered collections that can hold multiple values.

### Types of Lists

**Same type values:**
```python
numbers = [1, 2, 3, 4]
```

**Mixed values:**
```python
data = ["AI", 2026, True]
```

**Nested lists:**
```python
matrix = [[1, 2], [3, 4]]
```

### Role in GenAI

Lists are useful for storing:
- multiple inputs  
- sequences of data  
- conversation history  

```python
prompts = [
    "What is AI?",
    "Explain Machine Learning"
]

print(prompts[0])

prompts.append("Explain Deep Learning")
print(prompts)
```

They help maintain order and manage multiple values efficiently.

---

## 3. Dictionaries – Structuring Information

### What are Dictionaries?

Dictionaries store data in key-value format, making it easy to organize and access information.

### Examples

**Basic dictionary:**
```python
user = {
    "name": "Arun",
    "age": 21
}
```

**Nested structure:**
```python
user = {
    "name": "Arun",
    "details": {
        "age": 21,
        "city": "Chennai"
    }
}
```

**Dictionary with list (common in AI):**
```python
data = {
    "messages": [
        {"role": "user", "content": "Hi"},
        {"role": "assistant", "content": "Hello"}
    ]
}
```

### Role in GenAI

Dictionaries are critical because AI models expect structured input.

```python
message = {
    "role": "user",
    "content": "Write a short story"
}

print(message["role"])
print(message["content"])
```

They define *who* is speaking and *what* is being communicated.

---

## Combining Lists and Dictionaries

Real-world AI systems combine lists and dictionaries to represent conversations.

```python
chat_history = [
    {"role": "user", "content": "Hello"},
    {"role": "assistant", "content": "Hi! How can I help?"},
    {"role": "user", "content": "Explain AI"}
]

print(chat_history[-1]["content"])
```

This structure is widely used in chat-based AI applications.

---

## Final Thoughts

Understanding how to store and structure data is the first step in building AI systems.

- Variables → hold values  
- Lists → manage sequences  
- Dictionaries → organize structured data  

Together, they form the core data model behind modern GenAI applications.