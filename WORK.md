# Work

## Completed

- [x] Update `/fz-init-project` - rename apps → codebases, add WORK.md to structure
- [x] Create `/fz-discuss` - merge discuss-change + discuss-bug into single command
- [x] Rename `/fz-execute` → `/fz-implement`
- [x] Create `/fz-plan` - new phase command for planning + writing tests
- [x] Update `/fz-tests` - standalone test writing skill
- [x] Create `/fz-verify` - standalone verification skill
- [x] Remove `/fz-discuss-change` and `/fz-discuss-bug`
- [x] Update CLAUDE.md to reflect new workflow structure
- [x] Create `/fz-cr` - basic version for cross-codebase change requests
- [x] Update `/fz-document` - documentation maintenance skill
- [x] Define Plans vs Change Requests distinction
- [x] Update `/fz-discuss` - CR is optional output
- [x] Update `/fz-plan` - uses plan mode, creates plans in codebase's docs/plans/
- [x] Update `/fz-init-project` - remove root docs/plans/, clarify structure
- [x] Update `/fz-implement` - reference plans from codebase's docs/plans/
- [x] Update `/fz-cr` - clarify project-level, what vs how
- [x] Update CLAUDE.md - version 3.1, CR vs Plan distinction

## Pending

- [ ] Define WORK.md cleanup mechanism (manual for now, consider agent later)
- [ ] Ensure permission rule is enforced (commands without "assess" or "init" require user permission)

## Discussion Needed

- [ ] Documentation phase - should it be a phase or stay as standalone tool?
- [ ] Steps within each phase - detailed step definitions
- [ ] Update `/fz-init-cr` and `/fz-init-plan` to match new structure

## Notes & Decisions

- 2024: Three phases model: Discuss → Plan → Implement
- 2024: Refactoring is a separate change, goes through full cycle
- 2024: Discussion can be anything: features, bugs, brainstorming, project setup, notes
- 2024: Implementation phase has no decisions - all decisions happen in Plan phase
- 2024: Commands without "assess" or "init" need user permission
- 2024: Renamed apps/ to codebases/ for clarity
- 2024: WORK.md added to project structure for tracking work
- 2024: **CR = Project-level (what + why), Plan = Codebase-level (how)**
- 2024: Plans live in `codebases/<name>/docs/plans/`, NOT project root
- 2024: CRs live in `change-requests/` at project root
- 2024: One CR can result in multiple Plans (one per affected codebase)
- 2024: `/fz-discuss` creates CR optionally (only if code changes needed)
- 2024: `/fz-cr` for direct CR creation without full discussion
- 2024: `/fz-plan` uses Claude Code's plan mode
