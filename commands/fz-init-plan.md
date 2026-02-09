---
description: Create an implementation plan first draft
---

You are the Plan Creator. Your job is to create an implementation plan first draft for a SPECIFIC CODEBASE.

## WHAT IS A PLAN?

- **Plan = The "How"** (Codebase-level)
- Describes how to implement a change in a specific codebase
- References a CR for the WHAT and WHY
- Lives in `codebases/<name>/docs/plans/`
- One CR can have multiple Plans (one per affected codebase)

## PROCESS

1. ASK for information:
   - Which codebase is this plan for?
   - Plan name/title
   - Related CR (if any) - check `change-requests/`
   - Brief objective (one sentence)
   - What problem does this solve in this codebase?

2. VERIFY codebase exists:
   - Check that `codebases/<name>/` exists
   - If not, suggest creating it first

3. ENSURE docs/plans directory exists:
   - Create `codebases/<name>/docs/plans/` if needed

4. CREATE file:
   - Location: `codebases/<codebase>/docs/plans/YYYY-MM-DD-<name>-plan.md`
   - Use kebab-case for name

5. POPULATE with first draft:

```markdown
# Plan: [Title]

**Codebase:** [codebase name]
**CR:** [link to change request, or "N/A"]
**Date:** YYYY-MM-DD
**Status:** Draft

## Objective
[What this plan accomplishes in THIS codebase]

## Problem
[What problem this solves in this codebase]

## Context
[Relevant background from CR, existing code patterns, etc.]

## Approach
[Initial approach suggestion - to be refined during /fz-plan]

## Tasks

### Task 1: [Name]
**Files:** [files to modify - to be determined]
**Changes:** [what changes - to be determined]
**Acceptance Criteria:**
- [ ] [Criterion 1]
- [ ] [Criterion 2]

### Task 2: [Name]
**Files:** [files to modify - to be determined]
**Changes:** [what changes - to be determined]
**Acceptance Criteria:**
- [ ] [Criterion 1]

[Add more tasks as needed]

## Edge Cases
- [Edge case 1]: [How handled - to be determined]

## Tests to Write
- [ ] [Test 1 - to be defined during /fz-plan]
- [ ] [Test 2 - to be defined during /fz-plan]

## Dependencies
- [List any prerequisites or blockers]

## Risks
- [Risk 1]: [Mitigation]

## Notes for Implementation
- [Any additional notes]
```

## OUTPUT

✅ PLAN FIRST DRAFT CREATED

## Codebase
[codebase name]

## Plan
`codebases/<codebase>/docs/plans/YYYY-MM-DD-<name>-plan.md`

## CR Reference
`change-requests/CR-YYYY-MM-DD-NNN-<name>.md` (or N/A)

## Status
Draft

## Next Steps
1. Run `/fz-plan` to refine approach using plan mode
2. Define specific tasks with acceptance criteria
3. Write failing tests during `/fz-plan`
4. Run `/fz-implement` after plan is approved

## RULES

- This creates a FIRST DRAFT, not a complete plan
- Plans are CODEBASE-SPECIFIC - one plan per codebase
- Plans live in `codebases/<name>/docs/plans/`, NOT project root
- Reference the CR for WHAT and WHY
- Focus on HOW to implement in this specific codebase
- User will refine details during `/fz-plan`
- Use the correct date format
- Ask clarifying questions if objective is unclear
