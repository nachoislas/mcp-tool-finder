---
name: mcp-finder
description: Find MCP (Model Context Protocol) servers. Use when user asks "find MCP server for X", "MCP server for database", "what MCP tools exist for web search", or needs external tools for an AI agent.
---

# Skill: MCP Finder

Find MCP servers from the awesome-mcp-servers collection and glama.ai catalog.

**Fast path**: Check `reference/top-servers.md` first. If the user's domain matches a listed server, use that directly — no search needed.

## When to Use

- User asks "find MCP server for X"
- User needs external tools for their AI agent (browser, database, files, search)
- User wants to know what MCP servers exist
- User is building an AI agent and needs tool access
- User asks how to give Claude access to GitHub / Postgres / web browsing

## When NOT to Use

- User needs agent instructions or how-to knowledge — use `skill-finder` instead
- User already knows the MCP package and just needs an install command
- User is asking about agent behaviors, not tool access
- Task is purely in-context reasoning with no external system access needed

## Workflow

### Step 1: Fast-path lookup

Check `reference/top-servers.md`. If the user's domain matches, present that server directly.

### Step 2: Search the catalog

Browse https://glama.ai/mcp/servers — searchable with filters for transport type, env vars, and category.

Or grep the community list:
```bash
curl -s https://raw.githubusercontent.com/punkpeye/awesome-mcp-servers/main/README.md | grep -i "keyword"
```

### Step 3: Handle no results

If glama.ai is unreachable or returns nothing:
1. Try a different keyword (e.g. `"browser"` instead of `"chrome"`)
2. Check `reference/top-servers.md` for the closest match
3. Search npm directly: `npm search mcp-server-[keyword]`

### Step 4: Present results

Show results with:
- Server name and npm package
- Transport type (`stdio` = local, `SSE` = remote)
- Required environment variables (critical — note if API key needed)

### Step 5: Install

```bash
npm install -g <package-name>
```

### Step 6: Verify installation

Always verify before asking user to update their config:

```bash
npm list -g <package-name>
# Expected: <package-name>@<version>
```

If it fails: `npm install -g <package-name> --force`

### Step 7: Add to MCP config

```json
{
  "mcpServers": {
    "server-name": {
      "command": "npx",
      "args": ["-y", "<package-name>"]
    }
  }
}
```

MCP config file locations:
- **Windows**: `%APPDATA%\Code\User\mcp.json`
- **macOS**: `~/Library/Application Support/Code/User/mcp.json`
- **Linux**: `~/.config/Code/User/mcp.json`

## Verify Multiple Packages (PowerShell)

```powershell
$packages = @("playwright", "puppeteer", "@anthropic/mcp-server-puppeteer")
foreach ($pkg in $packages) {
    $result = npm list -g $pkg 2>$null
    if ($LASTEXITCODE -eq 0) { Write-Host "[OK] $pkg" }
    else { Write-Host "[MISSING] $pkg" }
}
```

## Notes

- MCP servers provide **TOOLS** to AI agents (execution, access, data)
- Skills provide **INSTRUCTIONS** (how to use those tools)
- `stdio` transport = runs locally; `SSE` transport = remote endpoint
- Many servers require API keys — always check env vars before recommending