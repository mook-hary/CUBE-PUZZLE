# AI Task Template

> **Purpose:** Standard request format so AI delivers consistent quality every time.  
> **Usage:** Copy the template below into your message. Fill every section before sending.  
> **Scope:** Project-agnostic — works for Cube Puzzle, mini-rpg, or any repo using the AI doc stack.

### Before you send

Ensure the project has (or adapt names for):

- `docs/AI_RULES.md` — constitution
- `docs/DOCUMENT_PRIORITY.md` — read order
- `docs/AI_WORKFLOW.md` — workflow

---

## Copy from here

```markdown
## Task

<!-- One-line summary of what you want done -->
<!-- Example: Fix timer not pausing when PAUSE overlay is open -->

---

## Goal

<!-- What success looks like when this task is done -->
<!-- Example: PAUSE stops the countdown and resumes correctly on CONTINUE -->

---

## Current

### Spec (if known)

<!-- What should happen today — cite docs/current/ or code if possible -->
<!-- Example: docs/current/gameplay.md says timer stops on PAUSE -->

### Problem

<!-- What is wrong or missing (for bugs/fixes) -->
<!-- Leave blank or write "N/A" for greenfield features -->

### Actual behavior

<!-- What happens now — steps to reproduce for bugs -->
<!-- Example: 1. Start Normal 2. Press PAUSE 3. Timer still counts down -->

---

## Expected

<!-- Desired behavior after the task -->
<!-- Be concrete: UI text, timing, edge cases -->

---

## Scope

### In scope

<!-- Files, features, or areas AI may change -->
<!-- Example: script.js (timer/pause), docs/current/gameplay.md -->

### Out of scope

<!-- Explicitly forbidden changes -->
<!-- Example: Do not change scoring, do not refactor audio system, do not rename files -->

---

## Constraints

<!-- Check all that apply; add project-specific rules -->

- [ ] Follow `docs/AI_RULES.md`
- [ ] Follow `docs/DOCUMENT_PRIORITY.md`
- [ ] Follow `docs/AI_WORKFLOW.md`
- [ ] Minimal change — only what this task requires
- [ ] Preserve existing code style and naming
- [ ] Do not add libraries / dependencies
- [ ] Do not implement items from `docs/roadmap/` unless this task explicitly includes them
- [ ] Other: <!-- e.g. No code changes, docs only -->

---

## Output

When finished, report **all** of the following:

1. **Changed files** — list every path touched
2. **Summary of changes** — what and why
3. **Impact scope** — what was checked (related features, regressions)
4. **How to verify** — steps a human can run to confirm
5. **Open issues** — anything unresolved, blocked, or deferred (optional: proposals labeled 提案)

Do not treat suggestions as completed work unless implemented in this task.
```

---

## Example (filled)

```markdown
## Task

Fix timer continuing during PAUSE

---

## Goal

Countdown stops while pause overlay is visible and resumes from the same value on CONTINUE.

---

## Current

### Spec (if known)

docs/current/gameplay.md — "PAUSE 中は停止"

### Problem

Timer keeps decrementing while paused.

### Actual behavior

1. Start Normal mode
2. Press PAUSE
3. Wait 5 seconds — timer text and bar still update

---

## Expected

- PAUSE: interval cleared; displayed time frozen
- CONTINUE: countdown resumes from frozen value
- TIME UP cannot fire while paused

---

## Scope

### In scope

- script.js (pause/resume/timer)
- docs/current/gameplay.md if behavior note needs tightening

### Out of scope

- UI layout changes
- BGM behavior (unless broken by fix)
- Refactoring unrelated functions

---

## Constraints

- [x] Follow docs/AI_RULES.md
- [x] Follow docs/DOCUMENT_PRIORITY.md
- [x] Follow docs/AI_WORKFLOW.md
- [x] Minimal change
- [x] Preserve code style

---

## Output

(Report changed files, summary, impact, verification steps, open issues)
```

---

## Task-type hints

Use optional extra lines under **Task** or **Scope** when helpful.

| Type | Add to **Current** | Add to **Scope** |
|------|-------------------|------------------|
| **Bug fix** | Repro steps, expected vs actual | "Root-cause fix only" |
| **Feature** | Link roadmap item if any | "Implement only listed acceptance criteria" |
| **UI** | Screenshot or element id | Which screens/files |
| **Refactor** | "Behavior must stay identical" | Explicit list of allowed moves |
| **Docs only** | Source of truth (code paths) | "No code changes" |

---

## Related

- AI constitution: [AI_RULES.md](AI_RULES.md)
- Read order: [DOCUMENT_PRIORITY.md](DOCUMENT_PRIORITY.md)
- Workflow: [AI_WORKFLOW.md](AI_WORKFLOW.md)
