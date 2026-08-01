<!-- Context: project-intelligence/business | Priority: high | Version: 1.0 | Updated: 2026-08-01 -->

# Business Domain

> Why this repo exists: pass the AI-103 exam and build real, production-grade AI agent skills on Azure.

## Quick Reference

- **Purpose**: Understand the study goal and what "success" means here
- **Update When**: Study focus shifts, exam date changes, goals evolve
- **Audience**: Developers, AI agents, the owner (self-study)

## Project Identity

```
Project Name: Microsoft-Azure-AI-103 study workspace
Tagline: Exam prep + hands-on Azure AI agent development
Course: AI-103T00-A: Develop AI apps and agents on Azure (4-day instructor-led)
Exam: AI-103 — Developing AI Solutions on Azure
Problem Statement: Need to pass AI-103 (score ≥700) while building skills
                    that translate to real AI engineering work.
Solution: Structured, grounded study notes + hands-on module practice in this repo,
          sourced from official Microsoft Learn documentation.
```

## Target Users

| User Segment | Who They Are | What They Need | Pain Points |
|--------------|--------------|----------------|-------------|
| Owner (primary) | Solo learner, aspiring AI engineer | Pass exam (score ≥700), retain skills | Info overload, outdated docs, no practice |
| AI agents (secondary) | Assistants working in this repo | Clear patterns & structure to help effectively | Ambiguous conventions, template placeholders |

## Value Proposition

**For the owner**:
- Official, up-to-date study material (Microsoft Learn MCP) instead of stale training data
- One place for notes: exam guide + agent deep-dive + per-module folders
- Hands-on roadmap (Levels 1–8 in `Agents.md`) that builds exam skills AND production skills

**For agents**:
- Clear module structure (`modules/NN-<slug>`) to file work correctly
- Documented patterns (SDK usage, keyless auth, doc sourcing) to match conventions

## Success Metrics

| Metric | Definition | Target | Current |
|--------|------------|--------|---------|
| Exam pass | AI-103 score | ≥700 | Not taken |
| Modules completed | Course modules with checked-off units | 12/12 | 0/12 |
| Hands-on projects | Roadmap levels built (Agents.md §18) | 8 levels | 0/8 |
| Note coverage | Unit-by-unit notes in module folders | All units | M1 in progress |

## Business Model (if applicable)

```
Revenue Model: N/A (self-study investment)
Pricing Strategy: Azure pay-as-you-go / free credits for practice
Unit Economics: Time + Azure usage cost
Market Position: Solo study track toward AI-103 certification
```

## Key Stakeholders

| Role | Name | Responsibility | Contact |
|------|------|----------------|---------|
| Owner | himan | Study, practice, take exam | — |

## Roadmap Context

**Current Focus**: Module 01 — Plan and prepare to develop AI solutions on Azure (`modules/01-plan-and-prepare/`)
**Next Milestone**: Complete M1 units + notes, then M2 (create and consume Azure AI services)
**Long-term Vision**: Pass AI-103 and ship production-grade agents (containerized hosted agents, multi-agent orchestration, MCP tools)

## Business Constraints

- Time — study must fit around other commitments; notes should be efficient to review
- Azure cost — practice should use free tier / small models where possible (per `Agents.md` §16: cost-aware)
- Docs change — must ground notes in current Microsoft Learn content, not stale info

## Onboarding Checklist

- [x] Understand the problem statement (pass AI-103 + build real skills)
- [x] Identify target user (self) and needs
- [ ] Know the key value proposition
- [ ] Track success metrics as study progresses
- [ ] Know who the stakeholders are (self)
- [ ] Understand current constraints (time, cost, docs currency)

## 📂 Codebase References

- `AI-103-Study-Guide.md` — exam skills this study goal targets
- `Agents.md` — §17 skills map + §18 hands-on roadmap (the "how" behind this goal)
- `modules/01-plan-and-prepare/README.md` — current module being studied

## Related Files

- `technical-domain.md` - How this study goal is organized technically
- `business-tech-bridge.md` - Mapping between exam goals and technical topics
- `decisions-log.md` - Study decisions with context
