+++
title = 'Gentmini'
author = 'Abdullah Robbani'
date = 2025-09-03T20:30:06+08:00
draft = false
tags = ["Python", "Gemini", "AI Agent"]
categories = ["personal project"]
+++

📂 Repo: [github.com/babanini95/gentmini](https://github.com/babanini95/gentmini)

I've been curious about AI agent for a while now. It has been a hot topic in some of my social media timelines. And recently, I’ve been diving deeper into how AI agents work. Not just from the outside as a user of ChatGPT or Gemini, but how you can wire up a language model with tools and make it interact with an environment.  

To make the learning process hands on, I built [**Gentmini**](https://github.com/babanini95/gentmini): a minimal AI agent using Google’s Gemini API. It’s not a full fledged framework, but a focused learning project that helped me practice Python, functional programming, and understand the building blocks of agent design.

<!--more-->
___

## 🎯 Motivation & Learning Goals

The goals of this project are pretty simple:

- Explore multidirectory Python project structures  
- Understand **how AI agents work under the hood** instead of treating them as black boxes  
- Practice **Python + functional programming** in a practical setting  

The point wasn’t to reinvent the wheel by training a new LLM, but to see how to build an *agent layer* on top of an existing LLM.

___

## ⚙️ How Gentmini Works

At a high level, Gentmini acts as a bridge between user input, the Gemini API, and a set of predefined functions.  

Here’s the flow:  

1. User enters a task. Example: *“Add a new function to the calculator”*.  
2. Gemini processes the instruction.  
3. The agent checks if it needs to call one of its tools (functions). If needed, it calls the function with the right parameters. The checks and function call run in an iteration until the task is complete or a max step count is reached.
4. The function executes inside a controlled working directory (a simple calculator app).
5. The result is passed back through the agent to the user.  

Currently, Gentmini comes with four core functions:

- **Get file info**  
- **Read a file**  
- **Write to a file**  
- **Run Python code**  

This allows the agent to inspect, edit, and execute code in a constrained environment.

___

## 🗂️ Project Structure

```md
gentmini/
├── calculator/                 # A simple calculator app. Used for agent's working directory
├── functions/                  # Functions that the agent can call
│   ├── function_schema.py      # Function schemas for declaration
│   ├── get_file_content.py     
│   ├── get_files_info.py
│   ├── run_python.py
│   └── write_file.py         
├── call.py                     # Function that agent uses to call functions
├── config.py                   # Configuration file for the project
├── main.py                     # Main entry point for the agent
├── pyproject.toml              # Project metadata and dependencies
├── tests.py                    # Tests for the project
└── README.md                   # Documentation
```

___

## 🧩 Challenges & Learnings

A few key things I learned while building **Gentmini**:

- Schemas matter: structuring function definitions makes it easier for the LLM to call them reliably.
- Descriptions matter: writing clear, concise descriptions for each function helps the model understand their purpose. Few times, I had to iterate on the wording to make the agent behave as expected.
- Safety first: even though this was a toy project, it’s important to limit execution to a specific directory to avoid destructive file operations.
- Structure helps learning: organizing code into clear modules (instead of a single messy script) made it easier to see how everything connected.

This gave me a much clearer sense of what’s really happening when you hear the term “AI agent.”

___

## 🔮 What’s Next?

Gentmini is small by design, but there are plenty of directions it could grow:

- Add more tools (web search, data analysis).
- Improve error handling and logging.
- Expand beyond the calculator directory into broader environments.

__
