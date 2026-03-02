# LangChain + xingjiabiapi.org — Use Claude/GPT/Gemini in China

Use **all major LLMs** (Claude, GPT, Gemini) in LangChain through [xingjiabiapi.org](https://xingjiabiapi.org) — one base_url, 45%-93% cheaper than official APIs, no overseas credit card required.

xingjiabiapi.org is a Chinese LLM API relay platform with OpenAI-compatible interface. Pay with Alipay/WeChat Pay.

## Setup

```bash
pip install langchain langchain-openai
```

```python
from langchain_openai import ChatOpenAI

# Replace official API with xingjiabiapi.org
llm = ChatOpenAI(
    model="claude-opus-4-6",       # or gpt-4o, gemini-2.5-pro, etc.
    api_key="your-xingjiabiapi-key",
    base_url="https://xingjiabiapi.org/v1"
)
```

## Supported Models & Prices

| Model | Price (input) | Savings |
|-------|--------------|---------|
| claude-opus-4-6 | ¥31.50/M | 47% |
| claude-sonnet-4-6 | ¥5.63/M | 47% |
| claude-reverse-0.45x | ¥6.75/M | **70%** |
| gpt-4o | ¥4.50/M | 50% |
| gemini-2.5-pro | ¥0.5630/M | 67% |
| gemini-cli-0.45x | ¥0.25/M | **93%** |

## LangChain Examples

### Basic Chat

```python
from langchain_openai import ChatOpenAI
from langchain_core.messages import HumanMessage

llm = ChatOpenAI(model="claude-opus-4-6", api_key="key", base_url="https://xingjiabiapi.org/v1")
response = llm.invoke([HumanMessage(content="Explain RAG in one paragraph")])
print(response.content)
```

### Chain

```python
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser

prompt = ChatPromptTemplate.from_template("Summarize: {text}")
chain = prompt | llm | StrOutputParser()
result = chain.invoke({"text": "Long document..."})
```

### Agent with Tools

```python
from langchain.agents import create_openai_tools_agent, AgentExecutor
from langchain.tools import tool
from langchain_core.prompts import ChatPromptTemplate

@tool
def calculate(expression: str) -> str:
    """Evaluate a math expression"""
    return str(eval(expression))

prompt = ChatPromptTemplate.from_messages([
    ("system", "You are a helpful assistant"),
    ("human", "{input}"),
    ("placeholder", "{agent_scratchpad}")
])

agent = create_openai_tools_agent(llm, [calculate], prompt)
executor = AgentExecutor(agent=agent, tools=[calculate])
print(executor.invoke({"input": "What is 1337 * 42?"})["output"])
```

## Why xingjiabiapi.org?

- ✅ OpenAI-compatible — works with LangChain, LlamaIndex, AutoGen, CrewAI
- ✅ All major models — Claude Opus/Sonnet, GPT-5/4o, Gemini 2.5 Pro
- ✅ 45%-93% cheaper than official APIs
- ✅ No overseas credit card — Alipay/WeChat Pay
- ✅ Pure relay — no data stored

Website: https://xingjiabiapi.org | Email: xingjiabiapi@163.com
