### **Text Generation**
Generate articles, summaries, stories, or replies.

📌 **Examples**:
- Blog generator: “Write a blog on AI in education”
- Email reply assistant: “Reply to this email saying I’m unavailable”
- Resume writer: “Generate a resume for a cloud architect with 5 years experience”

🧠 **Model Used:** GPT-4, Claude, Mistral

### **Code Generation / Programming Assistant**

Generate or fix code, explain functions.

📌 **Examples**:
- “Write a Python function to parse JSON”
- “Convert this Python function to JavaScript”
- “Explain this regular expression: `^(\+\d{1,3}[- ]?)?\d{10}$`”

🧠 **Model Used:** OpenAI Codex, GPT-4, Code Llama

🧪 **Tool:** GitHub Copilot, Cursor, Replit AI

### **Question Answering over Documents / PDFs**

Query large documents using LLM + vector search (RAG).

📌 **Examples**:
- “What are the refund policies in this PDF contract?”
- “Summarize the health benefits section in this insurance document”

🧠 **Model Used:** GPT-4 + RAG with LangChain or LlamaIndex

📂 **Storage:** Pinecone / ChromaDB / Weaviate

### **SQL Assistant / Data-to-Text**

Translate human questions to SQL or read from DBs.

📌 **Examples**:

- “Show me the top 5 products sold in Q1”
- “How many users signed up in the last 7 days?”

🧠 **Model Used:** GPT-4, fine-tuned SQL models

⚙️ **Tech:** Natural language → SQL → DB query → result

### **Chatbots & Virtual Assistants**

Provide support, tutoring, recommendations, etc.

📌 **Examples**:

- Customer support bot
- AI tutor for coding or math
- WhatsApp bot to answer product queries

🧠 **Tools:** GPT-4 + LangChain + memory + FastAPI

### **Summarization**

Condense long text, transcripts, meetings, etc.

📌 **Examples**:

- “Summarize this YouTube transcript in 5 points”
- “TL;DR this long email chain”
- “Summarize customer feedback into pros & cons”

🧠 **Models:** GPT, T5, BART, Claude

#### Automation with GenAI + Tools
| Integration           | Use Case                             |
| --------------------- | ------------------------------------ |
| GenAI + Zapier        | Auto-generate email replies          |
| GenAI + Google Sheets | Summarize long comments              |
| GenAI + APIs          | Build travel assistant, meal planner |


|Use Case|Inputs|Outputs|Models|
|---|---|---|---|
|Text Generation|Prompt text|Paragraphs|GPT, Claude|
|Code Assistant|Natural language|Code|Codex, CodeLlama|
|Doc QA (RAG)|Query + PDF|Answers|GPT + LangChain|
|SQL Assistant|Question|SQL + Result|GPT, fine-tuned|
|Image Generation|Prompt|Images|DALL·E, SD|
|Audio Generation|Text|Voice/music|Suno, TTS models|