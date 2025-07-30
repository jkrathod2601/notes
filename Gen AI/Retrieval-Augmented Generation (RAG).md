RAG is a technique that **improves the factual accuracy** of Large Language Models (LLMs) by connecting them to **external data sources** like PDFs, websites, databases, or documents.

- **Information Retrieval** (find relevant documents)
- **Text Generation** (use LLM to answer using retrieved docs)

            +---------------------+
            |  User Input (Query) |
            +---------+-----------+
                      |
            +---------v-----------+
            |  Embed Query (e.g., |
            |  OpenAI Embeddings) |
            +---------+-----------+
                      |
        +-------------v------------+
        |  Vector DB (e.g. Pinecone)|
        |  Find top K similar docs |
        +-------------+------------+
                      |
        +-------------v------------+
        |  Compose Prompt with     |
        |  Retrieved Context       |
        +-------------+------------+
                      |
            +---------v-----------+
            |   LLM Generates     |
            |   Final Answer      |
            +---------------------+

## Pros of RAG

- ✅ Up-to-date answers
- ✅ No need to fine-tune model
- ✅ Personal/private data access
- ✅ Cheaper than training LLMs

#### Challenges
| Challenge                | Solution                              |
| ------------------------ | ------------------------------------- |
| Chunking large documents | Use smart chunking (e.g., 512 tokens) |
| Irrelevant retrieval     | Use hybrid search (keyword + vector)  |
| Prompt too long          | Summarize or rank retrieved chunks    |
| Security in private data | Auth, masking, logs                   |
#### RAG vs Fine-tuning
| Criteria         | RAG                        | Fine-Tuning          |
| ---------------- | -------------------------- | -------------------- |
| Speed            | Fast (real-time data)      | Slow (training time) |
| Cost             | Low                        | Expensive            |
| Data Flexibility | Can change docs anytime    | Need retraining      |
| Accuracy         | High (with good retrieval) | High (but rigid)     |

#### Core Architecture of RAG

#### Components:

1. **User Query**
2. **Retriever**
    - Vector Store (like FAISS, Chroma, Weaviate)
    - Embedding Model (like OpenAI, BGE, Instructor, etc.)
3. **Reranker (optional)**
4. **Context Builder (Chunking + Selection)**
5. **Prompt Builder**
6. **LLM**
7. **Answer Generation**
8. **(Optional) Feedback Loop / Logging**

### Types of RAG Workflows
#### **Classic RAG**

- Retrieve top-K documents → concatenate into prompt → LLM generates answer.
- Simple but effective.
#### **RAG with Reranking**

- Retrieve many docs (e.g., top-20) → use reranker (like Cohere Rerank or BERT) → select best top-K (e.g., 5).
- Improves retrieval quality.
#### **Multi-Hop RAG**

- Chain of retrievals:
    - Query A → Retrieve docs → Extract new sub-queries → Retrieve again → Combine results.
- Good for complex reasoning

#### **RAG with Structured Tools**

- Retrieval is not only from documents but also from:
    - SQL databases
    - APIs
    - Codebases
- Example: RAG with LangChain + SQL Agent.

#### **Agentic RAG (Advanced)**

- Combines retrieval with an agentic loop (plan + reason + act).
- Components:
    - **Planner**: Break down user task.
    - **Retriever Agent**: Calls search tool.
    - **Memory / Scratchpad**: Stores interim knowledge.
    - **LLM**: Uses context to finalize response.


## Agentic Workflow in RAG

**Step-by-Step Agentic Flow:**

1. User Query → Initial Thought
2. Action → Call Tool (search/retrieval/API/DB)
3. Observe → Retrieve Result
4. Reflect → Think → Next Action
5. Final Answer

#### Indexing & Retrieval Methods
#### Chunking Strategies:

- Sentence-level
- Paragraph-level
- Fixed window size (e.g., 512 tokens with overlap)
#### Embedding Models:

- OpenAI (`text-embedding-3-small`)
- BAAI/bge
- Cohere Embed
- Sentence Transformers
#### Vector Databases:

- FAISS (local, fast)
- ChromaDB (open-source)
- Pinecone, Weaviate, Qdrant (hosted)
- Azure Cognitive Search (enterprise)
#### Search Types:

- **Semantic Search (Dense Vector Search)**
- **Hybrid Search** (BM25 + vector)
- **Rerankers** (Cross-encoders)


### **Prompt Construction Techniques**

- **Stuffing**: Concatenate all retrieved docs
- **Map-Reduce**: Generate partial responses per doc, then combine
- **Refine**: Start with one doc and refine answer with others
- **Auto-Merge**: Combine top results and reduce redundancy

### **Evaluation in RAG**

#### Metrics:

- **Retrieval:**
    - Recall@K
    - Precision
    - MRR (Mean Reciprocal Rank)
- **Generation:**
    - Factual accuracy (human eval or models like G-Eval)
    - Faithfulness (alignment with retrieved context)
    - BLEU, ROUGE, METEOR (for structured QA)

### Tools & Frameworks
| Tool            | Purpose                            |
| --------------- | ---------------------------------- |
| LangChain       | Chains, agents, tools, retrievers  |
| LlamaIndex      | Graph-based retrieval, SQL RAG     |
| Haystack        | RAG pipelines, evaluation          |
| DSPy            | Declarative RAG, compiler for LLMs |
| Semantic Kernel | Embedding, memory, orchestration   |

### **Best Practices in RAG**

- Chunk based on **semantic boundaries**, not just tokens.
- Use **rerankers** to improve doc quality.
- Ensure **source attribution** in final output.
- Monitor hallucination via grounding.
- Use **Hybrid Search** for keyword + semantic strength.

#### Enterprise-Ready RAG Architecture (Azure)
[User Query]
    ↓
[Azure OpenAI Embedding] → [Azure Cognitive Search] → [Reranker (AzureML)] 
    ↓
[Chunk Selection + Prompt Engineering]
    ↓
[Azure OpenAI (GPT-4)]
    ↓
[Answer + Sources]

![[Pasted image 20250730124225.png]]

### Agentic RAG Architecture

![[Pasted image 20250730124328.png]]