# Work

## In Progress

(none)

## Pending

### Structure Changes
- [ ] Create `agents/` directory
- [ ] Update `plugin.json` version to 3.0.0 and update description

### Phase Commands - Content Updates

#### `commands/fz-discuss.md`
- [ ] Remove AskUserQuestion references (lines 69, 167, 175)
- [ ] Update RULES section - remove "ALWAYS use AskUserQuestion"
- [ ] Add rule: "No AskUserQuestion - messes up context on rewind"
- [ ] Update file access per FLOW.md: WORK.md (edit), CLAUDE.md (edit), change-requests/ (create), docs/ (create/edit)
- [ ] Add DISCUSS phase verb: "What + Why"
- [ ] Add phase description: "Exploring ideas, problems, decisions / Understanding before acting"

#### `commands/fz-plan.md`
- [ ] Add that PLAN reads: CLAUDE.md, CRs, root docs/, all codebase files
- [ ] Clarify output location: `codebases/<name>/docs/plans/`
- [ ] Emphasize: tests must fail (RED)
- [ ] Add: "Resolve ALL ambiguity - implementation should have NO questions"
- [ ] Add PLAN phase verb: "How"
- [ ] Remove any AskUserQuestion references

#### `commands/fz-implement.md`
- [ ] Add report creation step: create in `codebases/<name>/docs/reports/`
- [ ] Add rule: "Tests are sacred - edit only with user permission"
- [ ] Add rule: "Can create NEW tests, but EDIT tests requires permission"
- [ ] Emphasize: "Never make decisions - all decisions in plan"
- [ ] Add IMPLEMENT phase verb: "Execute"
- [ ] Update WORK.md handling per FLOW.md

#### `commands/fz-document.md` (move from skills/)
- [ ] Rewrite as DOCUMENT phase command (currently too simple)
- [ ] Add phase verb: "Record + Capture"
- [ ] Add phase description: "Making docs consistent, comprehensive, clear, not outdated"
- [ ] Add orchestration of doc assessment agents
- [ ] Clarify: this is the DOCUMENT phase, different from "documenting action"
- [ ] Add file access: reads everything, edits WORK.md/CLAUDE.md/README/docs
- [ ] Add rule: "Never change functionality"

#### `commands/fz-init-project.md`
- [ ] Update to match current project structure (codebases/, change-requests/, etc.)
- [ ] Add WORK.md creation
- [ ] Update CLAUDE.md template to v3.4 format

### Commands to MOVE (from skills/ to commands/)

#### `skills/fz-verify.md` → `commands/fz-run-checks.md`
- [ ] Rename file
- [ ] Update frontmatter: name to "fz-run-checks"
- [ ] Update description: "Run tests, linter, build"
- [ ] Keep content mostly same (already good)

#### `skills/fz-audit.md` → `commands/fz-audit.md`
- [ ] Move file
- [ ] Update to clarify: "Audit against specs" (compare implementation vs plan/CR)
- [ ] This is different from fz-doc-audit and fz-code-audit orchestrators

#### `skills/fz-make-mermaid-diagram.md` → `commands/fz-make-mermaid-diagram.md`
- [ ] Move file (content OK)

#### `skills/fz-make-prototype.md` → `commands/fz-make-prototype.md`
- [ ] Move file (content OK)

### Commands to CREATE (new orchestrators)

#### `commands/fz-doc-audit.md`
- [ ] Create orchestrator command
- [ ] Spawns: fz-doc-scanner, fz-doc-consistency-checker, fz-doc-freshness-checker, fz-doc-gap-finder, fz-doc-reviewer
- [ ] Aggregates results into comprehensive report
- [ ] READ-ONLY - never makes changes
- [ ] Validates against git commit history

#### `commands/fz-code-audit.md`
- [ ] Create orchestrator command
- [ ] Spawns: fz-code-security-auditor, fz-code-deps-checker, fz-code-debt-analyzer, fz-code-secrets-scanner, fz-code-permissions-auditor
- [ ] Aggregates results into comprehensive report
- [ ] READ-ONLY - never makes changes

### Agents - Frontmatter Updates

All agents need this frontmatter format:
```yaml
---
name: <agent-name>
description: <what it does>
subagent_type: <agent-name>
---
```

#### Drafters (move from commands/ to agents/)

##### `commands/fz-init-cr.md` → `agents/fz-cr-drafter.md`
- [ ] Rename and move
- [ ] Update frontmatter to agent format
- [ ] Update content: receives context from parent, creates template
- [ ] Remove any user interaction (no asking questions)
- [ ] Focus on template creation, not refinement

##### `commands/fz-init-plan.md` → `agents/fz-plan-drafter.md`
- [ ] Rename and move
- [ ] Update frontmatter to agent format
- [ ] Update content: receives CR context, creates plan template
- [ ] Remove any user interaction
- [ ] Output to `codebases/<name>/docs/plans/`

##### `agents/fz-report-drafter.md` (CREATE NEW)
- [ ] Create new agent
- [ ] Receives implementation context
- [ ] Creates report template in `codebases/<name>/docs/reports/`
- [ ] Template includes: what was built, tests run, verification results

#### Other Agents (move from skills/ to agents/)

##### `skills/fz-tests.md` → `agents/fz-test-writer.md`
- [ ] Rename and move
- [ ] Update frontmatter to agent format
- [ ] Update: receives plan/requirements, writes failing tests
- [ ] Used by PLAN phase

##### `skills/fz-diagnose.md` → `agents/fz-debugger.md`
- [ ] Rename and move
- [ ] Update frontmatter to agent format
- [ ] Update: finds root cause, suggests fixes
- [ ] READ-ONLY - doesn't make changes

#### Doc Assessment Agents (move/create)

##### `agents/fz-doc-scanner.md` (CREATE NEW)
- [ ] Create new agent
- [ ] Scans project and codebases
- [ ] Builds doc inventory (what docs exist, where)
- [ ] Uses git history for last-modified info

##### `agents/fz-doc-consistency-checker.md` (CREATE NEW)
- [ ] Create new agent
- [ ] Compares docs vs code
- [ ] Compares docs vs docs
- [ ] Reports mismatches

##### `agents/fz-doc-freshness-checker.md` (CREATE NEW)
- [ ] Create new agent
- [ ] Uses git history to find stale content
- [ ] Flags docs not updated when related code changed

##### `agents/fz-doc-gap-finder.md` (CREATE NEW)
- [ ] Create new agent
- [ ] Identifies undocumented code
- [ ] Finds incomplete documentation
- [ ] Reports missing sections

##### `agents/fz-doc-reviewer.md` (CREATE NEW)
- [ ] Create new agent
- [ ] Quality review: clarity, structure, comprehensiveness
- [ ] Style consistency check

#### Code Assessment Agents (move from skills/ to agents/)

##### `skills/fz-assess-security.md` → `agents/fz-code-security-auditor.md`
- [ ] Rename and move
- [ ] Update frontmatter to agent format
- [ ] Keep OWASP top 10 checklist
- [ ] Ensure READ-ONLY

##### `skills/fz-assess-deps.md` → `agents/fz-code-deps-checker.md`
- [ ] Rename and move
- [ ] Update frontmatter to agent format
- [ ] Check for outdated/vulnerable dependencies

##### `skills/fz-assess-debt.md` → `agents/fz-code-debt-analyzer.md`
- [ ] Rename and move
- [ ] Update frontmatter to agent format
- [ ] Identify technical debt patterns

##### `skills/fz-assess-secrets.md` → `agents/fz-code-secrets-scanner.md`
- [ ] Rename and move
- [ ] Update frontmatter to agent format
- [ ] Scan for hardcoded secrets/credentials

##### `skills/fz-assess-permissions.md` → `agents/fz-code-permissions-auditor.md`
- [ ] Rename and move
- [ ] Update frontmatter to agent format
- [ ] Audit auth/permissions patterns

### Files to DELETE (not in spec)
- [ ] Delete `commands/fz-init-spec.md`
- [ ] Delete `skills/fz-cr.md`
- [ ] Delete `skills/fz-review.md`
- [ ] Delete `skills/fz-validate.md`
- [ ] Delete `skills/fz-assess-impact.md`
- [ ] Delete `skills/fz-assess-logic.md`
- [ ] Delete `skills/fz-assess-feasibility.md`
- [ ] Delete `skills/fz-assess-consistency.md`

### Documentation Updates
- [ ] Update TOOLS.md summary (says 10 commands, should be 11)
- [ ] Delete empty `skills/` folder after all moves complete

## Completed

- [x] Define four phases: DISCUSS, PLAN, IMPLEMENT, DOCUMENT
- [x] Define CR vs Plan distinction
- [x] Define file actions matrix (which phase does what to which file)
- [x] Clarify documenting (action) vs DOCUMENT (phase)
- [x] Define WORK.md status management (pending, in progress, done)
- [x] Define that "done" means full objective achieved, not just one phase
- [x] Update CLAUDE.md to v3.4
- [x] Update FLOW.md with full documentation
- [x] Remove CHANGELOG.md (rely on git for now)
- [x] Create FLOW.svg diagram with phases, commands, agents, files
- [x] Define tools structure (commands vs agents)
- [x] Create TOOLS.md documentation
- [x] Finalize command list (11 commands)
- [x] Finalize agent list (15 agents)
- [x] Assess current plugin files and document required changes

## Notes & Decisions

### Phases
- Four phases: DISCUSS -> PLAN -> IMPLEMENT -> DOCUMENT
- Documenting (action) != DOCUMENT (phase)
- WORK.md is edited directly from any phase
- "Done" = full objective achieved, not just one phase complete

### Files
- Tests are sacred - edit only with user permission
- IMPLEMENT creates reports in `codebases/*/docs/reports/` only (not root)
- CR = project-level (what + why), Plan = codebase-level (how)

### Tools Design
- No AskUserQuestion - messes up context on rewind
- Draft creators don't ask questions - receive context, create template, then refine
- Assessment tools validate against git commit history (recency = accuracy signal)
- Orchestrator pattern: one command runs multiple specialist agents
- Audit commands are READ-ONLY - report findings, never make changes
- `fz-doc-*` and `fz-code-*` are agents (spawned), not commands
- `/fz-run-checks` replaces `/fz-verify` (clearer name)
- Removed: `/fz-cr`, `/fz-tests`, `/fz-review`, `/fz-init-spec` (redundant)
- `/fz-diagnose` renamed to `fz-debugger` agent (debugging is an analysis task)
- Agent names use noun forms (e.g., `fz-debugger`, `fz-doc-scanner`, `fz-cr-drafter`)

### Frontmatter Formats

**Command frontmatter:**
```yaml
---
description: <what it does>
allowed_prompts:  # optional
  - tool: Bash
    prompt: <description>
---
```

**Agent frontmatter:**
```yaml
---
name: <agent-name>
description: <what it does>
subagent_type: <agent-name>
---
```

### Plugin Structure Change Summary
```
BEFORE:                          AFTER:
commands/ (7 files)              commands/ (11 files)
skills/ (17 files)               agents/ (15 files)
```

### Task Count Summary
- Structure changes: 2
- Phase command updates: 4
- Commands to move: 4
- Commands to create: 2
- Agents to move/rename: 9
- Agents to create: 6
- Files to delete: 8
- Doc updates: 2

**Total: ~37 tasks**
