<!-- Context: project-intelligence/nav | Priority: high | Version: 1.2 | Updated: 2026-08-01 -->

# Project Intelligence

> Start here for quick project understanding. These files bridge business and technical domains.

## Structure

```
.opencode/context/project-intelligence/
├── navigation.md              # This file - quick overview
├── business-domain.md         # Business context and study goal (filled 2026-08-01)
├── technical-domain.md        # Stack, architecture, study patterns (filled, critical)
├── business-tech-bridge.md    # How business needs map to solutions (template - unfilled)
├── decisions-log.md           # Major decisions with rationale (filled 2026-08-01)
└── living-notes.md            # Active study items, open questions (filled 2026-08-01)
```

## Quick Routes

| What You Need | File | Description | Priority |
|---------------|------|-------------|----------|
| Understand the "why" | `business-domain.md` | Problem, users, value proposition | high |
| Understand the "how" | `technical-domain.md` | Stack, architecture, study patterns (AI-103) | critical |
| See the connection | `business-tech-bridge.md` | Business → technical mapping | high |
| Know the context | `decisions-log.md` | Why decisions were made | high |
| Current state | `living-notes.md` | Active issues and open questions | high |
| All of the above | Read all files in order | Full project intelligence | — |

**Repo quick routes**:
| What You Need | File | Description |
|---------------|------|-------------|
| Exam skills measured | `AI-103-Study-Guide.md` (repo root) | Official skills + study resources |
| Agent deep-dive | `Agents.md` (repo root) | Agentic AI concepts, SDKs, production |
| Current module | `modules/01-ai-agent-fundamentals/` | Module 1 study notes (in progress) |

## Usage

**New Team Member / Agent**:
1. Start with `navigation.md` (this file)
2. Read all files in order for complete understanding
3. Follow onboarding checklist in each file

**Quick Reference**:
- Business focus → `business-domain.md`
- Technical focus → `technical-domain.md`
- Decision context → `decisions-log.md`

## Integration

This folder is referenced from:
- `.opencode/context/core/standards/project-intelligence.md` (standards and patterns)
- `.opencode/context/core/system/context-guide.md` (context loading)

See `.opencode/context/core/context-system.md` for the broader context architecture.

## Maintenance

Keep this folder current:
- Update when business direction changes
- Document decisions as they're made
- Review `living-notes.md` regularly
- Archive resolved items from decisions-log.md

**Management Guide**: See `.opencode/context/core/standards/project-intelligence-management.md` for complete lifecycle management including:
- How to update, add, and remove files
- How to create new subfolders
- Version tracking and frontmatter standards
- Quality checklists and anti-patterns
- Governance and ownership

See `.opencode/context/core/standards/project-intelligence.md` for the standard itself.
