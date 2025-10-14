# Contributing to Sati Claude Marketplace

Thank you for contributing to our Claude Code plugin marketplace! This guide will help you create and submit plugins.

## 🎯 Plugin Guidelines

### Quality Standards

- **Documentation:** Include clear README with installation and usage instructions
- **Testing:** Test plugins thoroughly before submission
- **Security:** Review code for security issues, especially hooks and MCP servers
- **Naming:** Use kebab-case for plugin names (e.g., `deployment-tools`)
- **Versioning:** Follow semantic versioning (MAJOR.MINOR.PATCH)

### Plugin Structure

Every plugin must include:

```
your-plugin/
├── .claude-plugin/
│   └── plugin.json          # Required: Plugin metadata
├── commands/                 # Optional: Slash commands
│   └── command-name.md
├── agents/                   # Optional: Subagents
│   └── agent-name.md
├── hooks/                    # Optional: Event handlers
│   └── hooks.json
├── .mcp.json                # Optional: MCP servers
└── README.md                # Required: Documentation
```

## 📝 Creating a Plugin

### Step 1: Use the Template

Copy the example plugin:

```bash
cp -r plugins/example-plugin plugins/your-plugin-name
cd plugins/your-plugin-name
```

### Step 2: Update Plugin Metadata

Edit `.claude-plugin/plugin.json`:

```json
{
  "name": "your-plugin-name",
  "description": "What your plugin does",
  "version": "1.0.0",
  "author": {
    "name": "Your Name",
    "email": "[email protected]"
  },
  "keywords": ["relevant", "keywords"],
  "license": "MIT"
}
```

### Step 3: Add Functionality

**Add a Slash Command** (`commands/yourcommand.md`):

```markdown
---
name: yourcommand
description: Brief description of what this command does
---

# Command Purpose

Detailed explanation of the command's functionality.

## Usage

/yourcommand [options]

## Examples

- Example 1
- Example 2
```

**Add a Subagent** (`agents/your-agent.md`):

```markdown
---
description: What this agent specializes in
capabilities: ["capability1", "capability2"]
---

# Agent Name

Detailed description of the agent's expertise and when to use it.

## When to Use

- Use case 1
- Use case 2
```

**Add Hooks** (`hooks/hooks.json`):

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "${CLAUDE_PLUGIN_ROOT}/scripts/your-script.sh"
          }
        ]
      }
    ]
  }
}
```

### Step 4: Write Documentation

Create a comprehensive `README.md` for your plugin:

```markdown
# Your Plugin Name

Brief description of what the plugin does.

## Installation

\`\`\`bash
/plugin install your-plugin-name@sati-marketplace
\`\`\`

## Features

- Feature 1
- Feature 2

## Usage

### Command: /yourcommand

Description and examples

## Configuration

Any required configuration steps

## Requirements

- Requirement 1
- Requirement 2
```

### Step 5: Add to Marketplace

Edit `.claude-plugin/marketplace.json` and add your plugin:

```json
{
  "name": "your-plugin-name",
  "source": "./plugins/your-plugin-name",
  "description": "Brief description",
  "version": "1.0.0",
  "author": {
    "name": "Your Name"
  },
  "category": "development",
  "keywords": ["keyword1", "keyword2"],
  "license": "MIT"
}
```

### Step 6: Test Locally

```bash
# From repository root
/plugin marketplace add ./

# Install your plugin
/plugin install your-plugin-name@sati-claude-marketplace

# Test functionality
/help  # Check if commands appear
/yourcommand  # Test your command
```

### Step 7: Submit PR

```bash
git checkout -b plugin/your-plugin-name
git add .
git commit -m "Add your-plugin-name plugin

- Brief description of what it does
- Key features
- Any special considerations"
git push origin plugin/your-plugin-name
```

Create a pull request with:
- Clear description of the plugin's purpose
- Screenshots or examples if applicable
- Any testing notes

## 🔍 Review Process

1. **Automated Checks:** JSON validation, structure verification
2. **Security Review:** Code review for security concerns
3. **Functionality Test:** Team member tests the plugin
4. **Documentation Review:** Ensure clear documentation
5. **Approval:** Merge and release

## 📦 Plugin Categories

Choose the appropriate category:

- **development** - Core development tools
- **devops** - CI/CD, deployment, infrastructure
- **security** - Security scanning, compliance
- **productivity** - Code quality, documentation
- **integration** - API integrations, external services
- **testing** - Test automation, quality assurance
- **utilities** - General-purpose utilities

## 🚫 What Not to Include

- Credentials or API keys (use environment variables)
- Large binary files (use external hosting)
- Proprietary code from external sources
- Malicious or harmful code
- Plugins that violate security policies

## 📄 Licensing

All plugins must include a license. We recommend MIT for maximum compatibility.

## 🆘 Getting Help

- Open a [Discussion](https://github.com/sati-technology/sati-claude-marketplace/discussions) for questions
- Open an [Issue](https://github.com/sati-technology/sati-claude-marketplace/issues) for bugs
- Contact the DevTools team for internal support

## 🎉 Recognition

Contributors will be recognized in:
- Plugin author credits
- Marketplace README
- Release notes

Thank you for making our tools better!
