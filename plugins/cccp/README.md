# CCCP - Claude Code Command Pack

A plugin for Claude Code that provides Git operations specialist agent and micro-commit command.

## Overview

This plugin extends Claude Code with powerful Git workflow tools:

- **git-operations-specialist agent**: Expert Git operations including history analysis, conflict resolution, branch strategy, and GitHub CLI operations
- **micro-commit command**: Create fine-grained commits following Lucas Rocha's micro-commit methodology

## Prerequisites

- [Claude Code](https://claude.com/claude-code) installed
- Git (version 2.0 or higher)
- [GitHub CLI (gh)](https://cli.github.com/) for GitHub operations

## Installation

1. Clone this repository or download the plugin files:
```bash
git clone https://github.com/gendosu/cccp.git
```

2. Install the plugin in Claude Code:
```bash
# Copy the plugin to Claude Code's plugins directory
cp -r cccp ~/.claude/plugins/
```

3. Restart Claude Code to load the plugin

## Features

### Git Operations Specialist Agent

The `git-operations-specialist` agent provides:

- **Git History Analysis**: Analyze commit history, branch relationships, and file changes
- **Conflict Resolution**: Guide through merge conflicts with appropriate strategies
- **Branch Strategy**: Recommend and implement branching workflows (GitFlow, GitHub Flow)
- **Advanced Git Operations**: Interactive rebase, cherry-picking, stash management, reflog operations
- **GitHub CLI Operations**: PR creation/management, issue tracking, API operations

### Micro-Commit Command

The `micro-commit` command helps you:

- Create fine-grained commits following test-driven development cycles
- Group related changes logically
- Maintain clean and meaningful commit history
- Follow one change per commit principle

## Usage

### Using the Git Operations Specialist

The agent is automatically invoked when you request Git-related assistance:

```
"Analyze the git history for this feature branch"
"Help me resolve this merge conflict"
"Create a pull request for the current branch"
"Suggest a branching strategy for this project"
```

### Using Micro-Commit

Invoke the micro-commit command:

```
/micro-commit
```

This will analyze your staged changes and create appropriately scoped commits.

## Project Structure

```
cccp/
├── .claude-plugin/
│   └── plugin.json          # Plugin configuration
├── agents/
│   └── git-operations-specialist.md  # Agent definition
├── commands/
│   └── micro-commit.md      # Micro-commit command definition
├── LICENSE                  # MIT License
└── README.md                # This file
```

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Based on Git best practices and workflows
- Implements Lucas Rocha's micro-commit methodology
- Designed for Claude Code plugin ecosystem
