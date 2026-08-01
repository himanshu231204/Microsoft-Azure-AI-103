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
**Status**: Decided (updated)
**Owner**: himan

### Context
Starting Course AI-103T00-A (4-day instructor-led). Needed a consistent place for per-module study notes, with room for all 12 course modules.

### Decision
Use `modules/NN-<module-slug>/` folders: a two-digit number matching the course day/module order, plus a descriptive slug (e.g., `modules/01-plan-and-prepare/`). Each module has a `README.md` (objectives, unit checklist, key takeaways) and a `notes/` directory.

### Rationale
Numbered prefixes keep modules ordered naturally; using descriptive slugs keeps a stable link to the official course module and avoids renaming if titles change.

### Alternatives Considered
| Alternative | Pros | Cons | Why Rejected? |
|-------------|------|------|---------------|
| Top-level folders per module | Simple | No ordering, no namespace | Numbered `modules/` keeps things tidy |
| Title-based names (e.g., `module-1-agents/`) | Human-readable | Breaks link to official slug, renaming risk | Official slug is stable & linkable |

### Impact
- **Positive**: Consistent, ordered, extensible structure for 12 modules
- **Negative**: Folder names are technical (slugs), not friendly titles
- **Risk**: Low

### Related
- `technical-domain.md` — "Study Notes Patterns"
- `modules/01-plan-and-prepare/README.md` — first example

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

## Decision: Restructure repo for AI-103T00-A course (12 modules)

**Date**: 2026-08-01
**Status**: Decided
**Owner**: himan

### Context
Discovered user is taking Course AI-103T00-A (4-day instructor-led), not the self-paced "Develop AI agents on Azure" learning path (7 modules). The previous module structure was based on the wrong learning path and has been deleted.

### Decision
Restructure the repo with 12 module folders mapping to the 4-day course:
- Day 1 (Modules 01–03): Plan & Manage Azure AI Solutions (Exam §1: 25–30%)
- Day 2 (Modules 04–06): Generative AI Apps (Exam §2: 30–35%)
- Day 3 (Modules 07–09): AI Agents (Exam §2 continued)
- Day 4 (Modules 10–12): Vision, Text & Information Extraction (Exam §3–5: 35% total)

### Rationale
Aligns repo with the actual course the user is attending. The 12-module structure is based on exam sections + corresponding learning paths. Module list is a best-guess; will be confirmed/corrected when user shares the actual course outline from their training portal.

### Alternatives Considered
| Alternative | Pros | Cons | Why Rejected? |
|-------------|------|------|---------------|
| Wait for exact module list | Perfect accuracy | Blocks all module folder creation | Can proceed with exam-aligned structure now |
| Keep self-paced learning path | Already created | Wrong course — user is in instructor-led | Mismatch with actual course |

### Impact
- **Positive**: Repo matches actual course, notes will be directly useful during class
- **Negative**: Module list may need minor renaming if actual course differs
- **Risk**: Low — structure is exam-aligned regardless of exact module names

### Related
- `README.md` — course overview with module table
- `technical-domain.md` — course structure section
- `business-domain.md` — project identity and success metrics

---

## Deprecated Decisions

| Decision | Date | Replaced By | Why |
|----------|------|-------------|-----|
| Module structure based on self-paced learning path (7 modules) | 2026-08-01 | Course-based structure (12 modules) | User is taking AI-103T00-A (4-day instructor-led), not self-paced learning path |

## Onboarding Checklist

- [x] Understand philosophy behind major choices
- [x] Know why technologies/conventions were chosen
- [x] Understand trade-offs made
- [x] Know where to find decision context
- [ ] Review pending decisions as study progresses

## 📂 Codebase References

- `modules/01-plan-and-prepare/` — created per "module folder structure" decision
- `Agents.md` — §14 security/deploy patterns behind the keyless-auth decision
- `.opencode/env.example` — env var pattern behind keyless config decision

## Related Files

- `technical-domain.md` - Technical implementation affected by these decisions
- `business-tech-bridge.md` - How decisions connect business and technical
- `living-notes.md` - Current open questions that may become decisions
