# FZ Workflow Tools

## Overview

This document defines the tools (commands and agents) used in the FZ Workflow system.

**Key Principles:**
- Use Claude Code's built-in tools (Read, Write, Edit, Glob, Grep, Bash, Task) for basic operations
- No AskUserQuestion - messes up context on rewind
- Draft creators receive context from parent, create template, then refine
- Assessment tools validate against git commit history for recency/accuracy signals
- Audit commands are **read-only** - they report findings, never make changes

---

## Tool Categories

| Category | Type | Purpose |
|----------|------|---------|
| **Phase Commands** | Command | Guide each workflow phase |
| **Initialization** | Command | Set up project structure |
| **Orchestrators** | Command | Run multiple assessment agents |
| **Standalone** | Command | Utility operations |
| **Makers** | Command | Create artifacts |
| **Drafters** | Agent | Create initial file templates |
| **Doc Assessment** | Agent | Documentation-specific checks |
| **Code Assessment** | Agent | Code-specific checks |
| **Other** | Agent | Debugging, test writing |

---

## Commands (User-Invoked)

### Phase Commands

Commands that guide each workflow phase with context and rules.

| Command | Phase | Purpose |
|---------|-------|---------|
| `/fz-discuss` | DISCUSS | Guide discussion, brainstorming, decisions |
| `/fz-plan` | PLAN | Guide planning, uses plan mode |
| `/fz-implement` | IMPLEMENT | Guide implementation, follow plan exactly |
| `/fz-document` | DOCUMENT | Guide documentation, ensure consistency |

---

### Initialization

| Command | Purpose |
|---------|---------|
| `/fz-init-project` | Generate project structure |

---

### Orchestrators (Read-Only)

Commands that spawn assessment agents and aggregate results. **They do not make changes.**

| Command | Purpose | Spawns |
|---------|---------|--------|
| `/fz-doc-audit` | Full documentation audit | All `fz-doc-*` agents |
| `/fz-code-audit` | Full code audit | All `fz-code-*` agents |

#### What They Do

| They DO | They DON'T |
|---------|------------|
| Read files | Make changes |
| Assess/analyze | Edit code |
| Investigate | Fix issues |
| Generate reports | Modify docs |
| Provide findings | Auto-correct |
| Suggest fixes | |

#### Output

Generates a comprehensive audit report with:
- Issues found (categorized by type)
- Priority ranking
- Suggested fixes
- Files that need attention

---

### Standalone

Utility commands usable anytime.

| Command | Purpose |
|---------|---------|
| `/fz-run-checks` | Run tests, linter, build |
| `/fz-audit` | Audit against specs |

---

### Makers

Commands that create artifacts.

| Command | Purpose |
|---------|---------|
| `/fz-make-mermaid-diagram` | Create Mermaid diagrams |
| `/fz-make-prototype` | Create UI mockups |

---

## Agents (Spawned)

Agents are spawned by commands or phases. They run in background and return results.

### Drafters

Create initial file templates. They don't ask questions - they receive context and create structured templates.

| Agent | Input | Output | Location |
|-------|-------|--------|----------|
| `fz-cr-drafter` | Discussion summary | CR template | `change-requests/CR-*.md` |
| `fz-plan-drafter` | CR context | Plan template | `codebases/*/docs/plans/*.md` |
| `fz-report-drafter` | Implementation context | Report template | `codebases/*/docs/reports/*.md` |

#### How They Work

```
Parent provides context (summary)
        ↓
Agent spawned with prompt
        ↓
Creates file with template structure
        ↓
Return to parent, refine the file
```

---

### Doc Assessment

Specialized agents for documentation checks. All validate against git commit history.

| Agent | Purpose |
|-------|---------|
| `fz-doc-scanner` | Index all docs, build inventory |
| `fz-doc-consistency-checker` | Find mismatches (docs vs code, docs vs docs) |
| `fz-doc-freshness-checker` | Find outdated docs using git history |
| `fz-doc-gap-finder` | Find missing/incomplete documentation |
| `fz-doc-reviewer` | Quality review (clarity, structure) |

#### Git History Integration

| Signal | Meaning |
|--------|---------|
| Recent commits | Likely more accurate |
| Old last-modified | Potentially outdated |
| Change tracking | What changed between versions |

---

### Code Assessment

Specialized agents for code checks. All are read-only.

| Agent | Purpose |
|-------|---------|
| `fz-code-security-auditor` | Security vulnerabilities |
| `fz-code-deps-checker` | Dependency issues |
| `fz-code-debt-analyzer` | Technical debt |
| `fz-code-secrets-scanner` | Secrets/credentials scan |
| `fz-code-permissions-auditor` | Auth/permissions audit |

---

### Other Agents

| Agent | Purpose |
|-------|---------|
| `fz-test-writer` | Write tests based on plan/requirements |
| `fz-debugger` | Debug bugs, find root cause, suggest fixes |

---

## Permission Rule

| Command Type | Permission |
|--------------|------------|
| Contains "audit" or "init" | Read-only, can run automatically |
| Other commands | Require user permission before changes |

---

## Design Principles

### 1. No AskUserQuestion
Messes up context on rewind. Agents receive context from parent, work with what they have.

### 2. Templates Over Questions
Draft creators use structured templates. Content comes from refinement, not upfront questions.

### 3. Git History as Truth
Assessment agents validate against git commit history. Recent = likely accurate.

### 4. Orchestrators Over Manual
When multiple related checks exist, provide an orchestrator that runs them all.

### 5. Read-Only Audits
Audit commands analyze and report. They never modify files.

### 6. Phase Awareness
Tools know which phase they belong to and follow phase rules.

---

## Summary

**10 Commands:**
- 4 Phase commands
- 1 Initialization command
- 2 Orchestrators
- 2 Standalone
- 2 Makers

**15 Agents:**
- 3 Drafters
- 5 Doc assessment
- 5 Code assessment
- 2 Other (test-writer, debugger)
