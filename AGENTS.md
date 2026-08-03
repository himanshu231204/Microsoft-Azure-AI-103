# AGENTS.md

## What This Repo Is

Study notes and module tracker for the **Microsoft AI-103 exam** (Developing AI Solutions on Azure). This is a documentation repo, not a software project. There is no code to build, test, or lint.

## Reference Files

| File | Purpose |
|------|---------|
| `Context.md` | **Primary knowledge base.** 800+ lines of deep-dive notes on Azure AI agents, SDKs, MCP, multi-agent, production patterns. Sections 1–25 cover everything from agent fundamentals to CI/CD. |
| `AI-103-Study-Guide.md` | Official exam skills measured (April 2026). 5 sections with weights. Use this to verify what's testable. |
| `README.md` | Course module tracker. 34 modules across 4 learning paths with status tables, links to Microsoft Learn, and practice questions. |

## Content Source

All module notes are derived from the **Microsoft AI-103T00-A course** on Microsoft Learn. When creating or updating module content, use the **Microsoft Learn MCP server** to fetch the latest course material:

- `microsoft_docs_search` — find relevant docs pages for a module topic
- `microsoft_code_sample_search` — pull code examples for Azure SDK patterns
- `microsoft_docs_fetch` — get full page content when search results are truncated

This ensures content stays current with the live course, which Microsoft updates periodically.

## Repo Structure

```
modules/
├── 01-genai/          # LP1: Develop generative AI apps (8 modules)
├── 02-agents/         # LP2: Develop AI agents (9 modules)
├── 03-language/       # LP3: Natural language solutions (9 modules)
└── 04-vision/         # LP4: Extract insights from visual data (8 modules)
```

Each module directory follows the pattern:
```
NN-module-name/
├── README.md              # Notes from Microsoft Learn module
├── practice-questions.md  # 50 practice Qs (when created)
└── .gitkeep               # Placeholder for empty modules
```

## Current Progress

**2 / 34 modules completed** (as of 2026-08-02):
- `modules/01-genai/01-plan-and-prepare/` — has README.md + practice-questions.md
- `modules/01-genai/02-choose-deploy-models/` — has README.md + practice-questions.md

All other module directories exist but are empty (`.gitkeep` only).

## How to Work in This Repo

### Adding module notes
1. Create or edit `modules/{LP}/{NN}-{slug}/README.md`
2. Follow the existing format: heading, source link, TOC, sections with tables and exam insights
3. Add practice questions in `practice-questions.md` (50 Qs per module)
4. Update status in `README.md` main tracker table (change ☐ to ✅)

### Content conventions
- Use `> Exam insight:` callouts for testable material
- Use tables for comparisons (service vs service, tool vs tool)
- Include code snippets from `Context.md` when they clarify Azure SDK patterns
- Reference Microsoft Learn URLs as source for each module

### Updating the tracker
- Edit the learning path tables in `README.md`
- Update the Progress section metrics
- Update `Last Updated` badge date

## .opencode/ Directory

The `.opencode/` directory contains the OpenAgents Control (OAC) agent framework configuration — context files, agent definitions, and workflows for the AI coding assistant. This is infrastructure for tooling, not repo content. Don't modify it unless explicitly asked.
