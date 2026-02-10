# Work

## In Progress

(none)

## Pending

- [ ] Update `/fz-discuss` command to match new flow
- [ ] Update `/fz-plan` command to match new flow
- [ ] Update `/fz-implement` command to match new flow
- [ ] Update `/fz-document` command to match new flow
- [ ] Create `/fz-init-report` command
- [ ] Create `/fz-doc-scan` agent
- [ ] Create `/fz-doc-consistency` agent
- [ ] Create `/fz-doc-freshness` agent
- [ ] Create `/fz-doc-gaps` agent
- [ ] Create `/fz-doc-review` agent
- [ ] Create `/fz-doc-audit` orchestrator
- [ ] Ensure permission rule is enforced (commands without "assess" or "init" require user permission)

## Completed

- [x] Define four phases: DISCUSS, PLAN, IMPLEMENT, DOCUMENT
- [x] Define CR vs Plan distinction
- [x] Define file actions matrix (which phase does what to which file)
- [x] Clarify documenting (action) vs DOCUMENT (phase)
- [x] Define WORK.md status management (pending, in progress, done)
- [x] Define that "done" means full objective achieved, not just one phase
- [x] Update `/fz-init-cr` - project-level, what+why
- [x] Update `/fz-init-plan` - codebase-specific, how
- [x] Update `/fz-init-project` - clarify structure
- [x] Update CLAUDE.md to v3.3
- [x] Update FLOW.md with full documentation
- [x] Remove CHANGELOG.md (rely on git for now)
- [x] Create FLOW.svg diagram with phases and file actions
- [x] Define tools/skills structure
- [x] Create TOOLS.md documentation

## Notes & Decisions

- Four phases: DISCUSS → PLAN → IMPLEMENT → DOCUMENT
- Documenting (action) ≠ DOCUMENT (phase)
- WORK.md is edited directly from any phase
- "Done" = full objective achieved, not just one phase complete
- Tests are sacred - edit only with user permission
- IMPLEMENT creates reports in `codebases/*/docs/reports/` only (not root)
- DOCUMENT phase = making docs consistent, comprehensive, clear, not outdated
- CR = project-level (what + why), Plan = codebase-level (how)
- No AskUserQuestion - messes up context on rewind
- Draft creators don't ask questions - receive context, create template, then refine
- Documentation tools validate against git commit history (recency = accuracy signal)
- Orchestrator pattern: one command runs multiple specialist agents
