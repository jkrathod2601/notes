**LangChain** is a **framework to build applications powered by large language models (LLMs)**.  
It helps you chain together LLMs, memory, tools, APIs, databases, and documents in structured workflows.

Think of LangChain as the “backend logic” layer that lets LLMs interact with data and make decisions in a smart way.

| Feature       | Benefit                                                               |
| ------------- | --------------------------------------------------------------------- |
| **Chains**    | You can connect LLM outputs as inputs to other components.            |
| **Memory**    | Enable multi-turn conversations that feel contextual.                 |
| **Agents**    | Let the LLM decide which tools or APIs to use.                        |
| **Retrieval** | Plug in a vector DB and search relevant documents.                    |
| **Tools**     | Extend LLMs with capabilities like search, calculator, DB query, etc. |

**Core Component of LangChain**

|Component|Description|Example|
|---|---|---|
|🧾 `PromptTemplate`|Structured, dynamic prompt with variables|`"Tell me a joke about {topic}"`|
|🧠 `LLM`|Connect to OpenAI, Anthropic, etc.|`ChatOpenAI(model="gpt-4")`|
|🔗 `Chain`|Combine LLM + PromptTemplate + Output Parsing|`LLMChain(prompt, llm)`|
|🧰 `Tool`|Add search, calculator, DB tools|`SerpAPI`, `Python REPL`, etc.|
|🧠 `Memory`|Retain chat history|`ConversationBufferMemory()`|
|🤖 `Agent`|LLM decides which tool to use|“Should I search or calculate?”|

|Feature|Use Case|Core Benefit|
|---|---|---|
|**LCEL**|Build chains declaratively|Clean, readable, composable logic|
|**LangGraph**|Stateful, multi-agent workflows|Graph-based orchestration|
|**LangSmith**|Logging, debugging, evaluation|Production monitoring|
|**Streaming**|Real-time LLM output|Better UX|
|**Evaluation**|Test LLM response quality|Prompt/model comparison|