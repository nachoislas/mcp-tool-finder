# MCP Database Connector

Connect to databases (PostgreSQL, MySQL, SQLite, MSSQL) via MCP servers.

## Trigger

- "connect to database"
- "query postgres"
- "need database tool"
- Auto-trigger when task involves DB

## Supported Databases

| Database | MCP Server | Install |
|----------|-----------|---------|
| PostgreSQL | `@modelcontextprotocol/server-postgres` | `npx -y @modelcontextprotocol/server-postgres postgresql://...` |
| SQLite | `@modelcontextprotocol/server-sqlite` | `npx -y @modelcontextprotocol/server-sqlite --url path/to/db` |
| MySQL | `@modelcontextprotocol/server-mysql` | `npx -y @modelcontextprotocol/server-mysql` |
| Universal | `@adevguide/mcp-database-server` | `npm i -g @adevguide/mcp-database-server` |

## Connection Patterns

### PostgreSQL
```bash
npx -y @modelcontextprotocol/server-postgres "postgresql://user:pass@localhost/mydb"
```

### SQLite
```bash
npx -y @modelcontextprotocol/server-sqlite --url ./data.db
```

### Universal (multi-db)
```bash
mcp-server --url postgres://localhost/app --url sqlite:analytics.db
```

## Schema Discovery

Auto-discovers:
- Tables and columns
- Indexes and constraints
- Foreign key relationships
- Table statistics

## Safety Controls

- Read-only by default
- Configurable allow/deny rules
- Query timeout (default 30s)
- Row limit (default 100)

## Configuration

```json
{
  "databases": {
    "postgres": {
      "url": "postgresql://localhost/mydb",
      "readOnly": true,
      "rowLimit": 1000
    }
  }
}
```

## Boundaries

- Never execute destructive writes without --allow-write
- Timeout long queries
- Cache schema for performance