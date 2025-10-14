# Docker MCP Toolkit Integration Guide

This guide explains how Sati Technology uses Docker MCP Toolkit for managing MCP servers in Claude Code.

## What is Docker MCP Toolkit?

Docker MCP Toolkit simplifies MCP server management by providing:

- **200+ Pre-built Servers**: GitHub, Browser, AWS, databases, and more
- **One-Click Installation**: Install servers through Docker Desktop UI
- **Automatic Configuration**: No manual setup or dependency management
- **Built-in Security**: Containerized, resource-limited, isolated servers

## Setup

### Prerequisites

- **Docker Desktop** installed and running
- **Claude Code** installed

### Installing MCP Servers

1. **Open Docker Desktop**
2. **Navigate to Settings → MCP**
   - Or search for "MCP" in the settings search bar
3. **Browse Available Servers**
   - View 200+ pre-built MCP servers
4. **Click Install** on desired servers
5. **Authorize** when prompted (GitHub, AWS, etc.)

That's it! Claude Code will automatically connect to all installed MCP servers.

## Recommended Servers for Sati

- **GitHub** - Repository management, PRs, Issues, Actions
- **Browser** - Web automation and testing
- **AWS CDK** - Infrastructure as code guidance
- **Docker Hub** - Container registry operations
- **Context7** - Documentation for popular libraries

## Using MCP Tools in Plugins

### In Commands

Reference MCP functionality in command documentation:

```markdown
---
name: deploy
description: Deploy via GitHub Actions
---

# Deploy Command

This command uses GitHub MCP Server to trigger deployments.

## Requirements
- Docker Desktop with GitHub MCP Server installed
```

### In Agents

Specify MCP tools in agent frontmatter:

```markdown
---
name: pr-reviewer
tools: Read, Grep, mcp__MCP_DOCKER__get_pull_request
---

# PR Review Agent

Reviews pull requests using GitHub MCP tools.
```

See [Agent Development Guidelines](AGENT-GUIDELINES.md) for complete details.

### In Plugin Documentation

Always document which MCP servers your plugin requires:

```markdown
## Requirements

### Docker MCP Toolkit

This plugin requires:
- **GitHub MCP Server** - For PR and issue operations

### Installation

1. Install Docker Desktop and enable MCP Toolkit
2. Install GitHub MCP Server via Docker Desktop → Settings → MCP
3. Install this plugin: `/plugin install your-plugin@sati-marketplace`
```

## Best Practices

### ✅ DO

- **Use Docker MCP Toolkit** for all external integrations
- **Document required servers** in plugin README
- **Link to official docs** for setup instructions

### ❌ DON'T

- **Don't include `.mcp.json`** in plugins (Docker MCP handles it)
- **Don't create custom servers** unless truly necessary
- **Don't document manual configuration** (Docker Desktop handles it)

## Troubleshooting

### MCP Tools Not Available

**Solution**: Open Docker Desktop → Settings → MCP and verify required servers are installed and running.

### Authorization Needed

**Solution**: Open Docker Desktop → Settings → MCP, find the server, and click **Authorize**.

### Tools Not Working After Install

**Solution**: Restart Claude Code to pick up newly installed MCP servers.

## Official Documentation

For complete Docker MCP Toolkit documentation, see:

- **[Docker MCP Toolkit Docs](https://docs.docker.com/ai/mcp-catalog-and-toolkit/toolkit/)** - Official setup and usage guide
- **[Docker MCP Catalog](https://docs.docker.com/ai/mcp-catalog-and-toolkit/)** - Browse all available servers
- **[MCP Protocol Spec](https://modelcontextprotocol.io/)** - Technical protocol details

---

**Maintained by:** Sati Technology DevTools Team
**Last Updated:** 2025-10-14
