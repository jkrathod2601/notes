**Prompt Engineering** is the art and science of crafting inputs (prompts) to get desired, reliable outputs from LLMs.

Instead of fine-tuning the model, you "program" it using plain language.

#### Common Prompting Techniques

##### **Zero-shot Prompting**
Give **no examples**, just instructions.

```
Translate this sentence to Spanish:
"How are you?"
```

#### One-shot Prompting
Give **1 example** along with the task.

```
Translate English to French.

English: "Good morning"
French: "Bonjour"

English: "How are you?"
French:
```

#### **Few-shot Prompting**
Give **a few examples** to guide the model.

```
Classify the sentiment of the text.

Text: "I love this phone." → Positive  
Text: "It’s a waste of money." → Negative  
Text: "Delivery was late." →
```

#### Chain-of-Thought Prompting (CoT)
Ask the model to **show its reasoning** step by step.

```
If a train travels 60 km in 2 hours, what is its speed?

Let's think step by step.
```

```
Speed = Distance / Time  
= 60 / 2  
= 30 km/h
```

#### Role Prompting
Ask the model to play a specific **role or persona**.

```
You are a senior Python developer.  
Explain what a decorator is to a beginner.
```

#### Instruction Prompting
Explicit, direct task — used in models like GPT-4, Claude, or T5 (in “text-to-text” form).

```
Summarize this article in 2 bullet points.
[article text]
```

#### Delimiters & Format Control
Use clear **boundaries** in your prompt: triple quotes, XML tags, etc.

```
Summarize the paragraph below:

"""The Indian economy grew 7.8% last quarter..."""
```

#### Output Constraints
You can ask for structured output: JSON, tables, etc.

```
Give a JSON object with this information:
- Name
- Age
- Occupation

Name: Jay
Age: 26
Occupation: Cloud Architect
```

### Things to Watch Out For
| Problem        | Fix                           |
| -------------- | ----------------------------- |
| Hallucination  | Add constraints or references |
| Over-answering | Ask for fewer points / tokens |
| Vague output   | Give format examples          |
| Biases         | Specify tone / persona        |

## Tools That Help Prompt Engineering

- **LangChain** / **LlamaIndex** — orchestration and memory
- **PromptLayer** — prompt versioning
- **Guardrails AI** — validate structure/output
- **OpenAI playground** — experiment live

#### Prompt Engineering in Real GenAI Apps
| App Type      | Prompt Use Case                             |
| ------------- | ------------------------------------------- |
| Chatbot       | Persona, memory, tone control               |
| SQL Assistant | Convert natural language → SQL              |
| Doc QA        | RAG-based context injection + summarization |
| Email Helper  | Prompt as: “Write a reply to this email…”   |

#### Prompt Tuning 
Instead of manually writing prompts, **Prompt Tuning** involves learning prompts as vectors during training — better for performance at scale.