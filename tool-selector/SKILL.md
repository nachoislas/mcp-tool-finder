---
name: tool-selector
description: Find the best tools for any task - both agent skills and MCP servers. Use when user says "I need to do X, what tools exist?", "what can help me with X?", or wants to discover both agent skills and MCP servers for a task.
---

# Skill: Tool Selector

Find the best tools for any task - orchestrates skill-finder and mcp-finder.

## When to Use This Skill

- User says "I need to do X, what tools exist?"
- User wants both skills and MCP servers for a task
- User is setting up a new AI agent workflow

## How It Works

1. Analyze user's request to identify the task
2. Run skill-finder (for behaviors/instructions)
3. Run mcp-finder (for external tools)
4. Combine and rank results

## Decision Guide

| Need | Use |
|------|-----|
| Agent needs to KNOW how to do something | skill-finder |
| Agent needs EXTERNAL tools | mcp-finder |
| Complete AI workflow | tool-selector |

## Skills vs MCP

| Type | Provides | Example |
|------|----------|---------|
| Skill | INSTRUCTIONS | "How to write tests" |
| MCP Server | TOOLS | Playwright browser |

## Complete Workflows

For complete AI workflows, install BOTH:

| Task | Install |
|------|---------|
| E2E testing | skill: testing + MCP: puppeteer |
| Database app | skill: sql-patterns + MCP: postgres |

## Notes

- Skills = agent "knowledge" (how to)
- MCP Servers = agent "tools" (what to use)
- Use both for complete workflows