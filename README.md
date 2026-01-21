# Simple AI Agent

A demonstration of an AI agent built with LangChain that can search the web and retrieve weather information using Ollama (local LLM).

## Overview

This project implements a ReAct (Reasoning and Acting) agent that can:
- Search the web using DuckDuckGo
- Fetch real-time weather information for any city
- Chain multiple tools together to answer complex queries

## Features

- **Web Search**: Uses DuckDuckGo search to find information on the internet
- **Weather Information**: Retrieves current weather data including temperature, humidity, wind speed, and conditions
- **ReAct Agent**: Implements the ReAct pattern for step-by-step reasoning and action
- **Local LLM**: Uses Ollama with Llama 3.1:8b model (no API costs!)

## Prerequisites

- Python 3.7+
- Ollama installed with the `llama3.1:8b` model
- OpenWeatherMap API key

## Installation

1. Clone this repository or download the notebook

2. Install Ollama from [https://ollama.ai](https://ollama.ai) and pull the model:
```bash
ollama pull llama3.1:8b
```

3. Install required Python dependencies:
```bash
pip install langchain_ollama langchain_community langchain_core duckduckgo-search
```

## Setup

1. **Ollama**: Make sure Ollama is running with the `llama3.1:8b` model

2. **OpenWeatherMap API Key**: Replace the API key in the `get_weather` function:
```python
api_key = 'your-openweathermap-api-key'
```

## Usage

The notebook demonstrates a complete workflow:

1. **Initialize the LLM**:
```python
llm = ChatOllama(model='llama3.1:8b')
```

2. **Set up tools**:
   - DuckDuckGo search tool for web searches
   - Custom weather tool for weather information

3. **Create the agent**:
```python
agent = create_react_agent(
    llm=llm,
    tools=[search_tool, get_weather],
    prompt=prompt
)
```

4. **Execute queries**:
```python
response = agent_executor.invoke({
    "input": "find the capital of Andhra Pradesh and what is the current weather of that city?"
})
```

## Example Query

The notebook includes an example that demonstrates the agent's ability to chain multiple operations:
- First, it searches for the capital of Andhra Pradesh (Amaravati/Vijayawada)
- Then, it retrieves the current weather in that city

## Project Structure

```
Simple AI Agent/
├── Agent.ipynb          # Main Jupyter notebook with agent implementation
└── README.md           # This file
```

## How It Works

The agent uses the ReAct pattern:
1. **Thought**: The agent thinks about what to do next
2. **Action**: It selects a tool and executes it
3. **Observation**: It observes the result
4. **Repeat**: The process continues until the answer is found

## Dependencies

- `langchain_ollama`: Ollama integration for LangChain (local LLM)
- `langchain_community`: Community tools including DuckDuckGo search
- `langchain_core`: Core LangChain framework components
- `langchain`: LangChain framework
- `requests`: HTTP library for API calls
- `duckduckgo-search`: DuckDuckGo search integration

## Notes

- The agent runs in verbose mode to show the reasoning process
- Uses Ollama for local LLM inference - no API costs!
- Weather API key should be kept secure and not committed to version control
- Weather data is provided in metric units (Celsius)

## License

This is a demonstration project for educational purposes.
