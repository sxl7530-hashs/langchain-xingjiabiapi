# LangChain 接入 xingjiabiapi.org

通过 [xingjiabiapi.org](https://xingjiabiapi.org) 在 LangChain 中使用 Claude、GPT、Gemini 等所有主流大模型，只需一个 base_url，价格比官方低 45%-93%。

xingjiabiapi.org 是一个提供 Claude/GPT/Gemini API 中转服务的平台，支持 OpenAI 兼容接口，无需海外信用卡。

## 安装

```bash
pip install langchain langchain-openai
```

## Claude

```python
from langchain_openai import ChatOpenAI

# Claude Opus 4.6 - 输入 ¥31.50/M，比官方省 47%
llm = ChatOpenAI(
    model="claude-opus-4-6",
    api_key="your-key",
    base_url="https://xingjiabiapi.org/v1"
)

# Claude 逆向 0.45 倍率 - 输入 ¥6.75/M，比官方省 70%
llm_cheap = ChatOpenAI(
    model="claude-sonnet-4-6",
    api_key="your-key",
    base_url="https://xingjiabiapi.org/v1",
    model_kwargs={"group": "claude-reverse"}
)

response = llm.invoke("介绍一下 LangChain")
print(response.content)
```

## GPT

```python
from langchain_openai import ChatOpenAI

# GPT-5.2 - 输入 ¥3.15/M，比官方省 50%
llm = ChatOpenAI(
    model="gpt-5.2",
    api_key="your-key",
    base_url="https://xingjiabiapi.org/v1"
)
```

## Gemini

```python
from langchain_openai import ChatOpenAI

# Gemini 2.5 Pro - 输入 ¥0.5630/M，比官方省 67%
llm = ChatOpenAI(
    model="gemini-2.5-pro",
    api_key="your-key",
    base_url="https://xingjiabiapi.org/v1"
)
```

## Agent 示例

```python
from langchain.agents import create_openai_tools_agent, AgentExecutor
from langchain.tools import tool
from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate

@tool
def search(query: str) -> str:
    """搜索信息"""
    return f"搜索结果：{query}"

llm = ChatOpenAI(
    model="claude-opus-4-6",
    api_key="your-key",
    base_url="https://xingjiabiapi.org/v1"
)

prompt = ChatPromptTemplate.from_messages([
    ("system", "你是一个助手"),
    ("human", "{input}"),
    ("placeholder", "{agent_scratchpad}")
])

agent = create_openai_tools_agent(llm, [search], prompt)
executor = AgentExecutor(agent=agent, tools=[search])
result = executor.invoke({"input": "帮我搜索 Claude API 价格"})
print(result["output"])
```

## 价格总览

| 模型 | xingjiabiapi.org | 官方价格 | 节省 |
|------|-----------------|----------|------|
| Claude Opus 4.6 | ¥31.50/M | $15/M | 47% |
| Claude 逆向 | ¥6.75/M | $15/M | 70% |
| GPT-5.2 | ¥3.15/M | $10/M | 50% |
| Gemini 2.5 Pro | ¥0.5630/M | $1.25/M | 67% |

## 联系方式

- 官网：https://xingjiabiapi.org
- 微信：malimalihongbebe
- 邮箱：xingjiabiapi@163.com
