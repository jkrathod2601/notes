A **Chain** is a pipeline that links together multiple components:

- PromptTemplates
- LLMs
- Tools
- Memory
- Output Parsers

**Why use Chains?**

| Feature    | Benefit                                       |
| ---------- | --------------------------------------------- |
| Modular    | Break complex workflows into simple steps     |
| Reusable   | Components (LLM, Prompt, Tools) can be reused |
| Composable | Stack Chains inside Chains                    |
| Scalable   | Easy to add memory, logic, or branching       |
**Types of Chains in LangChain**

| Chain Type                      | Description                                          | Example Use Case                             |
| ------------------------------- | ---------------------------------------------------- | -------------------------------------------- |
| 🔹 `LLMChain`                   | Single-step: Prompt → LLM → Output                   | Simple Q&A or rewriting text                 |
| 🔹 `SimpleSequentialChain`      | Run one chain after another, no input/output mapping | Translate then summarize                     |
| 🔹 `SequentialChain`            | Run chains sequentially **with variable management** | Extract info → summarize → reformat          |
| 🔹 `RouterChain`                | Dynamically choose sub-chain based on input          | Multilingual bot routing to different chains |
| 🔹 `TransformChain`             | Apply Python function between steps                  | Custom logic step                            |
| 🔹 `APIChain`                   | Call REST APIs and pass results to LLM               | Fetch weather/news before answering          |
| 🔹 `RetrievalQA` / `VectorDBQA` | RAG Chain using vector search + LLM                  | Document-based Q&A                           |

**`LLMChain` — The Most Basic Chain**

```
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate
from langchain.chat_models import ChatOpenAI

llm = ChatOpenAI()
prompt = PromptTemplate.from_template("Explain {topic} like I'm five.")
chain = LLMChain(llm=llm, prompt=prompt)

print(chain.run("machine learning"))
```

**SimpleSequentialChain**

```
from langchain.chains import SimpleSequentialChain

# Chain 1: Translate English → French
chain1 = LLMChain(llm=llm, prompt=PromptTemplate.from_template("Translate to French: {input}"))

# Chain 2: Summarize French sentence
chain2 = LLMChain(llm=llm, prompt=PromptTemplate.from_template("Summarize this: {input}"))

sequential_chain = SimpleSequentialChain(chains=[chain1, chain2])
print(sequential_chain.run("LangChain is amazing!"))
```

**`SequentialChain` (Advanced, with variable passing)**

```
from langchain.chains import SequentialChain

chain1 = LLMChain(llm=llm,
  prompt=PromptTemplate.from_template("Give a catchy name for a company that makes {product}."),
  output_key="company_name")

chain2 = LLMChain(llm=llm,
  prompt=PromptTemplate.from_template("Write a tagline for {company_name}."))

seq_chain = SequentialChain(
  chains=[chain1, chain2],
  input_variables=["product"],
  output_variables=["company_name", "text"]
)

print(seq_chain.run({"product": "AI-powered sneakers"}))
```

**TransformChain**

```
from langchain.chains import TransformChain

def lowercase(inputs):
    return {"output": inputs["text"].lower()}

transform_chain = TransformChain(
    input_variables=["text"],
    output_variables=["output"],
    transform=lowercase
)
```

**`RetrievalQA` / `VectorDBQA` — For RAG**

```
from langchain.chains import RetrievalQA

qa_chain = RetrievalQA.from_chain_type(
    llm=llm,
    retriever=my_vectorstore.as_retriever()
)

qa_chain.run("What does the document say about transformers?")
```


| Chain Type              | Purpose                               | Use Case                              |
| ----------------------- | ------------------------------------- | ------------------------------------- |
| `LLMChain`              | Prompt + LLM                          | Rewriting, answering                  |
| `SimpleSequentialChain` | Chain1 → Chain2 (no variable mapping) | Translate → summarize                 |
| `SequentialChain`       | Controlled variable flow              | Extract → Analyze → Reuse             |
| `RouterChain`           | Dynamic route logic                   | Lang detection, domain-specific logic |
| `TransformChain`        | Custom Python logic                   | Filter, convert, adjust               |
| `APIChain`              | Call API + pass result to LLM         | Live weather, stock price             |
| `RetrievalQA`           | RAG-style Doc Q&A                     | PDF / KB QA                           |