Title: Day 5 – Running LLM Locally with llama.cpp  
Date: 2026-04-19  
Category: GenAI  
Tags: GenAI, llama.cpp, LLM, LocalAI  
Slug: day5-llama-cpp-local-llm  
Status: published  

## Introduction  

In Generative AI systems, most models are accessed through APIs. However, running models locally is becoming increasingly important for privacy, cost efficiency, and offline usage.

To understand how local inference works, I ran a Large Language Model (LLM) on my system using llama.cpp.

In this session, I focused on:

- Setting up llama.cpp  
- Loading a GGUF model  
- Running a model locally using CLI  
- Integrating the model with Python  

These concepts are essential for building offline AI applications.

---

## Setting Up llama.cpp  

### Installation  

To begin, I cloned and built llama.cpp from source:

### Command  

git clone https://github.com/ggerganov/llama.cpp  
cd llama.cpp  
cmake -B build  
cmake --build build --config Release  

### Explanation  

- Clones the repository  
- Builds the project using CMake  
- Generates the executable (llama-cli)  

### Role in GenAI  

This acts as the engine that runs LLMs locally without relying on cloud APIs.

---

## Understanding GGUF Models  

### What is GGUF?  

GGUF is a file format used to store optimized LLM models for efficient local inference.

### Example Model  

- TinyLlama  

### Model Type  

- Q4_K_M (quantized model)  

### Purpose  

- Reduces model size  
- Improves performance  
- Makes local execution feasible  

### Role in GenAI  

GGUF models allow developers to run AI models directly on personal machines.

---

## Running the Model (CLI)  

### Command  

./build/bin/llama-cli -m model.gguf -p "What is AI?"  

### Explanation  

- Loads the model file  
- Takes input prompt  
- Generates response locally  

### Output Behavior  

- Tokens are generated step-by-step  
- No internet connection required  

### Role in GenAI  

This is how local inference works without API calls.

---

## Python Integration  

### Installation  

pip install llama-cpp-python  

### Code  

```python
from llama_cpp import Llama

llm = Llama(model_path="model.gguf")

output = llm("What is AI?")
print(output["choices"][0]["text"])

```

---

### Explanation  

- Loads the model in Python  
- Sends prompt as input  
- Receives generated response  

### Role in GenAI  

Enables integration of LLMs into real-world applications like chatbots and tools.

---

## Key Concepts  

### GGUF Format  
Optimized format for running models efficiently on local systems.

### Quantization  
- Compresses model size  
- Improves speed  
- Slight reduction in accuracy  

### Local Inference  
Running AI models directly on a personal computer without cloud services.

---

## Advantages of Local LLM  

- No internet required  
- No API cost  
- Better data privacy  
- Fully offline usage  

---

## Final Thoughts  

Running LLMs locally is a powerful step in understanding how AI systems work beyond APIs.

- llama.cpp enables local model execution  
- GGUF models make it efficient  
- Python integration makes it usable in applications  

This approach helps in building cost-effective, private, and offline AI systems.