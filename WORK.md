# Work

## In Progress

(none)

## Pending

(none)

## Completed

### Plugin Restructure v3.0

#### Structure Changes
- [x] Create `agents/` directory
- [x] Update `plugin.json` version to 3.0.0 and update description

#### Phase Commands - Content Updates
- [x] `commands/fz-discuss.md` - Updated to DISCUSS phase format
- [x] `commands/fz-plan.md` - Updated to PLAN phase format
- [x] `commands/fz-implement.md` - Updated to IMPLEMENT phase format
- [x] `commands/fz-document.md` - Moved from skills/, rewrote as DOCUMENT phase command
- [x] `commands/fz-init-project.md` - Updated with v3.4 CLAUDE.md template

#### Commands Moved/Created
- [x] `skills/fz-verify.md` → `commands/fz-run-checks.md`
- [x] `skills/fz-audit.md` → `commands/fz-audit.md`
- [x] `skills/fz-make-mermaid-diagram.md` → `commands/fz-make-mermaid-diagram.md`
- [x] `skills/fz-make-prototype.md` → `commands/fz-make-prototype.md`
- [x] Created `commands/fz-doc-audit.md` (orchestrator)
- [x] Created `commands/fz-code-audit.md` (orchestrator)

#### Drafter Agents Created
- [x] `commands/fz-init-cr.md` → `agents/fz-cr-drafter.md`
- [x] `commands/fz-init-plan.md` → `agents/fz-plan-drafter.md`
- [x] Created `agents/fz-report-drafter.md`

#### Other Agents Moved
- [x] `skills/fz-tests.md` → `agents/fz-test-writer.md`
- [x] `skills/fz-diagnose.md` → `agents/fz-debugger.md`

#### Doc Assessment Agents Created
- [x] `agents/fz-doc-scanner.md`
- [x] `agents/fz-doc-consistency-checker.md`
- [x] `agents/fz-doc-freshness-checker.md`
- [x] `agents/fz-doc-gap-finder.md`
- [x] `agents/fz-doc-reviewer.md`

#### Code Assessment Agents Moved
- [x] `skills/fz-assess-security.md` → `agents/fz-code-security-auditor.md`
- [x] `skills/fz-assess-deps.md` → `agents/fz-code-deps-checker.md`
- [x] `skills/fz-assess-debt.md` → `agents/fz-code-debt-analyzer.md`
- [x] `skills/fz-assess-secrets.md` → `agents/fz-code-secrets-scanner.md`
- [x] `skills/fz-assess-permissions.md` → `agents/fz-code-permissions-auditor.md`

#### Files Deleted
- [x] `commands/fz-init-spec.md`
- [x] `skills/fz-cr.md`
- [x] `skills/fz-review.md`
- [x] `skills/fz-validate.md`
- [x] `skills/fz-assess-impact.md`
- [x] `skills/fz-assess-logic.md`
- [x] `skills/fz-assess-feasibility.md`
- [x] `skills/fz-assess-consistency.md`
- [x] Removed empty `skills/` folder

#### Documentation Updates
- [x] Updated TOOLS.md summary (11 commands, 15 agents)

### Earlier Work
- [x] Define four phases: DISCUSS, PLAN, IMPLEMENT, DOCUMENT
- [x] Define CR vs Plan distinction
- [x] Define file actions matrix
- [x] Create FLOW.md with full documentation
- [x] Create FLOW.svg diagram
- [x] Create TOOLS.md documentation
- [x] Update CLAUDE.md to v3.4

## Notes & Decisions

### Plugin Structure (Final)
```
commands/ (11 files)
├── fz-discuss.md          (DISCUSS phase)
├── fz-plan.md             (PLAN phase)
├── fz-implement.md        (IMPLEMENT phase)
├── fz-document.md         (DOCUMENT phase)
├── fz-init-project.md     (initialization)
├── fz-doc-audit.md        (orchestrator)
├── fz-code-audit.md       (orchestrator)
├── fz-run-checks.md       (standalone)
├── fz-audit.md            (standalone)
├── fz-make-mermaid-diagram.md  (maker)
└── fz-make-prototype.md   (maker)

agents/ (15 files)
├── fz-cr-drafter.md
├── fz-plan-drafter.md
├── fz-report-drafter.md
├── fz-test-writer.md
├── fz-debugger.md
├── fz-doc-scanner.md
├── fz-doc-consistency-checker.md
├── fz-doc-freshness-checker.md
├── fz-doc-gap-finder.md
├── fz-doc-reviewer.md
├── fz-code-security-auditor.md
├── fz-code-deps-checker.md
├── fz-code-debt-analyzer.md
├── fz-code-secrets-scanner.md
└── fz-code-permissions-auditor.md
```

### Key Design Decisions
- No AskUserQuestion - messes up context on rewind
- Tests are sacred - edit only with user permission
- Audit commands are READ-ONLY
- Agent names use noun forms (debugger, scanner, etc.)
- Drafters receive context and create templates (no questions)
