# Work

## In Progress

(none)

## Pending

### Commands
- [ ] Update `/fz-discuss` command to match new flow
- [ ] Update `/fz-plan` command to match new flow
- [ ] Update `/fz-implement` command to match new flow
- [ ] Update `/fz-document` command to match new flow
- [ ] Create `/fz-init-project` command
- [ ] Create `/fz-doc-audit` orchestrator command
- [ ] Create `/fz-code-audit` orchestrator command
- [ ] Create `/fz-run-checks` command
- [ ] Create `/fz-audit` command
- [ ] Create `/fz-make-mermaid-diagram` command
- [ ] Create `/fz-make-prototype` command

### Agents
- [ ] Create `fz-cr-drafter` agent
- [ ] Create `fz-plan-drafter` agent
- [ ] Create `fz-report-drafter` agent
- [ ] Create `fz-test-writer` agent
- [ ] Create `fz-doc-scanner` agent
- [ ] Create `fz-doc-consistency-checker` agent
- [ ] Create `fz-doc-freshness-checker` agent
- [ ] Create `fz-doc-gap-finder` agent
- [ ] Create `fz-doc-reviewer` agent
- [ ] Create `fz-code-security-auditor` agent
- [ ] Create `fz-code-deps-checker` agent
- [ ] Create `fz-code-debt-analyzer` agent
- [ ] Create `fz-code-secrets-scanner` agent
- [ ] Create `fz-code-permissions-auditor` agent
- [ ] Create `fz-debugger` agent

### Other
- [ ] Ensure permission rule is enforced (commands with "audit" or "init" = read-only)

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
- [x] Finalize command list (10 commands)
- [x] Finalize agent list (15 agents)

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
