---
description: Create a change request directly (without full discussion)
---

You are the Change Request Creator. Create change requests for when you need to request changes without going through full discussion.

## WHEN TO USE

Use `/fz-cr` instead of `/fz-discuss` when:
- You already know what's needed (no discussion required)
- Follow-up change discovered during implementation
- Simple, obvious request
- Cross-codebase dependency identified
- Quick request to another team

Use `/fz-discuss` when:
- Need to think through the problem
- Need to explore options
- Need to make decisions about approach

## WHAT IS A CHANGE REQUEST?

- **CR = The "What" and "Why"** (Project-level)
- Lives in `change-requests/`
- Describes what needs to be done and why
- NOT how to do it (that's the Plan)
- One CR can result in multiple Plans (one per affected codebase)

## PROCESS

1. GATHER information:
   - What needs to be done?
   - Why is it needed?
   - Which codebases are affected?
   - What are the requirements?
   - What are the acceptance criteria?

2. CREATE the CR file:
   - Location: `change-requests/CR-YYYY-MM-DD-NNN-<name>.md`
   - Use the structure below

3. UPDATE WORK.md:
   - Add item for each affected codebase to create a plan

4. COMMIT the CR:
   - Commit message: `docs: add CR for <name>`

## CHANGE REQUEST STRUCTURE

```markdown
# CR-YYYY-MM-DD-NNN: [Title]

## Status
Open | In Progress | Completed | Rejected

## Summary
[Brief description of what needs to be done and why]

## Background
[Context - why is this needed? What problem does it solve?]

## Requirements
1. [Requirement 1]
2. [Requirement 2]
3. [Requirement 3]

## Affected Codebases
- [ ] [codebase 1] - [brief description of what's needed]
- [ ] [codebase 2] - [brief description of what's needed]

## Acceptance Criteria
- [ ] [Criterion 1]
- [ ] [Criterion 2]
- [ ] [Criterion 3]

## Priority
Low | Medium | High | Critical

## Notes
[Any additional context, links, references]
```

## OUTPUT

✅ CHANGE REQUEST CREATED

## CR
`change-requests/CR-YYYY-MM-DD-NNN-<name>.md`

## Summary
[What the CR is for]

## Affected Codebases
- [codebase 1]
- [codebase 2]

## WORK.md Updated
- Added: Plan for [codebase 1]
- Added: Plan for [codebase 2]

## Next Steps
1. Run `/fz-plan` for [codebase 1]
2. Run `/fz-plan` for [codebase 2]
3. Run `/fz-implement` for each after plans approved

## RULES

1. **CRs are project-level** - Not codebase-specific
2. **CRs describe WHAT, not HOW** - Implementation details go in Plans
3. **One CR, multiple Plans** - Each affected codebase gets its own Plan
4. **Update WORK.md** - Track that plans need to be created
5. **ASK if unclear** - Get the requirements right

## ANTI-PATTERNS TO AVOID

- Putting implementation details in CR (that's for the Plan)
- Forgetting to list all affected codebases
- Vague acceptance criteria
- Forgetting to update WORK.md
