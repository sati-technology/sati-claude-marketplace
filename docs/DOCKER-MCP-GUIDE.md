# Docker MCP Toolkit Integration Guide

This guide explains how Sati Technology uses Docker MCP Toolkit for managing MCP servers in Claude Code.

## What is Docker MCP Toolkit?

Docker MCP Toolkit is a gateway that simplifies MCP server management by:

- **Single Configuration**: One `MCP_DOCKER` entry connects to all MCP servers
- **Containerized Servers**: 200+ pre-built, isolated MCP servers
- **One-Click Deployment**: Install servers through Docker Desktop UI
- **Zero Manual Setup**: No dependency management or runtime configuration
- **Built-in Security**: Resource limits, no filesystem access by default

## Architecture

```
Claude Code
    ↓
MCP_DOCKER (single connection)
    ↓
Docker MCP Toolkit Gateway (port 8811)
    ↓
├── GitHub MCP Server (container)
├── Browser MCP Server (container)
├── AWS CDK MCP Server (container)
├── Context7 MCP Server (container)
└── Custom MCP Servers (containers)
```

## Configuration

### Global Configuration

Claude Code connects to Docker MCP Toolkit via a single entry in `~/.claude/settings.json`:

```json
{
  "mcpServers": {
    "MCP_DOCKER": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "alpine/socat",
        "STDIO",
        "TCP:host.docker.internal:8811"
      ]
    }
  }
}
```

### Per-Project Configuration

Projects can specify additional MCP servers in `.mcp.json`:

```json
{
  "mcpServers": {
    "project-specific-server": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@your-org/custom-mcp-server"]
    }
  }
}
```

**Important**: Docker MCP Toolkit is managed globally. Project `.mcp.json` files are for project-specific MCP servers only.

## Best Practices for Sati Plugins

### ✅ DO: Use Docker MCP Toolkit

- **Leverage existing servers**: GitHub, Browser, AWS/CDK, Docker Hub, etc.
- **Reference tools in commands**: Write commands that use MCP tools
- **Document required servers**: List which Docker MCP servers your plugin needs

### ❌ DON'T: Include `.mcp.json` in Plugins

- **Avoid duplicate configurations**: Docker MCP handles most MCP servers
- **No `.mcp.json` in plugins**: Unless absolutely necessary for custom servers
- **Use global setup**: Team members install MCP servers via Docker Desktop

## Example Plugin Using Docker MCP

### Plugin Structure

```
deployment-plugin/
├── .claude-plugin/
│   └── plugin.json
├── commands/
│   └── deploy.md
├── agents/
│   └── deploy-agent.md
└── README.md
```

### Command Using GitHub MCP

`commands/deploy.md`:

```markdown
---
name: deploy
description: Deploy to production via GitHub Actions
---

# Deploy Command

Triggers a production deployment using GitHub Actions workflow.

## Usage

/deploy [environment]

## What This Does

1. Checks the current branch via GitHub MCP
2. Creates a deployment via GitHub Actions
3. Monitors the deployment status
4. Reports results

This command requires:
- Docker MCP Toolkit with GitHub MCP Server enabled
- GitHub authentication configured in Docker Desktop
```

### Plugin Documentation

`README.md`:

```markdown
# Deployment Plugin

Automates deployment workflows using GitHub Actions.

## Requirements

### Docker MCP Toolkit

This plugin requires Docker MCP Toolkit with the following servers:

- **GitHub MCP Server** - For repository and Actions API access

### Installation

1. Install Docker MCP Toolkit (if not already installed)
2. Enable GitHub MCP Server in Docker Desktop:
   - Open Docker Desktop
   - Go to Settings → MCP
   - Install "GitHub MCP Server"
   - Authorize with your GitHub account

3. Install this plugin:
   ```bash
   /plugin install deployment-plugin@sati-marketplace
   ```

## Commands

- `/deploy [env]` - Deploy to specified environment
```

## Installing MCP Servers

### Via Docker Desktop (Recommended)

1. Open Docker Desktop
2. Navigate to **Settings → MCP** (or search "MCP" in settings)
3. Browse available MCP servers
4. Click **Install** on desired servers
5. Authorize with required credentials (GitHub, etc.)

### Available Sati-Recommended Servers

- **GitHub** - Repository management, PRs, Issues, Actions
- **Browser** - Web automation and testing
- **AWS CDK** - Infrastructure as code guidance
- **Docker Hub** - Container registry operations
- **Context7** - Documentation fetching for popular libraries
- **Sequential Thinking** - Advanced reasoning and planning

## Security Benefits

Docker MCP Toolkit provides built-in security:

- **Isolation**: Each MCP server runs in its own container
- **Resource Limits**: 1 CPU, 2GB RAM per server
- **No Filesystem Access**: Servers can't access host files by default
- **Image Signing**: Verified and attested container images
- **SBOM**: Software Bill of Materials for transparency

## Troubleshooting

### "MCP Server Not Found"

**Problem**: Plugin references MCP tools that aren't available.

**Solution**:
1. Check Docker Desktop → Settings → MCP
2. Verify required servers are installed and running
3. Restart Claude Code if needed

### "Permission Denied"

**Problem**: MCP server needs authorization.

**Solution**:
1. Open Docker Desktop → Settings → MCP
2. Find the server and click **Authorize**
3. Complete OAuth flow

### Custom MCP Servers

If your plugin truly needs a custom MCP server:

1. **Publish to Docker Hub**: Create a containerized MCP server
2. **Submit to Docker MCP Catalog**: Make it available to all users
3. **Document installation**: Provide clear setup instructions

Only create custom servers for functionality not available in existing Docker MCP servers.

## Migration Guide

### From Individual MCP Servers

If your team previously managed individual MCP servers:

**Before** (multiple configurations):
```json
{
  "mcpServers": {
    "github": { "command": "npx", "args": ["@github/mcp-server"] },
    "browser": { "command": "npx", "args": ["@browser/mcp-server"] },
    "aws-cdk": { "command": "uvx", "args": ["awslabs.cdk-mcp-server"] }
  }
}
```

**After** (single Docker MCP):
```json
{
  "mcpServers": {
    "MCP_DOCKER": {
      "command": "docker",
      "args": ["run", "-i", "--rm", "alpine/socat", "STDIO", "TCP:host.docker.internal:8811"]
    }
  }
}
```

Then install servers via Docker Desktop UI.

## Resources

- [Docker MCP Toolkit Documentation](https://docs.docker.com/ai/mcp-catalog-and-toolkit/toolkit/)
- [Docker MCP Catalog](https://docs.docker.com/ai/mcp-catalog-and-toolkit/)
- [Model Context Protocol Specification](https://modelcontextprotocol.io/)

---

**Maintained by:** Sati Technology DevTools Team
**Last Updated:** 2025-10-14
