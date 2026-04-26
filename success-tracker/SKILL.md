# Success Tracker

Track tool execution success rates for learning.

## Trigger

- "track success"
- "log result"
- Auto-trigger after execution

## What It Does

1. **Record** execution result
2. **Calculate** success rate
3. **Update** tool rankings
4. **Identify** failure patterns

## Memory Schema

```json
{
  "executions": [
    {
      "id": "exec_001",
      "tool": "@modelcontextprotocol/server-postgres",
      "task": "query database",
      "success": true,
      "duration_ms": 234,
      "tokens": 1500,
      "timestamp": "2026-01-15T10:30:00Z"
    }
  ],
  "tool_stats": {
    "@modelcontextprotocol/server-postgres": {
      "total_runs": 42,
      "successes": 38,
      "success_rate": 0.905,
      "avg_duration_ms": 250,
      "avg_tokens": 1400
    }
  }
}
```

## Success Rate Calculation

```
success_rate = successes / total_runs

weighted_score = (success_rate * 0.6) + 
                 (1 / avg_duration_normalized * 0.2) + 
                 (1 / tokens_normalized * 0.2)
```

## Failure Patterns

```json
{
  "error_type": "ECONNREFUSED",
  "tool": "@modelcontextprotocol/server-postgres",
  "count": 3,
  "last_occurrence": "2026-01-14T16:00:00Z",
  "suggestion": "Check if database is running"
}
```

## Tracking Events

- Tool execution start
- Tool execution end (success/fail)
- Error occurrence
- Performance metrics

## Boundaries

- Persist to Supabase or local
- Aggregate daily/weekly
- Never log sensitive data