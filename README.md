# CCMP - Claude Code Marketplace

A collection of development utility plugins for Claude Code.

## Overview

CCMP (Claude Code Marketplace) is a monorepo containing productivity plugins for Claude Code. It provides skills and commands to streamline your daily development workflow.

## Available Plugins

### CCCP (Claude Code Command Pack)

Git operations specialist skill and micro-commit command for test-driven development workflows.

**Features:**
- Git operations specialist skill for comprehensive version control management
- Micro-commit command following Lucas Rocha's methodology
- Support for test-driven change cycles
- Conventional commit message generation
- Automated commit workflow optimization

**Version:** 0.1.0

**Documentation:** [plugins/cccp/README.md](./plugins/cccp/README.md)

### awesome-statusline

Claude Code statusline setup skill for automatic statusline configuration.

**Features:**
- Automated statusline setup with one command
- Displays directory name, Git branch, model name, and token statistics
- Preserves existing settings with automatic backups
- Idempotent operation - safe to run multiple times
- Rich information display in the status line

**Version:** 0.1.0

**Documentation:** [plugins/awesome-statusline/README.md](./plugins/awesome-statusline/README.md)

### Codex

Codex MCP integration plugin for comprehensive code review, technical research, documentation generation, and custom queries.

**Features:**
- Code Review with automatic context gathering and security analysis
- Technical Research with project context and best practices
- Documentation Generation with auto-generated API specs
- Custom Queries for flexible technical questions
- Automatic tech stack detection and design principles loading
- Optimized prompt construction for each use case

**Version:** 0.1.0

**Documentation:** [plugins/codex/README.md](./plugins/codex/README.md)

**Prerequisites:** Requires Codex MCP Server to be configured

## Installation

### Add Marketplace

```bash
/plugin marketplace add gendosu/ccmp
```

### Install Plugin

```bash
# Install CCCP (Git operations specialist)
/plugin install cccp@gendosu-claude-plugins

# Install awesome-statusline
/plugin install awesome-statusline@gendosu-claude-plugins

# Install Codex (requires Codex MCP Server)
/plugin install codex@gendosu-claude-plugins
```

## Plugin Development

### Directory Structure

```
ccmp/
├── .claude-plugin/
│   └── marketplace.json       # Marketplace manifest
├── plugins/
│   └── cccp/                  # CCCP plugin
│       ├── .claude-plugin/
│       │   └── plugin.json
│       ├── skills/
│       ├── commands/
│       ├── README.md
│       └── LICENSE
├── docs/
│   └── memory/                # Investigation and planning records
├── README.md                  # English marketplace documentation
├── README.ja.md               # Japanese marketplace documentation
├── LICENSE                    # MIT License
└── .gitignore
```

### Adding a New Plugin

1. Create a new directory under `plugins/`
2. Add `.claude-plugin/plugin.json` with plugin metadata
3. Implement skills and/or commands
4. Update `marketplace.json` to register the new plugin
5. Add documentation in the plugin's README.md

### Plugin Self-Containment (Critical)

Claude Code copies plugins to cache, so relative path references using `../` are not supported. Each plugin must be self-contained with all necessary files included.

## Version Management

- **Marketplace Version:** Managed in `marketplace.json` (current: v1.0.0)
- **Individual Plugin Versions:** Managed within each plugin entry
- **Git Tags:** Versioned for the entire marketplace

## Troubleshooting

### Plugin Not Found

Ensure the marketplace has been added correctly:

```bash
/plugin marketplace list
```

### Installation Fails

1. Verify the marketplace.json syntax with `jq`:
   ```bash
   jq . .claude-plugin/marketplace.json
   ```

2. Check that the plugin's `plugin.json` exists:
   ```bash
   ls plugins/*/. claude-plugin/plugin.json
   ```

### Plugin Not Loading

Ensure all required files are within the plugin directory and no external dependencies via `../` are used.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Author

**Gendosu**

## Repository

[https://github.com/gendosu/ccmp](https://github.com/gendosu/ccmp)
