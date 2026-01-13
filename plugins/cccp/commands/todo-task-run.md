---
description: Execute tasks from TODO file and create pull request [/todo-task-run xxx]
arguments:
  - name: file_path
    type: string
    required: true
    description: Path to the TODO file to execute
  - name: no-pr
    description: Skip pull request creation (--no-pr)
    type: boolean
    required: false
---

## context

- Pull Request Template
  @.github/PULL_REQUEST_TEMPLATE.md

## 📋 Development Rules

### 🚨 Lucas Rocha's micro-commit (Details: CLAUDE.md)
- One change per commit, strict adherence to test-driven change cycle

### Task Completion Procedure

**IMPORTANT**: When completing a task, be sure to follow these steps:

1. **Check task** - Change `- [ ]` to `- [x]`
2. **Document related files** - List names of created/modified files

## 📚 Reference Documentation

- [Related Documentation List](@docs)

## 📋 Investigation Results Storage Guidelines

### Memory File Naming Conventions
- **Investigation files**: `/docs/memory/investigation-YYYY-MM-DD-{topic}.md`
- **Pattern files**: `/docs/memory/patterns/{category}-{pattern-name}.md`
- **Technical insight files**: `/docs/memory/insights/{technology}-{insight}.md`

### Information to Save
- **Investigation process**: Investigation methods, tools used, reference materials
- **Findings**: Important technical discoveries, unexpected behaviors or constraints
- **Solutions**: Problem-solving methods, workarounds, best practices
- **Impact scope**: Impact on other components, future implications
- **Reference information**: Related documentation, external resources, code examples

### Storage Timing
- **At investigation start**: Record investigation target and purpose
- **Upon important discovery**: Record immediately even during investigation (consolidate later)
- **At task completion**: Organize and consolidate results to create final version
- **At project completion**: Abstract and generalize overall knowledge

## Processing Flow

### Task Creation (Using Task Tool)
- Read $ARGUMENTS
- Thoroughly understand and convert $ARGUMENTS content into tasks
- Use TDD method (Kent Beck style) for task creation
  - **Red**: Write minimum failing test first
  - **Green**: Write minimum code to pass the test
  - **Refactor**: Eliminate duplication and improve design
  - Complete each cycle within a few minutes
  - Clarify specifications with test-first approach before starting implementation
- Maintain tasks in Todos
- Add created todos to $ARGUMENTS

### Initial Setup (Using Task Tool)
- Execute `git fetch -a -p`
- **Only when --no-pr flag is NOT specified**:
  - Create branch from origin/develop
  - Create empty commit with [skip ci]
  - If an open pull request is already linked to the issue
    - Review already implemented content and continue implementation
  - Create pull request (convert todos into checklist)
    - Pull request template: @.github/PULL_REQUEST_TEMPLATE.md
- **When --no-pr flag is specified**: Continue work on current branch as is

### Task Execution (Use separate Task Tool for each process)
- Recite the contents of `## 📋 Rules` before execution
- Execute each task sequentially
- **Additional steps for investigation tasks**:
  - Create `/docs/memory/investigation-YYYY-MM-DD-{topic}.md` file at investigation start
  - Record important findings and insights immediately to memory file even during investigation
  - Save technical patterns and reusable knowledge categorized in `/docs/memory/patterns/`
- **Required steps after each task completion**:
  1. Commit changes (with appropriate commit message)
     Use /commit command
  2. Push to remote with `git push`
  3. **Only when --no-pr flag is NOT specified**: Update PR checklist (`- [ ]` → `- [x]`)
  4. **Update file specified in $ARGUMENTS**:
     - Change completed task from `- [ ]` to `- [x]`
     - Add related file information
     - Record implementation details and notes
  5. **Save investigation results**:
     - Consolidate and organize insights from investigation into memory file
     - Record technical discoveries and problem-solving methods for future reference
     - Include links to related documentation and reference materials
  6. Report implemented content and update results
- Repeat until no incomplete tasks remain
- Use return values from previously executed tasks appropriately for information needed for next task execution

### Final Completion Process (Using Task Tool)
**Required steps upon all tasks completion**:
1. **Final push confirmation**: Confirm all changes are pushed to remote with `git push`
2. **Final update of file specified in $ARGUMENTS**:
   - Confirm all tasks are in completed state (`- [x]`)
   - Add completion date/time and overall implementation summary
   - Record reference information for future maintenance
3. **Final consolidation of investigation results**:
   - Final organization of all investigation results in memory file
   - Record project-wide impact and future prospects
   - Prepare in a form that can be utilized as reference information for similar tasks
4. **Only when --no-pr flag is NOT specified**:
   - **Update PR title/description**: Update to comprehensive description reflecting implementation content
     - Details of implemented features
     - Quality metrics (number of tests, coverage, etc.)
     - List of main changed files
     - Technical value and effectiveness
     - Summary of important insights from investigation
   - **Completion report comment**: Add detailed completion comment to pull request
   - **Final confirmation**: Present PR page URL and report review readiness
