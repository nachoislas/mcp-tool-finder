# Top MCP Servers by Domain

Use this as a fast-path when glama.ai is unreachable or `npx` search returns nothing.

## Browser & Web

| Package | Purpose | Transport | Env Vars Required |
|---------|---------|-----------|------------------|
| `@anthropic/mcp-server-puppeteer` | Chrome automation | stdio | None |
| `@modelcontextprotocol/server-playwright` | Playwright multi-browser | stdio | None |
| `@modelcontextprotocol/server-fetch` | HTTP GET/POST requests | stdio | None |

## Database

| Package | Purpose | Transport | Env Vars Required |
|---------|---------|-----------|------------------|
| `@modelcontextprotocol/server-postgres` | PostgreSQL read/write | stdio | `DATABASE_URL` |
| `@modelcontextprotocol/server-sqlite` | SQLite local DB | stdio | `DATABASE_PATH` |

## Search

| Package | Purpose | Transport | Env Vars Required |
|---------|---------|-----------|------------------|
| `@modelcontextprotocol/server-brave-search` | Brave web search | stdio | `BRAVE_API_KEY` |

## Files & Filesystem

| Package | Purpose | Transport | Env Vars Required |
|---------|---------|-----------|------------------|
| `@modelcontextprotocol/server-filesystem` | Read/write local files | stdio | Allowed directories (arg) |

## GitHub & Dev

| Package | Purpose | Transport | Env Vars Required |
|---------|---------|-----------|------------------|
| `@modelcontextprotocol/server-github` | GitHub repos, PRs, issues | stdio | `GITHUB_TOKEN` |

## Memory & Storage

| Package | Purpose | Transport | Env Vars Required |
|---------|---------|-----------|------------------|
| `@modelcontextprotocol/server-memory` | Persistent vector memory | stdio | None |

## Fallback Path

If glama.ai is unreachable or no match found:

1. Grep the awesome-mcp-servers README:
   ```bash
   curl -s https://raw.githubusercontent.com/punkpeye/awesome-mcp-servers/main/README.md | grep -i "keyword"
   ```
2. Check this file for a close match
3. Search npm directly: `npm search mcp-server-[keyword]`
4. Tell the user to browse https://glama.ai/mcp/servers manually

## Verification After Install

Always verify before recommending the user adds it to their config:

```bash
npm list -g <package-name>
# Should show: <package-name>@<version>
```

If it fails, try: `npm install -g <package-name> --force`
