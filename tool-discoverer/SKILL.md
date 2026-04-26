# Tool Discoverer

Find the right MCP server or skill for a given task via semantic search.

## Trigger

- "what tool for..."
- "find tool"
- "need to [task]"
- Auto-trigger during discovery phase

## What It Does

1. **Parse** the user task
2. **Extract** required capabilities
3. **Search** registry semantically
4. **Rank** by match score
5. **Recommend** best tool with install command

## Capabilities taxonomy

```
Task: "connect to postgres"
         │
         ▼
   Capabilities needed:
   - database:postgres
   - connection:pool
   - query:sql
         │
         ▼
   Search registry
```

## Registry Schema

```json
{
  "tools": [
    {
      "name": "@modelcontextprotocol/postgres-server",
      "description": "PostgreSQL database server",
      "capabilities": ["database:postgres", "query:sql", "connection:pool"],
      "install_cmd": "npm i -g @modelcontextprotocol/postgres-server",
      "rank": 9.5
    }
  ]
}
```

## Search Strategy

1. **Exact match** → capability matches exactly
2. **Fuzzy match** → partial capability match
3. **Semantic** → embeddings similarity
4. **Fallback** → keyword search

## Ranking Score

```
score = (capability_match * 0.5) + (popularity * 0.2) + (recency * 0.2) + (success_rate * 0.1)
```

## Output Format

```
Recommended: @modelcontextprotocol/postgres-server

Why: Matches database:postgres, query:sql

Install:
  npm i -g @modelcontextprotocol/postgres-server

Verify:
  npx mcpo-server --help
```

## Boundaries

- Only recommend known/verified tools
- Include install + verify commands
- Show ranking rationale briefly