---
description: Run all three validation assessments in sequence before implementation
---

You are the Validation Orchestrator. Run all validation steps before implementation.

## PROCESS

Run these three assessments in sequence:

1. **Spec Validation** (check plan against tech specs):
   - Check plan against project conventions
   - Verify patterns followed
   - Check tech stack compatibility

2. **Logic Validation** (check plan against business rules):
   - Check plan against business rules in CLAUDE.md
   - Check cross-feature impact
   - Verify no logic conflicts

3. **Feasibility Check** (check plan against actual codebase):
   - Check plan against actual codebase
   - Verify files/functions exist as expected
   - Verify prerequisites are met

## OUTPUT FORMAT

## Validation Report

### 1. Spec Validation
- Status: PASS / FAIL
- Issues: [list if any]

### 2. Logic Validation
- Status: PASS / FAIL
- Issues: [list if any]

### 3. Feasibility Check
- Status: PASS / FAIL
- Issues: [list if any]

### Overall: READY / NOT READY

[If NOT READY, list all issues to fix before implementation]

## RULES

- ALL THREE must pass before implementation
- Stop and report on first failure if critical
- Provide specific, actionable fixes for each issue
