# FZ Workflow System Plugin

> **Version:** 3.1
> **Author:** FERAS ALZAIDI

A comprehensive AI-assisted development workflow built on top of Claude Code.

---

## Core Philosophy

### The Iron Laws

| Law | Description |
|-----|-------------|
| Discussion = Documents Only | Never write code during discussion phase |
| Planning = Tests + Plans Only | Write failing tests, never implementation |
| Implementation = Code Only | Make tests pass, never create new plans |
| Evidence Before Claims | Never claim success without running verification |
| Libraries First | Always check for existing solutions before building custom |

### Three Phases

| Phase | Command | Purpose | Output |
|-------|---------|---------|--------|
| Discussion | `/fz-discuss` | Decisions, brainstorming, any discussion | CR (optional), WORK.md, CLAUDE.md |
| Planning | `/fz-plan` | Define how to implement, write failing tests | Plan (codebase-specific), failing tests |
| Implementation | `/fz-implement` | Execute plan, make tests pass | Working code, passing tests |

### Permission Rule

Commands **without** "assess" or "init" in name require user confirmation before making changes.

Commands **with** "assess" or "init" can run automatically (read-only or draft generation).

---

## Key Concepts

### Change Request (CR) vs Plan

| Aspect | Change Request | Plan |
|--------|---------------|------|
| **Level** | Project | Codebase |
| **Content** | What + Why | How |
| **Location** | `change-requests/` | `codebases/<name>/docs/plans/` |
| **Quantity** | One per change | One per affected codebase |

**CR = The "What" and "Why"** - Describes what needs to be done
**Plan = The "How"** - Describes how to implement it in a specific codebase

### Flow

```
/fz-discuss ─→ CR (if change needed)
                 │
                 ├─→ /fz-plan (codebase A) → /fz-implement (codebase A)
                 │
                 └─→ /fz-plan (codebase B) → /fz-implement (codebase B)
```

---

## Project Structure

```
project-root/
├── CLAUDE.md                    # Project decisions, conventions
├── WORK.md                      # Work tracking
├── README.md
├── .gitignore
├── change-requests/             # CRs live here (project-level)
│   └── CR-YYYY-MM-DD-NNN.md
└── codebases/
    ├── frontend/
    │   ├── docs/
    │   │   └── plans/           # Frontend plans only
    │   └── ... (frontend code)
    └── backend/
        ├── docs/
        │   └── plans/           # Backend plans only
        └── ... (backend code)
```

---

## Command Categories

### Phase Commands (The Workflow)
- `/fz-discuss` - Discuss anything: features, bugs, ideas, decisions, brainstorming
- `/fz-plan` - Create implementation plan and write failing tests (uses plan mode)
- `/fz-implement` - Execute plan, make tests pass

### Initialization Commands (Draft Generation)
- `/fz-init-project` - Generate project structure
- `/fz-init-cr` - Generate a change request first draft
- `/fz-init-plan` - Generate an implementation plan first draft
- `/fz-init-spec` - Generate a specification first draft

### Standalone Skills (Usable Anytime)
- `/fz-tests` - Write tests independently
- `/fz-verify` - Run verification (tests, linter, build)
- `/fz-cr` - Create change request directly (without full discussion)
- `/fz-review` - Code quality review
- `/fz-audit` - Audit against specs
- `/fz-diagnose` - Bug investigation
- `/fz-document` - Documentation maintenance

### Assessment Skills (/fz-assess-*)
- `/fz-validate` - Run all validations
- `/fz-assess-impact` - Analyze change impact
- `/fz-assess-logic` - Check business rules
- `/fz-assess-feasibility` - Check codebase state
- `/fz-assess-security` - Security vulnerability assessment
- `/fz-assess-deps` - Dependency scan
- `/fz-assess-secrets` - Secrets scan
- `/fz-assess-permissions` - Auth audit
- `/fz-assess-debt` - Technical debt check
- `/fz-assess-consistency` - Consistency check

### Maker Skills (/fz-make-*)
- `/fz-make-mermaid-diagram` - Create diagrams
- `/fz-make-prototype` - Create UI mockups

---

## Workflow Rules

### Discussion Phase
- Can discuss ANYTHING: features, bugs, ideas, project setup, brainstorming
- Updates WORK.md with work items (always)
- Updates CLAUDE.md with decisions/conventions (if applicable)
- Creates CR in `change-requests/` (if code changes needed)
- NEVER writes code

### Planning Phase
- Uses Claude Code's plan mode
- Creates detailed implementation plan in `codebases/<name>/docs/plans/`
- Writes failing tests (RED)
- Resolves ALL ambiguity - implementation should have no questions
- NEVER writes implementation code
- One plan per codebase

### Implementation Phase
- Follows the plan exactly
- Makes tests pass (GREEN)
- No decisions - just execution
- Updates WORK.md when done
- Works within the specific codebase

### Refactoring
- Refactoring is a SEPARATE change
- Goes through full cycle: discuss → plan → implement
- Not part of implementation phase

### Verification Rules
1. Evidence before claims - Run tests, show output
2. Fresh verification - Don't trust old results
3. Full verification - Partial checks prove nothing
4. Exit code matters - Check for 0 (success)

---

## Anti-Patterns to Avoid

### Discussion Phase
- Writing code instead of documents
- Skipping library/package research
- Building custom when a library exists
- Making decisions without using AskUserQuestion
- Forgetting to update WORK.md
- Creating CR when no code changes needed

### Planning Phase
- Skipping plan mode
- Writing implementation code
- Creating tests that pass immediately
- Leaving ambiguity for implementation
- Creating plans at project root (should be in codebase)

### Implementation Phase
- Creating new plans
- Making decisions
- "While I'm here" additions
- Claiming success without verification
- Working at project root instead of in codebase

### General
- Mixing phases
- Committing to main directly
- Reinventing the wheel
- Confusing CRs with Plans
