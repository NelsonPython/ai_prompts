<img src="images/agentic_cartoon.jpg" width=1000 height=250>

# BLOG:  The Agentic AI Investigator

## Agentic Experiments with Ollama, ReAct, and DuckDuckGo

*In-progress - use with caution - expect updates*

Example using LangChain prompt handling with a custom Ollama model and ReAct agent architecture to search DuckDuckGo.

### 1. Imports and Setup

```python
from langchain_core.prompts import PromptTemplate
from langchain_ollama import ChatOllama
from langchain_classic.agents import create_react_agent, AgentExecutor
from langchain_community.tools import DuckDuckGoSearchResults

```

* **Imports:** These modules pull in LangChain's prompt handling, Ollama integration, classic ReAct agent architecture, and the DuckDuckGo search tool.

---

### 2. Defining Tools

```python
search_tool = DuckDuckGoSearchResults(max_results=5)
tools = [search_tool]

```

* **Tools:** A single tool (`search_tool`) is configured to fetch up to 5 results from DuckDuckGo when the agent requires real-time or external web data.

---

### 3. Initializing the Local LLM

```python
llm = ChatOllama(
    model="factual-llama3.2:latest",
    temperature=0
)

```

* **Model:** Connects to your local Ollama instance running the `factual-llama3.2:latest` model. Setting `temperature=0` ensures deterministic, factual, and consistent responses.  `factual-llama3.2` was customized per instructions in the **Appendix:  Customize an Ollama Model** below.

---

### 4. Setting Up the ReAct Prompt

```python
template = """..."""
prompt = PromptTemplate.from_template(template)

```

* **ReAct Framework:** This custom template enforces a strict **Thought -> Action -> Action Input -> Observation** loop.
* **Critical Rules:** It instructs the model on exact tool names, forces it to skip searching for common knowledge, and provides placeholders for chat history, available tools, user input, and the agent's scratchpad.

---

### 5. Creating the Agent Executor

```python
agent = create_react_agent(llm, tools, prompt)
agent_executor = AgentExecutor(
    agent=agent, 
    tools=tools, 
    verbose=True, 
    handle_parsing_errors=True,
    max_iterations=3,
    max_execution_time=30
)

```

* **Agent & Executor:** `create_react_agent` binds the model and tools to the prompt template. The `AgentExecutor` manages the execution loop, including safety limits like `max_iterations=3` (preventing infinite loops) and `handle_parsing_errors=True` (catching formatting mistakes if the model outputs invalid text).

---

### 6. Interactive Chat Loop

```python
if __name__ == "__main__":
    ...
    while True:
        ...
        response = agent_executor.invoke({
            "input": user_input,
            "chat_history": chat_history
        })
        ...

```

* **CLI Loop:** Runs a continuous `while True` loop in your terminal. It accepts user input, passes it along with the running string-based `chat_history` to the agent executor, prints the output, and updates the history for the next turn.


### Appendix:  Customize an Ollama model

You can customize an Ollama model to be factual by using a Modelfile to lower the generation temperature, set strict behavioral constraints, and define factual guardrails in the system prompt.

#### Step 1: Create a Modelfile

Create a plain text file named Modelfile (without any file extension) in your working directory.  Write your configuration using FROM, PARAMETER, and SYSTEM directives:

```
# Choose a reliable base model
FROM llama3.1:8b

# Lower temperature to reduce hallucination and creativity (range 0.0 to 1.0)
PARAMETER temperature 0.1

# Restrict top_p sampling for more deterministic outputs
PARAMETER top_p 0.8

# Define strict factual system instructions
SYSTEM """
You are a strictly factual, objective assistant. 
- Rely only on verified facts.
- If you do not know an answer or are unsure, explicitly state "I do not know" rather than guessing or making up information.
- Do not speculate, fabricate citations, or embellish details.
"""
Use code with caution.
```

#### Step 2: Build the Custom Model

Open your terminal in the directory containing your Modelfile and run the ollama create command to build the model:

```
ollama create factual-llama -f ./Modelfile
Use code with caution.
```

#### Step 3: Test and Verify

Run your newly created custom model from the terminal:

```
ollama run factual-llama
Use code with caution.
```
