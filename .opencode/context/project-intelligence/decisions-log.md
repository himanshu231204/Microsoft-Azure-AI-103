<!-- Context: project-intelligence/decisions | Priority: high | Version: 1.0 | Updated: 2026-08-01 -->

# Decisions Log

> Record major decisions with full context so future work stays consistent.

## Quick Reference

- **Purpose**: Document decisions so the owner and agents understand why things are structured this way
- **Format**: Each decision as a separate entry
- **Status**: Decided | Pending | Under Review | Deprecated

---

## Decision: Module folder structure `modules/NN-<slug>/`

**Date**: 2026-08-01
**Status**: Decided
**Owner**: himan

### Context
Starting the "Develop AI agents on Azure" learning path. Needed a consistent place for per-module study notes, with room for modules 2–7.

### Decision
Use `modules/NN-<module-slug>/` folders: a two-digit number matching the learning-path order, plus the official Microsoft Learn module slug (e.g., `modules/01-ai-agent-fundamentals/`). Each module has a `README.md` (objectives, unit checklist, key takeaways) and a `notes/` directory.

### Rationale
Numbered prefixes keep modules ordered naturally; using the official slug keeps a stable 1:1 link to the Microsoft Learn module and avoids renaming if titles change.

### Alternatives Considered
| Alternative | Pros | Cons | Why Rejected? |
|-------------|------|------|---------------|
| Top-level folders per module | Simple | No ordering, no namespace | Numbered `modules/` keeps things tidy |
| Title-based names (e.g., `module-1-agents/`) | Human-readable | Breaks link to official slug, renaming risk | Official slug is stable & linkable |

### Impact
- **Positive**: Consistent, ordered, extensible structure for 7 modules
- **Negative**: Folder names are technical (slugs), not friendly titles
- **Risk**: Low

### Related
- `technical-domain.md` — "Study Notes Patterns"
- `modules/01-ai-agent-fundamentals/README.md` — first example

---

## Decision: Use official Microsoft Learn as the primary study source

**Date**: 2026-08-01
**Status**: Decided
**Owner**: himan

### Context
Study notes need to be accurate and current. AI docs change fast; general knowledge can be stale.

### Decision
Ground all study content in official Microsoft Learn via the Microsoft Learn MCP server (search → code sample search → fetch). Use Context7/ExternalScout for external library docs (e.g., SDKs). Cite source URLs in notes.

### Rationale
First-party, current, and exam-aligned. The AI-103 study guide and learning path are official Microsoft resources, matching what's on the exam.

### Alternatives Considered
| Alternative | Pros | Cons | Why Rejected? |
|-------------|------|------|---------------|
| General web search | Broad coverage | Stale/unofficial info | Official docs are authoritative |
| Training data only | Fast | Outdated (e.g., Next.js-style API drift) | Docs change frequently |

### Impact
- **Positive**: Accurate, citable, current notes
- **Negative**: Requires MCP tool access to fetch
- **Risk**: Low

### Related
- `technical-domain.md` — "Doc-Fetching Workflow"
- `AI-103-Study-Guide.md` — source document

---

## Decision: Keyless authentication as the only Azure auth pattern

**Date**: 2026-08-01
**Status**: Decided
**Owner**: himan

### Context
Azure SDK code samples in this repo should model production best practices, not quick hacks.

### Decision
Use `DefaultAzureCredential` (CLI → managed identity → env) and managed identity for all Azure authentication. Never commit API keys. Config via `.env` + `python-dotenv`.

### Rationale
Matches Microsoft production guidance (`Agents.md` §14: keyless & least privilege) and is exam-relevant (managed identity, keyless credentials are tested skills).

### Alternatives Considered
| Alternative | Pros | Cons | Why Rejected? |
|-------------|------|------|---------------|
| API keys in code | Fast to write | Insecure, anti-pattern, exam-wrong | Never acceptable |
| Hardcoded connection strings | Simple | Secrets leak risk | Use `.env` instead |

### Impact
- **Positive**: Secure, production-ready, exam-aligned
- **Negative**: Slightly more setup for local dev
- **Risk**: Low

### Related
- `technical-domain.md` — "Security Requirements"
- `Agents.md` — §9 Python SDK essentials, §14 security

---

## Deprecated Decisions

| Decision | Date | Replaced By | Why |
|----------|------|-------------|-----|
| — | — | — | None yet |

## Onboarding Checklist

- [x] Understand philosophy behind major choices
- [x] Know why technologies/conventions were chosen
- [x] Understand trade-offs made
- [x] Know where to find decision context
- [ ] Review pending decisions as study progresses

## 📂 Codebase References

- `modules/01-ai-agent-fundamentals/` — created per "module folder structure" decision
- `Agents.md` — §14 security/deploy patterns behind the keyless-auth decision
- `.opencode/env.example` — env var pattern behind keyless config decision

## Related Files

- `technical-domain.md` - Technical implementation affected by these decisions
- `business-tech-bridge.md` - How decisions connect business and technical
- `living-notes.md` - Current open questions that may become decisions
