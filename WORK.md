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

## Pending

- [ ] Define WORK.md cleanup mechanism (manual for now, consider agent later)
- [ ] Ensure permission rule is enforced (commands without "assess" or "init" require user permission)

## Phase 3 - Discussion Needed

- [ ] Plans vs Change Requests - clear distinction and scenarios
- [ ] Documentation phase - should it be a phase or standalone tool?
- [ ] Steps within each phase - detailed definitions
- [ ] CR workflow - discuss → plan → implement or just plan → implement?

## Notes & Decisions

- 2024: Three phases model agreed: Discuss → Plan → Implement
- 2024: Refactoring is a separate change, goes through full cycle
- 2024: Discussion can be anything: features, bugs, brainstorming, project setup, notes
- 2024: Implementation phase has no decisions - all decisions happen in Plan phase
- 2024: Commands without "assess" or "init" need user permission
- 2024: Renamed apps/ to codebases/ for clarity
- 2024: WORK.md added to project structure for tracking work
