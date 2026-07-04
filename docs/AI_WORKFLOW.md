# AI Workflow

> **Audience:** AI agents (Cursor, ChatGPT, Claude, etc.)  
> **Scope:** Cube Puzzle project — reusable pattern for other projects  
> **Authority:** This file defines **how to work**. Document reading rules are in [DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md).

---

## 1. Development Flow

Every task — implementation, fix, refactor, or bugfix — follows this sequence.

```
1. Understand the request
        ↓
2. Read source code
        ↓
3. Read docs per DOCUMENT_PRIORITY.md
        ↓
4. Define scope of changes
        ↓
5. Minimize the diff
        ↓
6. Modify code
        ↓
7. Verify impact
        ↓
8. Update docs if needed
```

### Step details

| Step | Action |
|------|--------|
| **1. Understand** | Restate goal, constraints, and what is *out of scope*. Ask only if blocked. |
| **2. Read code** | Open relevant files (`script.js`, `index.html`, `style.css`, etc.). Find existing patterns. |
| **3. Read docs** | Follow [DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md): code → `current/` → `CUBE_SPEC.md` (if any) → `decisions/` (if needed) → `roadmap/` (only when relevant). |
| **4. Scope** | List files and functions to touch. Confirm no unrequested extras. |
| **5. Minimize** | Smallest correct change. Match existing style and naming. |
| **6. Modify** | Apply changes. One concern per logical edit when possible. |
| **7. Verify impact** | Check callers, UI, storage, audio, and edge cases affected by the change. |
| **8. Update docs** | If behavior changed: update `docs/current/`. Move completed items from `roadmap/`. Add ADR to `decisions/` if design choice is non-obvious. See [DOCUMENT_PRIORITY.md §4](DOCUMENT_PRIORITY.md#4-document-update-rules). |

---

## 2. Implementation Principles

The AI **MUST**:

- Change **only what the request requires**
- **Not** add unrequested improvements, refactors, or “while we’re here” edits
- **Not** rename symbols, files, or folders unless explicitly asked
- **Not** move files unless explicitly asked
- **Not** change architecture or design unless explicitly asked

When in doubt: **do less**, match surrounding code, and report trade-offs in the completion summary instead of expanding scope.

---

## 3. Bug Fixes

```
Identify cause
        ↓
Minimal fix
        ↓
Verify impact
        ↓
Report
```

| Phase | Rule |
|-------|------|
| **Cause** | Reproduce or trace in code. Do not guess from docs alone. |
| **Minimal fix** | Fix the root cause at the narrowest point. No drive-by refactors. |
| **Impact** | Confirm the fix does not break related flows (score, timer, save, UI overlays, audio). |
| **Report** | State cause, fix, and what was checked. Note doc drift if code and `current/` disagreed. |

---

## 4. Refactoring

| Allowed | Forbidden |
|---------|-----------|
| Improve readability (extract function, clarify names **when requested**) | **Behavior changes** |
| Reduce duplication **within requested scope** | Changing public behavior, scores, rules, or UI flow |
| Align with existing conventions | Renaming/moving files without explicit request |

**Rule:** Refactoring must be **observable-neutral** — same inputs, same outputs, same user-visible behavior.

If a refactor would change behavior, **stop** and treat it as a feature or bugfix with explicit user approval.

---

## 5. New Features

```
Check docs/roadmap/
        ↓
   Listed? ──No──→ Propose only (do not implement)
        │
       Yes
        ↓
User explicitly requested?
        ↓
   No ──→ Do not implement
        │
       Yes
        ↓
Follow Development Flow (§1)
```

| Situation | AI action |
|-----------|-----------|
| Idea in `roadmap/` but **not** requested | Mention it if relevant; **do not implement** |
| Idea **not** in `roadmap/` | **Propose** as future work; **do not implement** |
| User **explicitly** requests the feature | Implement; then `roadmap/` → `current/` and update docs |
| Spec missing from `current/` and code | Do not invent — ask or propose; code is truth for existing behavior |

---

## 6. Completion Report

Every task **MUST** end with this structure:

### ■ Changed files

List paths created or modified (code and docs separately).

### ■ Summary of changes

What changed and **why** ( tied to the request ).

### ■ Impact scope

What was checked: affected screens, game rules, localStorage, audio, mobile layout, etc.

### ■ Notes / follow-ups

- Doc updates made or still needed  
- Items left intentionally out of scope  
- Risks or manual verification the user should run  

---

## Quick Reference

| Task type | Flow section | Extra rule |
|-----------|--------------|------------|
| New implementation | §1, §5 | No roadmap features without explicit request |
| Bug fix | §3 | Minimal diff only |
| Refactor | §4 | No behavior change |
| Docs only | §1 step 8 | Follow [DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md) |

---

## Related

- Document read order: [DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md)
- Implemented spec: [current/](current/)
- Future work: [roadmap/](roadmap/)
- Design rationale: [decisions/](decisions/)
- Human overview: [../README.md](../README.md)
