# FZ Workflow System Plugin

> **Version:** 3.0
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

| Phase | Command | Purpose | Output | Never Produces |
|-------|---------|---------|--------|----------------|
| Discussion | `/fz-discuss` | Decisions, brainstorming, any discussion | Updated WORK.md, CLAUDE.md, docs | Code |
| Planning | `/fz-plan` | Define how to implement, write failing tests | Plan document, failing tests | Implementation code |
| Implementation | `/fz-implement` | Execute plan, make tests pass | Working code, passing tests | New plans or decisions |

### Permission Rule

Commands **without** "assess" or "init" in name require user confirmation before making changes.

Commands **with** "assess" or "init" can run automatically (read-only or draft generation).

---

## Command Categories

### Phase Commands (The Workflow)
- `/fz-discuss` - Discuss anything: features, bugs, ideas, decisions, brainstorming, project setup
- `/fz-plan` - Create implementation plan and write failing tests (RED phase)
- `/fz-implement` - Execute plan, make tests pass (GREEN phase)

### Initialization Commands (Draft Generation)
- `/fz-init-project` - Generate project structure
- `/fz-init-cr` - Generate a change request first draft
- `/fz-init-plan` - Generate an implementation plan first draft
- `/fz-init-spec` - Generate a specification first draft

### Standalone Skills (Usable Anytime)
- `/fz-tests` - Write tests independently
- `/fz-verify` - Run verification (tests, linter, build)
- `/fz-cr` - Create cross-codebase change request
- `/fz-review` - Code quality review
- `/fz-audit` - Audit against specs
- `/fz-diagnose` - Bug investigation
- `/fz-document` - Documentation generation

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

## Project Structure

Projects using this workflow should have:

```
project-root/
├── CLAUDE.md              # Project decisions, conventions
├── WORK.md                # Checklist of pending work
├── README.md
├── .gitignore
├── codebases/             # Contains all codebases (each with own git)
├── docs/
│   └── plans/             # Implementation plans
└── change-requests/       # Cross-codebase requests
```

---

## Workflow Rules

### Discussion Phase
- Can discuss ANYTHING: features, bugs, ideas, project setup, brainstorming
- Updates WORK.md with work items
- Updates CLAUDE.md with decisions/conventions
- Updates other docs as needed
- NEVER writes code

### Planning Phase
- Creates detailed implementation plan
- Writes failing tests (RED)
- Resolves ALL ambiguity - implementation should have no questions
- NEVER writes implementation code

### Implementation Phase
- Follows the plan exactly
- Makes tests pass (GREEN)
- No decisions - just execution
- Updates WORK.md when done

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

### Planning Phase
- Writing implementation code
- Creating tests that pass immediately
- Leaving ambiguity for implementation
- Skipping test writing when applicable

### Implementation Phase
- Creating new plans
- Making decisions
- "While I'm here" additions
- Claiming success without verification

### General
- Mixing phases
- Committing to main directly
- Reinventing the wheel
