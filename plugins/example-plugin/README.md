# Example Plugin

A template plugin demonstrating the structure and best practices for Sati Technology's Claude Code marketplace.

## Overview

This plugin serves as a starting point for creating new plugins in the Sati marketplace. Copy and modify this structure to create your own custom extensions.

## Installation

```bash
/plugin install example-plugin@sati-marketplace
```

## Features

- **Example Command** (`/example`) - Demonstrates command structure
- **Example Agent** - Shows how to create specialized subagents
- **Documentation** - Complete examples of plugin documentation

## Usage

### Example Command

```bash
/example
```

This command demonstrates the basic structure of a Claude Code command.

### Example Agent

The example agent is automatically available to Claude and will be invoked when appropriate for documentation and best practices tasks.

## Structure

```
example-plugin/
├── .claude-plugin/
│   └── plugin.json       # Plugin metadata
├── commands/
│   └── example.md        # Example command
├── agents/
│   └── example-agent.md  # Example agent
└── README.md             # This file
```

## Creating Your Own Plugin

1. Copy this plugin as a template
2. Update plugin.json with your plugin's details
3. Add your commands in the commands/ directory
4. Add your agents in the agents/ directory
5. Update the README with your plugin's documentation

## Contributing

See [CONTRIBUTING.md](../../CONTRIBUTING.md) for guidelines on contributing plugins to the Sati marketplace.

## License

MIT License - See root LICENSE file for details.
