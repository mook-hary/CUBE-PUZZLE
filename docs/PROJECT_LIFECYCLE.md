# Project Lifecycle

> **Purpose:** Shared view of **which phase the project is in** and **which docs apply when**.  
> **Audience:** Humans and AI agents.  
> **Scope:** Cube Puzzle — pattern reusable for other projects.  
> **Note:** This file describes **when** to use other docs, not the rules inside them.

---

## Overview

```
Phase 1  企画      →  roadmap
Phase 2  設計      →  decisions (+ read current)
Phase 3  実装      →  code (+ AI_RULES → … → AI_TASK_TEMPLATE)
Phase 4  レビュー  →  確認結果
Phase 5  更新      →  current / roadmap / archive / README
Phase 6  保守      →  roadmap (+ repeat Phases 3–5 as needed)
```

---

## Phase 1 — 企画 (Planning)

**Goal:** Decide what the project should achieve and what might come later.

| Activity | Detail |
|----------|--------|
| Define **Goal** | What success looks like for the product or milestone |
| Capture future work | Ideas not yet built |

### Docs used

| Document | Role in this phase |
|----------|-------------------|
| [roadmap/ideas.md](roadmap/ideas.md) | Collect improvement ideas and features |
| [roadmap/milestones.md](roadmap/milestones.md) | Define major stages (M0, M1, …) |
| [roadmap/backlog.md](roadmap/backlog.md) | Task-level candidates |
| [README.md](../README.md) | Human-facing project summary (optional touch) |

### Output

→ **`docs/roadmap/`** updated. Nothing goes into `current/` until implemented.

---

## Phase 2 — 設計 (Design)

**Goal:** Understand existing behavior and record choices before changing code.

| Activity | Detail |
|----------|--------|
| Read **current spec** | What is already implemented |
| Read **past decisions** | Why things are the way they are |
| Add **new ADRs** | When a non-obvious design choice is made |

### Docs used

| Document | Role in this phase |
|----------|-------------------|
| [current/](current/) | Implemented spec — do not redesign against unknown facts |
| [decisions/](decisions/) | Prior rationale |
| [DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md) | Read order: code first, then `current/` |
| [PROJECT_STRUCTURE.md](PROJECT_STRUCTURE.md) | Where new files may live |
| [decisions/](decisions/) (write) | New file: `YYYY-MM-DD-topic.md` when needed |

### Output

→ **`docs/decisions/`** (if new choices). **`docs/current/`** read-only unless fixing doc drift.

---

## Phase 3 — 実装 (Implementation)

**Goal:** Build or change code following the AI stack.

### Doc chain (follow in order)

```
AI_RULES.md              ← constitution (must obey)
        ↓
DOCUMENT_PRIORITY.md     ← what to read
        ↓
AI_WORKFLOW.md           ← how to work step-by-step
        ↓
AI_TASK_TEMPLATE.md      ← human fills request; AI follows it
        ↓
Source code              ← ground truth
```

| Document | Role in this phase |
|----------|-------------------|
| [AI_RULES.md](AI_RULES.md) | Prohibitions, minimal change, no guessing |
| [DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md) | code → `current/` → `CUBE_SPEC.md` → … |
| [AI_WORKFLOW.md](AI_WORKFLOW.md) | Understand → read → scope → minimize → edit → verify |
| [AI_TASK_TEMPLATE.md](AI_TASK_TEMPLATE.md) | Standard request format from human |
| [current/](current/) | Spec check — do not invent rules |
| [roadmap/](roadmap/) | **Read only** unless task explicitly implements an item |

### Output

→ **Code** (`index.html`, `script.js`, `style.css`, assets, sounds).

---

## Phase 4 — レビュー (Review)

**Goal:** Confirm the change is correct before locking docs.

| Check | Action |
|-------|--------|
| **Behavior** | Manual or described verification steps |
| **Impact scope** | Related UI, gameplay, audio, save, mobile |
| **Doc update need** | Apply [DOC_UPDATE_POLICY.md §4](DOC_UPDATE_POLICY.md#4-post-implementation-checklist) |

### Docs used

| Document | Role in this phase |
|----------|-------------------|
| [AI_WORKFLOW.md §6](AI_WORKFLOW.md#6-completion-report) | Completion report structure |
| [DOC_UPDATE_POLICY.md §4](DOC_UPDATE_POLICY.md#4-post-implementation-checklist) | What docs might need updates |

### Output

→ **確認結果** (verification notes) — part of the task completion report.

---

## Phase 5 — ドキュメント更新 (Documentation Update)

**Goal:** Align docs with code and clean up planning artifacts.

Follow **[DOC_UPDATE_POLICY.md](DOC_UPDATE_POLICY.md)** in full.

| If… | Update… |
|-----|---------|
| Behavior changed | `docs/current/` |
| Roadmap item done | `docs/current/` + clean `docs/roadmap/` |
| New future idea | `docs/roadmap/` |
| Design rationale worth keeping | `docs/decisions/` |
| Spec obsolete | `docs/archive/` |
| Human entry changed | `README.md` (brief only) |

### Docs used

| Document | Role in this phase |
|----------|-------------------|
| [DOC_UPDATE_POLICY.md](DOC_UPDATE_POLICY.md) | Where each kind of content goes |
| [DOCUMENT_PRIORITY.md §4](DOCUMENT_PRIORITY.md#4-document-update-rules) | Move roadmap → current when done |

### Output

→ **`docs/current/`** (primary). Also `roadmap/`, `decisions/`, `archive/`, `README.md` as needed.

---

## Phase 6 — 保守 (Maintenance)

**Goal:** Keep the product running; feed future work back into planning.

| Activity | Typical path |
|----------|--------------|
| **Bug fix** | Phase 3 (minimal fix) → Phase 4 → Phase 5 |
| **Improvement proposal** | Add to `docs/roadmap/` — Phase 1; implement only when requested |
| **Future ideas** | `docs/roadmap/ideas.md` or `backlog.md` |

### Docs used

| Document | Role in this phase |
|----------|-------------------|
| [roadmap/](roadmap/) | Queue for ideas and fixes not yet scheduled |
| [AI_RULES.md](AI_RULES.md) | No silent scope expansion during maintenance |
| Phases 3–5 docs | Repeat cycle per task |

### Output

→ **`docs/roadmap/`** grows; implemented items cycle back through Phases 3–5.

---

## Deliverables by Phase

| Phase | Primary deliverable | Location |
|-------|---------------------|----------|
| **1 企画** | Future plan | `docs/roadmap/` |
| **2 設計** | Design decisions | `docs/decisions/` |
| **3 実装** | Working code | Root + `assets/` + `sounds/` |
| **4 レビュー** | Verification result | Task report / PR description |
| **5 更新** | Accurate spec | `docs/current/` (+ others per policy) |
| **6 保守** | Next work queue | `docs/roadmap/` |

---

## Doc Map — When Each File Is Used

| Document | Phases |
|----------|--------|
| [AI_RULES.md](AI_RULES.md) | 3, 4, 6 |
| [DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md) | 2, 3, 5 |
| [AI_WORKFLOW.md](AI_WORKFLOW.md) | 3, 4 |
| [AI_TASK_TEMPLATE.md](AI_TASK_TEMPLATE.md) | 3 (request) |
| [PROJECT_STRUCTURE.md](PROJECT_STRUCTURE.md) | 2, 3 |
| [DOC_UPDATE_POLICY.md](DOC_UPDATE_POLICY.md) | 4, 5 |
| [PROJECT_LIFECYCLE.md](PROJECT_LIFECYCLE.md) | All (this map) |
| [current/](current/) | 2 (read), 3 (read), 5 (write) |
| [roadmap/](roadmap/) | 1 (write), 3 (read), 5 (clean), 6 (write) |
| [decisions/](decisions/) | 2 (read/write), 5 (write) |
| [archive/](archive/) | 5 (move retired docs) |
| [README.md](../README.md) | 1, 5 (brief entry only) |
| `CUBE_SPEC.md` | 3, 5 (optional consolidated spec) |

---

## Typical Loops

### New feature (explicitly requested)

```
Phase 1 (optional: roadmap item exists)
  → Phase 2 (if design unclear)
  → Phase 3 → 4 → 5
  → Phase 6 idle until next idea
```

### Bug fix

```
Phase 3 → 4 → 5
(skip Phase 1 unless root cause suggests roadmap item)
```

### Docs-only task

```
Phase 5 only (still follow DOC_UPDATE_POLICY + AI_RULES)
```

---

## Related

- Update rules: [DOC_UPDATE_POLICY.md](DOC_UPDATE_POLICY.md)
- Folder roles: [PROJECT_STRUCTURE.md](PROJECT_STRUCTURE.md)
- AI constitution: [AI_RULES.md](AI_RULES.md)
