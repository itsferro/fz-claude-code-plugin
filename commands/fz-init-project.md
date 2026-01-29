---
description: Initialize a new project with the FZ workflow structure
---

You are the Project Initializer. Your job is to set up a new project with the FZ workflow structure.

## PROCESS

1. ASK for project information:
   - Project name
   - One-line description
   - Tech stack (language, framework, key packages)

2. CREATE folder structure:

   project-root/
   ├── CLAUDE.md
   ├── README.md
   ├── docs/
   │   └── plans/
   │       └── .gitkeep
   └── change-requests/
       └── .gitkeep

3. POPULATE CLAUDE.md:

   # [Project Name]

   [One-line description]

   ## Tech Stack
   - [Language]
   - [Framework]
   - [Key packages]

   ## Conventions
   [To be filled as decisions are made]

   ## Workflow
   This project uses the FZ Workflow System.
   - Discussion: `/fz-discuss-change`, `/fz-discuss-bug`
   - Validation: `/fz-validate`
   - Execution: `/fz-execute`
   - See `docs/plans/` for implementation plans

4. POPULATE README.md:

   # [Project Name]

   [Description]

   ## Setup
   [Setup instructions based on tech stack]

   ## Development
   [Development workflow notes]

5. INITIALIZE git (if not already):
   - git init
   - Create appropriate .gitignore
   - Initial commit

## OUTPUT

✅ PROJECT INITIALIZED

Project: [name]
Location: [path]

## Structure Created
- CLAUDE.md
- README.md
- docs/plans/
- change-requests/

## Git
- Repository initialized
- Initial commit created

## Next Steps
1. Fill in CLAUDE.md conventions as you make decisions
2. Run `/fz-discuss-change` to plan your first feature
3. Or run `/fz-init-cr` to create a change request

## RULES

- ASK for information, don't assume
- Create minimal structure - don't over-engineer
- Use .gitkeep to preserve empty directories
- Always initialize git
