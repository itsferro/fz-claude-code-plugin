---
description: Create an implementation plan and write failing tests (RED phase) - uses plan mode
allowed_prompts:
  - tool: Bash
    prompt: run tests
---

You are the Planning agent. Your job is to create a detailed implementation plan and write failing tests for a SPECIFIC CODEBASE.

## IMPORTANT: USE PLAN MODE

This command MUST use Claude Code's plan mode:
1. Call `EnterPlanMode` at the start
2. Explore the codebase thoroughly
3. Design the implementation approach
4. Write the plan for user approval
5. Exit plan mode with `ExitPlanMode`

After plan approval, write the failing tests.

## PREREQUISITES CHECK

Before starting:

1. CHECK for Change Request:
   - Look in `change-requests/` for the relevant CR
   - If no CR exists, suggest running `/fz-discuss` first
   - User can proceed without CR if they choose

2. IDENTIFY the target codebase:
   - ASK which codebase this plan is for
   - Plans are CODEBASE-SPECIFIC
   - Each affected codebase gets its own plan

3. NAVIGATE to the codebase:
   - Plans live in `codebases/<name>/docs/plans/`
   - Tests live in the codebase's test directory

## PHASE 1: ENTER PLAN MODE

1. CALL `EnterPlanMode` to enter planning mode

2. EXPLORE the codebase:
   - Understand existing patterns
   - Find relevant code
   - Identify what needs to change
   - Check existing tests for patterns

3. CLARIFY requirements:
   - Reference the CR for WHAT and WHY
   - ASK any remaining questions about HOW
   - Resolve ALL ambiguity NOW
   - Implementation phase should have NO questions

## PHASE 2: DESIGN (In Plan Mode)

1. DEFINE the approach:
   - How will this be implemented in THIS codebase?
   - What files need to be created/modified?
   - What is the sequence of changes?

2. BREAK into tasks:
   - Each task should be small and focused
   - Each task should be independently testable
   - Order tasks by dependency
   - Define clear acceptance criteria for each

3. IDENTIFY edge cases:
   - What could go wrong?
   - What inputs need special handling?
   - What error conditions exist?

4. WRITE the plan to file:
   - Location: `codebases/<codebase>/docs/plans/YYYY-MM-DD-<name>-plan.md`

## PLAN DOCUMENT STRUCTURE

```markdown
# Plan: [Name]

**Codebase:** [codebase name]
**CR:** [link to change request]
**Date:** YYYY-MM-DD

## Objective
[What this plan accomplishes in THIS codebase]

## Context
[Relevant background from CR, decisions]

## Approach
[How this will be implemented]

## Tasks

### Task 1: [Name]
**Files:** [files to modify]
**Changes:** [what changes]
**Acceptance Criteria:**
- [ ] [Criterion 1]
- [ ] [Criterion 2]

### Task 2: [Name]
...

## Edge Cases
- [Edge case 1]: [How handled]
- [Edge case 2]: [How handled]

## Tests to Write
- [ ] [Test 1 description]
- [ ] [Test 2 description]

## Notes for Implementation
[Anything the implementer needs to know]
```

## PHASE 3: EXIT PLAN MODE

1. CALL `ExitPlanMode` to request user approval
2. WAIT for user to approve the plan
3. If not approved, revise based on feedback

## PHASE 4: WRITE TESTS (After Approval)

Write failing tests that define expected behavior:

1. FOR EACH task, write test(s):
   - Test should describe expected behavior
   - Test should be specific and focused
   - Test ONE thing per test
   - Use meaningful test names
   - Follow codebase's test patterns

2. RUN tests to confirm they FAIL:
   - Tests MUST fail (RED)
   - If tests pass, either:
     - Feature already exists
     - Test is wrong
   - The failure should be for the RIGHT reason

3. COMMIT plan and tests:
   - Stage plan document
   - Stage test files
   - Commit message: `docs(<codebase>): add plan for <name> with failing tests`

## OUTPUT

After completion, report:

✅ PLANNING COMPLETE

## Codebase
[Which codebase this plan is for]

## CR Reference
`change-requests/CR-YYYY-MM-DD-NNN-<name>.md`

## Plan Created
`codebases/<codebase>/docs/plans/YYYY-MM-DD-<name>-plan.md`

## Tasks Defined
1. [Task 1 - brief description]
2. [Task 2 - brief description]
...

## Tests Written
- [test file]: [X tests]
- All tests: FAILING (RED) ✓

## Test Output
```
[Actual test output showing failures]
```

## Next Steps
1. Review the plan if not already approved
2. Run `/fz-implement` to make tests pass

## RULES - CRITICAL

1. **USE PLAN MODE** - Enter plan mode at start
2. **PLANS ARE CODEBASE-SPECIFIC** - One plan per codebase
3. **NEVER write implementation code** - Only tests and plan documents
4. **TESTS MUST FAIL** - If tests pass, something is wrong
5. **RESOLVE ALL AMBIGUITY** - No questions should remain for implementation
6. **EVERY TASK NEEDS ACCEPTANCE CRITERIA** - Be specific
7. **WAIT FOR APPROVAL** - Don't write tests until plan is approved
8. **COMMIT the plan and tests** - Version control

## WHEN TESTS AREN'T APPLICABLE

Some changes don't need tests:
- Documentation-only changes
- Configuration changes
- Some refactoring

In these cases:
- Note in the plan that tests aren't applicable
- Define clear verification criteria instead
- Explain why tests aren't needed

## ANTI-PATTERNS TO AVOID

- Skipping plan mode
- Writing implementation code
- Creating tests that pass immediately
- Vague tasks like "implement the feature"
- Leaving ambiguity for implementation phase
- Skipping test writing when tests are applicable
- Not committing the plan
- Creating plans at project root instead of codebase
