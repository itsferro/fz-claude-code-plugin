# FZ Workflow Tools

## Overview

This document defines the tools (skills/agents) used in the FZ Workflow system.

**Key Principles:**
- Use Claude Code's built-in tools (Read, Write, Edit, Glob, Grep, Bash, Task) for basic operations
- No AskUserQuestion - messes up context on rewind
- Draft creators receive context from parent agent, create from template, then we refine
- Documentation tools validate against git commit history for recency/accuracy signals

---

## Tool Categories

| Category | Purpose |
|----------|---------|
| **Phase Commands** | Guide each workflow phase |
| **Draft Creators** | Create initial file templates |
| **Doc Specialists** | Specialized documentation checks |
| **Doc Orchestrator** | Run all doc specialists at once |
| **Validators/Assessors** | Quality and security checks |
| **Makers** | Create diagrams, prototypes |

---

## Phase Commands

Commands that guide each workflow phase with context and rules.

| Command | Phase | Purpose |
|---------|-------|---------|
| `/fz-discuss` | DISCUSS | Guide discussion, brainstorming, decisions |
| `/fz-plan` | PLAN | Guide planning, uses plan mode |
| `/fz-implement` | IMPLEMENT | Guide implementation, follow plan exactly |
| `/fz-document` | DOCUMENT | Guide documentation, ensure consistency |

---

## Draft Creators

Agents that create initial file templates. They don't ask questions - they receive context from the parent agent and create a structured template.

### How They Work

```
Parent agent provides context (summary)
        ↓
Draft creator spawned with prompt
        ↓
Creates file with template structure
        ↓
Return to discussion, refine the file
```

### Available Draft Creators

| Command | Input | Output | Location |
|---------|-------|--------|----------|
| `/fz-init-cr` | Summary of discussion | CR template | `change-requests/CR-*.md` |
| `/fz-init-plan` | CR context | Plan template | `codebases/*/docs/plans/*.md` |
| `/fz-init-spec` | Requirements context | Spec template | `docs/` |
| `/fz-init-report` | Implementation context | Report template | `codebases/*/docs/reports/*.md` |
| `/fz-init-project` | Project info | Project structure | Root directory |

### Template Principle

Templates are just structured layouts:
- Consistent sections
- Placeholder content
- Ready for refinement

The actual content comes from discussion and refinement after creation.

---

## Documentation Specialists

Specialized agents for specific documentation checks. All validate against git commit history.

### Git History Integration

| Signal | Meaning |
|--------|---------|
| Recent commits | Likely more accurate data |
| Old last-modified | Potentially outdated |
| Change tracking | What changed between versions |

### Available Specialists

| Command | Purpose | Checks |
|---------|---------|--------|
| `/fz-doc-scan` | Index all docs | Scans project and codebases, builds doc inventory |
| `/fz-doc-consistency` | Find mismatches | Compares docs vs code, docs vs docs |
| `/fz-doc-freshness` | Find outdated docs | Uses git history, flags stale content |
| `/fz-doc-gaps` | Find missing docs | Identifies undocumented code, incomplete docs |
| `/fz-doc-review` | Quality review | Checks clarity, comprehensiveness, structure |

---

## Documentation Orchestrator

Runs all documentation specialists in one command.

| Command | Purpose |
|---------|---------|
| `/fz-doc-audit` | Full documentation audit |

### What It Does

1. Spawns `/fz-doc-scan` - Index everything
2. Spawns `/fz-doc-consistency` - Find mismatches
3. Spawns `/fz-doc-freshness` - Find outdated
4. Spawns `/fz-doc-gaps` - Find missing
5. Spawns `/fz-doc-review` - Quality check
6. Aggregates results into audit report

### Output

Generates a comprehensive audit report with:
- Issues found (categorized by type)
- Priority ranking
- Suggested fixes
- Files that need attention

---

## Validators & Assessors

Quality and security checks that can run anytime.

| Command | Purpose |
|---------|---------|
| `/fz-validate` | Run all validations |
| `/fz-assess-security` | Security vulnerability audit |
| `/fz-assess-deps` | Dependency check |
| `/fz-assess-impact` | Change impact analysis |
| `/fz-assess-logic` | Business rules check |
| `/fz-assess-feasibility` | Codebase state check |
| `/fz-assess-secrets` | Secrets scan |
| `/fz-assess-permissions` | Auth audit |
| `/fz-assess-debt` | Technical debt check |
| `/fz-assess-consistency` | General consistency check |

---

## Makers

Tools that create artifacts.

| Command | Purpose |
|---------|---------|
| `/fz-make-mermaid-diagram` | Create Mermaid diagrams |
| `/fz-make-prototype` | Create UI mockups |

---

## Standalone Skills

Utility skills usable anytime.

| Command | Purpose |
|---------|---------|
| `/fz-cr` | Create CR directly (without full discussion) |
| `/fz-tests` | Write tests independently |
| `/fz-verify` | Run verification (tests, linter, build) |
| `/fz-review` | Code quality review |
| `/fz-audit` | Audit against specs |
| `/fz-diagnose` | Bug investigation |

---

## Task Management (Future)

Custom WORK.md integration tools - to be developed.

| Command | Purpose |
|---------|---------|
| `/fz-work-add` | Add work item with phase tag |
| `/fz-work-status` | Update work item status |
| `/fz-work-list` | List/filter work items |

---

## Tool Design Principles

### 1. No AskUserQuestion
Messes up context on rewind. Agents receive context from parent, work with what they have.

### 2. Templates Over Questions
Draft creators use structured templates. Content comes from refinement, not upfront questions.

### 3. Git History as Truth
Documentation tools validate against git commit history. Recent = likely accurate (mostly).

### 4. Orchestrators Over Manual
When multiple related checks exist, provide an orchestrator that runs them all.

### 5. Phase Awareness
Tools know which phase they belong to and follow phase rules.
