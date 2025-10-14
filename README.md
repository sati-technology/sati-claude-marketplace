# Sati Technology - Claude Code Marketplace

Official plugin marketplace for Sati Technology's Claude Code extensions. This marketplace provides custom commands, agents, hooks, and MCP integrations tailored for our development workflows.

## 🚀 Quick Start

### Install the Marketplace

```bash
/plugin marketplace add sati-technology/sati-claude-marketplace
```

### Browse Available Plugins

```bash
/plugin
```

Select "Browse Plugins" to see all available Sati plugins.

### Install a Plugin

```bash
/plugin install plugin-name@sati-marketplace
```

## 📦 Available Plugins

### Example Plugin
**Status:** ✅ Active
**Version:** 1.0.0
**Category:** Example

Example plugin demonstrating marketplace structure. Use this as a template for creating new plugins.

**Installation:**
```bash
/plugin install example-plugin@sati-marketplace
```

---

## 🏗️ Plugin Categories

- **Development** - Core development tools and workflows
- **DevOps** - Deployment, CI/CD, and infrastructure automation
- **Security** - Security scanning, compliance, and audit tools
- **Productivity** - Code quality, documentation, and team workflows
- **Integration** - Third-party service integrations and APIs

## 🔧 For Sati Team Members

### Automatic Installation

Add this to your project's `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "sati-marketplace": {
      "source": {
        "source": "github",
        "repo": "sati-technology/sati-claude-marketplace"
      }
    }
  },
  "enabledPlugins": {
    "example-plugin@sati-marketplace": true
  }
}
```

When team members trust the repository folder, plugins install automatically.

## 📝 Contributing

We welcome contributions from the Sati team! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Quick Plugin Creation

1. **Copy the example plugin:**
   ```bash
   cp -r plugins/example-plugin plugins/your-plugin-name
   ```

2. **Update plugin metadata:**
   - Edit `plugins/your-plugin-name/.claude-plugin/plugin.json`
   - Update name, description, and version

3. **Add to marketplace:**
   - Edit `.claude-plugin/marketplace.json`
   - Add your plugin to the `plugins` array

4. **Submit a PR:**
   - Create a branch: `git checkout -b plugin/your-plugin-name`
   - Commit changes: `git commit -am "Add your-plugin-name"`
   - Push and create PR

## 🔐 Private Repository

This is a private marketplace for Sati Technology. Access requires:
- Sati GitHub organization membership
- Configured Git authentication (SSH keys or tokens)

## 🐳 Docker MCP Integration

Sati uses **Docker MCP Toolkit** for managing MCP servers. This provides:

- **Single Configuration**: One `MCP_DOCKER` connection to all servers
- **200+ Pre-built Servers**: GitHub, Browser, AWS/CDK, and more
- **One-Click Installation**: Via Docker Desktop UI
- **Built-in Security**: Containerized, resource-limited, isolated

### Quick Setup

1. **Install Docker MCP Toolkit** (included with Docker Desktop)
2. **Enable MCP Servers** in Docker Desktop → Settings → MCP
3. **Start Building Plugins** that leverage MCP tools

See [Docker MCP Integration Guide](docs/DOCKER-MCP-GUIDE.md) for detailed documentation.

## 📚 Documentation

- **[Docker MCP Integration Guide](docs/DOCKER-MCP-GUIDE.md)** - Sati's MCP setup
- [Claude Code Plugin Guide](https://docs.claude.com/en/docs/claude-code/plugins)
- [Plugin Marketplaces](https://docs.claude.com/en/docs/claude-code/plugin-marketplaces)
- [Plugin Reference](https://docs.claude.com/en/docs/claude-code/plugins-reference)
- [Docker MCP Toolkit Docs](https://docs.docker.com/ai/mcp-catalog-and-toolkit/toolkit/)

## 🆘 Support

- **Issues:** [GitHub Issues](https://github.com/sati-technology/sati-claude-marketplace/issues)
- **Discussions:** [GitHub Discussions](https://github.com/sati-technology/sati-claude-marketplace/discussions)
- **Internal:** Contact the DevTools team

## 📄 License

MIT License - See [LICENSE](LICENSE) for details.

---

**Maintained by:** Sati Technology DevTools Team
**Last Updated:** 2025-10-14
