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

## Installation

### Add Marketplace

```bash
/plugin marketplace add gendosu/ccmp
```

### Install Plugin

```bash
/plugin install cccp@gendosu-claude-plugins
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
