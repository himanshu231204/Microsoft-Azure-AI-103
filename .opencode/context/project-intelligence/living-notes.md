<!-- Context: project-intelligence/notes | Priority: high | Version: 1.0 | Updated: 2026-08-01 -->

# Living Notes

> Active study items, open questions, and insights. Keep this alive as you progress.

## Quick Reference

- **Purpose**: Capture current state of study progress and open questions
- **Update**: When module status changes or new questions arise
- **Archive**: Move resolved items to bottom with status

## Technical Debt

| Item | Impact | Priority | Mitigation |
|------|--------|----------|------------|
| Sibling context files were unfilled templates | Agents had no real patterns | Med | Filled in 2026-08-01 (technical/business/decisions) |
| Study notes not yet written for M1 units | No review material yet | Med | Write unit notes as you complete each unit |

### Technical Debt Details

**Filled templates**  
*Priority*: Med  
*Impact*: Agents couldn't match your conventions  
*Root Cause*: Initial context scaffold used generic templates  
*Proposed Solution*: Fill remaining files as study evolves  
*Effort*: Small  
*Status*: In Progress (business-domain + decisions-log done; living-notes in progress)

## Open Questions

| Question | Stakeholders | Status | Next Action |
|----------|--------------|--------|-------------|
| Fill `business-tech-bridge.md` template? | himan | Open | Map exam skills → technical topics |
| Which Azure services to spin up for M1 exercise? | himan | Open | Check free-tier / Foundry portal |
| Confirm course module list with actual AI-103T00-A outline? | himan | Open | Paste real module list from training portal |

### Open Question Details

**Course module list confirmation**  
*Context*: Proposed 12-module structure based on exam sections + learning paths; actual AI-103T00-A module list not publicly available  
*Stakeholders*: himan  
*Options*: Use proposed structure (valid for exam prep) vs wait for exact course outline  
*Timeline*: Before M1 start  
*Status*: Open — proceed with proposed structure unless contradicted by actual course

## Known Issues

| Issue | Severity | Workaround | Status |
|-------|----------|------------|--------|
| `.opencode/context/core/standards/` referenced but missing on disk | Low | Read files directly; standards not yet materialized | Known |

### Issue Details

**Missing standards files**  
*Severity*: Low  
*Impact*: Agents fall back to repo-root AGENTS.md conventions  
*Reproduction*: `glob .opencode/context/core/standards/*.md` → empty  
*Workaround*: Use `technical-domain.md` (project-intelligence) + `AGENTS.md` as conventions  
*Root Cause*: Scaffold referenced files that were never created  
*Fix Plan*: Optionally generate standards files later  
*Status*: Known

## Insights & Lessons Learned

### What Works Well
- `modules/NN-<slug>/` convention — ordered, linkable to official docs
- MVI-style notes (tables, checklists, scannable) — fast to review
- Grounding notes in Microsoft Learn MCP — accurate & current

### What Could Be Better
- Study pacing — M1 units not yet converted to notes
- Context standards files not materialized

### Lessons Learned
- Ground study in official docs (Learn MCP), not training data — AI docs drift fast
- Establish conventions early (folder naming, note format) so agents stay consistent
- Verify the actual course/learning path before building module structure — course mismatch wastes effort

## Patterns & Conventions

### Code Patterns Worth Preserving
- `DefaultAzureCredential` keyless auth in all Azure code — lives in `technical-domain.md` §Code Patterns
- Module README checklist format (objectives/units/key takeaways) — see `modules/01-plan-and-prepare/README.md`

### Gotchas for Maintainers
- Don't rename module folders without updating links in `Agents.md` §17–18 and `navigation.md`
- Keep notes cited — add source URLs when fetching new content

## Active Projects

| Project | Goal | Owner | Timeline | Status |
|---------|------|-------|----------|--------|
| Module 01 study | Complete `plan-and-prepare` (9 units) | himan | 2026-08-01 | In Progress |
| Module 02 prep | `create-consume-ai-services` — create and use Azure AI services | himan | Next | Pending |

## Archive (Resolved Items)

### Resolved: technical-domain.md template
- **Resolved**: 2026-08-01
- **Resolution**: Filled from generic template → v1.0 real content (priority critical)
- **Learnings**: Templates are scaffolds; fill them early so agents produce consistent work

## Onboarding Checklist

- [ ] Review open questions and decide on course module list confirmation
- [ ] Convert M1 units to `notes/` as completed
- [ ] Know current active project (Module 01)
- [ ] Keep decisions-log and living-notes current

## 📂 Codebase References

- `modules/01-plan-and-prepare/README.md` — active study project referenced in Active Projects
- `Agents.md` — §17 study path, §18 project roadmap (drives "Next Action" items)
- `.opencode/context/project-intelligence/technical-domain.md` — patterns referenced in Insights

## Related Files

- `decisions-log.md` - Past decisions that inform current state
- `business-domain.md` - Business context for current priorities
- `technical-domain.md` - Technical context for current state
- `business-tech-bridge.md` - Context for current trade-offs
