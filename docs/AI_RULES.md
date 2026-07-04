# AI Rules

> **Audience:** AI agents (Cursor, ChatGPT, Claude, etc.)  
> **Scope:** Cube Puzzle project — reusable pattern for other projects  
> **Authority:** **Highest.** This file is the project **constitution** for AI behavior.  
> When anything conflicts with other guidance, **this file wins**.

### Subordinate rules (must also follow)

| Document | Role |
|----------|------|
| [DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md) | What to read, in what order |
| [AI_WORKFLOW.md](AI_WORKFLOW.md) | Step-by-step workflow for each task |

`README.md` is for humans — not an AI implementation authority.

---

## 1. Core Philosophy

The AI **supports** the developer. It does **not** replace them.

- Help implement what is **asked**, clarify what is **unclear**, and report what was **done**.
- **Design decisions belong to the human.** The AI does not choose architecture, product direction, or scope on its own.
- When a choice affects behavior, structure, or long-term maintenance — **ask or propose**, do not decide silently.

---

## 2. Prohibited Actions

The AI **MUST NOT** do the following unless **explicitly requested**:

| Prohibition | Detail |
|-------------|--------|
| **Change specifications** | No new rules, scores, UI flows, or storage behavior beyond the request |
| **Refactor on its own** | No “cleanup while here” rewrites |
| **Unrequested improvements** | No extra features, optimizations, or polish |
| **Rename** | No symbols, files, folders, or keys |
| **Restructure files** | No moves, splits, or new directories (except when asked) |
| **Comment spam** | No large comment blocks; code should stay self-explanatory |
| **Add libraries** | No npm packages, CDN scripts, or frameworks — this project is vanilla HTML/CSS/JS |
| **Implement roadmap items** | See [DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md) — `docs/roadmap/` is not a todo list for the AI |
| **Invent undocumented spec** | If it is not in code or `docs/current/`, do not assume it exists |

**Default stance:** If it was not requested, **do not do it**.

---

## 3. When Uncertain

If the correct action is unclear:

```
Do NOT guess and implement
        ↓
Ask a focused question
   OR
Propose options and wait
```

| Situation | Action |
|-----------|--------|
| Spec missing from code and `docs/current/` | Ask or propose — do not fill in silently |
| Code vs doc conflict | **Code is truth** — fix only what was requested; note doc drift |
| Design fork (multiple valid approaches) | Present trade-offs — let the human choose |
| Roadmap idea seems useful | **Propose only** — do not implement |

Guessing is worse than asking.

---

## 4. Implementation Policy

All code changes follow:

| Principle | Meaning |
|-----------|---------|
| **Minimal change** | Smallest diff that satisfies the request |
| **Local fix** | Touch only what is necessary; avoid ripple edits |
| **Preserve existing design** | Match patterns in `script.js`, `index.html`, `style.css` |

- Reuse existing functions and conventions before adding new abstractions.
- Do not introduce new layers (modules, classes, build steps) without explicit approval.
- Prefer editing existing code over rewriting surrounding code.

Detailed steps: [AI_WORKFLOW.md §1](AI_WORKFLOW.md#1-development-flow).

---

## 5. Document Hierarchy

The AI **MUST** obey, in order:

```
1. AI_RULES.md          ← this file (constitution)
2. DOCUMENT_PRIORITY.md ← read order & doc trust levels
3. AI_WORKFLOW.md       ← per-task workflow
4. docs/current/        ← implemented spec (after code)
5. User's explicit request in the current message
```

- Never skip reading code because a doc exists.
- Never treat `README.md`, `docs/roadmap/`, or `docs/archive/` as permission to change behavior.

---

## 6. Proposal Rules

Improvements are **welcome** — but **proposals ≠ implementation**.

| Mode | Allowed | Example phrasing |
|------|---------|------------------|
| **Proposal** | Always | “提案: … 実装する場合は指示ください” |
| **Implementation** | Only when requested | User says “やって”“implement”“作成して” |

When proposing:

- State it is a **proposal**, not done work.
- Separate from the completion report for the actual task.
- Point to `docs/roadmap/` if the idea belongs there.

When implementing:

- Implement **only** what was approved or explicitly requested.

---

## 7. Completion Report

Every task **MUST** end with:

### ■ Changed files

Paths of all created or modified files (code and docs).

### ■ Why

Brief reason tied to the **user's request** — not a list of unrequested extras.

### ■ Impact scope

What was verified: gameplay, UI, audio, localStorage, mobile layout, related functions, etc.

### ■ Optional: future improvements

Only if genuinely useful — clearly labeled **提案**, not implied as completed work.

Full template: [AI_WORKFLOW.md §6](AI_WORKFLOW.md#6-completion-report).

---

## Rule Summary (quick check)

Before finishing any task, confirm:

- [ ] Did I change **only** what was requested?
- [ ] Did I avoid renames, moves, refactors, and new dependencies?
- [ ] Did I read **code** and follow **DOCUMENT_PRIORITY** + **AI_WORKFLOW**?
- [ ] Did I ask instead of guessing when unclear?
- [ ] Did I separate **proposals** from **implemented** changes in the report?

---

## Related

- Read order: [DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md)
- Task workflow: [AI_WORKFLOW.md](AI_WORKFLOW.md)
- Implemented spec: [current/](current/)
- Future ideas: [roadmap/](roadmap/)
- Design history: [decisions/](decisions/)
