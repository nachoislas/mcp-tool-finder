---
name: mcp-finder
description: Find MCP (Model Context Protocol) servers. Use when user asks "find MCP server for X", "MCP server for database", "what MCP tools exist for web search", or needs external tools for an AI agent.
---

# Skill: MCP Finder

Find MCP servers from the awesome-mcp-servers collection.

## When to Use This Skill

- User asks "find MCP server for X"
- User needs external tools for their AI agent
- User wants to know what MCP servers exist
- User is building an AI agent and needs tool access

## Available MCP Servers

**Main source**: https://github.com/punkpeye/awesome-mcp-servers
**Alternative**: https://glama.ai/mcp/servers

## Usage

### Browse glama.ai (Recommended)

Visit https://glama.ai/mcp/servers - searchable catalog with:
- Server descriptions
- Transport types (stdio, SSE)
- Environment variables needed

### Search via GitHub

```bash
curl -s https://raw.githubusercontent.com/punkpeye/awesome-mcp-servers/main/README.md | grep -i "keyword"
```

## Common Categories

| Category | MCP Server |
|----------|-----------|
| Database | @modelcontextprotocol/server-postgres |
| Files | @modelcontextprotocol/server-filesystem |
| GitHub | @modelcontextprotocol/server-github |
| Web Search | @modelcontextprotocol/server-brave-search |
| Browser | @anthropic/mcp-server-puppeteer |
| Memory | @modelcontextprotocol/server-memory |

## Workflow

1. User describes what they need
2. Map to MCP category keyword
3. Search on glama.ai or awesome-mcp-servers
4. Present results with:
   - Server name and npm package
   - Transport type
   - Required env vars

## Setup Example

```bash
# Install
npm install -g @modelcontextprotocol/server-filesystem

# Add to MCP config
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem"]
    }
  }
}
```

## Notes

- MCP servers provide TOOLS to AI agents
- Skills provide INSTRUCTIONS (how-to use tools)
- Many require API keys (check env vars)
- stdio = local, SSE = remote

## Check & Install MCP Servers

### Verify Installation

```bash
npm list -g <package-name>
```

### Install MCP Server

```bash
npm install -g <package-name>
```

### Check Available Tools

The MCP config is typically in:
- Windows: `%APPDATA%\Code\default\user\mcp.json`
- macOS: `~/Library/Application Support/Code/User/mcp.json`
- Linux: `~/.config/Code/User/mcp.json`

### Quick Install & Test

```bash
# Install puppeteer for browser automation
npm install -g @anthropic/mcp-server-puppeteer

# Verify it's installed
npm list -g @anthropic/mcp-server-puppeteer
```

### MCP Server Status Check Script

```bash
# Check all common MCP dependencies
$packages = @("playwright", "puppeteer", "@anthropic/mcp-server-puppeteer")
foreach ($pkg in $packages) {
    $result = npm list -g $pkg 2>$null
    if ($LASTEXITCODE -eq 0) { Write-Host "[OK] $pkg" }
    else { Write-Host "[MISSING] $pkg" }
}
```

## MCP Server Categories

### Browser Automation

| Package | Purpose | Env Vars |
|---------|---------|---------|
| @anthropic/mcp-server-puppeteer | Chrome automation | None |
| @modelcontextprotocol/server-playwright | Playwright browser | None |

### Database

| Package | Purpose | Env Vars |
|---------|---------|---------|
| @modelcontextprotocol/server-postgres | PostgreSQL | DATABASE_URL |
| @modelcontextprotocol/server-sqlite | SQLite | DATABASE_PATH |

### Search & Web

| Package | Purpose | Env Vars |
|---------|---------|---------|
| @modelcontextprotocol/server-brave-search | Brave Web Search | BRAVE_API_KEY |
| @modelcontextprotocol/server-fetch | HTTP requests | None |

### Development

| Package | Purpose | Env Vars |
|---------|---------|---------|
| @modelcontextprotocol/server-filesystem | File operations | Allowed directories |
| @modelcontextprotocol/server-github | GitHub API | GITHUB_TOKEN |
| @modelcontextprotocol/server-memory | Vector storage | None |

## Auto-Install Workflow

When user needs a specific MCP server:

1. Check if already installed: `npm list -g <package>`
2. If missing, offer to install: `npm install -g <package>`
3. Provide MCP config snippet to add
4. Verify installation worked