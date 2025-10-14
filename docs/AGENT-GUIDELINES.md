# Agent Development Guidelines for Docker MCP

This guide explains how to create agents that effectively use Docker MCP Toolkit tools in the Sati Claude Code Marketplace.

## Understanding Agent Tool Access

Agents in Claude Code plugins can access tools through frontmatter configuration. When using Docker MCP Toolkit, tools are namespaced as `mcp__MCP_DOCKER__toolname`.

## Tool Naming Pattern

### Docker MCP Tools (Sati Standard)

**All MCP tools accessed through Docker MCP Toolkit use this pattern:**

```
mcp__MCP_DOCKER__<tool_name>
```

**Key Points**:
- Use `MCP_DOCKER` as the namespace (not the individual server name)
- Docker MCP Toolkit aggregates all servers under one namespace
- Tool names are case-sensitive and must match exactly

**Examples**:
- `mcp__MCP_DOCKER__get_pull_request` (from GitHub MCP Server)
- `mcp__MCP_DOCKER__search_code` (from GitHub MCP Server)
- `mcp__MCP_DOCKER__browser_navigate` (from Browser MCP Server)
- `mcp__MCP_DOCKER__browser_snapshot` (from Browser MCP Server)
- `mcp__MCP_DOCKER__CDKGeneralGuidance` (from AWS CDK MCP Server)
- `mcp__MCP_DOCKER__search_documentation` (from AWS Documentation MCP Server)

**Note**: If you see references to tools like `mcp__awslabs_cdk-mcp-server__CDKGeneralGuidance`, that's the old pattern for project-specific `.mcp.json` files. Sati uses Docker MCP Toolkit, so **always use** `mcp__MCP_DOCKER__` prefix

### Core Claude Code Tools

Standard tools available to all agents:
- `Bash` - Execute shell commands
- `Read` - Read files
- `Write` - Create files
- `Edit` - Modify files
- `Glob` - Find files by pattern
- `Grep` - Search file contents
- `TodoWrite` - Manage task lists
- `WebFetch` - Fetch web content
- `WebSearch` - Search the web

## Agent Frontmatter Configuration

### Basic Structure

```markdown
---
name: agent-name
description: Brief description of when to invoke this agent
tools: Read, Write, Bash, mcp__MCP_DOCKER__get_pull_request
model: sonnet
color: blue
---

# Agent Name

Your agent instructions...
```

### Frontmatter Fields

- **name**: Unique identifier for the agent (kebab-case)
- **description**: When Claude should invoke this agent (with examples)
- **tools**: Comma-separated list of allowed tools
- **model**: Model to use (sonnet, opus, haiku)
- **color**: Visual indicator in UI (blue, green, red, etc.)

## Specifying Docker MCP Tools

### Pattern 1: Specific Tools

List exact tools the agent needs:

```markdown
---
name: pr-reviewer
description: Reviews GitHub pull requests and provides feedback
tools: Read, Grep, mcp__MCP_DOCKER__get_pull_request, mcp__MCP_DOCKER__get_pull_request_files, mcp__MCP_DOCKER__get_pull_request_diff, mcp__MCP_DOCKER__add_issue_comment
model: opus
color: purple
---
```

### Pattern 2: Wildcard Access (Use Sparingly)

For agents that need broad MCP access:

```markdown
---
name: deployment-agent
description: Manages deployments across multiple services
tools: Read, Write, Bash, mcp__MCP_DOCKER__*
model: sonnet
color: orange
---
```

**Note**: Wildcard `*` grants access to all Docker MCP tools. Only use for agents that truly need broad access.

### Pattern 3: Core Tools + Selective MCP

Most agents should use this pattern:

```markdown
---
name: issue-analyzer
description: Analyzes GitHub issues and suggests solutions
tools: Read, Glob, Grep, mcp__MCP_DOCKER__get_issue, mcp__MCP_DOCKER__get_issue_comments, mcp__MCP_DOCKER__search_code
model: sonnet
color: blue
---
```

## Writing Agent Instructions

### Referencing MCP Tools

When instructing agents to use Docker MCP tools, be explicit:

```markdown
# Issue Analyzer Agent

You are an expert at analyzing GitHub issues and suggesting solutions.

## Available Docker MCP Tools

You have access to the following GitHub MCP tools:

- **get_issue**: Fetch issue details by number
- **get_issue_comments**: Retrieve all comments on an issue
- **search_code**: Search codebase for relevant code

## Workflow

1. **Fetch Issue**: Use `get_issue` to retrieve the issue details
2. **Read Comments**: Use `get_issue_comments` to understand discussion
3. **Search Code**: Use `search_code` to find relevant implementation
4. **Analyze**: Use standard tools (Read, Grep) to examine code
5. **Suggest**: Provide solution with code examples

## Example

When the user says "analyze issue #123":

1. Call `mcp__MCP_DOCKER__get_issue` with owner, repo, and issue number
2. Review the issue description and labels
3. Call `mcp__MCP_DOCKER__get_issue_comments` to see discussion
4. Use `mcp__MCP_DOCKER__search_code` to find related code
5. Use Read tool to examine relevant files
6. Provide comprehensive analysis and solution
```

### Handling Missing Tools

Instruct agents what to do if required MCP tools aren't available:

```markdown
## Prerequisites

This agent requires Docker MCP Toolkit with:
- **GitHub MCP Server** installed and authorized

If tools are not available, inform the user:
"This agent requires GitHub MCP Server. Please install it via Docker Desktop → Settings → MCP → GitHub."
```

## Complete Agent Examples

### Example 1: GitHub PR Review Agent

```markdown
---
name: pr-review-agent
description: Use this agent to review pull requests, analyze code changes, and provide constructive feedback. Invoke when user asks to review a PR, analyze changes, or check code quality in a pull request.
tools: Read, Grep, Glob, TodoWrite, mcp__MCP_DOCKER__get_pull_request, mcp__MCP_DOCKER__get_pull_request_files, mcp__MCP_DOCKER__get_pull_request_diff, mcp__MCP_DOCKER__add_issue_comment
model: opus
color: purple
---

# Pull Request Review Agent

You are an expert code reviewer with deep knowledge of software engineering best practices, security, performance, and maintainability.

## Available Docker MCP Tools

- **get_pull_request**: Fetch PR details (title, description, status)
- **get_pull_request_files**: List all changed files with stats
- **get_pull_request_diff**: Get the full unified diff
- **add_issue_comment**: Post review comments

## Review Process

1. **Fetch PR Details**
   ```
   Use mcp__MCP_DOCKER__get_pull_request with:
   - owner: repository owner
   - repo: repository name
   - pullNumber: PR number
   ```

2. **Analyze Changes**
   - Use `get_pull_request_files` to see what files changed
   - Use `get_pull_request_diff` to review the diff
   - Use Read tool to examine full file context when needed

3. **Review Criteria**
   - Code quality and maintainability
   - Security vulnerabilities
   - Performance implications
   - Test coverage
   - Documentation updates

4. **Provide Feedback**
   - Use TodoWrite to track review items
   - Structure feedback as: Issues, Suggestions, Praise
   - Use `add_issue_comment` to post review to PR

## Prerequisites

Requires Docker MCP Toolkit with GitHub MCP Server.

Install via: Docker Desktop → Settings → MCP → Install "GitHub MCP Server"
```

### Example 2: AWS CDK Helper Agent

```markdown
---
name: cdk-helper
description: Provides AWS CDK guidance, best practices, and code examples. Use when user asks about CDK patterns, infrastructure design, or needs help with AWS CDK constructs.
tools: Read, Write, Edit, WebSearch, mcp__MCP_DOCKER__CDKGeneralGuidance, mcp__MCP_DOCKER__ExplainCDKNagRule, mcp__MCP_DOCKER__CheckCDKNagSuppressions, mcp__MCP_DOCKER__search_documentation
model: sonnet
color: orange
---

# AWS CDK Helper Agent

You are an AWS CDK expert specializing in infrastructure as code best practices and AWS Well-Architected Framework principles.

## Available Docker MCP Tools

### AWS CDK MCP Server
- **CDKGeneralGuidance**: Get prescriptive CDK advice
- **ExplainCDKNagRule**: Explain specific CDK Nag security rules
- **CheckCDKNagSuppressions**: Verify Nag suppressions need review

### AWS Documentation MCP Server
- **search_documentation**: Search AWS docs for specific topics
- **read_documentation**: Fetch full AWS documentation pages

## Workflow

1. **Understand Request**
   - Identify if user needs patterns, debugging, or best practices

2. **Get CDK Guidance**
   ```
   Use mcp__MCP_DOCKER__CDKGeneralGuidance for:
   - Architecture recommendations
   - CDK patterns and constructs
   - Best practices
   ```

3. **Search Documentation**
   ```
   Use mcp__MCP_DOCKER__search_documentation when:
   - User needs service-specific details
   - Implementation examples required
   - API references needed
   ```

4. **Provide Solution**
   - Give working CDK code examples
   - Explain security implications
   - Reference Well-Architected principles

## Prerequisites

Requires Docker MCP Toolkit with:
- AWS CDK MCP Server
- AWS Documentation MCP Server

Install via: Docker Desktop → Settings → MCP
```

### Example 3: Browser Testing Agent

```markdown
---
name: browser-test-agent
description: Automates browser testing and web page interaction. Use when user needs to test web pages, capture screenshots, or automate browser workflows.
tools: TodoWrite, mcp__MCP_DOCKER__browser_navigate, mcp__MCP_DOCKER__browser_snapshot, mcp__MCP_DOCKER__browser_click, mcp__MCP_DOCKER__browser_type, mcp__MCP_DOCKER__browser_take_screenshot
model: sonnet
color: green
---

# Browser Testing Agent

You are a browser automation expert specializing in web testing and interaction.

## Available Docker MCP Tools

- **browser_navigate**: Navigate to URLs
- **browser_snapshot**: Capture accessibility snapshot for analysis
- **browser_click**: Click elements on page
- **browser_type**: Type into form fields
- **browser_take_screenshot**: Capture visual screenshots

## Testing Workflow

1. **Navigate to Page**
   ```
   Use mcp__MCP_DOCKER__browser_navigate with URL
   ```

2. **Analyze Page**
   ```
   Use mcp__MCP_DOCKER__browser_snapshot to:
   - Get page structure
   - Find interactive elements
   - Analyze accessibility
   ```

3. **Interact**
   ```
   Use browser_click and browser_type to:
   - Fill forms
   - Click buttons
   - Test workflows
   ```

4. **Capture Evidence**
   ```
   Use browser_take_screenshot for:
   - Visual regression testing
   - Bug reports
   - Documentation
   ```

## Prerequisites

Requires Docker MCP Toolkit with Browser MCP Server.

Install via: Docker Desktop → Settings → MCP → Install "Browser MCP Server"
```

## Best Practices

### ✅ DO

1. **List Required Tools Explicitly**: Specify exact MCP tools needed
2. **Document Prerequisites**: List required Docker MCP servers
3. **Provide Usage Examples**: Show how to call MCP tools
4. **Handle Missing Tools**: Gracefully inform user if tools unavailable
5. **Use TodoWrite**: Track multi-step agent workflows

### ❌ DON'T

1. **Don't Use Wildcards Unnecessarily**: Avoid `mcp__MCP_DOCKER__*` unless truly needed
2. **Don't Assume Tool Availability**: Always document prerequisites
3. **Don't Mix Patterns**: Be consistent with tool namespacing
4. **Don't Omit Tool Lists**: Always specify tools in frontmatter
5. **Don't Forget Core Tools**: Include Bash, Read, Write as needed

## Testing Your Agent

### Local Testing

1. **Install Required MCP Servers**
   ```
   Docker Desktop → Settings → MCP → Install servers
   ```

2. **Create Test Plugin**
   ```bash
   cp -r plugins/example-plugin plugins/test-agent
   # Add your agent to plugins/test-agent/agents/
   ```

3. **Install Locally**
   ```bash
   /plugin marketplace add ./
   /plugin install test-agent@sati-claude-marketplace
   ```

4. **Test Agent**
   - Trigger agent via natural language
   - Verify MCP tools are accessible
   - Check agent performs expected actions

### Troubleshooting

**"Tool not found" errors**:
- Verify MCP server installed in Docker Desktop
- Check tool name matches exactly (case-sensitive)
- Ensure `mcp__MCP_DOCKER__` prefix is correct

**Agent not invoked**:
- Check description clearly states when to use
- Add more specific examples
- Verify agent name is unique

**Permission errors**:
- Check MCP server is authorized (GitHub, etc.)
- Verify tool is listed in frontmatter `tools:` field

## Resources

- [Docker MCP Integration Guide](DOCKER-MCP-GUIDE.md)
- [Claude Code Agent Documentation](https://docs.claude.com/en/docs/claude-code/agents)
- [MCP Protocol Specification](https://modelcontextprotocol.io/)

---

**Maintained by:** Sati Technology DevTools Team
**Last Updated:** 2025-10-14
