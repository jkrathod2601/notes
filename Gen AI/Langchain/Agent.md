An **Agent** is an LLM-powered controller that can:

- **Decide** what action to take (like calling a tool or asking follow-up questions)
- **Call tools/APIs** based on reasoning
- **Use memory and context** across multiple steps
- **Plan** and execute multiple steps autonomously

**Agent Workflow (ReAct Pattern)**
1. **User asks a question**
2. LLM **thinks** → picks the right tool
3. **Tool is called**, result returned
4. LLM **thinks again**, may call another tool or finalize answer
5. Final **Answer** returned

```Thought: I should use the Calculator
Action: Calculator
Action Input: 4 * 12
Observation: 48
Final Answer: The result is 48
```

**Components of an Agent**

| Component            | Role                                           |
| -------------------- | ---------------------------------------------- |
| 🧠 LLM               | Brain of the agent                             |
| 🧾 Prompt            | ReAct or custom format                         |
| 🧰 Tools             | Search, calculator, API, DB, Python REPL, etc. |
| 📦 Memory (optional) | Track prior conversations                      |
| 🧩 AgentExecutor     | Wraps it all together                          |

Basic Example

```
from langchain.agents import initialize_agent, load_tools
from langchain.chat_models import ChatOpenAI

llm = ChatOpenAI(model="gpt-4")
tools = load_tools(["serpapi", "llm-math"], llm=llm)

agent = initialize_agent(
    tools=tools,
    llm=llm,
    agent="zero-shot-react-description",
    verbose=True
)

response = agent.run("What's the weather in Mumbai and what is 13 squared?")
```


**Types of Agents in LangChain**

| Agent Type               | Description                          | When to Use                    |
| ------------------------ | ------------------------------------ | ------------------------------ |
| 🧠 `ZeroShotAgent`       | Uses ReAct and tool descriptions     | Most common                    |
| 🔁 `ConversationalAgent` | Designed for chat + memory           | Chatbot agents                 |
| 📍 `PlanAndExecuteAgent` | Breaks task into plan, then executes | Multi-step task solving        |
| ⚙️ `MultiActionAgent`    | Calls multiple tools per step        | Parallel tool usage (advanced) |
| 🔎 `StructuredChatAgent` | Structured input/output              | Controlled tool inputs         |

**Agent vs Chain — Key Difference**

| Feature    | Chain                 | Agent                                        |
| ---------- | --------------------- | -------------------------------------------- |
| Flow       | Fixed sequence        | Dynamic, LLM decides                         |
| Tools      | Usually no tool use   | Can call tools                               |
| Complexity | Simple to moderate    | Good for open-ended or unknown steps         |
| Example    | Translate → summarize | "Find weather, analyze stock, write summary" |

#### **Types of Agnets**

##### **ZeroShotAgent** (most common)
**Uses**: Decides tool usage by analyzing the input and matching tool descriptions. Based on ReAct (Reason + Act) framework.

```
from langchain.agents import load_tools, initialize_agent
from langchain.chat_models import ChatOpenAI

llm = ChatOpenAI(model="gpt-4")
tools = load_tools(["llm-math"], llm=llm)

agent = initialize_agent(
    tools=tools,
    llm=llm,
    agent="zero-shot-react-description",
    verbose=True
)

response = agent.run("What is 23 * 7?")
```

#### **ConversationalAgent**
Best for chatbots. Remembers context (with memory), good for follow-up questions.

```
from langchain.memory import ConversationBufferMemory
from langchain.agents import ConversationalAgent, AgentExecutor

memory = ConversationBufferMemory(memory_key="chat_history")

agent_chain = initialize_agent(
    tools=tools,
    llm=llm,
    agent="conversational-react-description",
    memory=memory,
    verbose=True
)

agent_chain.run("Who is the president of India?")
agent_chain.run("What is his age?")
```

#### **PlanAndExecuteAgent**
For **multi-step tasks**, breaks the goal into subgoals and executes them.

```
from langchain.agents import PlanAndExecuteAgent
from langchain.experimental.plan_and_execute import load_agent_executor

planner_executor = load_agent_executor(
    llm=llm,
    tools=tools,
    verbose=True
)

planner_executor.run("Get today's weather in Mumbai and summarize it in 10 words.")
```

The LLM will:

1. Plan steps:
    - Search for weather
    - Extract temp
    - Summarize
2. Use tools with parameters like:
    - `SerpAPI("Weather in Mumbai")`
    - `LLM("Summarize in 10 words")`


#### **MultiActionAgent**
Can call multiple tools **in parallel** at each step. (Advanced, usually used in LangGraph)

🔧 Currently requires custom setup.

#### **StructuredChatAgent**
Forces the LLM to provide structured input to the tool (like JSON keys for params)

| Agent Type          | Key Feature                  | Example Use                    |
| ------------------- | ---------------------------- | ------------------------------ |
| ZeroShotAgent       | Decides tool use from prompt | “What is 23 * 7?” → Calculator |
| ConversationalAgent | Maintains memory             | Chatbots, context-aware Q&A    |
| PlanAndExecuteAgent | Long task → break → execute  | Research + summarize           |
| MultiActionAgent    | Calls many tools at once     | Parallel analysis (advanced)   |
| StructuredChatAgent | Structured input/output      | JSON input to tools            |

| Tool Type                               | Can Accept Multiple Params?      | Example                          |
| --------------------------------------- | -------------------------------- | -------------------------------- |
| `Tool(func=lambda x: f(...(**eval(x)))` | ✅ Yes, if input is dict          | `{"a": ..., "b": ...}`           |
| `StructuredTool` + `Pydantic`           | ✅✅ Yes (recommended)             | Cleaner, safer multi-param calls |
| `Tool(func: Callable[[str], str])`      | 🚫 No (only single string param) | Limited                          |