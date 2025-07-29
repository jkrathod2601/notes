An LLM is a **deep learning model** trained on **massive amounts of text** to understand and generate human-like language.

- Learns grammar, facts, reasoning, and context.
- Can write code, summarize, translate, answer questions.

- **GPT-4, GPT-3.5 (OpenAI)** — ChatGPT
- **LLaMA (Meta)** — open-source
- **Gemini (Google)** — multi-modal
- **Claude (Anthropic)** — safety focused

**Transformers: The Backbone of LLMs**
- Introduced by Google’s 2017 paper: **“Attention Is All You Need”**
- **No RNNs/CNNs** — works with full sentences using _attention_.
- **Processes words in parallel**, not sequentially → fast & scalable.

## Key Concept: **Attention Mechanism**

Instead of processing word-by-word like RNNs, Transformers use **attention** to focus on **relevant parts of**

Input sentence:
"The animal didn't cross the street because it was too tired."

“it” refers to “the animal” — attention helps the model figure that out.

Mathematically, attention assigns **weights** to each word in the sentence depending on its relevance.

#### Transformer Components
###  a. **Encoder**
- Takes input and converts to embeddings (used in BERT).
###  b. **Decoder**
- Takes embeddings and generates output (used in GPT).
### c. **Positional Encoding**
- Since transformers don’t use time steps, they add “position” manually so models know word order.

### Tokenization
Text → Tokens → Input to model
LLMs work with **tokens**, not words. Even a word like “unbelievable” might be split as `["un", "believable"]`.