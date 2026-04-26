# Context Manager

Optimize and manage context window during long agent sessions. Prevents context rot.

## Trigger

- "optimize context"
- "reduce context"
- "summary"
- Auto-trigger when context > 70%

## What It Does

1. **Measure** current context usage
2. **Identify** redundant content
3. **Compress** non-essential info
4. **Preserve** critical state
5. **Summarize** completed work

## Context Tiers

### Tier 1: Keep Always (essential)
- Current task goals
- Active plan/PROJECT.md
- Critical config

### Tier 2: Summarize (important)
- Completed subtasks → 1-line summaries
- Research findings → Key insights only
- Tool outputs → Critical results only

### Tier 3: Drop (can rebuild)
- Verbose explanations
- Redundant retries
- Old verification logs

## Compression Rules

```
Before: "I tried three approaches to solve this..."
After:  "Attempts: 1) X failed (reason), 2) Y succeeded"
```

```
Before: "[full research output]"
After:  "[research]: Key insights X, Y, Z"
```

```
Before: long stack trace
After:  "[stack]: TypeError at line N - undefined property"
```

## When to Trigger

- Context > 70% (warning)
- Context > 85% (action required)
- Before new complex phase

## Boundaries

- Never drop user requests
- Preserve file paths
- Keep active plan reference