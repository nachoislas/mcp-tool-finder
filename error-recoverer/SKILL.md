# Error Recoverer

Automatically diagnose and recover from errors during agent execution.

## Trigger

- On any execution error
- "fix this error"
- "why did it fail"
- Auto-trigger on tool failure

## What It Does

1. **Capture** full error context
2. **Classify** error type (syntax, runtime, network, config, permissions)
3. **Analyze** stack trace
4. **Suggest** fix
5. **Execute** recovery
6. **Verify** fix worked
7. **Log** pattern for learning

## Error Classification

| Type | Pattern | Recovery |
|------|---------|----------|
| `syntax` | Parse error, unexpected token | Fix syntax, retry |
| `runtime` | TypeError, ReferenceError | Analyze stack, fix logic |
| `network` | ECONNREFUSED, timeout | Retry with backoff |
| `config` | ENV missing, wrong value | Prompt/fill config |
| `permissions` | EACCES, EPERM | Fix permissions |
| `import` | Cannot find module | Install/declare dependency |
| `version` | Unsupported version | Upgrade/downgrade |

## Recovery Strategy

```
Error detected
         │
         ▼
   Capture context: error + stack + state
         │
         ▼
   Classify error type
         │
         ▼
   Lookup pattern in memory?
         │      │
         ▼      Yes
    No    ──→ Apply known fix
         │
         ▼
   Analyze stack trace
         │
         ▼
   Generate fix suggestion
         │
         ▼
   Execute + verify
         │
         ▼
   Success? → Log pattern
         │        Fail → escalate
```

## Memory Format

```json
{
  "error_pattern": "Cannot find module '*'",
  "fix": "npm install <module>",
  "success_rate": 0.95,
  "occurrence_count": 42
}
```

## Boundaries

- Max 3 retry attempts
- Timeout per retry: 30s
- Escalate after max retries
- Never modify user code unexpectedly