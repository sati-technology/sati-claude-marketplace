# Example Plugin

A template plugin demonstrating the structure and best practices for Sati Technology's Claude Code marketplace.

## Overview

This plugin serves as a starting point for creating new plugins in the Sati marketplace. Copy and modify this structure to create your own custom extensions.

**Key Features**:
- Demonstrates plugin structure and metadata
- Shows command and agent patterns
- Follows Docker MCP Toolkit best practices
- No unnecessary `.mcp.json` (uses Docker MCP instead)

## Requirements

### Docker MCP Toolkit (Recommended)

This example demonstrates best practices for leveraging Docker MCP Toolkit. While this specific plugin doesn't require MCP tools, production plugins should use Docker MCP for:

- **GitHub operations** - Via GitHub MCP Server
- **Browser automation** - Via Browser MCP Server
- **AWS/CDK guidance** - Via AWS CDK MCP Server
- **And 200+ more servers** - Available through Docker Desktop

See [Docker MCP Integration Guide](../../docs/DOCKER-MCP-GUIDE.md) for setup instructions.

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

Note: No .mcp.json file - Docker MCP Toolkit handles MCP servers!
```

## Creating Your Own Plugin

1. Copy this plugin as a template
2. Update plugin.json with your plugin's details
3. Add your commands in the commands/ directory
4. Add your agents in the agents/ directory
5. Update the README with your plugin's documentation
6. Document Docker MCP server requirements (if any)
7. Avoid adding `.mcp.json` unless you have a truly custom MCP server

### When to Use Docker MCP vs Custom MCP

**Use Docker MCP Toolkit (Recommended)**:
- GitHub, GitLab, Bitbucket operations
- Browser automation and testing
- AWS, Azure, GCP cloud operations
- Database connections (Postgres, MySQL, MongoDB)
- Popular APIs (Stripe, Slack, Linear, etc.)

**Only use custom `.mcp.json` if**:
- Your plugin requires a proprietary internal MCP server
- No Docker MCP server exists for your use case
- You're developing a new MCP server for the community

## Contributing

See [CONTRIBUTING.md](../../CONTRIBUTING.md) for guidelines on contributing plugins to the Sati marketplace.

## License

MIT License - See root LICENSE file for details.
