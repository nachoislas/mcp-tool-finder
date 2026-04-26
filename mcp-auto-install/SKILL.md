# MCP Auto Install

Auto-install and configure MCP servers dynamically during agent execution.

## Trigger

- "install MCP server"
- "provision tool"
- "setup server"
- "need [server-name]"

## What It Does

1. **Parse** the MCP server name/requirement
2. **Check** if already installed
3. **Fetch** install command from registry
4. **Install** via npm/docker
5. **Configure** env vars
6. **Verify** installation works
7. **Register** in active tools

## Flow

```
User: "need postgres server"
         │
         ▼
   Parse: @modelcontextprotocol/postgres-server
         │
         ▼
   Check installed? → No
         │
         ▼
   Fetch install: npx @modelcontextprotocol/...
         │
         ▼
   Install + configure
         │
         ▼
   Verify: can connect?
         │
         ▼
   Register as active
```

## Config Schema

```json
{
  "mcp_servers": {
    "postgres": {
      "package": "@modelcontextprotocol/postgres-server",
      "install_cmd": "npm install -g @modelcontextprotocol/postgres-server",
      "env_vars": ["DATABASE_URL"],
      "verify_cmd": "psql -c 'SELECT 1'"
    }
  }
}
```

## Error Handling

- **Install fails**: Try alternative package or skip
- **Config missing**: Prompt user for missing vars
- **Verify fails**: Log error, suggest fix

## Boundaries

- Only install from known MCP registries
- Never install unverified packages
- Timeout: 120s per install