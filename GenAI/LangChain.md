---
tags:
  - langchain
  - agentic
  - genai
---
# What is LangChain?
---
- Its an open-source Python framework for developing LLM applications.
- It provides components and interfaces to integrate LLMs into AI applications
- Provides methods to respond to complex prompts, by retrieving data and generating a coherent summary.
- It *chains* together the *retrieval, extraction, processing, generation* operations from large amounts of text, and multiple sources.
- Easily integrates with *Vector Databases* for efficient semantic searches and information retrieval.
- Has *decomposition capabilities*, where a complex task is broken into manageable steps.

# Installing LangChain
---
```shell
uv init
uv add "langchain[openai]"
uv add python-dotenv
```

In the above example, we are going to use LangChain with OpenAI provider.
In the `.env` file, add the API key using `OPENAI_API_KEY`.

> Add a `.gitignore` file to ensure you do not upload `.env` file online

# Hello, World!
---

```python
# main.py file
from dotenv load_dotenv
from langachain.chat_models import init_chat_model

load_dotenv()

model = init_chat_model(
	model = 'gpt-4.1-mini',
	temperature = 0.1
)

response = model.invoke('Hello! What is LangChain?')

print(response.content)
```

# Message History
----

```python
# main.py file
from dotenv load_dotenv
from langachain.chat_models import init_chat_model
from langchain.messages import HumanMessage, AIMessage, SystemMessage

load_dotenv()

model = init_chat_model(
	model = 'gpt-4.1-mini',
	temperature = 0.1
)

conversaton = [
	SystemMessage("You are a senior programmer"),
	HumanMessage("What is Python?"),
	AIMessage()
	
]


response = model.invoke('Hello! What is LangChain?')

print(response.content)
```

# Prompt Templates
---
Prompt Templates are *pre-defined* recipes for generating effective prompts for LLMs. These templates include:
- Instructions for the LLM
- A few-shot examples to help the model understand context and expected responses
- Specific question directed at the LLM

```python
from langchain_core.prompts import PromptTemplate

# prompt template has placeholders for adjective and content
prompt_template = PromptTemplate.from_template(
	"Tell me a {adjective} joke about {content}"
)

# using the template
prompt_template.format(adjective="funny", content="math")
```

# LangChain Expression Language (LCEL)
---
**LCEL: LangChain Expression Language** is a pattern for building LangChain applications using the pipe `|` operator. It ensures a readable flow from input to output.

Below are the steps for creating an *LCEL Pattern*: 

1. Define a template with variables in curly braces, `{}`
2. Create a `PromptTemplate` instance
3. Build a chain using `|` to connect components
4. Invoke the chain with input values.


# Runnables
---

Runnables are the building blocks of LCEL, and connect different components (LLMs, Prompts, Output Parsers, Retainers) into a *pipeline*.  Each component is a "runnable", and they all speak the same language, i.e. there is no glue code required to connect them, allowing us to snap them together using the pipe operator.
The object we create using the pipe operator is called a *chain* or a `RunnableSequence`, and it chains components sequentially. It passes output from one component input to the next.


```python
# These two are identical:

# Method A: The Pipe (Standard)
chain = prompt | model | parser

# Method B: The Explicit Class
from langchain_core.runnables import RunnableSequence
chain = RunnableSequence(first=prompt, middle=[model], last=parser)
```

`RunnableParallel` runs components concurrently, and is created using a *dictionary*. 

```python
from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser

# 1. Setup
model = ChatOpenAI(model="gpt-4o", temperature=0.7)
parser = StrOutputParser()

# 2. Define your individual "Logic Branches"
pros_chain = ChatPromptTemplate.from_template("List 3 pros of {topic}.") | model | parser
poem_chain = ChatPromptTemplate.from_template("Write a 4-line poem about {topic}.") | model | parser

# 3. The Elegant LCEL Syntax
# Wrapping runnables in a dict {} automatically triggers parallel execution
chain = {
    "pros": pros_chain,
    "poem": poem_chain
}

# 4. Execute
# This still runs both branches simultaneously!
result = chain.invoke({"topic": "Space Exploration"})

print(result["pros"])
print(result["poem"])
```

LCEL provides elegant syntax shortcuts: instead of creating a `RunnableSequence`, the same syntax can be created using the pipe operator. Additionally, t treats a standard Python dictionary as an implicit `RunnableParallel`. By simply using `{ "key": ... }` inside your pipe sequence, you achieve the exact same parallel execution with much cleaner, more readable code.


