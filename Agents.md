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
19. [Key Links & Reference](#19-key-links--reference)

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

## 19. Key Links & Reference

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

*Last updated: 2026-08-01 · Content sourced from Microsoft Learn via the Microsoft Learn MCP server.*
