#  ReAct Agent from Scratch

A simple, end-to-end implementation of a **ReAct (Reason + Act) AI Agent** using OpenAI and custom tools.

This project demonstrates how to build an AI agent that can:

* Reason about a problem
* Decide when to call tools (APIs/functions)
* Execute those tools
* Use results to generate a final answer

---

## What is ReAct?

ReAct stands for:

> **Reason → Act → Observe → Repeat → Answer**

Instead of answering in one step, the LLM:

1. Thinks about what it needs (**Reason**)
2. Calls a tool (**Act**)
3. Receives the result (**Observe**)
4. Repeats until it can answer (**Loop**)
5. Returns the final response

---

## Example Flow

User:

```
What's the weather in Bangalore? Should I carry an umbrella?
```

Agent:

```
→ Think: I need weather data
→ Call get_weather tool
→ Receive result
→ Think again: Do I need more info?
→ Generate final answer
```

---

## Agent Loop (Core Idea)

```python
while True:
    response = LLM(messages, tools)

    if response has tool_calls:
        execute tools
        append results to messages
    else:
        return final answer
```

---

## Features

* Custom tool definitions using JSON schema
* Manual ReAct loop implementation (no frameworks)
* Tool execution + result injection
* Multi-step reasoning using LLMs
* Supports multiple tools (weather, currency, etc.)

---

## Tech Stack

* Python
* OpenAI API
* JSON-based tool schema

---

## Project Structure

```
react-agent-from-scratch/
│
├── agent.py             # Main ReAct loop code
├── requirements.txt     # Dependencies
├── notebook.ipynb       # Colab-friendly version
└── README.md            # Project documentation
```

---

## Installation

```bash
pip install -r requirements.txt
```

---

## Setup

### Option 1: Environment Variable

```bash
export OPENAI_API_KEY=your_key_here
```

### Option 2: Direct in Code

```python
from openai import OpenAI
client = OpenAI(api_key="your_key_here")
```

---

## Run the Agent

```bash
python agent.py
```

---

## Tool Definition (What LLM Sees)

```python
tools = [
    {
        "type": "function",
        "function": {
            "name": "get_weather",
            "description": "Get weather for a city",
            "parameters": {
                "type": "object",
                "properties": {
                    "city": {"type": "string"}
                },
                "required": ["city"]
            }
        }
    }
]
```

The LLM ONLY sees this schema — not your code.

---

## Tool Implementation (Backend Logic)

```python
def get_weather(city):
    return {
        "temperature": "26°C",
        "condition": "Sunny"
    }
```

---

##Full Flow

```
User Question
   ↓
LLM decides → needs tool
   ↓
Tool is executed
   ↓
Result returned to LLM
   ↓
LLM reasons again
   ↓
Final answer
```

---

## Example Output

```
LLM decided to call tool:
→ get_weather(city="Bangalore")

Tool result:
→ {"temperature": "26°C", "condition": "Sunny"}

Final Answer:
The weather in Bangalore is 26°C and sunny. You likely don't need an umbrella.
```

---

## Key Concepts

* **Tools** → Functions LLM can call
* **Tool Schema** → JSON definition of tools
* **Agent Loop** → ReAct pattern
* **Tool Execution** → Your backend logic
* **Messages** → Memory of conversation

---

## Important Considerations

* Add max loop limit to avoid infinite loops
* Handle tool errors gracefully
* Monitor token usage (cost)
* Keep tool descriptions clear and specific

---

## Why This Matters

This is the foundation of:

* AI Agents (ChatGPT, AutoGPT)
* AI Copilots
* LLM-powered backend systems
* Autonomous workflows
* Tool-augmented reasoning systems

---

## Future Improvements

* Add more tools (currency, database, APIs)
* Add conversation memory
* Use LangGraph for orchestration
* Add streaming responses
* Add UI (React / Next.js frontend)

---

## Resume Bullet (Use This)

```
Built a ReAct-based AI agent using OpenAI that dynamically invokes external tools via JSON schema definitions, enabling multi-step reasoning and real-time data integration.
```

---

## Author

Sowmya
