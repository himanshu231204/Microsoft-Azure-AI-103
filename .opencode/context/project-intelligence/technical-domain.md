<!-- Context: project-intelligence/technical | Priority: critical | Version: 1.1 | Updated: 2026-08-03 -->

# Technical Domain

> Tech stack, structure, and patterns for this AI-103T00-A study workspace (exam prep + hands-on Azure practice).

## Quick Reference

- **Purpose**: Understand how this repo is structured and how agents should work in it
- **Update When**: Tech stack changes, new module folders, new patterns
- **Audience**: Developers, AI agents, study-note maintainers

## Primary Stack

| Layer | Technology | Rationale |
|-------|-----------|-----------|
| Course | AI-103T00-A: Develop AI apps and agents on Azure (4-day instructor-led) | Maps to Exam AI-103 |
| Purpose | AI-103 exam prep: study notes + hands-on Azure practice | Agentic AI is the largest weighted section (30–35%) |
| Cloud | Azure AI Foundry (Agent Service, projects) | Managed agents, model deployments, tools |
| AI services | Azure OpenAI, AI Search, AI Speech, Document Intelligence, Content Understanding, Content Safety | Map to exam skill areas |
| SDKs (Python) | `azure-ai-projects`, `azure-identity`, `agent-framework`, `semantic-kernel`, `python-dotenv` | Agent development + keyless auth |
| Docs sources | Microsoft Learn (MCP server), Parallel Search, Context7 | Grounded, current documentation |

## Repo Structure

```
modules/
├── 01-genai/          # LP1: Develop generative AI apps (8 modules)
├── 02-agents/         # LP2: Develop AI agents (9 modules)
├── 03-language/       # LP3: Develop natural language solutions (9 modules)
└── 04-vision/         # LP4: Extract insights from visual data (8 modules)
README.md              # Course overview with module list and progress tracker
AI-103-Study-Guide.md  # Full exam skills (from Microsoft Learn)
AGENTS.md              # Agent instruction file
Context.md             # Primary knowledge base (Azure AI agents deep dive)
.opencode/context/     # Agent knowledge base
```

**Module structure:**
```
modules/01-genai/01-plan-and-prepare/
├── README.md              # Module overview, learning objectives
├── practice-questions.md  # 50 practice Qs
├── notes/                 # Unit-by-unit detailed notes
│   ├── unit-1.md
│   ├── unit-2.md
│   └── ...
└── .gitkeep
```

## Course Structure (AI-103T00-A)

| Learning Path | Modules | Focus |
|---------------|---------|-------|
| 01-genai | 8 modules | Generative AI apps (Foundry SDK, RAG, fine-tuning, prompt flow) |
| 02-agents | 9 modules | AI agents (Foundry Agent Service, custom tools, MCP, multi-agent, A2A) |
| 03-language | 9 modules | Natural language (text analysis, speech, translation, CLU) |
| 04-vision | 8 modules | Computer vision (image analysis, OCR, faces, video, image generation) |

## Study Notes Patterns

- **Module folders**: `modules/NN-<learning-path-slug>/` — numbered learning path with sub-modules (e.g., `modules/01-genai/01-plan-and-prepare/`)
- **Each module structure**:
  ```
  NN-module-name/
  ├── README.md              # Module overview, learning objectives, prerequisites
  ├── practice-questions.md  # 50 practice Qs per module
  ├── notes/                 # Unit-by-unit detailed notes
  │   ├── unit-1.md
  │   ├── unit-2.md
  │   └── ...
  └── .gitkeep
  ```
- **README format**: learning objectives → prerequisites → unit checklist table → key takeaways → notes → related resources
- **Notes format**: one file per unit (`notes/unit-N.md`), concise scannable content
- **Tracking**: checkbox lists (☐) for objectives and units, updated as modules are completed

## Doc-Fetching Workflow

- Fetch Microsoft content via **Microsoft Learn MCP** (search → code sample search → fetch for depth)
- Fetch external libraries via **Context7 / ExternalScout** (mandatory for external packages — training data can be outdated)
- Always cite source URLs (e.g., `learn.microsoft.com/...`) in study notes
- For deep-dive notes, follow the structure used in `Agents.md` (concepts → tables → exam insights → hands-on)

## Code Patterns (Azure SDK)

```python
from azure.identity import DefaultAzureCredential
credential = DefaultAzureCredential()  # CLI -> managed identity -> env

from azure.ai.projects import AIProjectClient
project = AIProjectClient.from_connection_string(conn_str, credential=credential)
```

- Client + credential pattern: `AIProjectClient` / `FoundryChatClient` + `DefaultAzureCredential`
- Never hardcode keys; use `.env` + `python-dotenv` (see `.opencode/env.example`)

## Naming Conventions

| Type | Convention | Example |
|------|-----------|---------|
| Learning path dirs | `NN-<slug>` | `01-genai`, `02-agents` |
| Module dirs | `NN-<slug>` | `01-plan-and-prepare` |
| Notes files | kebab-case | `unit-2-notes.md` |
| Markdown docs | PascalCase/Caps | `AI-103-Study-Guide.md` |
| Code files | snake_case (Python) | `agent_client.py` |

## Code Standards

- Python SDK client + `DefaultAzureCredential` pattern for all Azure code
- Keyless auth — no API keys in code or docs
- Config via `.env` + `python-dotenv`; env vars documented in `.opencode/env.example`
- Notes follow MVI style: concise, scannable, tables over prose, code examples where helpful

## Security Requirements

- Managed identity / `DefaultAzureCredential` — never keys in code
- Least privilege RBAC (Foundry User/Owner, Project Manager roles)
- Treat conversation history and study content as potentially sensitive data
- Use private networking / scoped APIs for production agent deployments (from `Agents.md` §14)

## 📂 Codebase References

- `Agents.md` — §9 Python SDK essentials, §14 production security & deployment
- `AI-103-Study-Guide.md` — full exam skills measured
- `modules/01-genai/01-plan-and-prepare/README.md` — module template example
- `.opencode/env.example` — environment variable pattern

## Related Files

- `business-domain.md` — why this repo exists (study goal)
- `decisions-log.md` — decision history
- `living-notes.md` — open questions, active study items
