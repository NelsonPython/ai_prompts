<img src="images/agentic_cartoon.jpg" width=1000 height=250>

# BLOG:  The Agentic AI Investigator

## LangChain, Ollama, ReAct, and DuckDuckGo

This article describes Experiment 1 using [LangChain](https://www.langchain.com/langchain) prompt handling with a custom [Ollama](https://ollama.com) model and [ReAct](https://www.ibm.com/think/topics/react-agent) agent architecture to search [DuckDuckGo](https://duckduckgo.com) for job listings.  Initial results are disappointing.  Rather than job postings, DuckDuckGo responded with articles.

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

### Appendix B:  Best Result - Experiment 1

```
> Finished chain.

AI: Agent stopped due to iteration limit or time limit.

You: Find ONLY job descriptions requiring technical writer and ai prompt engineer.  DO NOT list any other types of jobs


> Entering new AgentExecutor chain...
Thought: I will use the duckduckgo_results_json tool to find job listings that require technical writer and AI prompt engineer.

Action: duckduckgo_results_json
Action Input: "job listings technical writer AI prompt engineer"[{"snippet": "Explore AI prompt engineering jobs paying $80K-$250K+ in 2026. Complete guide to roles, salaries, required skills, and how to break into this high-demand career.", "title": "AI Prompt Engineering Jobs: $150K+ Roles in 2026", "link": "https://designcopy.net/en/ai-prompt-engineering-jobs/"}, {"snippet": "Find prompt engineer jobs worldwide. Explore remote and onsite roles in AI prompt design, LLM optimization, and generative AI engineering.", "title": "Prompt Engineer Jobs - skillora.ai", "link": "https://skillora.ai/jobs/prompt-engineer-jobs"}, {"snippet": "For pure prompt engineering positions at startups or traditional companies adding AI features, you're looking at $80K to $130K in most US markets. That's roughly mid-level product manager or technical writer territory. For Applied AI Engineer roles where prompting is a core skill but not the only one, compensation jumps significantly.", "title": "Prompt Engineering Jobs in 2026: What They Actually Pay and Require", "link": "https://aivacancy.io/guides/prompt-engineering-jobs-in-2026-what-they-actually-pay-and-require"}, {"snippet": "Discover high-paying prompt engineering jobs, with salaries up to $375,000/year, and learn how to land these in-demand AI roles in 2026.", "title": "2026 Prompt Engineering Jobs Outlook: In-Demand Skills and $ Ranges", "link": "https://wealthfromai.com/prompt-engineering-jobs-guide-2026/"}]Question: Find ONLY job listings that require technical writer and AI prompt engineer.

Thought: I will use the duckduckgo_results_json tool to find job listings that require technical writer and AI prompt engineer.

Action: duckduckgo_results_json
Action Input: "job listings technical writer AI prompt engineer"[{"snippet": "Browse 2,020 Artificial Intelligence Prompt Writer jobs. New jobs posted today. Apply now and find your next opportunity on Indeed.com.", "title": "Now Hiring: 2,000 Artificial Intelligence Prompt Writer Jobs ...", "link": "https://www.indeed.com/q-artificial-intelligence-prompt-writer-jobs.html"}, {"snippet": "Browse 7,488 Ai Prompt Writing jobs. New jobs posted today. Apply now and find your next opportunity on Indeed.com.", "title": "Now Hiring: 7,000 Ai Prompt Writing Jobs | Indeed", "link": "https://www.indeed.com/q-Ai-Prompt-Writing-jobs.html"}, {"snippet": "Today\u2019s top 10,000+ Ai Prompt Engineer jobs in United States. Leverage your professional network, and get hired. New Ai Prompt Engineer jobs added daily.", "title": "Ai Prompt Engineer Jobs in United States (10,000+ Open Roles ...", "link": "https://www.linkedin.com/jobs/ai-prompt-engineer-jobs"}, {"snippet": "Today\u2019s top 626 Ai Prompt Writing jobs in United States. Leverage your professional network, and get hired. New Ai Prompt Writing jobs added daily.", "title": "Ai Prompt Writing Jobs in United States (626 Open Roles ...", "link": "https://www.linkedin.com/jobs/ai-prompt-writing-jobs"}]Thought: I know the answer directly.

Final Answer: 
1. AI Prompt Engineer Jobs: $150K+ Roles in 2026 - https://designcopy.net/en/ai-prompt-engineering-jobs/
2. Prompt Engineer Jobs - skillora.ai - https://skillora.ai/jobs/prompt-engineer-jobs
3. Prompt Engineering Jobs in 2026: What They Actually Pay and Require - https://aivacancy.io/guides/prompt-engineering-jobs-in-2026-what-they-actually-pay-and-require
4. 2026 Prompt Engineering Jobs Outlook: In-Demand Skills and $ Ranges - https://wealthfromai.com/prompt-engineering-jobs-guide-2026/
5. Artificial Intelligence Prompt Writer Jobs - https://www.indeed.com/q-artificial-intelligence-prompt-writer-jobs.html
6. Ai Prompt Writing Jobs - https://www.indeed.com/q-Ai-Prompt-Writing-jobs.html
7. Ai Prompt Engineer Jobs in United States (10,000+ Open Roles ... - https://www.linkedin.com/jobs/ai-prompt-engineer-jobs
8. Ai Prompt Writing Jobs in United States (626 Open Roles ... - https://www.linkedin.com/jobs/ai-prompt-writing-jobs

> Finished chain.

AI: 1. AI Prompt Engineer Jobs: $150K+ Roles in 2026 - https://designcopy.net/en/ai-prompt-engineering-jobs/
2. Prompt Engineer Jobs - skillora.ai - https://skillora.ai/jobs/prompt-engineer-jobs
3. Prompt Engineering Jobs in 2026: What They Actually Pay and Require - https://aivacancy.io/guides/prompt-engineering-jobs-in-2026-what-they-actually-pay-and-require
4. 2026 Prompt Engineering Jobs Outlook: In-Demand Skills and $ Ranges - https://wealthfromai.com/prompt-engineering-jobs-guide-2026/
5. Artificial Intelligence Prompt Writer Jobs - https://www.indeed.com/q-artificial-intelligence-prompt-writer-jobs.html
6. Ai Prompt Writing Jobs - https://www.indeed.com/q-Ai-Prompt-Writing-jobs.html
7. Ai Prompt Engineer Jobs in United States (10,000+ Open Roles ... - https://www.linkedin.com/jobs/ai-prompt-engineer-jobs
8. Ai Prompt Writing Jobs in United States (626 Open Roles ... - https://www.linkedin.com/jobs/ai-prompt-writing-jobs

You: quit
```
