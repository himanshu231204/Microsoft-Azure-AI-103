<div align="center">

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

# Module 1.4: Get Started with Prompt Flow

</div>

> **Source**: [Microsoft Learn — Get started with prompt flow to develop language model apps in the Azure AI Foundry](https://learn.microsoft.com/training/modules/get-started-prompt-flow-ai-studio/)
> **Learning objectives**: Understand the development lifecycle when creating language model applications, understand what a flow is in prompt flow, explore the core components when working with prompt flow
> **Module units (8)**: Introduction · Understand the development lifecycle of an LLM app · Understand core components and explore flow types · Explore connections and runtimes · Explore variants and monitoring options · Exercise · Module assessment · Summary

---

## Table of Contents

1. [What is Prompt Flow?](#1-what-is-prompt-flow)
2. [LLM App Development Lifecycle](#2-llm-app-development-lifecycle)
3. [Flow Types in Prompt Flow](#3-flow-types-in-prompt-flow)
4. [Core Components of a Flow](#4-core-components-of-a-flow)
5. [Connections and Runtimes](#5-connections-and-runtimes)
6. [Variants and Monitoring](#6-variants-and-monitoring)
7. [Key Takeaways for AI-103](#7-key-takeaways-for-ai-103)

---

## 1. What is Prompt Flow?

Prompt flow is a development tool designed to streamline the entire development cycle of AI applications powered by Large Language Models (LLMs). It provides a comprehensive solution for prototyping, experimenting, iterating, and deploying AI applications.

### Key Capabilities

| Capability | Description |
|------------|-------------|
| **Orchestrate flows** | Link LLMs, prompts, and Python tools through a visualized graph |
| **Test & debug** | Easily test, debug, and iterate on flows |
| **Create variants** | Create prompt variants and compare their performance |
| **Deploy** | Deploy flows as real-time endpoints for production use |

> **Exam insight**: Prompt flow provides an interactive, visual authoring experience with a DAG (Directed Acyclic Graph) representation of your workflow, making it easier to understand complex LLM applications.

### Prompt Engineering Benefits

| Benefit | Description |
|---------|-------------|
| **Interactive authoring** | Visual representation of flow structure with notebook-like coding |
| **Variants for tuning** | Create and compare multiple prompt variants for iterative refinement |
| **Evaluation** | Built-in evaluation flows to assess prompt quality and effectiveness |
| **Comprehensive resources** | Library of built-in tools, samples, and templates |

---

## 2. LLM App Development Lifecycle

When developing LLM-based applications, you follow a systematic lifecycle:

### Development Lifecycle Stages

```
┌─────────────────────────────────────────────────────────────────┐
│                    LLM App Development Lifecycle                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐  │
│  │  Design  │───▶│  Build   │───▶│  Test    │───▶│  Deploy  │  │
│  └──────────┘    └──────────┘    └──────────┘    └──────────┘  │
│       │              │               │               │          │
│       ▼              ▼               ▼               ▼          │
│  Define flow    Author prompts   Run evaluations   Production  │
│  structure      & Python code    & variants        endpoint    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

| Stage | Activities | Prompt Flow Tools |
|-------|------------|-------------------|
| **Design** | Define inputs, outputs, flow structure | Flow editor, DAG visualization |
| **Build** | Create prompts, Python tools, LLM nodes | Node editor, code editor |
| **Test** | Run flows inline, debug issues | Inline execution, logs |
| **Evaluate** | Test variants, measure quality | Evaluation flows, metrics |
| **Deploy** | Create real-time endpoints | Deployment configuration |

> **Exam insight**: The development lifecycle emphasizes iterative refinement — you don't just build once; you continuously test, evaluate variants, and improve prompts.

---

## 3. Flow Types in Prompt Flow

Prompt flow offers three distinct flow types for different scenarios:

### Flow Type Comparison

| Flow Type | Purpose | Use Case |
|-----------|---------|----------|
| **Standard flow** | General application development | Text classification, summarization, extraction |
| **Chat flow** | Conversational applications | Chatbots, Q&A systems, dialog agents |
| **Evaluation flow** | Assessing previous run outputs | Quality metrics, performance evaluation |

### Standard Flow

- Designed for general LLM application development
- Uses built-in tools (LLM, Python, Prompt, Serp API, Content Safety)
- Flexible and versatile across different domains

### Chat Flow

- Tailored for conversational applications
- Provides enhanced support for chat inputs/outputs
- Manages chat history automatically

| Component | Required | Description |
|-----------|----------|-------------|
| **Chat input** | ✅ | Messages/queries from users |
| **Chat history** | ✅ | Record of all interactions (auto-managed) |
| **Chat output** | ✅ | AI-generated responses |

> **Exam insight**: Chat flow automatically manages `chat_history` as a list of inputs/outputs — you cannot manually set this value.

### Evaluation Flow

- Takes outputs from previous flow runs as inputs
- Evaluates performance and outputs relevant metrics
- Used for assessing model/application quality

### Creating a Flow

You can create a flow in three ways:

| Method | Description |
|--------|-------------|
| **Clone from gallery** | Start from built-in samples/templates available in the gallery |
| **Create from scratch** | Start a new flow from a Standard/Chat/Evaluation flow type |
| **Import files** | Import existing flow files from local storage or a file share |

Each flow folder contains a `flow.dag.yaml` file (the flow definition), source code files, and system folders.

> **Exam insight**: Flows are defined in **`flow.dag.yaml`**. Create from the gallery, from scratch, or by importing existing flow files.

---

## 4. Core Components of a Flow

### Flow Structure

A flow consists of:

| Component | Description |
|-----------|-------------|
| **Nodes** | Individual tools with specific capabilities (LLM, Python, Prompt) |
| **Edges** | Connections between nodes showing data flow |
| **Inputs** | Data passed into the flow (defined schema with name and type) |
| **Outputs** | Data produced by the flow (references node outputs) |

### DAG Visualization

The flow is visualized as a **Directed Acyclic Graph (DAG)**:
- Shows connectivity and dependencies between nodes
- Provides clear overview of workflow structure
- Can zoom in/out and use auto layout

### Flow Inputs and Outputs

```yaml
# Example flow definition
inputs:
  question:
    type: string
outputs:
  answer:
    type: string
    reference: ${llm_node.output}
```

| Reference Type | Syntax | Example |
|----------------|--------|---------|
| Flow input | `${input.<name>}` | `${input.question}` |
| Node output | `${<node>.output}` | `${llm_node.output}` |
| Node output field | `${<node>.output.<field>}` | `${llm_node.output.text}` |

### Built-in Tools

| Tool | Purpose |
|------|---------|
| **LLM** | Call language models with prompts |
| **Python** | Execute custom Python code |
| **Prompt** | Create reusable prompt templates |
| **Serp API** | Web search integration |
| **Content Safety** | Content filtering and safety checks |

> **Exam insight**: LLM and Prompt tools use **Jinja templating** (`{{variable}}`) to dynamically generate prompts based on inputs.

> **Exam insight**: The **LLM tool does not support reasoning models** (e.g., OpenAI o-series). For reasoning model integration, use the **Python tool** to call the model APIs directly.

---

## 5. Connections and Runtimes

### Connections

Connections are resources that link your flow to external services:

| Connection Type | Service |
|-----------------|---------|
| **Azure OpenAI** | GPT models, DALL-E |
| **OpenAI** | OpenAI API directly |
| **Azure AI Search** | Vector search, indexing |
| **Custom** | Any endpoint with API keys |

### Connection Authentication

For Azure OpenAI connections, prompt flow supports two authentication modes:

| Auth mode | When to use |
|-----------|-------------|
| **API Key** | Development, quick setup |
| **Microsoft Entra ID** | Production, managed identity / role-based access |

### Creating Connections

```python
# Connections can be created via:
# 1. Portal UI (Prompt flow → Connections → Create)
# 2. REST API
# 3. Python SDK
```

> **Exam insight**: Connections are defined at the workspace level and can be shared across multiple flows within the same project. Azure OpenAI connections support **API Key** or **Microsoft Entra ID** authentication.

### Compute Sessions (Runtimes)

A compute session provides the computing resources required to run flows:

| Feature | Description |
|---------|-------------|
| **Docker image** | Contains all necessary dependency packages |
| **Auto-management** | Lifecycle managed by the system |
| **Package customization** | Add packages via `requirements.txt` |
| **Serverless compute** | System manages VM selection based on quota/cost/performance |

### Compute Session vs Compute Instance

| Compute Session | Compute Instance |
|-----------------|------------------|
| ✅ Automatically managed lifecycle | ❌ Manual management required |
| ✅ Serverless (auto-select VM) | ❌ Fixed VM size |
| ✅ Customize via `requirements.txt` | ✅ Custom environments |

### Requirements.txt Configuration

```txt
# Don't pin promptflow versions - they're in base image
requests
numpy
pandas
```

> **Exam insight**: The idle shutdown is one hour when using CLI/SDK to submit flow runs.

---

## 6. Variants and Monitoring

### What are Variants?

A variant is a specific version of a tool node with distinct settings. Currently supported only for **LLM tools**.

| Variant | Prompt | Temperature |
|---------|--------|-------------|
| Variant 0 | `Summary: {{input}}` | 1.0 |
| Variant 1 | `Summary: {{input}}` | 0.7 |
| Variant 2 | `What is the main point? {{input}}` | 1.0 |
| Variant 3 | `What is the main point? {{input}}` | 0.7 |

### Benefits of Variants

| Benefit | Description |
|---------|-------------|
| **Enhance quality** | Identify optimal prompt/configuration combinations |
| **Save time** | Track and compare performance of each prompt version |
| **Boost productivity** | Streamline optimization process |
| **Easy comparison** | Compare results side by side for data-driven decisions |

### Monitoring Options

| Monitoring Feature | Purpose |
|--------------------|---------|
| **Flow runs** | Track execution history and results |
| **Metrics** | Collect performance data per variant |
| **Logs** | Debug and trace issues |
| **Variant comparison** | Compare outputs across different variants |

### GenAIOps Integration

Prompt flow supports GenAIOps practices:

| Feature | Description |
|---------|-------------|
| **Centralized code** | Single repository for all flows |
| **Lifecycle management** | Local experimentation → production deployment |
| **Variant & hyperparameter experimentation** | Test combinations of variants across multiple nodes |
| **Multiple deployment targets** | Docker images deployable to App Service, Kubernetes, Azure managed compute |
| **A/B deployment** | Compare different flow versions in production |
| **Many-to-many dataset-to-flow relationships** | Multiple datasets per standard and evaluation flow |
| **Conditional data & model registration** | Register new dataset/model versions only when data changes |
| **Comprehensive reporting** | Detailed metrics for variant configurations |

### Enterprise Readiness

| Benefit | Description |
|---------|-------------|
| **Collaboration** | Multiple users work together, share knowledge, maintain version control |
| **All-in-one platform** | Development → evaluation → deployment → monitoring in one place |
| **Enterprise readiness solutions** | Secure, scalable, reliable foundation for flows |

> **Exam insight**: Variants enable systematic prompt engineering by allowing you to test multiple configurations and compare results before deploying to production.

---

## 7. Key Takeaways for AI-103

### Must-Know Facts

1. **Prompt flow** = development tool for LLM-based AI applications
2. **Three flow types**: Standard, Chat, Evaluation
3. **DAG visualization** = Directed Acyclic Graph showing workflow structure
4. **Nodes** = individual tools (LLM, Python, Prompt, etc.)
5. **Connections** = links to external services (Azure OpenAI, AI Search, etc.); Azure OpenAI supports API Key or Microsoft Entra ID auth
6. **Compute sessions** = managed runtime for executing flows
7. **Variants** = different versions of LLM nodes for comparison
8. **Jinja templating** = `{{variable}}` syntax for dynamic prompts
9. **LLM tool does NOT support reasoning models** — use the Python tool to call reasoning model APIs
10. **Retirement**: Prompt flow retires **April 20, 2027** — migrate to Microsoft Agent Framework

### Flow Type Decision Matrix

| Scenario | Recommended Flow Type |
|----------|----------------------|
| Text classification | Standard flow |
| Summarization | Standard flow |
| Chatbot | Chat flow |
| Q&A system | Chat flow |
| Quality evaluation | Evaluation flow |
| Model comparison | Evaluation flow |

### Code Patterns to Remember

| Task | Pattern |
|------|---------|
| Reference flow input | `${input.question}` |
| Reference node output | `${llm_node.output}` |
| Jinja template | `{{variable_name}}` |
| Flow definition | `flow.dag.yaml` |
| Dependencies | `requirements.txt` |

### Connections to Other Modules

| This module | Connects to |
|-------------|-------------|
| Prompt flow basics | Module 1.1 (Foundry platform overview) |
| Flow creation | Module 1.2 (Model deployment) |
| LLM node configuration | Module 1.3 (Foundry SDK) |
| Evaluation flows | Module 1.8 (Evaluate gen AI performance) |
| Deployment | Module 1.5 (RAG solutions) |

---

> ⚠️ **Important Note**: Prompt flow in Microsoft Foundry and Azure Machine Learning will be **retired on April 20, 2027**. It is no longer recommended for new development. Prompt flow container images (including `promptflow-runtime`, `promptflow-runtime-stable`, and `promptflow-python`) are no longer receiving security or package updates. After retirement, the web authoring experience, VS Code extensions, and related container images will no longer be supported. Migrate existing Prompt flow applications and deployments to **Microsoft Agent Framework** before the retirement date.

---

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

*Notes created: 2026-08-03 · Updated: 2026-08-04 · Source: Microsoft Learn module via MCP*