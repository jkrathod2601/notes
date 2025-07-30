A **Tool** is a wrapper around a function (or API) that an **Agent can call** when it decides it needs to take an action.

|Tool Name|Functionality|
|---|---|
|`llm-math`|Math operations using LLM|
|`serpapi`|Google search results|
|`wikipedia`|Fetch content from Wikipedia|
|`python_repl`|Run Python code|
|`terminal`|Run terminal commands (dangerous)|
|`requests`|Make HTTP requests|
|`sql_database`|Query SQL databases|

```
def reverse_text(text: str):
    return text[::-1]

reverse_tool = Tool(
    name="TextReverser",
    func=reverse_text,
    description="Reverses the given text string. Input should be a string."
)
```

**Custom Tool with Multiple Parameters (StructuredTool)**

```
from langchain.tools import StructuredTool
from pydantic import BaseModel

class WeatherInput(BaseModel):
    city: str
    date: str

def get_weather(city: str, date: str):
    return f"The weather in {city} on {date} is 32°C and sunny."

weather_tool = StructuredTool.from_function(
    func=get_weather,
    name="GetWeather",
    description="Use this to get the weather for a city on a specific date.",
    args_schema=WeatherInput
)
```

## How Agents Choose Tools

LangChain agents use the tool descriptions to:

1. Parse user intent
2. Choose a tool
3. Format the input
4. Call the tool
5. Use the output in the next reasoning step