# Document Update Policy

> **Purpose:** Define **where** and **when** to update docs after implementation.  
> **Audience:** Humans and AI agents.  
> **Authority:** Operational rule — subordinate to [AI_RULES.md](AI_RULES.md).  
> Read order for docs: [DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md). Workflow: [AI_WORKFLOW.md](AI_WORKFLOW.md).

---

## 1. Basic Principles

| Principle | Action |
|-----------|--------|
| **Code changed → check docs** | After any behavior or structure change, decide if related docs need updating |
| **Implemented spec → `docs/current/`** | Only what matches running code |
| **Not yet built → `docs/roadmap/`** | Ideas, backlog, milestones stay here until done |
| **Design rationale → `docs/decisions/`** | Record *why*, not full spec duplication |
| **Obsolete content → `docs/archive/`** | Move retired docs; do not delete |
| **`README.md` = overview only** | Entry point for humans — not the detailed spec SSOT |

**SSOT for implemented behavior:** source code + `docs/current/` (code wins on conflict until `current/` is updated).

---

## 2. Update Decision Rules

| What happened | Update target | Typical action |
|---------------|---------------|----------------|
| **Spec / behavior changed** | `docs/current/` | Edit the relevant `gameplay.md`, `ui.md`, `audio.md`, or `save.md` |
| **New feature implemented** | `docs/current/` + `docs/roadmap/` | Add or update `current/`; remove or mark done in `roadmap/` (ideas, backlog, milestones) |
| **Future idea added (not built)** | `docs/roadmap/` | Add to `ideas.md`, `backlog.md`, or `milestones.md` |
| **Significant design choice made** | `docs/decisions/` | New ADR: `YYYY-MM-DD-topic.md` |
| **Doc superseded or wrong** | `docs/archive/` | Move old file or section; leave a stub link in source if helpful |
| **Entry-level info changed** | `README.md` | Short summary only — link to `docs/` for detail |
| **Consolidated spec view needed** | `CUBE_SPEC.md` (root) | Optional mirror; must stay aligned with `docs/current/` |

### Flow after implementation

```
Implementation complete
        ↓
Update docs/current/     (facts)
        ↓
Clean docs/roadmap/      (remove / mark done)
        ↓
Add docs/decisions/      (if non-obvious why)
        ↓
Move to docs/archive/    (if something replaced)
        ↓
Touch README.md          (only if human-facing entry changed)
```

---

## 3. Prohibited Actions

| Do NOT | Reason |
|--------|--------|
| Write **unimplemented** content in `docs/current/` | `current/` is facts only |
| Treat **`roadmap/` as implemented spec** | AI and humans must not implement from roadmap without request |
| Put **detailed spec in `README.md`** | Duplication and drift — use `docs/current/` |
| **Duplicate** the same spec in README, `CUBE_SPEC.md`, and multiple `current/` files | One SSOT per topic in `current/` |
| **Move or delete docs without reason** | Record rationale in commit message or `decisions/` when non-obvious |

Also follow [AI_RULES.md §2](AI_RULES.md#2-prohibited-actions): no unrequested doc restructures or new top-level folders.

---

## 4. Post-Implementation Checklist

After **every** code or doc task, confirm:

- [ ] **`docs/current/`** — Does behavior differ from what is written? Update the right file(s).
- [ ] **`docs/roadmap/`** — Was a roadmap item completed? Mark done / remove / move description to `current/`.
- [ ] **`docs/decisions/`** — Was there a non-obvious trade-off (architecture, naming, scope)? Add an ADR.
- [ ] **`docs/archive/`** — Is any doc now wrong or retired? Move it here instead of deleting.
- [ ] **`README.md`** — Did the human-facing entry change (new AI doc link, play URL, one-line description)? Update briefly if yes.
- [ ] **`CUBE_SPEC.md`** — If used on this project, sync with `current/` or note deferral.

If nothing needs updating, **state that explicitly** in the completion report with reason (e.g. "internal refactor, no user-visible change").

---

## 5. Completion Report (Doc Section)

Every task that touches code or docs **MUST** include:

### ■ Updated docs

List paths and one line per file on what changed.

### ■ Docs not updated (and why)

| Doc | Reason skipped |
|-----|----------------|
| e.g. `docs/current/ui.md` | No UI change |
| e.g. `README.md` | Entry overview unchanged |

### ■ Open items

- Doc drift still present (code vs `current/`)  
- Deferred updates (user chose code-only)  
- Proposals for future doc work — label **提案**

Full task report template: [AI_TASK_TEMPLATE.md](AI_TASK_TEMPLATE.md) · [AI_WORKFLOW.md §6](AI_WORKFLOW.md#6-completion-report).

---

## Quick Reference

| Content type | Destination |
|--------------|-------------|
| Runs today (verified) | `docs/current/` |
| Might do later | `docs/roadmap/` |
| Why we chose X | `docs/decisions/` |
| No longer valid | `docs/archive/` |
| "What is this project?" | `README.md` (brief) |
| Folder roles | [PROJECT_STRUCTURE.md](PROJECT_STRUCTURE.md) |

---

## Related

- AI constitution: [AI_RULES.md](AI_RULES.md)
- Read priority: [DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md)
- Task workflow: [AI_WORKFLOW.md](AI_WORKFLOW.md)
- Folder roles: [PROJECT_STRUCTURE.md](PROJECT_STRUCTURE.md)
