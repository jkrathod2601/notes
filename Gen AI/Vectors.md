A **vector** is a numeric representation of data as a list/array of numbers (usually floats), capturing **semantic meaning** of the data. It’s often used in **machine learning**, **NLP**, and **retrieval systems**.

Because ML models like **BERT, OpenAI embeddings, etc.** convert words, sentences, or images into **dense vectors** that capture **meaning** and **context**.

**dense vectors** : They consist of arrays with real numbers, where most or all elements are non-zero.

- Word similarity: “dog” vs “puppy” = similar vectors.
- Sentence retrieval: Find similar questions/answers.
- Image similarity: Search visually similar images.

#### What is a Vector Database?

- A **vector database** stores, indexes, and searches **high-dimensional vector embeddings** efficiently.  
- It’s optimized for **similarity search** using methods like **Approximate Nearest Neighbor (ANN)**.

#### Architecture Components:
| Component           | Description                                      |
| ------------------- | ------------------------------------------------ |
| **Embedding store** | Stores the vectors (e.g. `[0.23, 0.87, ...]`)    |
| **Metadata**        | Stores ID, text, tags, etc. with each vector     |
| **ANN Index**       | For fast similarity search (e.g., HNSW, IVF, PQ) |
| **API**             | For inserting, updating, querying vectors        |

### Example Workflow:

1. 🔤 **Input**: "What is cloud computing?"
2. 🔎 **Embedding**: Convert it to a vector using OpenAI/BERT.
3. 🗂️ **Search**: Use vector DB to find similar questions stored as vectors.
4. 📤 **Return**: Top 5 semantically relevant answers.

### Why Not SQL DB?

- SQL works with **structured** data (text, number).
- Vector DB works with **semantic** data (meaning).

You **can’t do similarity search** (`cosine`, `dot product`) efficiently in SQL for high-dimensional vectors.

#### Similarity Metrics in Vector DB:
| Metric                 | Use Case                                      |
| ---------------------- | --------------------------------------------- |
| **Cosine Similarity**  | Measures angle → best for semantic similarity |
| **Euclidean Distance** | Measures distance → used in spatial search    |
| **Dot Product**        | Common in recommendation systems              |

| 🔍 **Search Type**       | ✅ **Condition** (What it does)                         | 🔢 **Vector-Based / Embedding-Based** | ⚙️ **Method / Algorithm**          | 💡 **Simple Example**                                    |
| ------------------------ | ------------------------------------------------------ | ------------------------------------- | ---------------------------------- | -------------------------------------------------------- |
| **Lexical Search**       | Matches exact words or phrases                         | ❌ No                                  | BM25, TF-IDF                       | Query: `AI tools` → Finds docs with **exact** words      |
| **Semantic Search**      | Finds meaningfully similar content                     | ✅ Yes (Embedding-based)               | Cosine similarity, ANN             | Query: `AI benefits` → Finds: “advantages of AI systems” |
| **Hybrid Search**        | Combines lexical + semantic match                      | ✅ + ❌                                 | BM25 + Embedding similarity        | Query: `serverless cost` → Uses keyword + meaning        |
| **Similarity Search**    | Retrieves closest vectors (top-k)                      | ✅ Yes                                 | ANN (HNSW, IVF, PQ), Cosine        | Finds similar docs/questions to a query vector           |
| **Filtered Semantic**    | Semantic + metadata filtering                          | ✅ Yes                                 | Vector search + metadata filter    | Search: `AI in finance` + filter: `industry=banking`     |
| **Cross-Encoder Search** | Scores relevance using deep model                      | ✅ (No precomputed vectors)            | BERT cross-encoder re-ranking      | Query + doc scored together: `"What is AI?" + doc`       |
| **Multi-Modal Search**   | Search across image, text, audio etc. using embeddings | ✅ Yes                                 | CLIP, BLIP, multi-modal embeddings | Upload image → find related articles/products            |