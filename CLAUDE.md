# FZ Workflow System Plugin

> **Version:** 3.4
> **Author:** FERAS ALZAIDI

A comprehensive AI-assisted development workflow built on top of Claude Code.

---

## Core Philosophy

### The Iron Laws

| Law | Description |
|-----|-------------|
| Phase Separation | Never mix phase activities |
| WORK.md is Direct | Edit from any phase, not through DOCUMENT phase |
| Done Means Objective Achieved | Not just one phase complete |
| Evidence Before Claims | Never claim success without running verification |
| Tests Are Sacred | Edit tests only with user permission |
| Libraries First | Always check for existing solutions before building custom |

### Four Phases

| Phase | Verb | Description | Output |
|-------|------|-------------|--------|
| **DISCUSS** | What + Why | Exploring ideas, problems, decisions | CR, WORK.md, CLAUDE.md |
| **PLAN** | How | Designing the solution | Plan, failing tests |
| **IMPLEMENT** | Execute | Building it | Working code, passing tests, reports |
| **DOCUMENT** | Record + Capture | Making docs consistent, comprehensive, clear, not outdated | Updated docs |

---

## Key Distinction

| Concept | What It Is |
|---------|------------|
| **Documenting (action)** | Editing WORK.md directly - happens from ANY phase |
| **DOCUMENT (phase)** | Making docs consistent, comprehensive, clear, not outdated |

These are **separate**. Recording in WORK.md is an action, not the DOCUMENT phase.

---

## WORK.md Management

### Direct Editing

Each phase can directly edit WORK.md:
- Add work items (discoveries)
- Update item status (pending -> in progress -> done)
- This is an **action**, not the DOCUMENT phase

### Work Item Statuses

| Status | When |
|--------|------|
| `[ ]` Pending | Item added, not started |
| `[~]` In Progress | Phase starts working on it |
| `[x]` Done | Item's **full objective** is achieved |

### WORK.md Format

```markdown
# Work

## In Progress
- [~] [DISCUSS] Add user authentication

## Pending
- [ ] [DISCUSS] Bug found - need root cause
- [ ] [PLAN] New feature - needs planning
- [ ] [IMPLEMENT] Quick typo fix

## Completed
- [x] Set up project structure
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

## CR vs Plan

| Aspect | Change Request (CR) | Plan |
|--------|---------------------|------|
| **Level** | Project | Codebase |
| **Content** | What + Why | How |
| **Location** | `change-requests/` | `codebases/<name>/docs/plans/` |
| **Quantity** | One per change | One per affected codebase |

---

## Commands & Agents

See `TOOLS.md` for full documentation.

### Commands (User-Invoked)

#### Phase Commands
| Command | Purpose |
|---------|---------|
| `/fz-discuss` | Explore ideas, problems, decisions (What + Why) |
| `/fz-plan` | Design solution, write failing tests (How) |
| `/fz-implement` | Execute plan, make tests pass (Execute) |
| `/fz-document` | Make docs consistent, clear, comprehensive (Record + Capture) |

#### Initialization
| Command | Purpose |
|---------|---------|
| `/fz-init-project` | Generate project structure |

#### Orchestrators (Read-Only)
| Command | Purpose |
|---------|---------|
| `/fz-doc-audit` | Run all doc assessment agents |
| `/fz-code-audit` | Run all code assessment agents |

#### Standalone
| Command | Purpose |
|---------|---------|
| `/fz-run-checks` | Run tests, linter, build |
| `/fz-audit` | Audit against specs |

#### Makers
| Command | Purpose |
|---------|---------|
| `/fz-make-mermaid-diagram` | Create Mermaid diagrams |
| `/fz-make-prototype` | Create UI mockups |

### Agents (Spawned)

#### Drafters
| Agent | Purpose |
|-------|---------|
| `fz-cr-drafter` | Create CR template |
| `fz-plan-drafter` | Create plan template |
| `fz-report-drafter` | Create report template |

#### Doc Assessment
| Agent | Purpose |
|-------|---------|
| `fz-doc-scanner` | Index all docs |
| `fz-doc-consistency-checker` | Find mismatches |
| `fz-doc-freshness-checker` | Find outdated |
| `fz-doc-gap-finder` | Find missing |
| `fz-doc-reviewer` | Quality review |

#### Code Assessment
| Agent | Purpose |
|-------|---------|
| `fz-code-security-auditor` | Security vulnerabilities |
| `fz-code-deps-checker` | Dependency issues |
| `fz-code-debt-analyzer` | Technical debt |
| `fz-code-secrets-scanner` | Secrets scan |
| `fz-code-permissions-auditor` | Auth audit |

#### Other
| Agent | Purpose |
|-------|---------|
| `fz-test-writer` | Write tests |
| `fz-debugger` | Debug bugs, find root cause, suggest fixes |

---

## Permission Rule

| Type | Permission |
|------|------------|
| Contains "audit" or "init" | Read-only, can run automatically |
| Other commands | Require user permission before changes |

---

## Phase Rules Quick Reference

| Phase | Never | Always |
|-------|-------|--------|
| DISCUSS | Write code | Update WORK.md |
| PLAN | Write implementation | Use plan mode, tests must fail, read codebase |
| IMPLEMENT | Make decisions | Follow plan, verify, create reports |
| DOCUMENT | Change functionality | Read everything, ensure consistency |

---

## Anti-Patterns

### Discussion Phase
- Writing code
- Skipping research
- Forgetting to update WORK.md

### Planning Phase
- Skipping plan mode
- Writing implementation code
- Creating tests that pass immediately
- Not reading codebase files

### Implementation Phase
- Making decisions
- "While I'm here" additions
- Editing tests without permission
- Claiming success without verification
- Not creating reports

### Document Phase
- Changing functionality
- Skipping inconsistency checks
- Not reading implementation reports

---

## Design Principles

1. **No AskUserQuestion** - Messes up context on rewind
2. **Templates Over Questions** - Draft creators use templates, refine after
3. **Git History as Truth** - Assessment agents validate against commits
4. **Orchestrators Over Manual** - Run multiple checks with one command
5. **Read-Only Audits** - Audit commands never modify files
