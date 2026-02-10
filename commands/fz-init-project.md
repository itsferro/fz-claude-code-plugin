---
description: Initialize a new project with the FZ workflow structure
---

You are the Project Initializer. Your job is to set up a new project with the FZ workflow structure.

## PROCESS

1. GATHER project information:
   - Project name
   - One-line description
   - Planned codebases (e.g., web frontend, API backend, mobile app)
   - For each codebase: name, path in codebases/, and tech stack

2. CREATE folder structure:

   ```
   project-root/
   ├── .gitignore
   ├── CLAUDE.md
   ├── README.md
   ├── WORK.md
   ├── codebases/              # Contains all codebases (each with own git)
   │   └── .gitkeep
   └── change-requests/        # Project-level change requests
       └── .gitkeep
   ```

   NOTE: Each codebase will have its own docs/plans/ directory.
   Plans are codebase-specific, NOT project-level.

3. CREATE .gitignore:

   ```
   # Ignore all codebase contents - each codebase has its own git
   codebases/*

   # But keep the codebases directory itself
   !codebases/.gitkeep
   ```

4. POPULATE WORK.md:

   ```markdown
   # Work

   ## In Progress

   (none)

   ## Pending

   - [ ] Set up first codebase
   - [ ] Define initial conventions in CLAUDE.md

   ## Completed

   (none)
   ```

5. POPULATE CLAUDE.md (v3.4 format):

   ```markdown
   # [Project Name]

   > **Version:** 1.0
   > **Author:** [Author Name]

   [One-line description]

   ---

   ## Core Philosophy

   ### The Iron Laws

   | Law | Description |
   |-----|-------------|
   | Discussion = Documents Only | Never write code during discussion phase |
   | Planning = Tests + Plans Only | Write failing tests, never implementation |
   | Implementation = Code Only | Make tests pass, never create new plans |
   | Evidence Before Claims | Never claim success without running verification |
   | Libraries First | Always check for existing solutions before building custom |

   ### Three Phases

   | Phase | Command | Purpose | Output |
   |-------|---------|---------|--------|
   | Discussion | `/fz-discuss` | Decisions, brainstorming, any discussion | CR (optional), WORK.md, CLAUDE.md |
   | Planning | `/fz-plan` | Define how to implement, write failing tests | Plan (codebase-specific), failing tests |
   | Implementation | `/fz-implement` | Execute plan, make tests pass | Working code, passing tests |

   ---

   ## Codebases

   | Codebase | Path | Tech Stack |
   |----------|------|------------|
   | [Name] | codebases/[path] | [Language, Framework, Key packages] |

   ---

   ## Conventions

   [To be filled as decisions are made]

   ---

   ## Key Concepts

   ### Change Request (CR) vs Plan

   | Aspect | Change Request | Plan |
   |--------|---------------|------|
   | **Level** | Project | Codebase |
   | **Content** | What + Why | How |
   | **Location** | `change-requests/` | `codebases/<name>/docs/plans/` |

   ### Flow

   ```
   /fz-discuss -> CR (if change needed)
                    |
                    +-> /fz-plan (codebase A) -> /fz-implement (codebase A)
                    |
                    +-> /fz-plan (codebase B) -> /fz-implement (codebase B)
   ```

   ---

   ## Commands

   ### Phase Commands
   - `/fz-discuss` - Discuss anything (features, bugs, ideas, decisions)
   - `/fz-plan` - Create implementation plan and write failing tests
   - `/fz-implement` - Execute plan, make tests pass
   - `/fz-document` - Documentation maintenance phase

   ### Other Commands
   - `/fz-init-project` - Initialize project structure
   - `/fz-run-checks` - Run tests, linter, build
   - `/fz-audit` - Audit against specs
   - `/fz-doc-audit` - Run documentation audit
   - `/fz-code-audit` - Run code audit
   - `/fz-make-mermaid-diagram` - Create diagrams
   - `/fz-make-prototype` - Create UI mockups

   ---

   ## Documents

   - `WORK.md` - Current work items
   - `change-requests/` - Change requests (what + why)
   - `codebases/<name>/docs/plans/` - Implementation plans (how)
   - `codebases/<name>/docs/reports/` - Implementation reports
   ```

6. POPULATE README.md:

   ```markdown
   # [Project Name]

   [Description]

   ## Project Structure

   This is a multi-codebase project. Each codebase in `codebases/` has its own repository.

   | Codebase | Description | Setup |
   |----------|-------------|-------|
   | [Name] | [Brief description] | See `codebases/[path]/README.md` |

   ## Development Workflow

   This project uses the FZ Workflow System.

   - **Discussion**: `/fz-discuss` - Discuss features, bugs, ideas, decisions
   - **Planning**: `/fz-plan` - Create plans and write failing tests
   - **Implementation**: `/fz-implement` - Execute plans, make tests pass

   ## Key Locations

   - `WORK.md` - Current work items
   - `change-requests/` - Change requests (what needs to be done)
   - `codebases/<name>/docs/plans/` - Implementation plans (how to do it)
   ```

7. INITIALIZE git:
   - git init
   - Initial commit with structure

## OUTPUT

After completion, report:

```
PROJECT INITIALIZED

Project: [name]
Location: [path]

## Structure Created
- .gitignore (ignores codebases/* contents)
- CLAUDE.md (v3.4 format with Iron Laws)
- README.md
- WORK.md (with In Progress/Pending/Completed sections)
- codebases/ (for codebases, each with own git)
- change-requests/ (for project-level change requests)

## Git
- Repository initialized
- Initial commit created

## Codebases Defined
| Codebase | Path | Tech Stack |
|----------|------|------------|
| ... | ... | ... |

## Next Steps
1. Clone or create each codebase in `codebases/`
2. For each codebase, create `docs/plans/` directory
3. Fill in CLAUDE.md conventions as you make decisions
4. Run `/fz-discuss` to discuss your first feature or change
```

## RULES

- GATHER information before creating - don't assume
- Create minimal structure - don't over-engineer
- Each codebase in codebases/ manages its own git repository
- Each codebase has its own docs/plans/ for implementation plans
- The root repo is for coordination and change requests only
- Always initialize git
