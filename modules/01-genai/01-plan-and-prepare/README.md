# Module 1.1: Plan and Prepare to Develop AI Solutions on Azure

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

> **Source**: [Microsoft Learn — Plan and prepare to develop AI solutions on Azure](https://learn.microsoft.com/training/modules/prepare-azure-ai-development/)
> **Learning objectives**: Identify AI capabilities, describe Azure AI Services & Foundry, pick developer tools/SDKs, understand responsible AI

---

## Table of Contents

1. [What is AI? — Core Capabilities](#1-what-is-ai--core-capabilities)
2. [Foundry Tools — Prebuilt AI Services](#2-foundry-tools--prebuilt-ai-services)
3. [Microsoft Foundry — The Platform](#3-microsoft-foundry--the-platform)
4. [Developer Tools and SDKs](#4-developer-tools-and-sdks)
5. [Responsible AI Principles](#5-responsible-ai-principles)
6. [Key Takeaways for AI-103](#6-key-takeaways-for-ai-103)

---

## 1. What is AI? — Core Capabilities

AI = software capabilities that enable applications to exhibit **human-like behavior** using machine learning models trained on massive datasets.

### The 5 AI Capabilities You Must Know

| Capability | What it does | Azure service(s) |
|------------|--------------|-------------------|
| **Generative AI & Agents** | LLMs generate original responses from natural language prompts. Agents combine LLMs + instructions + tools for autonomous task execution | Azure OpenAI, Foundry Agent Service |
| **Natural Language Processing (NLP)** | Statistical/semantic models for text understanding — entity extraction, sentiment, classification, summarization | Azure Language |
| **Computer Speech** | Speech-to-text (STT), text-to-speech (TTS), real-time conversation, transcription, multi-language support | Azure Speech |
| **Computer Vision** | Interpret images, video, camera streams. Multimodal models can also *generate* visual output | Azure Vision, Content Understanding |
| **Information Extraction** | Combine language, vision, and speech to extract structured data from documents, forms, images, recordings | Document Intelligence, Content Understanding |

> **Exam insight**: Know which capability maps to which service — this is tested directly.

### Generative AI vs Traditional AI

| Traditional AI | Generative AI |
|----------------|---------------|
| Classifies, predicts, extracts | *Generates* original content |
| Fixed output (label, number) | Open-ended output (text, code, images) |
| Task-specific models | Foundation models (LLMs) |
| Requires labeled training data | Prompt-based, few-shot learning |

### What Makes an Agent (not just an LLM call)

Agents are the next evolution — they combine:
1. **LLM** — the reasoning engine
2. **Instructions** — define scope, role, behavioral rules
3. **Tools** — APIs, code, databases, search, MCP connections

---

## 2. Foundry Tools — Prebuilt AI Services

**Foundry Tools** = out-of-the-box, prebuilt APIs and models you can integrate without building custom AI. More cost-effective and predictable than generative AI alone.

| Tool | Purpose | Key Features |
|------|---------|--------------|
| **Azure Language** | Analyze text | Entity extraction, sentiment analysis, summarization, conversational models, Q&A |
| **Azure Speech** | Voice I/O | Text-to-speech, speech-to-text, real-time live speech, conversational apps |
| **Azure Translator** | Language translation | State-of-the-art models, large number of languages |
| **Azure Document Intelligence** | Document extraction | Pre-built and custom models for invoices, receipts, forms |
| **Azure Content Understanding** | Multimodal analysis | Extract data from forms, images, video, audio streams |

### How to use Foundry Tools

```
Client App → Foundry Resource Endpoint → Tool-specific API/SDK
         ↳ Auth: project key or token-based (Entra ID)
```

- Some tools have UI for configuration/testing in the Foundry portal
- Previously called "Azure AI Services" and "Azure Cognitive Services" (still reflected in some APIs/SDKs)

> **Exam insight**: Match tool to scenario — "extract data from receipts" → Document Intelligence; "analyze sentiment" → Language; "transcribe speech" → Speech.

---

## 3. Microsoft Foundry — The Platform

Microsoft Foundry is the **recommended platform** for AI development on Azure (for all but the simplest solutions).

### Core Concepts

```
Foundry Resource (Azure resource)
  └── Project(s)  ← one resource supports multiple projects
       ├── Models      (LLM deployments from model catalog)
       ├── Agents      (LLM + instructions + tools)
       ├── Tools       (built-in + MCP connections)
       └── Knowledge   (data stores, Foundry IQ)
```

| Component | Description |
|-----------|-------------|
| **Foundry Resource** | Azure resource providing compute, storage, AI tools, services |
| **Project** | Organizational unit — manages models, agents, tools, knowledge, connections |
| **Models** | LLM deployments from Foundry Models catalog (Microsoft, OpenAI, third-party). Access via project endpoint or Azure OpenAI endpoint |
| **Agents** | Named AI configurations: LLM + instructions + tools. Developed/consumed via Foundry Agent Service |
| **Tools** | Built-in (web search, code interpreter) + custom/third-party via MCP |
| **Knowledge** | Data stores for agent context. Foundry IQ = central MCP-based knowledge connection |

### Foundry Portal

Web-based visual interface for:
- Find, compare, deploy, test models
- Create and test agents
- Create MCP connections to tools/knowledge
- Explore and test Foundry Tools
- Manage resource config and user access
- Find endpoints and keys for client apps

### Foundry SDK

Programmatic access for automation and CI/CD — create and manage assets via scripts or DevOps pipelines.

> **Exam insight**: Know the difference between Foundry Resource vs Project vs Model deployment. Projects are where you work; resources provide the infrastructure.

---

## 4. Developer Tools and SDKs

### IDEs and Editors

| Tool | Best for |
|------|----------|
| **Visual Studio** | .NET/C# developers, Windows-focused |
| **Visual Studio Code** | Cross-platform, open-source, web dev, Python |
| **GitHub Copilot** | AI-assisted coding in VS/VS Code |

### Foundry Toolkit for VS Code

Extension that simplifies Foundry development:
- Browse/manage project resources (models, agents, connections, vector stores)
- Deploy models from catalog
- Test models/agents in integrated playgrounds
- Configure declarative/hosted agents (visual designer + YAML)
- Generate integration code

### Key APIs and SDKs

| SDK/API | Purpose |
|---------|---------|
| **Microsoft Foundry SDK** | Connect to Foundry projects, access agents, Foundry IQ knowledge stores |
| **OpenAI API** | Use OpenAI SDKs with Foundry models (OpenAI-compatible syntax) |
| **Foundry Tools SDKs** | Service-specific libraries for Language, Speech, Vision, etc. Also available via REST APIs |

### Supported Languages

Python, C#, Node.js, TypeScript, Java, and others.

> **Exam insight**: For the exam, know the SDK names: `azure-ai-projects` (Foundry SDK), `azure-identity`, and that OpenAI SDKs work with Foundry models.

---

## 5. Responsible AI Principles

AI systems are probabilistic and human-like — users trust them heavily. Potential for harm through incorrect predictions or misuse is a major concern.

### Microsoft's 6 Responsible AI Principles

| Principle | Meaning | Example concern |
|-----------|---------|-----------------|
| **Fairness** | Treat all people fairly, no bias | Loan approval model must not discriminate by gender/ethnicity |
| **Reliability & Safety** | Perform reliably under all conditions | Autonomous vehicle or medical diagnosis system failure = risk to life |
| **Privacy & Security** | Protect data and respect privacy | Training data may contain personal details; predictions use new private data |
| **Inclusiveness** | Empower everyone, engage all people | AI should benefit all parts of society regardless of ability, gender, etc. |
| **Transparency** | Be understandable, explain limitations | Users should know training data size, prediction confidence, data usage |
| **Accountability** | People are responsible for AI systems | Developers must validate models, ensure legal/responsible standards |

### Responsible AI in Practice

- **Training data**: Review for representativeness, bias, quality
- **Model evaluation**: Test for fairness across subgroups, not just overall accuracy
- **Confidence thresholds**: Apply appropriate thresholds for predictions
- **User disclosure**: Inform users about AI limitations, data usage, and confidence scores
- **Governance framework**: Organizational principles ensuring legal and responsible standards

> **Exam insight**: "Implement responsible AI across generative AI and agentic systems" is a tested skill. Be ready to pick the right principle or guardrail for a scenario.

### Azure Tools for Responsible AI

- **Azure AI Content Safety** — detect/manage harmful content (text + images)
- **Content filters** — block violence, hate, sexual content, self-harm
- **Risk detection** — prompt injection, jailbreak detection
- **Tool-access controls** — approve/deny specific tools, scoped API endpoints
- **Auditing** — trace logging, provenance metadata, approval workflows

---

## 6. Key Takeaways for AI-103

### Must-Know Facts

1. **AI capabilities** map to specific Azure services — know the mapping
2. **Foundry Tools** = prebuilt APIs (Language, Speech, Translator, Document Intelligence, Content Understanding)
3. **Microsoft Foundry** = platform with Projects, Models, Agents, Tools, Knowledge
4. **Foundry SDK** = programmatic access; **Foundry Portal** = visual interface
5. **Responsible AI** = 6 principles: Fairness, Reliability/Safety, Privacy/Security, Inclusiveness, Transparency, Accountability
6. **OpenAI SDKs** work with Foundry models via OpenAI-compatible endpoint

### Connections to Other Modules

| This module | Connects to |
|-------------|-------------|
| AI capabilities overview | Modules 1.2–1.8 (model selection, RAG, fine-tuning, evaluation) |
| Foundry Tools | Modules 3.x (Language, Speech), 4.x (Vision, Document Intelligence) |
| Microsoft Foundry | Module 2.x (Agents on Foundry) |
| Responsible AI | Module 1.7 (Responsible generative AI deep dive) |

---

[![Module Badge](https://img.shields.io/badge/Microsoft_Learn-Module_Badge-0078D4?style=for-the-badge&logo=microsoftlearn&logoColor=white)](https://learn.microsoft.com/en-us/users/himanshukumar-1965/achievements/eghlmzmp)

*Notes created: 2026-08-02 · Source: Microsoft Learn module via MCP*
