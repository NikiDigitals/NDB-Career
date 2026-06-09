# NDB-CAREER — Decisions Log

**Document Code:** NDB-CAREER
**Location:** docs/decisions/DECISIONS.md
**Author:** Nicolette Martine Langendam — NikiDigitals

All decisions made during the NDB-CAREER programme are logged here. Format follows ADR (Architecture Decision Record) conventions adapted for programme management.

---

## Decision Log

| ID | Date | Decision | Status |
|---|---|---|---|
| NDB-DEC-001 | June 2026 | Separate repo from LES | Accepted |
| NDB-DEC-002 | June 2026 | Separate Obsidian vault from LES Zettelkasten | Accepted |
| NDB-DEC-003 | June 2026 | Build and host on Azure — not Vercel | Accepted |
| NDB-DEC-004 | June 2026 | GitFlow branching strategy | Accepted |
| NDB-DEC-005 | June 2026 | Conventional Commits format | Accepted |
| NDB-DEC-006 | June 2026 | Programme start deferred to post-9 July 2026 | Accepted |
| NDB-DEC-007 | June 2026 | Infrastructure built pre-start; no active work until trigger | Accepted |

---

## NDB-DEC-001 — Separate Repository from LES

**Date:** June 2026
**Status:** Accepted

**Context:**
NDB-CAREER is a Business Analyst career readiness programme, not a LES module. It has a distinct goal (job readiness), distinct outputs (portfolio evidence), and a distinct audience (employers). Commingling with the LES repo would create document code confusion and unclear commit history.

**Decision:**
Create a standalone repository: `NikiDigitals/NDB-Career`. All NDB-CAREER work lives here. LES work that also constitutes portfolio evidence remains in the LES repo and is referenced, not duplicated.

**Consequences:**
- Clear separation of concerns
- NDB-CAREER commit history is clean and employer-readable
- Cross-references between repos required for shared outputs

---

## NDB-DEC-002 — Separate Obsidian Vault from LES Zettelkasten

**Date:** June 2026
**Status:** Accepted

**Context:**
The LES vault is a Zettelkasten for system design, research, and technical knowledge. The career vault serves a different purpose: role research, application tracking, interview prep, financial services industry knowledge. Mixing these creates navigational friction and conceptual noise.

**Decision:**
Create a separate Obsidian vault at `C:\Projects\NDB-Career\vault\`. Career notes, role research, application tracking, interview prep, and industry knowledge live here. The LES vault remains unchanged.

**Consequences:**
- Two vault contexts to maintain
- Zotero integration configured separately for career vault
- No cross-vault linking (by design)

---

## NDB-DEC-003 — Build and Host on Azure

**Date:** June 2026
**Status:** Accepted

**Context:**
NikiDigitals standard. Azure is the designated platform for all builds. Vercel is not used.

**Decision:**
All NDB-CAREER tooling and any hosted outputs use Azure.

**Consequences:**
- Consistent with LES infrastructure decisions
- Azure familiarity compounds across tracks

---

## NDB-DEC-004 — GitFlow Branching Strategy

**Date:** June 2026
**Status:** Accepted

**Context:**
Consistent with NikiDigitals professional standard and LES infrastructure approach.

**Decision:**
GitFlow: `main` (stable, protected) and `develop` (integration). Feature branches per task: `feature/NDB-CAREER-[task-code]`. Hotfix branches if required: `hotfix/[description]`.

**Merge policy:** PRs from `feature/*` into `develop`. PRs from `develop` into `main` at phase milestones.

**Consequences:**
- Branch protection on `main` prevents direct pushes
- All work goes through `develop` first
- Commit history is clean and traceable

---

## NDB-DEC-005 — Conventional Commits Format

**Date:** June 2026
**Status:** Accepted

**Context:**
Consistent with NikiDigitals professional standard. Conventional Commits produce readable, machine-parseable commit history.

**Decision:**
All commits follow Conventional Commits specification:

```
<type>[optional scope]: <description>

Types: feat, fix, docs, chore, refactor, test, style
Scope: optional — use task code or component name
```

Examples:
- `chore: initialise NDB-Career repository`
- `docs(roadmap): add BA-Roadmap-v1.0`
- `feat(portfolio): add AHOLD financial analysis`

**Consequences:**
- Consistent, readable history
- Changelog generation possible if required

---

## NDB-DEC-006 — Programme Start Deferred to Post-9 July 2026

**Date:** June 2026
**Status:** Accepted

**Context:**
Active constraints as of June 2026:
- TMA02 due 2 July 2026
- ACCA BT exam 9 July 2026
- LES-LABS-DASH-001 still in progress

Starting NDB-CAREER active work before 9 July would fragment focus during a high-stakes examination period.

**Decision:**
NDB-CAREER active work (DAMA-DMBOK reading, financial analysis, LinkedIn article #2) does not begin until after 9 July 2026.

**Consequences:**
- Infrastructure built in advance (this setup session)
- Zero NDB-CAREER task execution before trigger date
- ACCA BT exam receives full attention

---

## NDB-DEC-007 — Infrastructure Built Pre-Start

**Date:** June 2026
**Status:** Accepted

**Context:**
Building infrastructure on the day the track opens wastes task time that should go to actual programme work. Preparing the repo, vault, and documentation in advance means the track is immediately productive on trigger day.

**Decision:**
Full infrastructure (repo, vault, documentation) built and committed before programme start. No active NDB-CAREER work undertaken until post-9 July 2026.

**Consequences:**
- On trigger day: open repo and begin DAMA-DMBOK Chapter 1
- Zero infrastructure friction at programme start

---

*Document Code: NDB-CAREER*
*Author: Nicolette Martine Langendam — NikiDigitals*
*Last Updated: June 2026*
