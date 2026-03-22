<!-- language-switch:start -->
[English](./README.md) | [中文](./README.zh-CN.md)
<!-- language-switch:end -->

<p align="center">
<a href="https://docs.mcp-agent.com"><img src="https://github.com/user-attachments/assets/c8d059e5-bd56-4ea2-a72d-807fb4897bde" alt="Logo" width="300" /></a>
</p>

<p align="center">
<em>使用简单、可组合的模式通过模型上下文协议构建有效的智能体。</em>

<p align="center">
<a href="https://github.com/lastmile-ai/mcp-agent/tree/main/examples" target="_blank"><strong>示例</strong></a>
  |
<a href="https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/overview" target="_blank"><strong>建筑有效剂</strong></a>
  |
<a href="https://modelcontextprotocol.io/introduction" target="_blank"><strong>MCP</strong></a>
</p>

<p align="center">
<a href="https://docs.mcp-agent.com"><img src="https://img.shields.io/badge/docs-8F?style=flat&link=https%3A%2F%2Fdocs.mcp-agent.com%2F" /><a/>
<a href="https://pypi.org/project/mcp-agent/"><img src="https://img.shields.io/pypi/v/mcp-agent?color=%2334D058&label=pypi" /></a>
<img alt="Pepy 总下载量" src="https://img.shields.io/pepy/dt/mcp-agent?label=pypi%20%7C%20downloads"/>
<a href="https://github.com/lastmile-ai/mcp-agent/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-Apache_2.0-blue.svg"/></a>
<a href="https://lmai.link/discord/mcp-agent"><img src="https://img.shields.io/badge/Discord-%235865F2.svg?logo=discord&logoColor=white" alt="discord"/></a>
</p>

<p align="center">
<a href="https://trendshift.io/repositories/13216" target="_blank"><img src="https://trendshift.io/api/badge/repositories/13216" alt="lastmile-ai%2Fmcp-agent | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>
</p>

## 概述

**`mcp-agent`** 是一个简单的可组合框架，用于使用[模型上下文协议](https://modelcontextprotocol.io/introduction) 构建有效的智能体。

> [！笔记]
> mcp-agent 的愿景是_MCP 是构建代理所需的一切，并且简单的模式比复杂的架构更强大，可以交付高质量的代理_。

`mcp-agent` 为您提供以下内容：

1. **完整的 MCP 支持**：它_完全_实现 MCP，并处理管理 MCP 服务器连接生命周期的烦人事务，因此您无需这样做。
2. **有效的代理模式**：它以_可组合_的方式实现了 Anthropic 的[构建有效代理](https://www.anthropic.com/engineering/building-effective-agents) 中描述的每个模式，允许您将这些模式链接在一起。
3. **持久代理**：它适用于简单代理，并可扩展到基于 [Temporal](https://temporal.io/) 构建的复杂工作流程，因此您可以暂停、恢复和恢复，而无需对代理进行任何 API 更改。

<u> 总而言之，这是构建健壮的代理应用程序的最简单、最容易的方法</u>。

我们欢迎各种[贡献](/CONTRIBUTING.md)、反馈以及您对改进此项目的帮助。

<a id="minimal-example"></a>
**最小示例**

```python
import asyncio

from mcp_agent.app import MCPApp
from mcp_agent.agents.agent import Agent
from mcp_agent.workflows.llm.augmented_llm_openai import OpenAIAugmentedLLM

app = MCPApp(name="hello_world")

async def main():
    async with app.run():
        agent = Agent(
            name="finder",
            instruction="Use filesystem and fetch to answer questions.",
            server_names=["filesystem", "fetch"],
        )
        async with agent:
            llm = await agent.attach_llm(OpenAIAugmentedLLM)
            answer = await llm.generate_str("Summarize README.md in two sentences.")
            print(answer)


if __name__ == "__main__":
    asyncio.run(main())

# Add your LLM API key to `mcp_agent.secrets.yaml` or set it in env.
# The [Getting Started guide](https://docs.mcp-agent.com/get-started/overview) walks through configuration and secrets in detail.

```

## 一目了然

<table>
<tr>
<td width="50%" valign="top">
<h3>建立代理</h3>
<p>以简单、可组合的模式（例如映射缩减、协调器、评估器优化器、路由器等）将 LLM 连接到 MCP 服务器。</p>
<p>
<a href="https://docs.mcp-agent.com/get-started/overview">Quick Start ↗</a> |
<a href="https://docs.mcp-agent.com/mcp-agent-sdk/overview">Docs ↗</a>
</p>
</td>
<td width="50%" valign="top">
<h3>创建任何类型的MCP服务器</h3>
<p>使用与 FastMCP 兼容的 API 创建 MCP 服务器。您甚至可以将代理公开为 MCP 服务器。</p>
<p>
<a href="https://docs.mcp-agent.com/mcp-agent-sdk/mcp/agent-as-mcp-server">MCP Agent Server ↗</a> |
<a href="https://docs.mcp-agent.com/cloud/use-cases/deploy-chatgpt-apps">🎨 Build a ChatGPT App ↗</a> |
<a href="https://github.com/lastmile-ai/mcp-agent/tree/main/examples/mcp_agent_server">Examples ↗</a>
</p>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<h3>完整的 MCP 支持</h3>
<p><b>核心：</b> 工具 ✅ 资源 ✅ 提示 ✅ 通知 ✅<br/>
<b>Advanced</b>：OAuth ✅ 采样 ✅ 启发 ✅ 根 ✅</p>
<p>
<a href="https://github.com/lastmile-ai/mcp-agent/tree/main/examples/mcp">Examples ↗</a> |
<a href="https://modelcontextprotocol.io/docs/getting-started/intro">MCP Docs ↗</a>
</p>
</td>
<td width="50%" valign="top">
<h3>持久执行（临时）</h3>
<p> 使用 Temporal 作为智能体运行时后端 <i> 扩展到生产工作负载，无需任何 API 更改</i>.</p>
<p>
<a href="https://docs.mcp-agent.com/mcp-agent-sdk/advanced/durable-agents">Docs ↗</a> |
<a href="https://github.com/lastmile-ai/mcp-agent/tree/main/examples/temporal">Examples ↗</a>
</p>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<h3>☁️ 部署到云端</h3>
<p><b>Beta:</b> 自行部署代理，或使用 <b>mcp-c</b> 作为托管智能体运行时。所有应用程序均部署为 MCP 服务器。</p>
<p>
<a href="https://www.youtube.com/watch?v=0C4VY-3IVNU">Demo ↗</a> |
<a href="https://docs.mcp-agent.com/get-started/cloud">Cloud Quickstart ↗</a> |
<a href="https://github.com/lastmile-ai/mcp-agent/tree/main/examples/cloud">Examples ↗</a>
</p>
</td>
</tr>
</table>

## 法学硕士的文档和构建

mcp-agent 的完整文档可从 **[docs.mcp-agent.com](https://docs.mcp-agent.com)** 获取，包括完整的 SDK 指南、CLI 参考和高级模式。本自述文件提供了高级概述以帮助您入门。

- [`llms-full.txt`](https://docs.mcp-agent.com/llms-full.txt)：包含完整文档。
- [`llms.txt`](https://docs.mcp-agent.com/llms.txt)：列出文档中关键页面的站点地图。
- [文档 MCP 服务器](https://docs.mcp-agent.com/mcp)

## 目录

- [概述](#overview)
- [最小示例](#minimal-example)
- [快速入门](#get-started)
- [为什么选择 mcp-agent](#why-use-mcp-agent)
- [核心概念](#core-components)
  - [MCP应用程序](#mcpapp)
  - [代理及代理规格](#agents--agentspec)
  - [强化法学硕士](#augmented-llm)
  - [工作流程和装饰器](#workflows--decorators)
  - [配置与秘密](#configuration--secrets)
  - [MCP集成](#mcp-integration)
- [工作流程模式](#workflow-patterns)
- [CLI 参考](#cli-reference)
- [认证](#authentication)
- [高级](#advanced)
  - [可观测性与控制](#observability--controls)
  - [撰写工作流程](#composing-workflows)
  - [持久执行](#durable-execution)
  - [代理服务器](#agent-servers)
  - [信号和人工输入](#signals--human-input)
  - [应用程序配置](#app-configuration)
  - [图标](#icons)
  - [MCP服务器管理](#mcp-server-management)
- [云部署](#cloud-deployment)
- [示例](#examples)
- [常见问题解答](#faqs)
- [社区与贡献](#contributing)

## 开始使用

> [！提示]
> CLI 可通过 `uvx mcp-agent` 获得。
> 要启动并运行，
> 使用 `uvx mcp-agent init` 构建项目并使用 `uvx mcp-agent deploy my-agent` 进行部署。
>
> 通过运行以下命令，您可以在 2 分钟内启动并运行：
>
> ```bash
> mkdir hello-mcp-agent && cd hello-mcp-agent
> uvx mcp 代理初始化
> 紫外线初始化
> uv 添加“mcp-agent[openai]”
> # 将openai API密钥添加到`mcp_agent.secrets.yaml`或设置`OPENAI_API_KEY`
> uv运行main.py
> ```

### 安装

我们建议使用 [uv](https://docs.astral.sh/uv/) 来管理您的 Python 项目 (`uv init`)。

```bash
uv add "mcp-agent"
```

或者：

```bash
pip install mcp-agent
```

还为 LLM 提供商添加可选包（例如 `uv add "mcp-agent[openai, anthropic, google, azure, bedrock]"`）。

### 快速入门

> [！提示]
> [`examples`](/examples) 目录有几个可供入门的示例应用程序。
> 要运行示例，请克隆此仓库（或使用 `uvx mcp-agent init --template basic --dir my-first-agent` 生成一个）
>
> ```bash
> cd Examples/basic/mcp_basic_agent # 或任何其他示例
> # 选项 A：秘密 YAML
> # cp mcp_agent.secrets.yaml.example mcp_agent.secrets.yaml && 编辑 mcp_agent.secrets.yaml
> uv运行main.py
> ```

这是一个基本的“查找器”代理，它使用获取和文件系统服务器来查找文件、阅读博客和编写推文。 [示例链接](./examples/basic/mcp_basic_agent/)：

<details open>
<summary>finder_agent.py</summary>

```python
import asyncio
import os

from mcp_agent.app import MCPApp
from mcp_agent.agents.agent import Agent
from mcp_agent.workflows.llm.augmented_llm_openai import OpenAIAugmentedLLM

app = MCPApp(name="hello_world_agent")

async def example_usage():
    async with app.run() as mcp_agent_app:
        logger = mcp_agent_app.logger
        # This agent can read the filesystem or fetch URLs
        finder_agent = Agent(
            name="finder",
            instruction="""You can read local files or fetch URLs.
                Return the requested information when asked.""",
            server_names=["fetch", "filesystem"], # MCP servers this Agent can use
        )

        async with finder_agent:
            # Automatically initializes the MCP servers and adds their tools for LLM use
            tools = await finder_agent.list_tools()
            logger.info(f"Tools available:", data=tools)

            # Attach an OpenAI LLM to the agent (defaults to GPT-4o)
            llm = await finder_agent.attach_llm(OpenAIAugmentedLLM)

            # This will perform a file lookup and read using the filesystem server
            result = await llm.generate_str(
                message="Show me what's in README.md verbatim"
            )
            logger.info(f"README.md contents: {result}")

            # Uses the fetch server to fetch the content from URL
            result = await llm.generate_str(
                message="Print the first two paragraphs from https://www.anthropic.com/research/building-effective-agents"
            )
            logger.info(f"Blog intro: {result}")

            # Multi-turn interactions by default
            result = await llm.generate_str("Summarize that in a 128-char tweet")
            logger.info(f"Tweet: {result}")

if __name__ == "__main__":
    asyncio.run(example_usage())

```

</details>

<details>
<summary>mcp_agent.config.yaml</summary>

```yaml
execution_engine: asyncio
logger:
  transports: [console] # You can use [file, console] for both
  level: debug
  path: "logs/mcp-agent.jsonl" # Used for file transport
  # For dynamic log filenames:
  # path_settings:
  #   path_pattern: "logs/mcp-agent-{unique_id}.jsonl"
  #   unique_id: "timestamp"  # Or "session_id"
  #   timestamp_format: "%Y%m%d_%H%M%S"

mcp:
  servers:
    fetch:
      command: "uvx"
      args: ["mcp-server-fetch"]
    filesystem:
      command: "npx"
      args:
        [
          "-y",
          "@modelcontextprotocol/server-filesystem",
          "<add_your_directories>",
        ]

openai:
  # Secrets (API keys, etc.) are stored in an mcp_agent.secrets.yaml file which can be gitignored
  default_model: gpt-4o
```

</details>

<details>
<summary>A代理输出</summary>
<img width="2398" alt="Image" src="https://github.com/user-attachments/assets/eaa60fdf-bcc6-460b-926e-6fa8534e9089" />
</details>

## 为什么使用`mcp-agent`？

已经有太多的人工智能框架了。但 `mcp-agent` 是唯一一款专为共享协议构建的协议 - [MCP](https://modelcontextprotocol.io/introduction)。[mcp-agent](https://docs.mcp-agent.com/get-started/welcome) 将 Anthropic 的构建有效代理模式与包含电池的 MCP 运行时配对，这样您就可以专注于行为，而不是样板文件。团队选择它是因为它：

- **可组合** – 每个模式都作为可重用的工作流程提供，您可以混合和匹配。
- **MCP-native** – 任何 MCP 服务器（文件系统、fetch、Slack、Jira、FastMCP 应用程序）无需自定义适配器即可连接。
- **生产就绪** – 时间支持的持久性、结构化日志记录、令牌会计和云部署都是一流的。
- **Pythonic** – 一些装饰器和上下文管理器将所有内容连接在一起。

文档：[欢迎使用 mcp-agent](https://docs.mcp-agent.com/get-started/welcome) • [有效模式概述](https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/overview)。

## 核心组件

每个项目都围绕一个 `MCPApp` 运行时来加载配置、注册代理和 MCP 服务器以及公开工具/工作流。 [核心组件指南](https://docs.mcp-agent.com/mcp-agent-sdk/overview) 介绍了这些构建块。

### MCP应用程序

初始化配置、日志记录、跟踪和执行引擎，以便所有内容共享一个上下文。

```python
from mcp_agent.app import MCPApp

app = MCPApp(name="finder_app")

async def main():
    async with app.run() as running_app:
        logger = running_app.logger
        logger.info("App ready", data={"servers": list(running_app.context.server_registry.registry)})
```

文档：[MCPApp](https://docs.mcp-agent.com/mcp-agent-sdk/core-components/mcpapp) • 示例：[`examples/basic/mcp_basic_agent`](./examples/basic/mcp_basic_agent/)。

### 代理及代理规格

代理将指令与它们可能调用的 MCP 服务器（和可选函数）结合起来。 `AgentSpec` 定义可以从磁盘加载并通过工厂助手转换为代理或增强的 LLM。

```python
from pathlib import Path
from mcp_agent.agents.agent import Agent
from mcp_agent.workflows.factory import load_agent_specs_from_file

agent = Agent(
    name="researcher",
    instruction="Research topics using web and filesystem access",
    server_names=["fetch", "filesystem"],
)

async with agent:
    tools = await agent.list_tools()

async with app.run() as running_app:
    specs = load_agent_specs_from_file(
        str(Path("examples/basic/agent_factory/agents.yaml")),
        context=running_app.context,
    )
```

文档：[代理](https://docs.mcp-agent.com/mcp-agent-sdk/core-components/agents) • [代理工厂助手](https://docs.mcp-agent.com/mcp-agent-sdk/core-components/agents#agentspec-and-factory-helpers) • 示例：[`examples/basic/agent_factory`](./examples/basic/agent_factory/)。

### 强化法学硕士

增强型 LLM 将提供者 SDK 与代理工具、内存和结构化输出助手一起包装。将一个附加到代理以解锁 `generate`、`generate_str` 和 `generate_structured`。

```python
from pydantic import BaseModel
from mcp_agent.workflows.llm.augmented_llm import RequestParams
from mcp_agent.workflows.llm.augmented_llm_openai import OpenAIAugmentedLLM

class Summary(BaseModel):
    title: str
    verdict: str

async with agent:
    llm = await agent.attach_llm(OpenAIAugmentedLLM)
    report = await llm.generate_str(
        message="Draft a 3-sentence release note from CHANGELOG.md",
        request_params=RequestParams(maxTokens=400, temperature=0.2),
    )
    structured = await llm.generate_structured(
        message="Return a JSON object with `title` and `verdict` summarising the README.",
        response_model=Summary,
    )
```

文档：[增强法学硕士](https://docs.mcp-agent.com/mcp-agent-sdk/core-components/augmented-llm) • 示例：[`examples/basic/mcp_basic_agent`](./examples/basic/mcp_basic_agent/) 以及[gallery.md](gallery.md#workflow-patterns) 中列出的工作流程项目。

### 工作流程和装饰器

`MCPApp` 装饰器将协程转换为持久的工作流程和工具。相同的注释适用于 `asyncio` 和临时执行。

```python
from datetime import timedelta
from mcp_agent.executor.workflow import Workflow, WorkflowResult

@app.workflow
class PublishArticle(Workflow[WorkflowResult[str]]):
    @app.workflow_task(schedule_to_close_timeout=timedelta(minutes=5))
    async def draft(self, topic: str) -> str:
        return f"- intro to {topic}\n- highlights\n- next steps"

    @app.workflow_run
    async def run(self, topic: str) -> WorkflowResult[str]:
        outline = await self.draft(topic)
        return WorkflowResult(value=outline)
```

文档：[装饰器参考](https://docs.mcp-agent.com/reference/decorators) • 示例：[`examples/workflows`](./examples/workflows/)。

### 配置和秘密

从 `mcp_agent.config.yaml`、`mcp_agent.secrets.yaml`、环境变量和可选预加载字符串加载设置。让秘密远离源代码控制。

```yaml
# mcp_agent.config.yaml
execution_engine: asyncio
mcp:
  servers:
    fetch:
      command: "uvx"
      args: ["mcp-server-fetch"]
    filesystem:
      command: "npx"
      args: ["-y", "@modelcontextprotocol/server-filesystem"]
openai:
  default_model: gpt-4o-mini

# mcp_agent.secrets.yaml (gitignored)
openai:
  api_key: "${OPENAI_API_KEY}"
```

文档：[配置参考](https://docs.mcp-agent.com/reference/configuration) • [指定机密](https://docs.mcp-agent.com/mcp-agent-sdk/core-components/specify-secrets)。

### MCP集成

以编程方式连接到现有的 MCP 服务器或将多个服务器聚合到一个外观中。

```python
from mcp_agent.mcp.gen_client import gen_client

async with app.run():
    async with gen_client("filesystem", app.server_registry, context=app.context) as client:
        resources = await client.list_resources()
        app.logger.info("Filesystem resources", data={"uris": [r.uri for r in resources.resources]})
```

文档：[MCP 集成概述](https://docs.mcp-agent.com/mcp/overview) • 示例：[`examples/mcp`](./examples/mcp/)。

## 工作流程模式

关键代理模式作为 `AugmentedLLM` 实现。使用工厂助手将它们连接起来或检查 [gallery.md](gallery.md#workflow-patterns) 中列出的可运行项目。

|图案|帮手|总结|文档 |
| --------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
|并行（Map-Reduce）| `create_parallel_llm(...)` |扇出专家和扇入汇总报告。<br><a href="https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F406bb032ca007fd1624f261af717d70e6ca86286-2401x1000.png&w=3840&q=75"><img src="https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F406bb032ca007fd1624f261af717d70e6ca86286-2401x1000.png&w=3840&q=75" width="260"/></a> | [并行](https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/map-reduce) |
|路由器| `create_router_llm(...)` / `create_router_embedding(...)` |将请求路由到最佳智能体、服务器或功能。<br><a href="https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F5c0c0e9fe4def0b584c04d37849941da55e5e71c-2401x1000.png&w=3840&q=75"><img src="https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F5c0c0e9fe4def0b584c04d37849941da55e5e71c-2401x1000.png&w=3840&q=75" width="260"/></a> | [路由器](https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/router) |
|意图分类器 | `create_intent_classifier_llm(...)` / `create_intent_classifier_embedding(...)` |在自动化之前将用户输入存储到意图中。                                                                                                                                                                                                                                                                                                                                                                                                                  | [意图分类器](https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/intent-classifier) |
|协调员工作者| `create_orchestrator(...)` |生成计划并协调工作智能体。<br><a href="https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F8985fc683fae4780fb34eab1365ab78c7e51bc8e-2401x1000.png&w=3840&q=75"><img src="https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F8985fc683fae4780fb34eab1365ab78c7e51bc8e-2401x1000.png&w=3840&q=75" width="260"/></a> | [策划](https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/planner) |
|深入研究 | `create_deep_orchestrator(...)` |具有知识提取和政策检查的长期研究。                                                                                                                                                                                                                                                                                                                                                                                                 | [深入研究](https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/deep-research) |
|评估优化器 | `create_evaluator_optimizer_llm(...)` |进行迭代，直到评估者批准结果。<br><a href="https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F14f51e6406ccb29e695da48b17017e899a6119c7-2401x1000.png&w=3840&q=75"><img src="https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F14f51e6406ccb29e695da48b17017e899a6119c7-2401x1000.png&w=3840&q=75" width="260"/></a> | [评估器-优化器](https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/evaluator-optimizer) |
|蜂群| `create_swarm(...)` |与 OpenAI Swarm 兼容的多代理切换。<br><a href="https://github.com/openai/swarm/blob/main/assets/swarm_diagram.png?raw=true"><img src="https://github.com/openai/swarm/blob/main/assets/swarm_diagram.png?raw=true" width="220"/></a> | [群](https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/swarm) |

## 持久的执行力

将 `execution_engine` 切换到 `temporal` 以实现暂停/恢复、重试、人工输入和持久历史记录，而无需更改工作流程代码。在您的应用程序旁边运行一个工作线程来托管活动。

```python
from mcp_agent.executor.temporal import create_temporal_worker_for_app

async with create_temporal_worker_for_app(app) as worker:
    await worker.run()
```

文档：[持久代理](https://docs.mcp-agent.com/mcp-agent-sdk/advanced/durable-agents) • [临时后端](https://docs.mcp-agent.com/advanced/temporal) • 示例：[`examples/temporal`](./examples/temporal/)。

## 代理服务器

将 `MCPApp` 公开为标准 MCP 服务器，以便 Claude Desktop、Cursor 或自定义客户端可以调用您的工具和工作流程。

```python
from mcp_agent.server import create_mcp_server_for_app

@app.tool
def grade_story(story: str) -> str:
    return "Report..."

if __name__ == "__main__":
    server = create_mcp_server_for_app(app)
    server.run_stdio()
```

文档：[代理服务器](https://docs.mcp-agent.com/mcp-agent-sdk/mcp/agent-as-mcp-server) • 示例：[`examples/mcp_agent_server`](./examples/mcp_agent_server/)。

## CLI 参考

`uvx mcp-agent` 搭建项目、管理机密、检查工作流程并部署到云。

```bash
uvx mcp-agent init --template basic             # Scaffold a new project
uvx mcp-agent deploy my-agent                   # Deploy to mcp-agent Cloud
```

文档：[CLI 参考](https://docs.mcp-agent.com/reference/cli) • [入门指南](https://docs.mcp-agent.com/get-started/quickstart)。

## 验证

从机密文件加载 API 密钥或使用内置 OAuth 客户端来获取并保留 MCP 服务器的令牌。

```yaml
# mcp_agent.config.yaml excerpt
oauth:
  providers:
    github:
      client_id: "${GITHUB_CLIENT_ID}"
      client_secret: "${GITHUB_CLIENT_SECRET}"
      scopes: ["repo", "user"]
```

文档： [高级身份验证](https://docs.mcp-agent.com/mcp-agent-sdk/advanced/authentication) • [服务器身份验证](https://docs.mcp-agent.com/mcp-agent-sdk/mcp/server-authentication) • 示例：[`examples/basic/oauth_basic_agent`](./examples/basic/oauth_basic_agent/)。

## 先进的

### 可观察性和控制

通过配置启用结构化日志记录和 OpenTelemetry，并以编程方式跟踪令牌使用情况。

```yaml
# mcp_agent.config.yaml
logger:
  transports: [console]
  level: info
otel:
  enabled: true
  exporters:
    - console
```

`TokenCounter` 跟踪智能体、工作流程和 LLM 节点的令牌使用情况。附加观察者以流式传输更新或触发警报。

```python
# Inside `async with app.run() as running_app:`
# token_counter lives on the running app context when tracing is enabled.
token_counter = running_app.context.token_counter

class TokenMonitor:
    async def on_token_update(self, node, usage):
        print(f"[{node.name}] total={usage.total_tokens}")

monitor = TokenMonitor()
watch_id = await token_counter.watch(
    callback=monitor.on_token_update,
    node_type="llm",
    threshold=1_000,
    include_subtree=True,
)

await token_counter.unwatch(watch_id)
```

文档：[可观测性](https://docs.mcp-agent.com/mcp-agent-sdk/advanced/observability) • 示例：[`examples/tracing`](./examples/tracing/)。

### 撰写工作流程

混合并匹配 AgentSpec，使用工厂助手（路由器、并行管道、协调器等）构建更高级别的工作流程。

```python
from mcp_agent.workflows.factory import create_router_llm

# specs are loaded via load_agent_specs_from_file as shown above.
async with app.run() as running_app:
    router = await create_router_llm(
        agents=specs,
        provider="openai",
        context=running_app.context,
    )
```

文档：[工作流程组成](https://docs.mcp-agent.com/mcp-agent-sdk/advanced/composition) • 示例：[`examples/basic/agent_factory`](./examples/basic/agent_factory/)。

### 信号和人工输入

暂停工作流程以获得批准或额外数据。临时存储状态持久直到操作员恢复运行。

```python
from mcp_agent.human_input.types import HumanInputRequest

response = await self.context.request_human_input(
    HumanInputRequest(
        prompt="Approve the draft?",
        required=True,
        metadata={"workflow_id": self.context.workflow_id},
    )
)
```

使用 `mcp-agent cloud workflows resume … --payload '{"content": "approve"}'` 继续。文档：[部署智能体 – 人工输入](https://docs.mcp-agent.com/cloud/use-cases/deploy-agents#human-in-the-loop-patterns) • 示例：[`examples/human_input/temporal`](./examples/human_input/temporal/)。

### 应用程序配置

当您需要动态配置（测试、多租户主机）而不是 YAML 文件时，以编程方式构建 `Settings` 对象。

```python
from mcp_agent.config import Settings, MCPSettings, MCPServerSettings

settings = Settings(
    execution_engine="asyncio",
    mcp=MCPSettings(
        servers={
            "fetch": MCPServerSettings(command="uvx", args=["mcp-server-fetch"]),
        }
    ),
)
app = MCPApp(name="configured_app", settings=settings)
```

文档：[配置您的应用程序](https://docs.mcp-agent.com/mcp-agent-sdk/core-components/configuring-your-application)。

### 图标

向代理和工具添加图标，以便支持图像（Claude Desktop、Cursor）的 MCP 客户端呈现更丰富的 UI。

```python
from base64 import standard_b64encode
from pathlib import Path
from mcp_agent.icons import Icon

icon_data = standard_b64encode(Path("my-icon.png").read_bytes()).decode()
icon = Icon(src=f"data:image/png;base64,{icon_data}", mimeType="image/png", sizes=["64x64"])

app = MCPApp(name="my_app_with_icon", icons=[icon])

@app.tool(icons=[icon])
async def my_tool() -> str:
    return "Hello with style"
```

文档：[`MCPApp` 图标](https://docs.mcp-agent.com/mcp-agent-sdk/core-components/mcpapp#icons) • 示例：[`examples/mcp_agent_server/asyncio`](./examples/mcp_agent_server/asyncio/)。

### MCP服务器管理

使用 `MCPAggregator` 或 `gen_client` 管理 MCP 服务器连接并公开组合工具集。

```python
from mcp_agent.mcp.mcp_aggregator import MCPAggregator

async with MCPAggregator.create(server_names=["fetch", "filesystem"]) as aggregator:
    tools = await aggregator.list_tools()
```

文档：[连接到MCP 服务器](https://docs.mcp-agent.com/mcp-agent-sdk/core-components/connecting-to-mcp-servers) • 示例：[`examples/basic/mcp_server_aggregator`](./examples/basic/mcp_server_aggregator/)。

## 云端部署

部署到 mcp-agent 云以用于托管临时执行、机密和 HTTPS MCP 端点。

```bash
uvx mcp-agent login
uvx mcp-agent deploy my-agent
uvx mcp-agent cloud apps list
```

文档：[云概述](https://docs.mcp-agent.com/cloud/overview) • [部署快速入门](https://docs.mcp-agent.com/cloud/deployment-quickstart) • 示例：[`examples/cloud`](./examples/cloud/)。

## 示例

浏览 [gallery.md](gallery.md) 以获取按概念分组的可运行示例、演示视频和社区项目。每个条目都引用了本地运行它所需的文档页面和命令。

## 常见问题解答

### 使用 mcp-agent 的核心优势是什么？

mcp-agent 提供了一种使用 **MCP**（模型上下文协议）服务器公开的功能来构建 AI 智能体的简化方法。

MCP 是相当低级的，该框架处理连接到服务器、与 LLM 合作、处理外部信号（如人工输入）以及通过持久执行支持持久状态的机制。这让您（开发人员）可以专注于 AI 应用程序的核心业务逻辑。

核心优势：

- 🤝 **互操作性**：确保任意数量的 MCP 服务器公开的任何工具都可以无缝插入您的智能体。
- ⛓️ **可组合性和可定制性**：实现定义良好的工作流程，但以可组合的方式实现复合工作流程，并允许跨模型提供程序、日志记录、编排器等进行完全自定义。
- 💻 **编程控制流**：让事情变得简单，因为开发人员只需编写代码，而不是在图形、节点和边中思考。对于分支逻辑，您可以编写 `if` 语句。对于循环，请使用 `while` 循环。
- 🖐️ **人工输入和信号**：支持暂停外部信号的工作流程，例如人工输入，这些信号作为代理可以进行的工具调用而公开。

### 您需要 MCP 客户端才能使用 mcp-agent 吗？

不，您可以在任何地方使用 mcp-agent，因为它会为您处理 MCPClient 创建。这允许您利用 MCP 主机之外的 MCP 服务器，例如 Claude Desktop。

以下是设置 mcp-agent 应用程序的所有方法：

#### MCP代理服务器

您可以将 mcp-agent 应用程序公开为 MCP 服务器本身（请参阅[示例](./examples/mcp_agent_server)），从而允许 MCP 客户端使用 MCP 服务器的标准工具 API 与复杂的 AI 工作流程进行交互。这实际上是一个服务器中的服务器。

#### MCP 客户端或主机

您可以直接在 MCP 客户端中嵌入 mcp-agent 以管理跨多个 MCP 服务器的编排。

#### 独立式

您可以以独立方式使用 mcp-agent 应用程序（即它们不是 MCP 客户端的一部分）。 [`examples`](/examples/) 都是独立应用程序。

### 如何部署到云端？

使用`uvx mcp-agent login`登录后运行`uvx mcp-agent deploy <app-name>`。 CLI 打包您的项目、提供机密并公开由持久的临时运行时支持的 MCP 端点。参见【云快速入门】(https://docs.mcp-agent.com/get-started/
cloud）获取分步屏幕截图和 CLI 输出。

### API 参考在哪里？

每个类、装饰器和 CLI 命令都记录在 [docs.mcp-agent.com](https://docs.mcp-agent.com) 上。 [API 参考](https://docs.mcp-agent.com/reference) 和 [`llms-full.txt`](https://docs.mcp-agent.com/llms-full.txt) 的设计使法学硕士（或您）可以轻松摄取整个表面积。

### 告诉我一个有趣的事实

我曾讨论过将这个项目命名为 _silsila_ (Sרց)，这在乌尔都语中是“一系列事件”的意思。 mcp-agent 更实事求是，但该项目中仍然有一个向 silsila 致敬的复活节彩蛋。

## 贡献

我们欢迎各种规模的贡献——错误修复、新示例、文档或功能请求。从 [CONTRIBUTING.md](./CONTRIBUTING.md) 开始，打开讨论，或访问 [Discord](https://lmai.link/discord/mcp-agent)。

如果没有许多开源贡献者的不懈努力，mcp-agent 就不可能实现。谢谢你！

<p align="center">
<a href="https://github.com/lastmile-ai/mcp-agent/graphs/contributors">
<img src="https://contrib.rocks/image?repo=lastmile-ai/mcp-agent" alt="Contributor faces" />
</a>
</p>
