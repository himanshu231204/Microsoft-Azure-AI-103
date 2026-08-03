# AI Agents on Azure — Deep Dive Notes (AI-103)

> **Purpose**: Personal learning notes for building, deploying, and operating AI agents on Microsoft Azure.
> Built for both **AI-103 exam prep** and **real-world production skills** as an AI Engineer.
> Source: Microsoft Learn (fetched via MCP) — study guide, Foundry Agent Service docs, Agent Framework, Semantic Kernel, MCP docs.
>
> **Course**: AI-103T00-A (4-day instructor-led) — 4 learning paths, 34 modules
> **Exam**: AI-103 — Developing AI Solutions on Azure
>
> **Related files**: [`AI-103-Study-Guide.md`](./AI-103-Study-Guide.md) (full exam skills), [`README.md`](./README.md) (course module tracker).

---

## Table of Contents

1. [Why Agents Are the Next Big Thing](#1-why-agents-are-the-next-big-thing)
2. [What Is an AI Agent? (Core Concepts)](#2-what-is-an-ai-agent-core-concepts)
3. [Agent vs RAG vs Copilot vs Workflow](#3-agent-vs-rag-vs-copilot-vs-workflow)
4. [The 5 Core Components of an Agent](#4-the-5-core-components-of-an-agent)
5. [Agent Development Options on Azure (the Spectrum)](#5-agent-development-options-on-azure-the-spectrum)
6. [Azure AI Foundry Agent Service — Deep Dive](#6-azure-ai-foundry-agent-service--deep-dive)
7. [The Tools Catalog — Extending Agent Capabilities](#7-the-tools-catalog--extending-agent-capabilities)
8. [Function Calling — How Tools Actually Work](#8-function-calling--how-tools-actually-work)
9. [Python SDK Essentials](#9-python-sdk-essentials)
10. [Agent Frameworks: Agent Framework, Semantic Kernel, LangGraph](#10-agent-frameworks-agent-framework-semantic-kernel-langgraph)
11. [Memory & Knowledge for Agents](#11-memory--knowledge-for-agents)
12. [Multi-Agent Orchestration](#12-multi-agent-orchestration)
13. [Model Context Protocol (MCP)](#13-model-context-protocol-mcp)
14. [Production: Deploy, Monitor, Secure](#14-production-deploy-monitor-secure)
15. [Responsible AI & Guardrails](#15-responsible-ai--guardrails)
16. [How a Real AI Engineer Works (Production Mindset)](#16-how-a-real-ai-engineer-works-production-mindset)
17. [AI-103 Agent Skills Map + Study Plan](#17-ai-103-agent-skills-map--study-plan)
18. [Hands-On Project Roadmap](#18-hands-on-project-roadmap)
19. [Model Selection & Catalog — Choosing the Right Model](#19-model-selection--catalog--choosing-the-right-model)
20. [CI/CD & Infrastructure — Setting Up AI Solutions in Foundry](#20-cicd--infrastructure--setting-up-ai-solutions-in-foundry)
21. [Evaluation & Observability — Measuring AI Quality](#21-evaluation--observability--measuring-ai-quality)
22. [Computer Vision — Image, Video & Multimodal](#22-computer-vision--image-video--multimodal)
23. [Text & Speech Analysis — Language, Translation, Audio](#23-text--speech-analysis--language-translation-audio)
24. [Information Extraction — Documents, OCR & RAG Ingestion](#24-information-extraction--documents-ocr--rag-ingestion)
25. [Key Links & Reference](#25-key-links--reference)

---

### Exam Coverage Map

| Exam Section | Weight | Covered In |
|-------------|--------|------------|
| **Plan & manage Azure AI solution** | 25–30% | §5, §6, §14, §17, §19, §20 |
| **Implement gen AI & agentic solutions** | 30–35% | §2–§13, §15, §16, §21 |
| **Implement computer vision solutions** | 10–15% | §22 |
| **Implement text analysis solutions** | 10–15% | §23 |
| **Implement information extraction solutions** | 10–15% | §24 |

---

## 1. Why Agents Are the Next Big Thing

AI agents represent the **next generation of intelligent applications**. Traditional apps follow fixed logic; agents **reason over requests and take action** autonomously or semi-autonomously.

**The shift:**
| Traditional | Agentic |
| --- | --- |
| Fixed rules & code paths | Model decides *what to do next* |
| Single request → single response | Multi-step reasoning & planning |
| No tool access | Calls APIs, code, databases, search |
| Stateless | Remembers context (memory) |
| Cannot self-correct | Evaluates, reflects, retries |

> Exam note: AI-103's "Implement generative AI and agentic solutions" is the **largest weighted section (30–35%)**. Agents are the core of this exam.

---

## 2. What Is an AI Agent? (Core Concepts)

**Definition** (from Microsoft Agent Framework docs):

> An **AI agent** is a software entity designed to perform tasks autonomously or semi-autonomously by receiving input, processing information, and taking actions to achieve specific goals. Agents send and receive messages, generating responses using a combination of models, tools, human inputs, or other customizable components.

**Four capabilities that make an agent (not just an LLM call):**
1. **Plan** — Break complex goals into sequential or parallel subtasks.
2. **Use tools** — Call APIs, execute code, query databases, interact with external services.
3. **Perceive** — Process multimodal inputs: text, images, audio, structured data.
4. **Remember** — Store and recall context from current and past interactions.

**Six core capabilities of effective agents:**
| Capability | Description |
| --- | --- |
| **Perception, understanding, memory** | Process multimodal inputs, understand context, maintain state |
| **Dynamic task decomposition & planning** | Break goals into subtasks, sequence, adapt plans |
| **Contextual retrieval & grounded generation** | Retrieve knowledge to produce grounded, accurate responses |
| **Tool use & orchestration** | Select and invoke the right tools for the task |
| **Evaluation, feedback, self-correction** | Assess output quality, detect errors, iterate |
| **Trust, safety, reliability** | Operate within guardrails, auditable & explainable |

### Agent types you should know
- **Copilots** — work *alongside* users, suggest/recommend, human approves (e.g., GitHub Copilot).
- **Autonomous agents** — operate independently toward a goal (with human-in-the-loop where needed).
- **Semi-autonomous agents** — act autonomously with **approval gates / oversight** for sensitive steps (this is what the exam calls *approval flow controls*).

---

## 3. Agent vs RAG vs Copilot vs Workflow

**RAG (Retrieval-Augmented Generation):**
- Fixed pipeline: `retrieve → pass as context → generate`.
- Great for simple Q&A, but **cannot** break down multi-step queries, choose between tools, remember prior interactions, or self-correct.
- Agent vs RAG: **agents add a reasoning loop** — the agent decides *when* to retrieve, *what* to search, *which* tool to use, and *whether* to try another approach.

**Workflow:**
- A workflow is a **deterministic, predefined sequence** of steps (rules engines, Power Automate, Logic Apps, Copilot Studio topics, Foundry workflows).
- Agents are **nondeterministic** — model-driven decisions at each step.
- Hybrid: workflows can call agents; agents can use workflow tools.

**Copilot vs Agent:**
- Copilot: suggests; human decides/edits.
- Agent: acts; may ask for approval on risky actions.

> Exam insight: Be able to pick *which pattern fits a scenario* — this appears both in exam questions and real architecture discussions.

---

## 4. The 5 Core Components of an Agent

From the Azure Cloud Adoption Framework — every agent is built on these components:

```
                 ┌──────────────────────────────────────────┐
                 │          Generative AI Model             │
                 │         (the reasoning engine)           │
                 └───────┬──────────────┬───────────────────┘
                         │              │
            ┌────────────▼─────┐   ┌────▼──────────────┐
            │   Instructions    │   │      Memory        │
            │ (scope & rules)   │   │ (state & history)  │
            └────────────┬─────┘   └────┬──────────────┘
                         │              │
            ┌────────────▼─────┐   ┌────▼──────────────┐
            │    Retrieval      │   │      Actions       │
            │ (knowledge/data)  │   │ (tools & APIs)     │
            └──────────────────┘   └───────────────────┘
```

1. **Generative AI model** — the reasoning engine; processes instructions, integrates tool calls, generates outputs.
2. **Instructions** — define scope, boundaries, behavioral guidelines. Clear instructions prevent scope creep.
3. **Retrieval / Knowledge** — grounding data; reduces hallucinations and ensures relevance.
4. **Actions / Tools** — functions, APIs, systems the agent calls; transforms it from passive retriever to active participant.
5. **Memory** — conversation history & state; enables multi-turn conversations and long-running tasks.

**Orchestration layer** (sometimes called the 6th component): the cyclical loop governing how the agent takes in info → reasons → decides next action → repeats until goal reached or stopping point.

---

## 5. Agent Development Options on Azure (the Spectrum)

Microsoft Foundry gives you a **spectrum from declarative to full code**:

```
Least control / fastest         ──────────►         Most control / most flexible
─────────────────────────────────────────────────────────────────────────────
1. Single model call            2. Prompt agent              3. Hosted agent
   (Responses API)                 (declarative config)         (your container/code)
```

| Option | What it is | When to use |
| --- | --- | --- |
| **Single model call** | Just prompt a deployed model, no tools/orchestration | Prototyping, simple completions |
| **Prompt agent** | Declarative: instructions + model + tools defined in portal/SDK; **Foundry runs it for you** | Fast start, production agents with no custom orchestration, internal tools |
| **Hosted agent** | Your code (Agent Framework, LangGraph, Semantic Kernel, custom) packaged as a **container**, Foundry manages endpoint/scale/identity/observability | Custom code, custom protocols, full control over compute and orchestration |
| **Frameworks in your own app** | Use Semantic Kernel / Agent Framework / LangGraph embedded in an existing app | Agents embedded inside existing applications, custom hosting |

> **Exam insight**: Know the differences between prompt vs hosted agents (comparison table in §6).

---

## 6. Azure AI Foundry Agent Service — Deep Dive

**What it is:** The managed agent platform in Microsoft Foundry (previously Azure AI Agent Service / Azure AI Foundry Agent Service). You define an agent (instructions + model + tools), and the service handles hosting, scaling, identity, state, and monitoring.

**Two main agent types:**

### Prompt agents
- Defined **entirely through configuration** (instructions, model selection, tools).
- Author in **portal** (quick start) or **code/SDK/REST** (CI/CD-friendly).
- Foundry runs it — **no app code to maintain, no compute to pay for, no containers**.
- Automatic, Foundry-managed autoscaling; project-level IP sharing.

### Hosted agents
- **Code-based**: Agent Framework, LangGraph, OpenAI Agents SDK, Anthropic Agent SDK, GitHub Copilot SDK, or your own code.
- Ship as a **container image** (to Azure Container Registry) or a **zip of source code** (Foundry builds the image).
- Foundry provides: managed endpoint, **automatic scaling**, **dedicated Microsoft Entra identity per agent**, **session-level state persistence**, **end-to-end observability**.
- Under the hood your code calls the **Responses API** on your Foundry project endpoint for model inference + tool orchestration.
- Runs on **Azure Container Apps** (you can pick CPU/memory pairs).

### Comparison table (memorize this for the exam)

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
| **Best for** | Fast start, agents w/o custom orchestration | Agents that call custom code, multi-agent, custom protocols |

### The Responses API
- The **single model and tools endpoint behind every agent type**.
- You can call it directly from your own code to get Foundry models + platform tools **without creating an agent resource**.
- Same code can later be packaged as a hosted agent — *additive pattern*.

### Workflows in Foundry (for orchestration)
- Newer preview API (`2025-11-15-preview`) supports **workflows** for multi-agent orchestration — declarative sequencing/parallel execution of agent steps. Useful when you need deterministic orchestration rather than free-form agent reasoning.

---

## 7. The Tools Catalog — Extending Agent Capabilities

Built-in tools in Foundry Agent Service (knowledge + action + custom):

### Knowledge tools (grounding)
| Tool | Description |
| --- | --- |
| **File Search** | Augment agents with knowledge from uploaded files / proprietary documents |
| **Azure AI Search** | Ground agents with data from an existing Azure AI Search index (chat with your data) |
| **Web Search / Grounding with Bing** | Real-time info from the web with inline citations |
| **SharePoint (preview)** | Chat with private documents stored in SharePoint |

### Action tools
| Tool | Description |
| --- | --- |
| **Code Interpreter** | Agent writes & runs Python code in a sandboxed environment |
| **Function calling** | You define custom functions; your app executes them and returns results |
| **Azure Functions** | Call your Azure Functions for custom, stateful actions |
| **OpenAPI 3.0 tool** | Connect to external APIs via OpenAPI spec |
| **Browser Automation (preview)** | Real-world browser tasks via natural language |
| **Computer Use (preview)** | Interact with computer systems through their UIs |
| **Image Generation (preview)** | Generate images in conversations/workflows |
| **Microsoft Fabric (preview)** | Connect to Fabric data agent for data analysis |
| **Deep Research** | Agentic research pipeline with `o3-deep-research` + Bing |

### Integration tools
- **MCP tool** — connect to tools hosted on an existing MCP endpoint (§13).
- **A2A / Connected agents** — agent-to-agent communication (§12).

> **Exam insight**: Match tool to scenario — e.g., "ground the agent with company data" → Azure AI Search or File Search; "let the agent run calculations on uploaded data" → Code Interpreter; "call an existing REST API" → OpenAPI tool or function calling.

---

## 8. Function Calling — How Tools Actually Work

The classic agent loop. **Memorize the 5-step pattern** (appears in exam and daily work):

1. **Define function tools** — describe each function's name, parameters, purpose (docstrings).
2. **Create an agent** — register the agent with your function definitions.
3. **Send a prompt** — the agent analyzes the prompt and *requests* function calls if needed.
4. **Execute and return** — **your app** runs the function and submits the output back to the agent.
5. **Get the final response** — the agent uses your function output to complete its response.

Key mechanics:
- The agent emits `function_call` output items; your code executes and submits a follow-up `function_call_output` item.
- **Runs expire 10 minutes after creation** — submit tool outputs before they expire.
- Function tools are configured via **SDK/REST** (portal doesn't support add/remove/update of function definitions).
- Two execution models: single `response`, or a `conversation` with multiple items (each item = one response).
- The portal/SDK can configure function calling, but **executing custom functions always requires your code**.

---

## 9. Python SDK Essentials

The primary SDK for agents is **`azure-ai-projects`** (Azure AI Projects SDK). Install alongside `azure-identity`.

```bash
# Core packages
pip install "azure-ai-projects>=2.0.0" azure-identity python-dotenv

# For hosted agents
pip install "azure-ai-projects>=2.3.0"
```

### Environment setup
```bash
# Foundry project endpoint (from portal → Overview → Libraries → Foundry)
# Format: https://<resource>.services.ai.azure.com/api/projects/<project>
export PROJECT_ENDPOINT="https://your-project.services.ai.azure.com/api/projects/your-project"

# Model deployment name (from Build → Deployments)
export MODEL_DEPLOYMENT_NAME="gpt-4o-mini"

# Hosted agent runtime injects these automatically:
# FOUNDRY_PROJECT_ENDPOINT, AZURE_AI_MODEL_DEPLOYMENT_NAME, APPLICATIONINSIGHTS_CONNECTION_STRING
```

### Authentication (real production pattern: keyless, Entra ID)
```bash
az login                    # interactive sign-in for development
# Production: managed identity (DefaultAzureCredential) — NO keys in code
```

```python
from azure.identity import DefaultAzureCredential
credential = DefaultAzureCredential()   # tries CLI, managed identity, env, etc. in order
```

### Minimal agent client (prompt agent consumption)
```python
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential

project = AIProjectClient.from_connection_string(
    conn_str="<PROJECT_ENDPOINT>;subscriptionid=<sub>;resourcegroupname=<rg>;projectname=<proj>",
    credential=DefaultAzureCredential(),
)
# or newer: pass endpoint directly

openai_client = project.inference.get_openai_client()   # OpenAI-compatible client
# ... create agent, thread, run, messages ...
```

### Minimal Agent Framework (new generation, Python-first)
```python
from agent_framework import Agent
from agent_framework.foundry import FoundryChatClient
from azure.identity import AzureCliCredential

agent = Agent(
    client=FoundryChatClient(
        project_endpoint="https://your-project.services.ai.azure.com",
        model="gpt-4o-mini",
        credential=AzureCliCredential(),
    ),
    name="FoundryWeatherAgent",
    instructions="You are a helpful assistant.",
)
```

> **Exam insight**: You will NOT need to write full SDK code on the exam, but you should understand SDK package names, the client-credential pattern, and the Responses API flow.

---

## 10. Agent Frameworks: Agent Framework, Semantic Kernel, LangGraph

### Microsoft Agent Framework (`agent_framework`)
- The **next-gen, unifies Semantic Kernel + AutoGen** concepts into one Python-first SDK.
- One `Agent` class works across all `ChatClient`-based services: **Foundry, OpenAI ChatCompletion, OpenAI Responses**.
- `FoundryChatClient` = Foundry-first path for direct inference; supports tools, structured outputs, streaming.
- Sits on `BaseAgent`; all agents implement `SupportsAgentRun`.
- **Sessions**: `agent.create_session()` (local) or `agent.get_session(service_session_id=...)` (service-managed), pass with `session=` to `agent.run(...)`.
- Migrating from Semantic Kernel: agent types are consolidated (no more `ChatCompletionAgent`/`AzureAIAgent` split — just `Agent` + client).

### Semantic Kernel (`semantic-kernel`)
- Agent types: `ChatCompletionAgent`, `OpenAIAssistantAgent`, `AzureAIAgent`, `OpenAIResponsesAgent`.
- Core concepts: **Kernel** (DI container of services + plugins), **plugins** (native functions / prompts), **function calling**, **memory/connectors**.
- `AzureAIAgent` integrates with Foundry projects: automates tool calling, manages conversation threads, supports built-in tools (file search, code interpreter, Bing, Azure AI Search, Azure Functions, OpenAPI).
- **Orchestration**: agent groups (e.g., `AgentGroupChat`) for collaboration.

```python
import semantic_kernel as sk
from semantic_kernel.agents import ChatCompletionAgent
from semantic_kernel.connectors.ai.open_ai import OpenAIChatCompletion

agent = ChatCompletionAgent(
    service=OpenAIChatCompletion(),
    name="Support",
    instructions="Answer in one sentence.",
)
```

### LangGraph
- Open-source orchestration framework (LangChain ecosystem) for building stateful, graph-based agent workflows.
- Popular for precise control over state, nodes/edges, checkpointing, human-in-the-loop interrupts.
- Can be deployed as a **hosted agent** container on Foundry, or on Container Apps / App Service.

### Choosing a framework (production decision)
| Need | Choose |
| --- | --- |
| Fastest time-to-agent, no code maintenance | **Prompt agent** (portal/SDK) |
| Python-first, unified modern SDK | **Microsoft Agent Framework** |
| Enterprise .NET or familiar SK abstractions | **Semantic Kernel** |
| Fine-grained graph control, custom state machine | **LangGraph** |
| Maximum control, custom hosting | Your own code + Responses API |

---

## 11. Memory & Knowledge for Agents

### Memory
Memory is what makes an agent **stateful** instead of stateless model inference.

- **Session/ephemeral memory**: conversation history for transactional agents (minimize retention).
- **Long-term/persistent memory**: historical recall for advisory agents, personalization.
- Storage options: Foundry **managed conversation state**, **Azure Cosmos DB** (vector database + chat memory), **PostgreSQL (HorizonDB)**, Redis.

> Production governance: treat conversation history as **sensitive enterprise data**. Align persistence model with agent function.

### Knowledge / Retrieval
- **Azure AI Search** — the primary grounding engine: vector search, semantic/hybrid search, indexing.
- **Embeddings** — `text-embedding-3-small`, `text-embedding-ada-002` convert text to vectors; cosine similarity finds semantically close content.
- **Retrieval methods**: vector search, full-text/keyword search, **hybrid** (both + semantic reranking).
- **File Search** tool — simplest: upload files, agent uses them.
- **Content Understanding** — produce clean, structured/markdown representations of documents for downstream RAG.

> Exam insight: "Choose an appropriate method for retrieval and indexing" + "Configure semantic search, hybrid search, and vector search for grounding" are tested skills. RAG ingestion flow includes OCR, layout analysis, field extraction (Document Intelligence / Content Understanding).

---

## 12. Multi-Agent Orchestration

When a task is too complex for one agent, split responsibilities across **specialized agents** coordinated by a main agent.

### Patterns
1. **Hierarchical / orchestrator-subagent** — main agent classifies intent and delegates to connected subagents (most common).
2. **Workflow-oriented (sequential)** — deterministic chain: Agent A → Agent B → ... (approval chains, ETL, compliance). Enforce pre/post-conditions, idempotency, retry/dead-letter, human approval gates (Teams/Outlook).
3. **Concurrent / parallel** — multiple agents run in parallel and results merge.
4. **AgentGroupChat (Semantic Kernel)** — agents collaborate through shared chat; coordinator, collaborator roles.

### Connected Agents (Foundry)
- **No custom orchestrator needed** — a primary agent delegates to purpose-built subagents via `ConnectedAgentToolDefinition`.
- Each connected agent specializes; main agent coordinates.
- **Real example — Contract Review Assistant**:
  - **Main agent (orchestrator)**: intent classification + delegation ("determine if clause summarization, comparison, or compliance, route accordingly").
  - **Agent 1 — clause summarizer**: File Search + Code Interpreter to extract/summarize clauses.
  - **Agent 2 — compliance validator**: File Search (policy docs) + OpenAPI tool (compliance API) + Azure Function/Logic Apps (logic checks).
- **Publish to production**: each agent (main + connected) publishes **separately** as an Agent Application with its own endpoint and Entra Agent Identity; routing keeps working via agent IDs.

### Multi-agent on custom compute
- **Microsoft Agent Framework + Azure Container Apps** for deterministic, code-driven orchestration: App Service frontend → Container Apps API orchestrator → Foundry GPT-4.1 → specialized agents; Cosmos DB for persistence; ACR for versioned images.

> Exam insight: Know how to "Implement orchestrated multi-agent solutions" and "Build autonomous or semiautonomous workflows with safeguards and approval flow controls."

---

## 13. Model Context Protocol (MCP)

**MCP** = open protocol for how LLMs interact with external **tools, memory, and context** in a safe, structured, stateful way.

### Architecture
- **Hosts** — apps that use MCP clients (e.g., VS Code).
- **Clients** — components managing connections and retrieving data from servers.
- **Servers** — provide tools (actions), resources (data), and prompts.

### On Azure
- **Consume existing MCP servers** (e.g., Azure MCP Server exposes Azure CLI/azd as tools).
- **Develop your own MCP server** (e.g., Container Apps building block, App Service as MCP server).
- **Foundry hosted MCP tools**: attach remote MCP servers to your agent (`MCPToolDefinition` with `serverLabel`, `serverUrl`, `AllowedTools`); Foundry hosts/manages the server; configurable **tool approval workflow**.
- **Foundry Toolboxes**: bundle multiple tools (Web Search, Code Interpreter, File Search, AI Search, MCP servers, OpenAPI, A2A) into a **single MCP-compatible endpoint**; reuse across agents; works with Agent Framework, LangGraph, Copilot SDK, any MCP client.

### Best practices
- Don't hardcode tool names — let the agent discover tools dynamically.
- Don't parse tool output programmatically — let the LLM interpret it.
- Let the LLM decide which tools to call from descriptions.

---

## 14. Production: Deploy, Monitor, Secure

### Deployment options
| Path | Tooling | Use case |
| --- | --- | --- |
| **Prompt agent** | Portal or SDK/REST (CI/CD) | Fast, managed, no infra |
| **Hosted agent (container)** | `docker build --platform linux/amd64` → `az acr login/push` → SDK/azd deploy | Custom code |
| **Hosted agent (source zip)** | `azd` builds image for you | Code-first without Docker |
| **azd (Azure Developer CLI)** | `azd provision` + `azd deploy` | Full provisioning + deploy |
| **Frameworks on own compute** | Container Apps / App Service | Custom hosting, hybrid |

**azd flow for hosted agents:**
```bash
azd provision   # creates resource group: Foundry instance, project, model deployment, App Insights, container registry
azd deploy      # packages agent as container, pushes to ACR, deploys to Agent Service
```

**Container requirements (hosted agents):**
- Must be `x86_64 (linux/amd64)` — use `docker build --platform linux/amd64 .` on ARM machines.
- Implement `IResponseHandler` / protocol library (`azure-ai-agentserver-responses` for `/responses`, `azure-ai-agentserver-invocations` for `/invocations` webhooks, `_ws` for real-time voice).
- Serves on port **8088** locally; Foundry gateway routes in production.
- Platform injects env vars: `FOUNDRY_PROJECT_ENDPOINT`, `AZURE_AI_MODEL_DEPLOYMENT_NAME`, `APPLICATIONINSIGHTS_CONNECTION_STRING`.

### Monitoring & Observability
- **Azure Monitor / Application Insights** — tracing, token analytics, latency breakdowns, safety signals.
- **Foundry tracing** — validates tool invocations, agent runs.
- Track: model performance, **drift**, **safety events**, **grounding quality**, data ingestion quality, search index health, relevance.
- Error analysis on deployed agents; evaluate agent behavior continuously.

### Security (keyless & least privilege)
- **Managed identity** (system-assigned) for agents — never API keys in code.
- **Entra ID Agent Identities** — dedicated identity per hosted agent; scope permissions with **least privilege**.
- RBAC roles: **Foundry User/Owner**, **Foundry Project Manager** (renamed from Azure AI User/Owner/Project Manager).
- **Private networking** — bring-your-own VNet, private endpoints, data proxy; subnet sizing: `/24` recommended for production hosted agents, `/27` minimum.
- **Keyless credentials** — DefaultAzureCredential, managed identity.
- Grant container registry role `Container Registry Repository Reader` (or `AcrPush`) to project's managed identity.

### Cost & Scale
- Quotas, scaling, **rate limits**, **TPM**, cost footprints for model + agent workloads.
- Hosted agent revision limits: 100 active / 1,000 total per agent; ~200 hosted agents per Foundry instance; ~250 project cap.
- Prompt agents: no hard count limit; IPs allocated at project level.

---

## 15. Responsible AI & Guardrails

For agentic systems, governance is critical because agents are **nondeterministic**.

- **Safety filters & guardrails** — Azure AI Content Safety; content moderation.
- **Risk detection** — prompt injection (including **indirect prompt injection via embedded text in images**), jailbreak detection.
- **Tool-access controls** — approve/deny specific tools; scoped API endpoints with strict input validation.
- **Oversight modes** — human-in-the-loop approval gates for high-risk actions; approval workflows for MCP tool invocations.
- **Auditing** — trace logging, **provenance metadata**, approval workflows.
- **Evaluation** — evaluators, safety evaluations, explanation tooling; detect fabrications, relevance, quality, safety.
- **Explainability** — chain-of-thought evaluations, self-critique loops, reflection.

> Exam insight: "Implement responsible AI across generative AI and agentic systems" is a tested area — be ready to pick the guardrail/oversight mechanism for a scenario.

---

## 16. How a Real AI Engineer Works (Production Mindset)

The exam teaches *what* Azure offers; **production skill is about the workflow**:

1. **Start declarative, go code when needed** — prototype a prompt agent, move to hosted agents for custom logic.
2. **Code-first everything** — define agents via SDK/REST in your CI/CD so they're versioned, reviewed, and rolled out automatically (GitOps).
3. **Keyless auth everywhere** — managed identity, `DefaultAzureCredential`; secrets in Key Vault; never keys in code.
4. **Test before deploy** — playground testing, then evaluation (groundedness, relevance, safety) before production.
5. **Design for evaluation** — instrument traces, token counts, safety signals from day one; evaluate agent behavior continuously.
6. **Human-in-the-loop by design** — approval gates for destructive/sensitive actions (email send, DB writes, payments).
7. **Security is scoped APIs** — expose capabilities through narrowly scoped, input-validated APIs; least privilege tokens; sandboxed tool execution; log every action to agent+conversation ID (audit trail).
8. **Versioning & rollback** — unique image tags (not `:latest`), revision limits, ACR versioned images.
9. **Cost-aware** — watch token usage, choose model size (small vs large models) per task, monitor rate limits/quotas.
10. **Memory governance** — treat conversation history as sensitive data; align persistence with agent role.

---

## 17. AI-103 Agent Skills Map + Study Plan

### Where agents appear in the exam (from the official study guide)
| Exam section | Agent-related skills |
| --- | --- |
| **Plan & manage (25–30%)** | Choose Foundry services for agents; model selection (LLM/small/multimodal); retrieval & indexing; memory/tool/knowledge services; deployment options; CI/CD; quotas/scaling/rate limits; monitoring (drift, safety, grounding); security (managed identity, keyless, private networking); responsible AI (safety filters, guardrails, approvals, trace logging) |
| **Implement gen AI & agentic (30–35%)** ⭐ | Deploy/consume models; RAG; workflows & tool-augmented flows; **build agents**: roles/goals/conversation tracking/tool schemas, retrieval+function calling+memory, tools (APIs/knowledge stores/search/custom), **orchestrated multi-agent**, **autonomous workflows w/ approval controls**, **monitor & evaluate agents, error analysis**; optimize: prompt engineering, reflection, self-critique, observability (tracing/token analytics) |
| **Computer vision (10–15%)** | Multimodal agents; Content Understanding pipelines; visual grounding Q&A |
| **Text analysis (10–15%)** | Speech as agent modality (STT/TTS); translation flows |
| **Information extraction (10–15%)** | Retrieval/grounding pipelines feeding agent tools; Content Understanding → clean grounded representations |

### Mapping exam sections → course learning paths
| Exam Section | Learning Path | Modules |
| --- | --- | --- |
| §1 Plan & manage (25–30%) | LP1: Develop generative AI apps in Azure | 1.1–1.8 (plan, deploy, SDK, RAG, fine-tune, responsible AI, eval) |
| §2 Implement gen AI & agentic (30–35%) ⭐ | LP2: Develop AI agents on Azure | 2.1–2.9 (Foundry agents, custom tools, MCP, multi-agent, A2A) |
| §2 (continued) | LP1: Generative AI (RAG, fine-tune, eval) | 1.5–1.8 |
| §3 Computer vision (10–15%) | LP4: Extract insights from visual data | 4.1–4.8 (image analysis, OCR, faces, video, vision gen-AI) |
| §4 Text analysis (10–15%) | LP3: Develop natural language solutions | 3.1–3.9 (text analytics, CLU, speech, translation) |
| §5 Info extraction (10–15%) | LP4: Extract insights from visual data | 4.1–4.8 (includes content understanding) |

### Suggested study path (agent-focused, mapped to course modules)
1. **LP1: Develop generative AI apps** — Start here for foundations (§1 + §2 basics)
   - Module 1.1: Plan and prepare to develop AI solutions on Azure
   - Module 1.2: Choose and deploy models from the model catalog
   - Module 1.3: Develop an AI app with the Azure AI Foundry SDK
   - Module 1.5: Develop a RAG-based solution with your own data
   - Module 1.7: Implement a responsible generative AI solution
   - Module 1.8: Evaluate generative AI performance
2. **LP2: Develop AI agents** — Core agent skills (§2 ⭐)
   - Module 2.1: Develop AI agents with Foundry and VS Code
   - Module 2.2: Integrate custom tools into your agent
   - Module 2.3: Integrate MCP Tools with Azure AI Agents
   - Module 2.7: Develop an AI agent with Microsoft Agent Framework
   - Module 2.8: Orchestrate a multi-agent solution
   - Module 2.9: Discover Azure AI Agents with A2A
3. **LP3: Develop natural language solutions** — Text & speech (§4)
   - Module 3.1: Analyze text with Azure AI Language
   - Module 3.7: Create speech-enabled apps
   - Module 3.9: Develop an audio-enabled generative AI application
4. **LP4: Extract insights from visual data** — Vision & extraction (§3 + §5)
   - Module 4.1: Analyze images
   - Module 4.6: Analyze video
   - Module 4.7: Develop a vision-enabled generative AI application

### Study tips
- **Know the difference**: RAG vs Agent; Prompt vs Hosted agent; Function calling flow; Copilot vs Autonomous.
- **Know the tools catalog** — match tool to scenario.
- **Know the SDK names** — `azure-ai-projects`, `azure-identity`, `agent-framework`, `semantic-kernel`.
- **Know RBAC & identity** — managed identity, keyless, Entra Agent Identity.
- **Hands-on**: everything sticks with the projects in §18.

---

## 18. Hands-On Project Roadmap

A progression that takes you from exam prep to production skills. Build each in this repo:

1. **Level 1 — Prompt agent**: Create a prompt agent in the Foundry portal with Web Search + File Search. Consume it from Python via `azure-ai-projects`. ✓ exam basics
   - *Course modules*: [1.1](modules/01-genai/01-plan-and-prepare/), [1.2](modules/01-genai/02-choose-deploy-models/), [1.3](modules/01-genai/03-develop-ai-app-foundry-sdk/)
2. **Level 2 — Custom tools**: Add function calling (your own Python functions). Build the weather/calculator/CRM-lookup pattern.
   - *Course modules*: [2.1](modules/02-agents/01-develop-agents-foundry-vscode/), [2.2](modules/02-agents/02-integrate-custom-tools/)
3. **Level 3 — RAG grounding**: Index documents into Azure AI Search (hybrid/vector), ground an agent with the index. Use Content Understanding for document prep.
   - *Course modules*: [1.5](modules/01-genai/05-rag-solution/), [2.4](modules/02-agents/04-knowledge-enhanced-agents-foundry-iq/)
4. **Level 4 — Multi-agent**: Connected agents — build the *Contract Review Assistant* example (orchestrator + summarizer + compliance validator).
   - *Course modules*: [2.8](modules/02-agents/08-orchestrate-multi-agent/), [2.9](modules/02-agents/09-discover-agents-a2a/)
5. **Level 5 — Framework agent**: Rebuild Level 2 in **Microsoft Agent Framework** and in **Semantic Kernel**. Compare.
   - *Course modules*: [2.7](modules/02-agents/07-develop-agent-agent-framework/)
6. **Level 6 — MCP**: Expose an existing API as an MCP server (Container Apps); connect it to your agent via hosted MCP tool; try a Foundry Toolbox.
   - *Course modules*: [2.3](modules/02-agents/03-integrate-mcp-tools/)
7. **Level 7 — Production**: Package a hosted agent as a container → ACR → deploy with `azd`. Enable Application Insights tracing, add Entra Agent Identity + managed identity, set approval gates.
   - *Course modules*: [1.7](modules/01-genai/07-responsible-generative-ai/), [2.6](modules/02-agents/06-agent-driven-workflows/)
8. **Level 8 — Eval & guardrails**: Run evaluations (groundedness/relevance/safety), content filters, trace audit. 
   - *Course modules*: [1.8](modules/01-genai/08-evaluate-genai-performance/)

---

## 19. Model Selection & Catalog — Choosing the Right Model

> **Exam weight**: Part of "Plan & manage" (25–30%) — "Choose an appropriate model for each task"

### Model Selection Criteria

| Factor | Considerations |
|--------|---------------|
| **Task type** | Text generation, code, reasoning, embeddings, image, audio, multimodal |
| **Model size** | LLMs (GPT-4o, GPT-4.1) vs SLMs (Phi-4, GPT-4o-mini) — bigger isn't always better |
| **Modality** | Text-only, vision, audio, multimodal (text+image+audio) |
| **Cost** | Per-token pricing, provisioned throughput vs pay-per-call |
| **Latency** | Real-time apps need low latency; batch processing can tolerate higher |
| **Context window** | 8K to 1M+ tokens — match to your document/query length |
| **Fine-tuning** | Available for some models (SFT, DPO, RFT) |
| **Deployment** | Serverless API (fastest) vs managed compute (more control) |

### Model Families Quick Reference

| Family | Best For | Context | Multimodal |
|--------|----------|---------|------------|
| **GPT-4o** | General-purpose, complex tasks | 128K | Yes |
| **GPT-4o-mini** | Cost-effective, high-volume | 128K | Yes |
| **GPT-4.1** | Latest generation, code, reasoning | 1M | Yes |
| **o3 / o4-mini** | Deep reasoning, math, chain-of-thought | 200K | Yes |
| **Phi-4** | Small, efficient, on-device potential | 16K | No |
| **DALL·E 3** | Image generation | N/A | Image out |
| **Whisper** | Speech-to-text | N/A | Audio in |
| **text-embedding-3-large** | Vector embeddings for RAG | 8K | No |
| **Llama 4** | Open-source, customizable | 1M | Yes |
| **Mistral Large** | European compliance, multilingual | 128K | Yes |
| **DeepSeek-R1** | Reasoning, cost-effective | 128K | No |

### Using Benchmarks to Select Models

The Foundry model catalog provides **benchmark data** and a **leaderboard** for objective comparison:

**Four benchmark dimensions:**
| Dimension | What It Measures | Higher/Lower Better |
|-----------|-----------------|---------------------|
| **Quality index** | Reasoning, coding, math, knowledge | Higher = better |
| **Safety scores** | Robustness against harmful content | Lower attack success = better |
| **Estimated cost** | Actual cost to run benchmarks (USD) | Lower = cheaper |
| **Throughput** | Tokens per second | Higher = faster |

**Scenario leaderboards:**
| Scenario | Datasets | Use When |
|----------|----------|----------|
| **Reasoning** | BIG-Bench Hard | Logical, multi-step reasoning |
| **Coding** | BigCodeBench, MBPPPlus | Code generation tasks |
| **Math** | MATH (500 subsample) | Mathematical reasoning |
| **Q&A** | Arena-Hard, GPQA | Adversarial human preference |
| **General Knowledge** | MMLU-Pro | Broad factual knowledge |
| **Groundedness** | TruthfulQA | Resistance to hallucination |

**Tools for comparison:**
- **Model Leaderboard** — sortable table across all dimensions
- **Trade-off charts** — visual scatter plot (e.g., quality vs. cost)
- **Side-by-side comparison** — select 2–3 models for feature/performance/cost comparison
- **Benchmarks tab** — detailed metrics on each model card

### Scenario → Model Mapping

| Scenario | Recommended Model | Why |
|----------|-------------------|-----|
| Simple chatbot / FAQ | GPT-4o-mini | Fast, cheap, good enough |
| Complex document analysis | GPT-4o / GPT-4.1 | Strong reasoning, large context |
| Deep reasoning / math / code | o3 / o4-mini | Chain-of-thought, analysis |
| Image generation | DALL·E 3 | Native text-to-image |
| Speech-to-text | Whisper | Optimized for audio |
| Vector embeddings for RAG | text-embedding-3-large | Semantic similarity |
| Cost-sensitive high-volume | GPT-4o-mini | Lowest per-token cost |
| Enterprise with SLA | GPT-4o (Provisioned PTU) | Guaranteed throughput |
| On-device / edge | Phi-4 | Small, efficient |
| Open-source customizable | Llama 4 | Self-host, fine-tune |

> **Exam insight**: "Choose an appropriate model for each task, including LLMs, small language models, multimodal models, and Foundry Tools" is a tested skill. Match model to scenario based on task requirements, not just model size.

---

## 20. CI/CD & Infrastructure — Setting Up AI Solutions in Foundry

> **Exam weight**: Part of "Plan & manage" (25–30%) — "Design Azure infrastructure" + "Integrate with CI/CD"

### Azure Infrastructure Design for AI

| Component | Purpose | Sizing Guidance |
|-----------|---------|-----------------|
| **Azure AI Foundry** | Central hub for models, agents, tools | Per-project, per-region |
| **Azure AI Services** | Cognitive services (Language, Vision, Speech) | Per-resource, per-region |
| **Azure AI Search** | Vector/hybrid search for RAG | S1 tier minimum for production |
| **Azure Container Registry** | Store agent container images | Standard tier for production |
| **Azure Container Apps** | Hosted agent compute | CPU/memory pairs (2–8 vCPU) |
| **Application Insights** | Monitoring, tracing, telemetry | Auto-provisioned with Foundry |
| **Azure Cosmos DB** | Agent memory, conversation state | Serverless or provisioned RU |
| **Azure Blob Storage** | Document storage for RAG | Hot/Cool tier based on access |
| **Azure Key Vault** | Secrets, keys, credentials | Always use; never keys in code |

### Infrastructure Best Practices

1. **Separate projects per environment** — Dev, Test, Prod as separate Foundry projects
2. **Separate subscriptions** — Enterprise isolation, billing separation, RBAC scope
3. **Private networking** — VNet, private endpoints, data proxy; `/24` subnet for production
4. **Managed identity everywhere** — System-assigned for each resource; never API keys
5. **Tagging strategy** — `env:dev|test|prod`, `team:ai`, `cost-center:xyz`

### CI/CD Pipeline for Agents

**Tool options:**
| Tool | Use Case |
|------|----------|
| **Azure Developer CLI (`azd`)** | Full lifecycle: provision + deploy + pipeline config |
| **GitHub Actions** | Git-native CI/CD, integrates with `azd` |
| **Azure DevOps Pipelines** | Enterprise CI/CD, variable groups, service connections |
| **Bicep / Terraform** | Infrastructure as Code for repeatable deployments |

**azd CI/CD Flow:**
```bash
# 1. Initialize agent project
azd ai agent init -m "<template-url>" --deploy-mode code

# 2. Configure pipeline (creates GitHub Actions or Azure DevOps YAML)
azd pipeline config

# 3. Pipeline runs on push to main:
#    azd provision  → creates/updates Azure infra from Bicep
#    azd deploy     → builds container, pushes to ACR, deploys agent
```

**Pipeline flags for unattended CI:**
| Flag | Purpose |
|------|---------|
| `--no-prompt` | Disable interactive prompts (required in CI) |
| `--output json` | Structured output for parsing |
| `--project-endpoint` | Pin Foundry project endpoint |

**Agent Definition (agent.yaml):**
```yaml
# yaml-language-server: $schema=https://raw.githubusercontent.com/microsoft/AgentSchema/refs/heads/main/schemas/v1.0/ContainerAgent.yaml
kind: hosted
name: customer-support
description: Handles customer inquiries
protocols:
  - protocol: responses
    version: v1
code_configuration:
  runtime: python_3_14
  entry_point: main.py
```

### Deployment Options Comparison

| Method | What It Does | When to Use |
|--------|-------------|-------------|
| **Portal (UI)** | Click-to-deploy, manual config | Quick start, prototyping |
| **SDK/REST** | Code-driven, CI/CD-friendly | Production, versioned deployments |
| **azd** | Full lifecycle: provision + deploy | Complete IaC, pipeline automation |
| **Docker + ACR** | Container image → ACR → deploy | Custom runtime, full control |
| **Source zip** | Foundry builds image for you | Code-first without Docker |

### Key RBAC Roles

| Role | Purpose |
|------|---------|
| **Foundry User** | Basic project access, model consumption |
| **Foundry Owner** | Full project management, CI/CD provisioning |
| **Foundry Project Manager** | Manage agents, deployments, tools |
| **Contributor** | Azure resource management |
| **Reader** | View-only access (benchmarks, catalog) |

> **Exam insight**: "Integrate Foundry projects with CI/CD pipelines" is tested. Know the azd flow (`azd provision` + `azd deploy`), the `agent.yaml` format, and pipeline flags.

---

## 21. Evaluation & Observability — Measuring AI Quality

> **Exam weight**: Part of "Implement gen AI & agentic" (30–35%) — "Evaluate models and apps" + "Set up observability"

### Evaluation Dimensions

| Dimension | What It Measures | How to Test |
|-----------|-----------------|-------------|
| **Groundedness** | Response based on provided context, not hallucinated | Compare response to source documents |
| **Relevance** | Response addresses the query | Semantic similarity, human judgment |
| **Coherence** | Response is logical, well-structured | Human evaluation, LLM-as-judge |
| **Fluency** | Response is grammatically correct, natural | Human evaluation, automated metrics |
| **Safety** | Response doesn't contain harmful content | Content Safety evaluators |
| **Fabrication detection** | Model makes up facts | Compare to source, human review |
| **Quality** | Overall response quality | Composite score across dimensions |

### Foundry Evaluation Tools

| Tool | Purpose |
|------|---------|
| **Evaluate playground** | Portal-based: upload test data, run eval, view results |
| **Evaluate API** | SDK/REST: automated eval in CI/CD pipelines |
| **Custom evaluators** | Define your own eval criteria |
| **AI-assisted evaluators** | LLM-as-judge for nuanced evaluation |
| **Red team** | Adversarial testing, safety evaluations |

### Evaluation in CI/CD

```python
# Example: Automated evaluation in pipeline
from azure.ai.projects import AIProjectClient

project = AIProjectClient(...)

# Run evaluation against test dataset
result = project.evaluations.create(
    evaluator_config={
        "groundedness": {"deployment_name": "gpt-4o"},
        "relevance": {"deployment_name": "gpt-4o"},
        "safety": {"deployment_name": "gpt-4o"},
    },
    input_data="./test-data.jsonl",
)

# Check results — fail pipeline if quality threshold not met
if result.properties["metrics"]["groundedness"] < 0.7:
    raise Exception("Groundedness below threshold")
```

### Observability Stack

| Component | What It Tracks |
|-----------|---------------|
| **Azure Monitor** | Infrastructure metrics, resource health |
| **Application Insights** | Request tracing, dependency calls, exceptions |
| **Foundry tracing** | Agent runs, tool invocations, model calls |
| **Token analytics** | Input/output tokens, cost estimation |
| **Latency breakdowns** | TTFT, time-between-tokens, P50/P90/P95/P99 |
| **Safety signals** | Content filter triggers, jailbreak attempts |
| **Drift detection** | Model performance degradation over time |
| **Grounding quality** | RAG retrieval relevance, search index health |

### Key Metrics to Monitor

| Metric | Why It Matters |
|--------|---------------|
| **Latency (TTFT)** | User experience — time to first response token |
| **Throughput (GTPS)** | Generation speed — tokens per second |
| **Token usage** | Cost control — input vs output token ratio |
| **Error rate** | Reliability — failed requests, timeouts |
| **Groundedness score** | Quality — are responses based on source data? |
| **Safety trigger rate** | Governance — how often content filters fire |
| **Tool invocation count** | Agent behavior — which tools are used, how often |
| **Cost per request** | Budget management — per-call cost tracking |

### Error Analysis for Agents

1. **Trace every agent run** — capture input, tool calls, outputs, timing
2. **Classify failures** — model hallucination, tool failure, timeout, safety block
3. **Root cause analysis** — was it the prompt, the tool, the model, or the data?
4. **Feedback loop** — use findings to improve prompts, tools, and model selection
5. **Continuous evaluation** — re-run evals after every change

> **Exam insight**: "Integrate monitoring into deployed agents, evaluate agent behavior, and perform error analysis" is a tested skill. Know the evaluation dimensions and observability tools.

---

## 22. Computer Vision — Image, Video & Multimodal

> **Exam weight**: "Implement computer vision solutions" (10–15%)

### Image Generation

| Service | What It Does | Use Case |
|---------|-------------|----------|
| **DALL·E 3** | Text-to-image, inpainting, edits | Creative content, product mockups |
| **Stable Diffusion** | Open-source text-to-image (managed compute) | Custom styles, fine-tuned generation |
| **Azure AI Vision** | Image analysis, not generation | Object detection, OCR, captions |

**Key operations:**
- **Text-to-image** — describe what you want, get an image
- **Inpainting** — mask a region, regenerate just that area
- **Image editing** — prompt-driven modifications (style, colors, composition)
- **Variations** — generate multiple versions of a concept

### Video Generation & Analysis

| Capability | Tool/Service | What It Does |
|------------|-------------|--------------|
| **Video generation** | Foundry models (preview) | Generate video from text prompts |
| **Video analysis** | Azure AI Video Indexer | Extract insights, transcripts, faces, scenes |
| **Video editing** | Foundry workflows | Edit generated video clips |
| **Frame extraction** | Content Understanding | Pull key frames for analysis |

### Multimodal Understanding

| Capability | How to Implement |
|------------|-----------------|
| **Image captioning** | GPT-4o vision, Azure AI Vision |
| **Visual Q&A** | GPT-4o with image input — "What's in this image?" |
| **Object detection** | Azure AI Vision — bounding boxes, labels |
| **OCR** | Azure AI Vision / Document Intelligence / Content Understanding |
| **Alt-text generation** | GPT-4o vision — accessibility-compliant descriptions |
| **Visual grounding** | "Based on the image, where is X?" — GPT-4o with coordinates |

### Content Understanding (Foundry Tool)

**What it is:** Multimodal AI service that extracts structured data from documents, images, audio, and video.

| Feature | Description |
|---------|-------------|
| **Prebuilt analyzers** | Invoices, receipts, tax forms, passports, loan applications |
| **Custom analyzers** | Build domain-specific extraction for your content types |
| **Document classification** | Auto-categorize documents by type |
| **OCR** | Industry-leading text extraction from images/PDFs |
| **Table extraction** | Cross-page tables preserved with structure |
| **Semantic chunking** | Intelligent text splitting for RAG |
| **AI-generated image descriptions** | Verbalize images for text search |

**Content Understanding pipeline modes:**
- **Single-task** — one extraction task per document
- **Pro-mode** — multiple tasks, custom schemas, advanced configuration

### Responsible AI for Multimodal

| Risk | Mitigation |
|------|-----------|
| **Unsafe visual content** | Content Safety filters (Hate, Self-Harm, Sexual, Violence) |
| **Indirect prompt injection** | Prompt Shields for embedded text in images |
| **Prohibited symbols** | Visual policy rules, watermarking |
| **Brand misuse** | Logo/symbol detection, usage policies |
| **Inappropriate content** | Classification + human review workflows |

> **Exam insight**: "Implement a solution that generates images from text prompts" + "Configure apps to produce concise or detailed captions" + "Implement visual understanding by configuring Azure Content Understanding" are all tested skills.

---

## 23. Text & Speech Analysis — Language, Translation, Audio

> **Exam weight**: "Implement text analysis solutions" (10–15%)

### Azure AI Language Service

| Feature | What It Does | API/Tool |
|---------|-------------|----------|
| **Entity recognition** | Extract people, places, organizations, dates | Named Entity Recognition (NER) |
| **Key phrase extraction** | Identify main topics/concepts | Key Phrase Extraction |
| **Sentiment analysis** | Positive/nutral/negative + confidence scores | Sentiment Analysis |
| **Language detection** | Identify language of input text | Language Detection |
| **PII detection** | Find and redact personal information | PII Detection |
| **Text summarization** | Extractive or abstractive summaries | Summarization |
| **Custom text classification** | Train models for your categories | Custom Text Classification |
| **Custom NER** | Train models for your entity types | Custom NER |

### Generative AI for Text Analysis (via Foundry)

| Task | How to Implement |
|------|-----------------|
| **Entity extraction** | GPT-4o with structured output prompt |
| **Topic extraction** | GPT-4o with "List the main topics" prompt |
| **Structured JSON output** | GPT-4o with JSON mode / structured outputs |
| **Compliance summarization** | GPT-4o with domain-specific instructions |
| **Domain-specific extraction** | Fine-tuned model or few-shot prompting |

### Speech Solutions

| Service | What It Does | Use Case |
|---------|-------------|----------|
| **Azure AI Speech — STT** | Speech-to-text transcription | Voice commands, dictation, meetings |
| **Azure AI Speech — TTS** | Text-to-speech synthesis | Virtual assistants, accessibility |
| **Custom Speech** | Train models on your audio data | Domain-specific vocabulary, accents |
| **Azure AI Speech — Translation** | Speech-to-speech translation | Real-time multilingual conversations |
| **Azure AI Speech — Speaker Diarization** | Identify who spoke when | Meeting transcripts |

### Speech as Agent Modality

| Pattern | Implementation |
|---------|---------------|
| **Voice-to-agent** | STT → Agent processing → TTS response |
| **Real-time conversation** | Streaming STT + streaming TTS |
| **Multimodal reasoning from audio** | Audio input → GPT-4o audio → text response |
| **Cross-language agent** | STT (language A) → Agent → TTS (language B) |

### Translation

| Tool | What It Does |
|------|-------------|
| **Azure Translator** | Text translation across 100+ languages |
| **LLM-powered translation** | GPT-4o with translation prompt — more natural, context-aware |
| **Speech translation** | Real-time speech-to-speech across languages |
| **Document translation** | Translate entire documents preserving formatting |

### Key Patterns

| Pattern | Example |
|---------|---------|
| **Sentiment + Agent** | "Analyze this customer feedback → route negative to support agent" |
| **Translation + Agent** | "Translate this email → draft a response in the same language" |
| **Speech + Agent** | "Transcribe this meeting → extract action items → send to Teams" |
| **PII + Agent** | "Detect PII in this document → redact before storage" |

> **Exam insight**: "Implement solutions to extract entities, topics, summaries, and structured JSON outputs" + "Integrate speech as an agent modality" + "Build solutions that translate text" are all tested skills.

---

## 24. Information Extraction — Documents, OCR & RAG Ingestion

> **Exam weight**: "Implement information extraction solutions" (10–15%)

### Document Extraction Pipeline

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  Source Files │───►│  Extraction  │───►│  Enrichment  │───►│   Indexing   │
│  (PDF, DOCX, │    │  (OCR, Layout │    │  (Chunking,  │    │  (Vector,    │
│   Images)    │    │   Analysis)  │    │   Embedding) │    │   Keyword)   │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘
```

### Extraction Methods

| Method | What It Does | When to Use |
|--------|-------------|-------------|
| **Document Intelligence** | Prebuilt models for invoices, receipts, forms | Standard document types |
| **Content Understanding** | Custom analyzers, multimodal, semantic chunking | Complex, varied, multimodal content |
| **Azure AI Vision OCR** | Text extraction from images | Simple image-to-text |
| **GPT-4o Vision** | Image understanding + structured extraction | Visual reasoning, complex layouts |

### Content Understanding vs Document Intelligence

| Feature | Content Understanding | Document Intelligence |
|---------|----------------------|----------------------|
| **Input types** | Documents, images, audio, video | Documents, images |
| **OCR** | Industry-leading | Industry-leading |
| **Custom schemas** | Zero-shot, no labeling needed | Prebuilt + custom models |
| **Table extraction** | Cross-page tables | Standard tables |
| **Semantic chunking** | Built-in | Not available |
| **Audio/Video** | Yes | No |
| **Best for** | Complex, multimodal, varied content | Standard document types (invoices, receipts) |

### RAG Ingestion Flow

| Step | What Happens | Tools |
|------|-------------|-------|
| **1. Extract** | Pull text, images, tables from documents | Content Understanding, Document Intelligence |
| **2. Chunk** | Split into manageable pieces | Text Split skill, semantic chunking |
| **3. Embed** | Convert to vectors for similarity search | text-embedding-3-large, Azure OpenAI |
| **4. Index** | Store in search index | Azure AI Search (vector + keyword) |
| **5. Retrieve** | Find relevant chunks at query time | Hybrid search (vector + semantic reranking) |
| **6. Ground** | Pass retrieved chunks as context to model | GPT-4o with RAG prompt |

### Azure AI Search Capabilities

| Feature | What It Does |
|---------|-------------|
| **Vector search** | Find semantically similar content using embeddings |
| **Keyword/full-text search** | Traditional text matching |
| **Hybrid search** | Combine vector + keyword for best results |
| **Semantic reranking** | LLM-powered re-ranking of results |
| **Knowledge store** | Store extracted images/objects for direct retrieval |
| **Skillsets** | Chain extraction, enrichment, and indexing skills |

### Multimodal RAG

For documents with images, tables, and text:

1. **Extract** — Content Understanding pulls text + images + structure
2. **Describe images** — GenAI Prompt skill creates text descriptions of images
3. **Embed** — Vectorize both text and image descriptions
4. **Index** — Store text vectors + image references in same index
5. **Retrieve** — Return text citations + associated image snippets

### Connecting Pipelines to Agents

| Pattern | How |
|---------|-----|
| **RAG tool** | Agent uses Azure AI Search as a knowledge tool |
| **File Search tool** | Agent searches uploaded files directly |
| **Custom function** | Your code calls search API, returns results to agent |
| **MCP server** | Expose search as MCP tool for any agent |

> **Exam insight**: "Configure semantic search, hybrid search, and vector search for grounding" + "Configure RAG ingestion flow, including OCR" + "Produce clean, grounded representations using Content Understanding" are all tested skills.

---

## 25. Key Links & Reference

- [AI-103 Exam page](https://learn.microsoft.com/credentials/certifications/exams/AI-103) | [Study guide](https://learn.microsoft.com/credentials/certifications/resources/study-guides/ai-103)
- [Microsoft Foundry Agent Service overview](https://learn.microsoft.com/azure/foundry/agents/overview)
- [Learning path: Develop AI agents on Azure](https://learn.microsoft.com/training/paths/develop-ai-agents-on-azure/)
- [Module: Get started with AI agent development](https://learn.microsoft.com/training/modules/ai-agent-fundamentals/)
- [Azure AI services](https://learn.microsoft.com/azure/ai-services/)
- [Azure OpenAI Service](https://learn.microsoft.com/azure/ai-services/openai/)
- [Azure AI Search](https://learn.microsoft.com/azure/search/)
- [Semantic Kernel docs](https://learn.microsoft.com/semantic-kernel/)
- [Microsoft Agent Framework](https://github.com/microsoft/agent-framework)
- [Azure AI Projects SDK (Python)](https://aka.ms/azsdk/azure-ai-projects/python/reference)
- [Foundry samples](https://github.com/microsoft-foundry/foundry-samples)
- [Azure MCP Server](https://learn.microsoft.com/azure/developer/azure-mcp-server/)
- [MCP spec](https://modelcontextprotocol.io/)
- [Foundry portal](https://ai.azure.com)
- [Azure AI Content Safety](https://learn.microsoft.com/azure/ai-services/content-safety/)

---

*Last updated: 2026-08-03 · Content sourced from Microsoft Learn via the Microsoft Learn MCP server.*
