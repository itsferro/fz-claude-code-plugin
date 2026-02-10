# FZ Workflow Flow

## Overview

**Four Phases:**
```
START → DISCUSS → PLAN → IMPLEMENT → DOCUMENT → END
        (What+Why)  (How)   (Execute)  (Record+Capture)
```

**Central Concept:** WORK.md is edited directly from any phase (not through DOCUMENT phase).

---

## Key Distinction

| Concept | What It Is |
|---------|------------|
| **Documenting (action)** | Editing WORK.md directly - happens from ANY phase |
| **DOCUMENT (phase)** | Making docs consistent, comprehensive, clear, not outdated |

These are **separate**. Recording in WORK.md is an action, not the DOCUMENT phase.

---

## Four Phases

### 1. DISCUSS

| Component | Definition |
|-----------|------------|
| **Verb** | What + Why |
| **Description** | Exploring ideas, problems, and decisions / Understanding before acting |
| **Output** | WORK.md updated, CLAUDE.md (if decisions), CR (if code change needed) |

**Rules:**
- ⛔ Never write code
- ✅ Always update WORK.md
- ✅ Use AskUserQuestion for decisions
- ✅ Research before building custom

**Steps:**

| # | Step | Action |
|---|------|--------|
| 1 | Listen | Understand what user wants |
| 2 | Context | Read CLAUDE.md, WORK.md, docs |
| 3 | Explore | Brainstorm, research, ask questions |
| 4 | Decide | Use AskUserQuestion for choices |
| 5 | Capture | Update WORK.md, CLAUDE.md, create CR if needed |

**Tools:** `/fz-discuss`, `/fz-cr`, `AskUserQuestion`, `Read`, `Write`, `WebSearch`

---

### 2. PLAN

| Component | Definition |
|-----------|------------|
| **Verb** | How |
| **Description** | Designing the solution |
| **Output** | Plan in `codebases/<name>/docs/plans/`, failing tests (RED) |

**Rules:**
- ⛔ Never write implementation code
- ✅ Use plan mode
- ✅ Tests must fail (RED)
- ✅ Resolve all ambiguity here

**Steps:**

| # | Step | Action |
|---|------|--------|
| 1 | Check | Verify CR exists, identify codebase |
| 2 | Enter | Start plan mode |
| 3 | Explore | Read codebase, CLAUDE.md, docs, understand patterns |
| 4 | Design | Define approach, break into tasks |
| 5 | Approve | Present plan, get user approval |
| 6 | Test | Write failing tests (RED) |
| 7 | Commit | Save plan and tests |

**Tools:** `/fz-plan`, `EnterPlanMode`, `ExitPlanMode`, `Read`, `Glob`, `Grep`, `Write`, `Edit`, `Bash`, `git`

---

### 3. IMPLEMENT

| Component | Definition |
|-----------|------------|
| **Verb** | Execute |
| **Description** | Building it |
| **Output** | Working code, passing tests (GREEN), reports in `codebases/<name>/docs/reports/` |

**Rules:**
- ⛔ Never make decisions
- ✅ Follow the plan exactly
- ✅ Verify before claiming done
- ✅ No "while I'm here" additions
- ⚠️ Can create new tests, but edit tests only with user permission

**Steps:**

| # | Step | Action |
|---|------|--------|
| 1 | Check | Verify plan exists, tests fail |
| 2 | Branch | Create feature/fix branch |
| 3 | Build | Write code to pass tests (GREEN) |
| 4 | Verify | Run ALL tests, linter, build |
| 5 | Report | Create report in `codebases/<name>/docs/reports/` |
| 6 | Update | Update WORK.md status |
| 7 | Commit | Save working code |

**Tools:** `/fz-implement`, `Read`, `Edit`, `Write`, `Bash`, `git`

---

### 4. DOCUMENT

| Component | Definition |
|-----------|------------|
| **Verb** | Record + Capture |
| **Description** | Making docs consistent, comprehensive, clear, not outdated |
| **Output** | Updated docs, improved documentation quality |

**Rules:**
- ⛔ Never change functionality
- ✅ Read everything (code, docs, plans, reports)
- ✅ Orchestrate agents to compare and review
- ✅ Ensure docs are consistent, inclusive, comprehensive, clear

**Steps:**

| # | Step | Action |
|---|------|--------|
| 1 | Read | Read all docs, code, plans, reports |
| 2 | Compare | Use agents to compare docs vs code vs plans |
| 3 | Identify | Find inconsistencies, outdated info, gaps |
| 4 | Update | Fix README, docs, ensure clarity |
| 5 | Capture | Add learnings to CLAUDE.md |
| 6 | Commit | Save documentation |

**Tools:** `/fz-document`, `Read`, `Edit`, `Write`, `Bash`, `git`

---

## WORK.md Management

### Direct Editing from Any Phase

Each phase can directly edit WORK.md:
- Add work items (discoveries)
- Update item status
- This is an **action**, not the DOCUMENT phase

### Work Item Statuses

| Status | When |
|--------|------|
| `[ ]` Pending | Item added, not started |
| `[~]` In Progress | Phase starts working on it |
| `[x]` Done | Item's **full objective** is achieved |

### Status Flow Example

```
Work item: "Add user authentication"

1. Added to WORK.md             → [ ] [DISCUSS] Add user authentication
2. DISCUSS starts               → [~] [DISCUSS] Add user authentication
3. DISCUSS creates CR           → [~] (still in progress - not done yet)
4. PLAN creates plan            → [~] (still in progress)
5. IMPLEMENT builds it          → [~] (still in progress)
6. Tests pass, objective done   → [x] Add user authentication
```

**Key:** Item is "done" when the **full objective** is achieved, not after a single phase.

### WORK.md Format

```markdown
# Work

## In Progress
- [~] [DISCUSS] Add user authentication

## Pending
- [ ] [DISCUSS] Bug found - need to discuss root cause
- [ ] [PLAN] New feature - needs planning
- [ ] [IMPLEMENT] Quick typo fix

## Completed
- [x] Set up project structure
- [x] Implement login form
```

---

## File Structure

```
project-root/
├── WORK.md                      # Central hub - edited by all phases
├── CLAUDE.md                    # Decisions, conventions
├── README.md
├── docs/                        # Root level docs
├── change-requests/             # CRs (project-level)
│   └── CR-*.md
└── codebases/
    └── <name>/
        ├── WORK.md              # Codebase-specific work
        ├── docs/
        │   ├── plans/           # Plans (codebase-level)
        │   └── reports/         # Reports from IMPLEMENT
        └── ... (any files)
```

---

## File Actions Matrix

| File/Directory | DISCUSS | PLAN | IMPLEMENT | DOCUMENT |
|----------------|---------|------|-----------|----------|
| `WORK.md` | Edit | Edit | Edit | Edit |
| `CLAUDE.md` | Edit | Read | - | Edit |
| `change-requests/CR-*.md` | Create | Read | - | Read |
| `docs/` (root) | Create/Edit | Read | - | Read/Edit |
| `codebases/*/docs/plans/*.md` | - | Create | Read | Read |
| `codebases/*/docs/reports/` | - | - | Create | Read |
| `codebases/*/**` (all files) | - | Read | Create/Edit | Read |
| `codebases/*/tests/*` | - | Create | Create / Edit* | Read |
| `README.md` (root) | - | - | - | Read/Edit |
| `codebases/*/README.md` | - | - | - | Read/Edit |

**\*Edit tests requires user permission** (tests = success criteria)

---

## Action Types

| Action | Color (for diagrams) | Description |
|--------|---------------------|-------------|
| Create | 🟢 Green | New file created |
| Read | ⚫ Gray | Read only, no changes |
| Edit | 🔵 Blue | Existing file modified |
| Create/Edit | 🟠 Orange | May create new or edit existing |
| Edit (permission) | 🔵 Blue dashed | Edit requires user permission |

---

## Flow Paths

### Happy Path

```
START → DISCUSS → PLAN → IMPLEMENT → DOCUMENT → END
```

| From | To | Condition |
|------|----|-----------|
| START | DISCUSS | Always start here |
| DISCUSS | PLAN | Code change needed |
| PLAN | IMPLEMENT | Plan approved |
| IMPLEMENT | DOCUMENT | Tests passing |
| DOCUMENT | END | Work complete |

### No Code Change Path

```
START → DISCUSS → DOCUMENT → END
```

When discussion reveals no code change is needed.

### Discovery (Any Phase)

When you discover something during any phase:
1. Edit WORK.md directly (add item with phase tag)
2. Continue or finish current work
3. New item starts at tagged phase

---

## CR vs Plan

| Aspect | Change Request (CR) | Plan |
|--------|---------------------|------|
| **Level** | Project | Codebase |
| **Content** | What + Why | How |
| **Location** | `change-requests/` | `codebases/<name>/docs/plans/` |
| **Quantity** | One per change | One per affected codebase |

**One CR → Multiple Plans** (one per affected codebase)

---

## Iron Laws

1. **Phase separation** — Never mix phase activities
2. **WORK.md is direct** — Edit from any phase, not through DOCUMENT
3. **Done means objective achieved** — Not just one phase complete
4. **Evidence before claims** — Run tests, show output
5. **Tests are sacred** — Edit only with user permission
6. **Libraries first** — Check existing solutions before building
7. **All decisions in Plan** — Implementation has zero decisions
