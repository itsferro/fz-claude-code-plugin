# FZ Workflow System Plugin

> **Version:** 2.1
> **Author:** FERAS ALZAIDI

A comprehensive AI-assisted development workflow built on top of Claude Code.

---

## Core Philosophy

### The Iron Laws

| Law | Description |
|-----|-------------|
| Discussion = Documents Only | Never write code during discussion phase |
| Implementation = Code Only | Never create new plans during implementation phase |
| Evidence Before Claims | Never claim success without running verification |
| Libraries First | Always check for existing solutions before building custom |

### Output-Based Separation

| Phase | Commands | Output | Never Produces |
|-------|----------|--------|----------------|
| Discussion | `/fz-discuss-*` | Documents, plans, specs | Code changes |
| Initialization | `/fz-init-*` | First drafts to refine | Finalized documents |
| Assessment | `/fz-assess-*` | Reports | Modifications |
| Maker | `/fz-make-*` | Artifacts (diagrams, prototypes) | Code changes |
| Implementation | `/fz-execute` | Code, tests, commits | New plans or specs |

---

## Command Categories

### Discussion Commands
- `/fz-discuss-change` - Plan features, refactors, or any change (includes library check)
- `/fz-discuss-bug` - Diagnose bugs and plan fixes (includes solution research)

### Implementation Commands
- `/fz-execute` - Execute an approved plan or change request

### Initialization Commands (Draft Generation)
- `/fz-init-project` - Generate project structure
- `/fz-init-cr` - Generate a change request first draft
- `/fz-init-plan` - Generate an implementation plan first draft
- `/fz-init-spec` - Generate a specification first draft

### Assessment Skills (/fz-assess-*)
- `/fz-validate` - Run all 3 validations
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

### Utility Skills
- `/fz-tests` - Run tests
- `/fz-review` - Code quality review
- `/fz-audit` - Audit against specs
- `/fz-diagnose` - Bug investigation
- `/fz-document` - Documentation generation

---

## Workflow Rules

### TDD Cycle
1. Test MUST fail first (RED)
2. Write MINIMUM code to pass (GREEN)
3. Refactor only with tests green
4. Repeat for each piece of functionality

### Branching Strategy
- `feature/<name>` - New features
- `fix/<bug-id>` - Bug fixes
- `refactor/<name>` - Refactoring
- `change/<name>` - Other changes

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

### Validation Phase
- Skipping validation before implementation
- Ignoring validation failures

### Implementation Phase
- Creating new plans
- Modifying approved plans
- Skipping TDD
- Claiming success without verification

### General
- Mixing discussion and implementation
- Committing to main directly
- Reinventing the wheel
