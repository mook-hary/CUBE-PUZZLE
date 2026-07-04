# AI Document Priority

> **Audience:** AI agents (Cursor, ChatGPT, Claude, etc.)  
> **Scope:** Cube Puzzle project — reusable pattern for other projects  
> **Authority:** This file is the **official rule** for AI document usage.  
> `README.md` is human-oriented overview only; do not treat it as the implementation SSOT.

---

## 1. Basic Principles

| Source | Role | Trust level |
|--------|------|-------------|
| **Source code** | Ground truth for what runs today | Highest |
| **`docs/current/`** | Documented **implemented** specification | High (must match code) |
| **`CUBE_SPEC.md`** | Consolidated spec reference (if present) | High (must match code + current) |
| **`docs/decisions/`** | **Why** a design was chosen | Context only — not a spec |
| **`docs/roadmap/`** | **Not yet implemented** ideas and plans | Do not implement without explicit user request |
| **`docs/archive/`** | Obsolete or retired docs | **Do not reference** for implementation |

### Core rules

1. **Code wins.** When code and docs disagree, treat **code as correct** and flag the doc for update.
2. **`current/` = facts only.** Nothing unimplemented belongs here.
3. **`roadmap/` = future.** Ideas stay ideas until implemented and moved to `current/`.
4. **`decisions/` = rationale.** Read for context; do not infer features from ADRs alone.
5. **`archive/` = ignore.** Historical material; never use as a spec source.

---

## 2. Read Priority (Implementation Tasks)

Read in this order. Stop when the question is answered; do not skip Priority 1.

| Priority | Source | When to read |
|----------|--------|--------------|
| **1** | **Source code** (`script.js`, `index.html`, `style.css`, assets) | Always — first |
| **2** | **`docs/current/`** | After code — confirm documented behavior |
| **3** | **`CUBE_SPEC.md`** (project root, if it exists) | Cross-check against `current/`; prefer `current/` if they conflict |
| **4** | **`docs/decisions/`** | When design intent or past choices are unclear |
| **5** | **`docs/roadmap/`** | Only when user asks about future work, or to avoid re-proposing known ideas |
| **6** | **`docs/archive/`** | **Never** for implementation |

### `docs/current/` file map

| File | Topic |
|------|-------|
| [current/gameplay.md](current/gameplay.md) | Rules, scoring, difficulty, win/lose |
| [current/ui.md](current/ui.md) | Screens, HTML elements, layout |
| [current/audio.md](current/audio.md) | SFX, BGM, playback conditions |
| [current/save.md](current/save.md) | localStorage keys and persistence |

---

## 3. Implementation Rules (AI MUST follow)

### Do

- Read **code → `current/`** before changing behavior.
- Implement only what **code already does** or what the **user explicitly requests**.
- If the user requests a **roadmap** item, treat it as a new task — still verify nothing in `current/` already covers it.
- When unsure about **why** something is designed a certain way, read **`docs/decisions/`**.
- On code/doc conflict: **follow code**, note the doc drift, suggest updating `current/` after implementation.

### Do NOT

- **Do not implement `roadmap/` items** unless the user explicitly asks.
- **Do not invent specs** missing from both code and `docs/current/`.
- **Do not use `archive/`** as a specification source.
- **Do not treat `README.md`** as authoritative for game rules, scores, or storage keys.
- **Do not assume `CUBE_SPEC.md` exists** — if absent, use `docs/current/` only.

### Ambiguity resolution

```
Question unclear?
  → Read code (Priority 1)
  → Read docs/current/ (Priority 2)
  → Still unclear why?
      → Read docs/decisions/ (Priority 4)
  → Proposed feature not in current?
      → It is NOT implemented — check docs/roadmap/ or ask the user
```

---

## 4. Document Update Rules

After **completing** an implementation:

```
docs/roadmap/          docs/current/         docs/decisions/
   (idea)      ──→      (fact)        +       (why, if non-obvious)
```

| Event | Action |
|-------|--------|
| Feature **implemented** | Move description from `roadmap/` → `current/` (or add to the right `current/*.md`) |
| Non-obvious **design choice** | Add or update an ADR in `docs/decisions/` |
| Spec **superseded** | Move old content to `docs/archive/` — do not delete |
| Code changed behavior | Update `docs/current/` in the same PR/session when possible |

### What goes where

| Content type | Destination |
|--------------|-------------|
| Verified behavior (matches code) | `docs/current/` |
| Future idea, backlog, milestone | `docs/roadmap/` |
| Rationale, trade-offs, ADR | `docs/decisions/` |
| Retired or wrong spec | `docs/archive/` |

---

## 5. AI Operational Workflow

### Before implementation

1. **Inspect source code** — locate relevant functions, DOM, styles.
2. **Read `docs/current/`** — confirm intended behavior is documented.
3. **Read `CUBE_SPEC.md`** — if present; reconcile with `current/`.
4. **Read `docs/decisions/`** — only if design intent is needed.
5. **Read `docs/roadmap/`** — only if the task explicitly targets future work.

### After implementation

Update docs **as needed** (user may request doc-only tasks):

| Updated? | File(s) |
|----------|---------|
| Behavior changed or newly specified | `docs/current/*.md` |
| Roadmap item completed | Remove or mark done in `docs/roadmap/`, reflect in `current/` |
| Significant design decision | New file in `docs/decisions/` (e.g. `YYYY-MM-DD-topic.md`) |
| Old spec replaced | Move to `docs/archive/` |

### Quick checklist

- [ ] Code read and understood
- [ ] `current/` checked — no invented rules
- [ ] `roadmap/` not implemented unless user asked
- [ ] Conflicts resolved in favor of code
- [ ] Docs updated if behavior changed

---

## 6. Multi-Project Extension (Future)

This layout is project-agnostic. When copying to another repo:

1. Keep **`docs/DOCUMENT_PRIORITY.md`** at the same path.
2. Replace **`docs/current/`** file names to match that project's domains.
3. Set **`CUBE_SPEC.md`** to the project's consolidated spec filename (or remove Priority 3 if unused).
4. Keep priority order and implementation rules unchanged.

---

## Related

- Implementation spec: [current/](current/)
- Future work: [roadmap/](roadmap/)
- Design history: [decisions/](decisions/)
- Doc structure ADR: [decisions/2026-07-04-doc-structure.md](decisions/2026-07-04-doc-structure.md)
