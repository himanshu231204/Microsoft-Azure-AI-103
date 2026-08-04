<div align="center">

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

# Module 2.1: Develop AI Agents with Microsoft Foundry and Visual Studio Code

</div>

> **Source**: [Microsoft Learn — Develop AI agents with Microsoft Foundry and Visual Studio Code](https://learn.microsoft.com/training/modules/develop-ai-agents-azure-vs-code/)
> **Learning objectives**: Describe AI agents, explain Foundry Agent Service, set up the VS Code extension, build agents via multiple approaches, extend with tools, test in playgrounds, deploy and integrate

---

## Table of Contents

1. [What Are AI Agents?](#1-what-are-ai-agents)
2. [Microsoft Foundry Agent Service](#2-microsoft-foundry-agent-service)
3. [Development Approaches](#3-development-approaches)
4. [Build Your First Agent in Microsoft Foundry](#4-build-your-first-agent-in-microsoft-foundry)
5. [Set Up Visual Studio Code for Agent Development](#5-set-up-visual-studio-code-for-agent-development)
6. [Configure and Manage Agents in VS Code](#6-configure-and-manage-agents-in-vs-code)
7. [Extend Agent Capabilities with Tools](#7-extend-agent-capabilities-with-tools)
8. [Test, Deploy, and Integrate Agents](#8-test-deploy-and-integrate-agents)
9. [Key Takeaways for AI-103](#9-key-takeaways-for-ai-103)

---

## 1. What Are AI Agents?

An **AI agent** is an application that uses a large language model (LLM) as its reasoning engine to **autonomously accomplish tasks** by combining three core elements:

1. **LLM** — the reasoning engine that interprets prompts and decides what to do
2. **Instructions** — define the agent's role, scope, and behavioral rules (system prompt)
3. **Tools** — APIs, code, databases, search, and MCP connections the agent can call

### Agent vs. plain LLM call

| Plain LLM call | AI agent |
|----------------|----------|
| One-shot prompt → response | Multi-step, goal-directed reasoning |
| No external access | Can call tools, query data, run code |
| Stateless | Maintains conversation state (threads) |
| Fixed output | Iterates until the task is complete |

### The agent loop (function calling)

The classic 5-step pattern that powers tool use:

1. **Define function tools** — describe each function's name, parameters, purpose
2. **Create an agent** — register the agent with your function definitions
3. **Send a prompt** — the agent analyzes it and *requests* function calls if needed
4. **Execute and return** — **your app** runs the function and submits the output back
5. **Get the final response** — the agent uses the output to complete its answer

> **Exam insight**: Know the three ingredients of an agent (LLM + instructions + tools) and the 5-step function-calling loop — both are tested.

---

## 2. Microsoft Foundry Agent Service

**Foundry Agent Service** is the **managed agent platform** in Microsoft Foundry (previously Azure AI Agent Service / Azure AI Foundry Agent Service). You define an agent (instructions + model + tools) and the service handles **hosting, scaling, identity, state, and monitoring** for you.

### Two main agent types (memorize this table)

| | Prompt agents | Hosted agents |
| --- | --- | --- |
| **Authoring surface** | Portal, SDK, REST | Agent Framework, LangGraph, OpenAI Agents SDK, custom code |
| **Foundry models + platform tools** | Yes | Yes (via Responses API) |
| **Runtime code to maintain** | None | Yes — your agent logic |
| **Compute to manage** | None — fully managed | Container compute (Foundry-managed) |
| **Managed endpoint** | Yes | Yes |
| **Autoscale** | Automatic (request volume) | Automatic (container instances per session & request) |
| **Agent identity (Entra)** | Yes | Yes — automatic, dedicated per agent |
| **Cost model** | Per-call inference + tool usage | Per-call inference + tool usage + container compute |
| **Best for** | Fast start, agents without custom orchestration | Agents that call custom code, multi-agent, custom protocols |

### The Responses API

- The **single model-and-tools endpoint behind every agent type**
- Call it directly from your own code to get Foundry models + platform tools **without creating an agent resource**
- The same code can later be packaged as a hosted agent — an *additive pattern*

### Key concepts

| Concept | Description |
|---------|-------------|
| **Thread** | A conversation session between an agent and a user; stores messages and auto-truncates to fit the model's context |
| **Message** | A single interaction that can include text, images, and other files |
| **Run** | A single execution of an agent that can span multiple threads and messages |

> **Exam insight**: Distinguish **prompt agents** (config-only, no code/compute to manage) from **hosted agents** (code-based, container compute). This is a high-yield comparison.

---

## 3. Development Approaches

You can build agents using **multiple development approaches**, depending on your needs:

| Approach | Where | Best for |
|----------|-------|----------|
| **Foundry portal** | [ai.azure.com](https://ai.azure.com) | Quick start, visual authoring, no code |
| **VS Code extension (designer)** | Visual Studio Code | Visual agent config + YAML, local workflow |
| **SDK / REST** | Your code | CI/CD, programmatic control, automation |
| **Agent Framework / other frameworks** | Your code | Custom orchestration, hosted agents |

The module focuses on the **portal** and the **VS Code extension** paths, with the SDK used to consume and integrate the deployed agent.

---

## 4. Build Your First Agent in Microsoft Foundry

The portal path lets you create an agent quickly without writing code.

### Prerequisites
- An Azure subscription
- A **Foundry project** with a **deployed model** (e.g., `gpt-4o`, `gpt-4o-mini`)
- Access to Foundry Agent Service

### High-level steps
1. Create a Foundry project (or use an existing one)
2. Deploy a model from the model catalog
3. Create an agent: give it a **name**, select the **model deployment**, add **instructions**, and configure **tools**
4. Test the agent in the **playground**
5. Deploy it to Agent Service so it runs in the cloud

> **Exam insight**: The agent's **model deployment name** (not the model family) is what you reference when configuring an agent and in SDK code.

---

## 5. Set Up Visual Studio Code for Agent Development

The **Microsoft Foundry Toolkit for Visual Studio Code** extension (aka.ms/foundrytk) brings Foundry development into VS Code.

### What the extension enables
- Browse/manage project resources (models, agents, connections, vector stores)
- Deploy models from the model catalog
- Create and configure agents via a **visual designer** + YAML
- Test agents in integrated **playgrounds**
- Generate **integration code** for your deployed agent
- Create, test, and deploy **hosted agent workflows** (with Agent Inspector for tracing)

### Setup checklist
1. Install [Visual Studio Code](https://code.visualstudio.com/)
2. Install the **Microsoft Foundry Toolkit** extension
3. **Sign in to your Azure resources** (Entra ID / `az login`)
4. **Set your default project** (create one if needed)
5. Ensure a **model is deployed** in the project

> **Exam insight**: The extension is the bridge between the Foundry portal and local development — know that it supports the designer, YAML, playgrounds, and code generation.

---

## 6. Configure and Manage Agents in VS Code

### Create an agent in the designer
1. In the **Foundry Toolkit** view → **Resources** → **Classic** section
2. Select the **+** next to **Classic Agents**
3. Configure: **name**, **model deployment**, **description**, **system instructions**, **tools**
4. Save the `.yaml` file

### The agent YAML definition
The designer writes a declarative YAML file alongside the visual editor:

```yaml
# yaml-language-server: $schema=https://aka.ms/ai-foundry-vsc/agent/1.0.0
version: 1.0.0
name: my-agent
description: Description of the agent
id: ''
metadata:
  authors:
    - author1
  tags:
    - tag1
model:
  id: 'gpt-4o-1'
  options:
    temperature: 1
    top_p: 1
instructions: Instructions for the agent
tools: []
```

### Manage a deployed agent
| Action | How |
|--------|-----|
| **Deploy** | Select **Create Agent on Microsoft Foundry** in the designer |
| **Edit** | **AGENT PREFERENCES** → **Edit Agent** → edit → **Update Agent on Microsoft Foundry** |
| **View code** | **View Code** → pick SDK, language, auth method → boilerplate generated |
| **Test** | **Open Playground** (remote agent playground) |
| **View threads** | **Resources** → **Classic** → **Threads** |
| **View run info** | On **THREAD DETAILS** → **View run info** (opens a `.json` with config, messages, tool calls) |
| **Delete** | Right-click agent/model in **Resources** → **Delete** |

> **Exam insight**: Agents are defined **declaratively in YAML** — the same config can be authored in the portal, VS Code, or SDK/REST. Updates to a deployed agent take effect immediately.

---

## 7. Extend Agent Capabilities with Tools

Agent Service provides built-in tools to extend capabilities and connect to data sources.

### Knowledge tools (grounding)
| Tool | Description |
| --- | --- |
| **File Search** | Augment agents with knowledge from uploaded files / proprietary documents |
| **Azure AI Search** | Ground agents with data from an existing Azure AI Search index |
| **Grounding with Bing search** | Real-time web info with inline citations |
| **SharePoint (preview)** | Chat with private documents stored in SharePoint |

### Action tools
| Tool | Description |
| --- | --- |
| **Code Interpreter** | Agent writes & runs Python code in a sandboxed environment |
| **Function calling** | You define custom functions; your app executes them and returns results |
| **Azure Functions** | Call your Azure Functions for custom, stateful actions |
| **OpenAPI 3.0 tool** | Connect to external APIs via an OpenAPI spec |
| **Browser Automation (preview)** | Real-world browser tasks via natural language |
| **Computer Use (preview)** | Interact with computer systems through their UIs |
| **Image Generation (preview)** | Generate images in conversations/workflows |
| **Deep Research** | Agentic research pipeline with `o3-deep-research` + Bing |

### Integration tools
- **MCP tool** — connect to tools hosted on an existing MCP endpoint
- **A2A / Connected agents** — agent-to-agent communication

### Adding a tool in the designer
1. In the **TOOL** section, select **Add tool**
2. Choose the tool type (Bing grounding, file search, code interpreter, OpenAPI, MCP)
3. Configure the tool (e.g., upload files for file search, provide an OpenAPI spec)
4. Select **Create and connect** / **Upload and save** / **Create Tool**

> **Exam insight**: Match tool to scenario — "ground the agent with company data" → Azure AI Search or File Search; "let the agent run calculations on uploaded data" → Code Interpreter; "call an existing REST API" → OpenAPI tool or function calling.

---

## 8. Test, Deploy, and Integrate Agents

### Test in the playground
- Open the **Remote Agent Playground** from the deployed agent
- Send prompts and view outputs, including **agent annotations** that highlight sources (e.g., Bing grounding citations)

### Deploy
- **Prompt agents**: deploy from the portal/VS Code — Foundry hosts and scales them, no containers
- **Hosted agents**: ship as a **container image** (to ACR) or **zip of source code**; Foundry builds the image and runs it on **Azure Container Apps**

### Integrate into applications (SDK pattern)
The extension can generate boilerplate code. The standard Python pattern uses the Foundry Projects SDK with keyless auth:

```python
from azure.identity import DefaultAzureCredential
from azure.ai.projects import AIProjectClient

credential = DefaultAzureCredential()  # CLI -> managed identity -> env

project = AIProjectClient.from_connection_string(
    conn_str="<PROJECT_ENDPOINT>;subscriptionid=<sub>;resourcegroupname=<rg>;projectname=<proj>",
    credential=credential,
)

openai_client = project.inference.get_openai_client()  # OpenAI-compatible client
# ... create agent, thread, run, messages ...
```

> **Exam insight**: You won't write full SDK code on the exam, but know the package names (`azure-ai-projects`, `azure-identity`), the client + `DefaultAzureCredential` pattern, and the Responses API flow. Never hardcode keys — use keyless auth.

---

## 9. Key Takeaways for AI-103

### Must-Know Facts
1. **AI agent** = LLM + instructions + tools, operating in a goal-directed loop
2. **Foundry Agent Service** = managed platform handling hosting, scaling, identity, state, monitoring
3. **Prompt agents** = config-only (no code/compute); **Hosted agents** = code-based (container compute)
4. **Responses API** = the single model-and-tools endpoint behind every agent type
5. **VS Code Toolkit** = designer + YAML + playgrounds + code generation for agent development
6. **Agents are declarative** — defined in YAML, authorable in portal, VS Code, or SDK/REST
7. **Tools** = knowledge (file search, AI Search, Bing) + action (code interpreter, functions, OpenAPI, MCP)
8. **SDK pattern** = `AIProjectClient` + `DefaultAzureCredential` (keyless auth)

### Connections to Other Modules

| This module | Connects to |
|-------------|-------------|
| Agent fundamentals + Agent Service | Module 2.2 (custom tools), 2.3 (MCP tools) |
| VS Code agent development | Module 2.6 (agent-driven workflows) |
| Prompt vs hosted agents | Module 2.7 (Agent Framework), 2.8 (multi-agent orchestration) |
| Agent Service overview | Module 2.9 (A2A agent discovery) |

---

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

*Notes created: 2026-08-04 · Source: Microsoft Learn module via MCP*