# Changelog

All notable changes to the CCCP plugin will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2026-01-18

### Added

- **todo-task-run**: `--no-push` flag to skip git push operations
  - Allows local-only commits without pushing to remote
  - Useful for offline development or when working with multiple commits before push
  - Can be combined with `--no-pr` flag

### Changed

- **todo-task-run**: Migrated commit process to `/cccp:micro-commit` command
  - Aligns with Lucas Rocha's micro-commit methodology
  - Provides consistent commit workflow across all commands
  - Ensures strict adherence to one change per commit principle

- **todo-task-run**: Delegated PR operations to `/cccp:pull-request` skill
  - Simplified PR creation and update workflow
  - Centralizes GitHub operations in git-operations-specialist agent
  - Improves separation of concerns

### Enhanced

- **todo-task-planning**: Added task granularity guidelines
  - One file or one feature per task
  - Tasks completable in 30 minutes to 2 hours
  - Clear dependency identification required
  - Prevents overly broad tasks during planning phase

- **todo-task-planning**: Added implementation guidance to TodoWrite structure
  - Target files specification
  - Implementation approach hints
  - Reference code pointers
  - Technical details and patterns
  - Prevents "what should I do?" confusion during execution

## [1.0.0] - 2026-01-18

### Breaking Changes

- **todo-task-run**: Removed planning functionality from execution command
  - Planning responsibilities moved exclusively to `todo-task-planning` command
  - `todo-task-run` now focuses solely on executing pre-created TODO.md files
  - Users must use two-phase workflow: planning → execution

### Changed

- **todo-task-run**: Clarified execution-only mode with explicit `mode: run` declaration
- **todo-task-run**: Removed Task Creation section and TDD conversion guidelines
- **todo-task-run**: Removed Investigation Results Storage Guidelines section
- **todo-task-run**: Simplified setup procedure to focus on TODO.md input contract

### Added

- **todo-task-run**: Command Overview section explaining execution mode and relationship with todo-task-planning
- **todo-task-run**: Prerequisites section documenting TODO.md input contract
- **todo-task-run**: Error Handling section with hybrid investigation approach
- **README**: Two-phase workflow documentation with clear planning/execution separation
- **README**: Workflow diagram showing complete task lifecycle

### Removed

- **todo-task-run**: Planning-related guidelines (moved to todo-task-planning)
- **todo-task-run**: Investigation guidelines (replaced with hybrid approach in Error Handling)

## [0.4.1] - 2025-01-XX

### Added

- Initial version with git-operations-specialist agent
- commit, micro-commit, pull-request commands
- todo-task-planning and todo-task-run commands
- project-manager agent
- key-guidelines skill

[1.0.0]: https://github.com/gendosu/ccmp/compare/v0.4.1...v1.0.0
[0.4.1]: https://github.com/gendosu/ccmp/releases/tag/v0.4.1
