---
name: tool-selector
description: Find the best tools for any task - both agent skills and MCP servers. Use when user says "I need to do X, what tools exist?", "what can help me with X?", or wants to discover both agent skills and MCP servers for a task.
---

# Skill: Tool Selector

Find the best tools for any task — orchestrates `skill-finder` and `mcp-finder` to deliver a complete recommendation.

**Fast path**: Check `reference/domain-pairs.md` first. If the user's task matches a listed domain, use that table directly — no search needed.

## When to Use

- User says "I need to do X, what tools exist?"
- User wants both skills and MCP servers for a task
- User is setting up a new AI agent workflow from scratch
- User is unsure whether they need a skill, an MCP server, or both

## When NOT to Use

- User specifically asks only about **skills** — use `skill-finder` directly
- User specifically asks only about **MCP servers** — use `mcp-finder` directly
- User already has their tooling set up and just needs implementation help
- The task is a simple coding question with no discovery needed

## Decision Guide

| Need | Use |
|------|-----|
| Agent needs to KNOW how to do something | `skill-finder` |
| Agent needs EXTERNAL tools (browser, DB, files) | `mcp-finder` |
| Complete AI workflow setup | `tool-selector` (this skill) |

## Skills vs MCP Servers

| Type | Provides | Example |
|------|----------|---------|
| **Skill** | Instructions / knowledge | "How to write integration tests" |
| **MCP Server** | External tool access | Playwright browser, Postgres DB |

## Workflow

### Step 1: Fast-path lookup

Check `reference/domain-pairs.md`. If the user's task matches:
- Present the recommended skill + MCP pair directly
- Skip Steps 2–3

### Step 2: Search (if no fast-path match)

Run both in parallel:
- `skill-finder`: `npx skills find [keyword]`
- `mcp-finder`: search https://glama.ai/mcp/servers for [keyword]

### Step 3: Combine & rank results

Merge results using this priority:
1. **Exact domain match** — highest confidence
2. **High install count** (skills) / **official packages** (MCP) — well-tested
3. **No env vars required** — lower friction for users

Discard results that are clearly off-topic (different domain, deprecated packages).

### Step 4: Present recommendation

Format the output as:
```
## Recommended for [Task]

**Skill**: `@owner/skill-name` — [brief description]
Install: npx skills add owner/repo@skill -g -y

**MCP Server**: `package-name` — [brief description]
Env vars: [NONE or list]
Install: npm install -g package-name

**Verify install**: npm list -g package-name
```

### Step 5: Handle no results

If both finders return nothing:
1. Try a broader keyword
2. Fall back to `reference/domain-pairs.md` for the closest match
3. Suggest the user browse https://skills.sh and https://glama.ai/mcp/servers

## Notes

- Skills = agent **knowledge** (how to think and act)
- MCP Servers = agent **tools** (what to execute or access)
- Use both for complete, production-ready agent workflows
- Always include a verification step after install recommendations