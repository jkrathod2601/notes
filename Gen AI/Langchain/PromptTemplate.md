`PromptTemplate` lets you create **prompt templates with variables** that can be filled dynamically.  
This avoids hardcoding prompt strings and makes your LLM workflows clean, modular, and scalable.

|Feature|Benefit|
|---|---|
|Reusability|Use the same template with different inputs|
|Readability|Clear separation between logic and text|
|Modularity|Easy to update prompts in one place|
|Few-shot Examples|You can include examples and variables|
```
from langchain.prompts import PromptTemplate

template = "What is a good name for a company that makes {product}?"
prompt = PromptTemplate.from_template(template)

formatted_prompt = prompt.format(product="AI-powered shoes")
print(formatted_prompt)
```

```
template = PromptTemplate(
    input_variables=["adjective", "animal"],
    template="Tell me a {adjective} story about a {animal}."
)

prompt_text = template.format(adjective="funny", animal="cat")
```

```
from langchain.chat_models import ChatOpenAI
from langchain.chains import LLMChain

prompt = PromptTemplate.from_template("Explain {topic} like I'm five.")
llm = ChatOpenAI()
chain = LLMChain(llm=llm, prompt=prompt)

output = chain.run(topic="quantum physics")
print(output)
```

### Few-shot PromptTemplate

```
example_prompt = PromptTemplate(
    input_variables=["question", "answer"],
    template="Q: {question}\nA: {answer}"
)

examples = [
    {"question": "What is 2+2?", "answer": "4"},
    {"question": "Capital of France?", "answer": "Paris"},
]

example_strings = [example_prompt.format(**ex) for ex in examples]
few_shot_prompt = "\n".join(example_strings)

final_template = PromptTemplate(
    input_variables=["context", "question"],
    template=f"{few_shot_prompt}\n\nContext: {context}\n\nQ: {question}\nA:"
)

print(final_template.format(context="Some general facts", question="What is 3+5?"))
```

