# AI Development Guide

> **Start here.** This is the first file an AI should read when joining this project.  
> **Scope:** Cube Puzzle — reusable entry pattern for other repos with the same doc stack.  
> **Depth:** Overview only. Details live in linked documents.

---

## Reading Order

Follow these steps **in order** when starting work. Skip steps only when the task type makes them irrelevant (see [When to skip](#when-to-skip)).

| Step | Document | Why read it |
|------|----------|-------------|
| **1** | [AI_RULES.md](AI_RULES.md) | **Constitution** — absolute rules; highest priority |
| **2** | [DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md) | **Read order** — code vs `current/` vs roadmap |
| **3** | [PROJECT_STRUCTURE.md](PROJECT_STRUCTURE.md) | **Folder roles** — where files belong |
| **4** | [AI_WORKFLOW.md](AI_WORKFLOW.md) | **How to work** — steps for each task |
| **5** | [AI_TASK_TEMPLATE.md](AI_TASK_TEMPLATE.md) | **Request format** — how humans will ask you |
| **6** | [PROJECT_LIFECYCLE.md](PROJECT_LIFECYCLE.md) | **Which phase** — planning → impl → docs → maintenance |
| **7** | [DOC_UPDATE_POLICY.md](DOC_UPDATE_POLICY.md) | **After implementation** — where to write updates |
| **8** | [current/](current/) | **Implemented spec** — facts that should match code |
| **9** | [roadmap/](roadmap/) | **Future ideas** — read only; do not implement unless asked |
| **10** | [decisions/](decisions/) | **Design rationale** — why past choices were made |

**Human overview (not spec):** [README.md](../README.md)

---

## Quick Map

```
AI_INDEX.md          ← you are here
        ↓
AI_RULES.md          ← must obey
DOCUMENT_PRIORITY.md ← what to read when
PROJECT_STRUCTURE.md ← where things go
AI_WORKFLOW.md       ← how to execute a task
AI_TASK_TEMPLATE.md  ← how requests are shaped
PROJECT_LIFECYCLE.md ← project phase context
DOC_UPDATE_POLICY.md ← post-task doc updates
        ↓
current/  roadmap/  decisions/  archive/
        ↓
Source code (always Priority 1 for facts)
```

---

## AI Principles (summary)

| Principle | Meaning |
|-----------|---------|
| **Code first** | Running code is ground truth; update docs if they drift |
| **No guessing** | If unclear, ask or propose — do not invent spec |
| **Minimal change** | Only what the request requires |
| **Proposals ≠ implementation** | Label suggestions **提案**; implement only when asked |
| **Roadmap is not a todo list** | `roadmap/` items need explicit user approval |

Full rules: [AI_RULES.md](AI_RULES.md)

---

## Message to a New AI

You **support** the developer — you do not replace them.

- **Design decisions** belong to the human.
- **When unsure**, ask a focused question instead of assuming.
- **Before editing**, read code and [current/](current/) per [DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md).
- **After editing**, check [DOC_UPDATE_POLICY.md](DOC_UPDATE_POLICY.md) and report per [AI_WORKFLOW.md §6](AI_WORKFLOW.md#6-completion-report).

---

## When to Skip

| Task type | You may skip |
|-----------|--------------|
| **Bug fix** | Step 6 (lifecycle) if obvious; Step 9 (roadmap) unless checking duplicates |
| **Docs only** | Steps 8–9 if not syncing spec; still read Steps 1–2, 7 |
| **Explicit small edit** | Step 6 if phase is clearly "implementation" |

Never skip **Step 1 (AI_RULES)** or reading **source code**.

---

## Related

- Implemented spec: [current/gameplay.md](current/gameplay.md) · [ui.md](current/ui.md) · [audio.md](current/audio.md) · [save.md](current/save.md)
- Doc structure ADR: [decisions/2026-07-04-doc-structure.md](decisions/2026-07-04-doc-structure.md)
