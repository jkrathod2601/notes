- **Memory** allows LangChain applications (especially Agents and Chains) to **store and recall information** from earlier interactions — just like a human would in a conversation.
- Without memory, every LLM prompt is stateless — it forgets previous messages.  
  With memory, your chatbot or agent becomes **context-aware**.

**Memory Types in LangChain**

|Memory Type|Description|Use Case|
|---|---|---|
|🧠 `ConversationBufferMemory`|Stores all messages in full|Chatbot with short conversations|
|📚 `ConversationBufferWindowMemory`|Only keeps last N exchanges|Lightweight chatbot with recent context|
|📜 `ConversationSummaryMemory`|Summarizes earlier conversation|Long-term, compressed memory|
|📖 `VectorStoreRetrieverMemory`|Semantic search over past chats|RAG + memory hybrid|
|📝 `ChatMessageHistory`|Stores chat messages only|Custom memory usage|
|📂 `CombinedMemory`|Mix multiple memories|Advanced use cases|

| Memory Type                         | Description                                              | Use Case                                 | Key Params                               | Sample Code                                                                                                                                       |
| ----------------------------------- | -------------------------------------------------------- | ---------------------------------------- | ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| **ConversationBufferMemory**        | Stores full conversation history                         | Short conversations, full context needed | `memory_key`, `return_messages`          | `python\nfrom langchain.memory import ConversationBufferMemory\nmemory = ConversationBufferMemory()\n`                                            |
| **ConversationBufferWindowMemory**  | Stores only last `k` interactions                        | Lightweight memory, short-term context   | `k` (number of recent messages)          | `python\nfrom langchain.memory import ConversationBufferWindowMemory\nmemory = ConversationBufferWindowMemory(k=3)\n`                             |
| **ConversationSummaryMemory**       | Summarizes older messages using LLM                      | Long sessions, compressed history        | `llm`, `memory_key`                      | `python\nfrom langchain.memory import ConversationSummaryMemory\nmemory = ConversationSummaryMemory(llm=llm)\n`                                   |
| **ConversationSummaryBufferMemory** | Combines summarization + recent buffer                   | Best of both: summary + recent detail    | `llm`, `max_token_limit`                 | `python\nfrom langchain.memory import ConversationSummaryBufferMemory\nmemory = ConversationSummaryBufferMemory(llm=llm, max_token_limit=1000)\n` |
| **ChatMessageHistory**              | Stores chat logs (no integration with chains by default) | Custom memory management                 | `add_user_message()`, `add_ai_message()` | `python\nfrom langchain.memory import ChatMessageHistory\nhistory = ChatMessageHistory()\nhistory.add_user_message(\"Hi\")\n`                     |
| **VectorStoreRetrieverMemory**      | Stores memories as embeddings, retrieves semantically    | Semantic memory / RAG hybrid             | `retriever`, `memory_key`                | `python\nfrom langchain.memory import VectorStoreRetrieverMemory\nmemory = VectorStoreRetrieverMemory(retriever=my_retriever)\n`                  |
| **CombinedMemory**                  | Combines multiple memory types                           | Advanced, multi-purpose agents           | `memories=[...]`                         | `python\nfrom langchain.memory import CombinedMemory\nmemory = CombinedMemory(memories=[memory1, memory2])\n`                                     |

```
from langchain.chains import ConversationChain
from langchain.chat_models import ChatOpenAI

llm = ChatOpenAI()

conversation = ConversationChain(
    llm=llm,
    memory=ConversationBufferMemory(),  # Replace with any memory from table
    verbose=True
)

conversation.run("Hello, I am Jay.")
conversation.run("What did I just say?")
```

