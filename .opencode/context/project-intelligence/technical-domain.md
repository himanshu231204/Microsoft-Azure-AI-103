<!-- Context: project-intelligence/technical | Priority: critical | Version: 1.0 | Updated: 2026-08-01 -->

# Technical Domain

> Tech stack, structure, and patterns for this AI-103 study workspace (exam prep + hands-on Azure practice).

## Quick Reference

- **Purpose**: Understand how this repo is structured and how agents should work in it
- **Update When**: Tech stack changes, new module folders, new patterns
- **Audience**: Developers, AI agents, study-note maintainers

## Primary Stack

| Layer | Technology | Rationale |
|-------|-----------|-----------|
| Purpose | AI-103 exam prep: study notes + hands-on Azure practice | Agentic AI is the largest weighted section (30–35%) |
| Cloud | Azure AI Foundry (Agent Service, projects) | Managed agents, model deployments, tools |
| AI services | Azure OpenAI, AI Search, AI Speech, Document Intelligence, Content Understanding, Content Safety | Map to exam skill areas |
| SDKs (Python) | `azure-ai-projects`, `azure-identity`, `agent-framework`, `semantic-kernel`, `python-dotenv` | Agent development + keyless auth |
| Docs sources | Microsoft Learn (MCP server), Parallel Search, Context7 | Grounded, current documentation |

## Repo Structure

```
modules/NN-<slug>/       # Per-module folders (01-ai-agent-fundamentals, ...)
AI-103-Study-Guide.md    # Full exam skills (from Microsoft Learn)
Agents.md                # Agentic deep-dive notes
.opencode/context/       # Agent knowledge base
```

## Study Notes Patterns

- **Module folders**: `modules/NN-<module-slug>/` — numbered + official Microsoft Learn slug (e.g., `01-ai-agent-fundamentals`)
- **Each module**: `README.md` (learning objectives, prerequisites, unit checklist, key takeaways) + `notes/` for unit-by-unit notes
- **README format**: learning objectives → prerequisites → unit checklist table → key takeaways → notes → related resources
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
| Module dirs | `NN-<slug>` | `01-ai-agent-fundamentals` |
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
- `modules/01-ai-agent-fundamentals/README.md` — module template example
- `.opencode/env.example` — environment variable pattern

## Related Files

- `business-domain.md` — why this repo exists (study goal)
- `decisions-log.md` — decision history
- `living-notes.md` — open questions, active study items
