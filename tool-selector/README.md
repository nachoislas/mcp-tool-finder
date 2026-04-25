# Tool Selector

Find the best tools for any AI agent task - both agent skills and MCP servers.

## Problem

When building AI agents, you need:
1. **Skills** - Instructions on how to do things
2. **MCP Servers** - Tools the agent can call

But finding the right ones is hard. This repo provides tools to discover both.

## Solution

A discovery system with 3 skills:

| Skill | What it does | Use when |
|-------|-------------|----------|
| skill-finder | Searches skills.sh catalog | You need "how-to" instructions |
| mcp-finder | Searches awesome-mcp-servers | You need external tools |
| tool-selector | Uses both | You need complete workflows |

## Installation

```bash
# Install via npx skills
npx skills add your-name/tool-selector --skill skill-finder --skill mcp-finder --skill tool-selector
```

## Usage

### Find Skills

```bash
npx skills find react
# → react-best-practices, react-native-skills, etc.
```

### Find MCP Servers

Visit https://glama.ai/mcp/servers and search for:
- "database" → PostgreSQL, SQLite servers
- "browser" → Puppeteer, Playwright servers
- "search" → Brave Search server

### Complete Workflows

For E2E testing, install both:
- Skill: testing patterns
- MCP: @anthropic/mcp-server-puppeteer

## Skills Structure

```
tool-selector/
├── skill-finder/     # Agent skills discovery
│   └── SKILL.md
├── mcp-finder/      # MCP servers discovery
│   └── SKILL.md
└── tool-selector/   # Orchestrator
    └── SKILL.md
```

## Contributing

1. Fork the repo
2. Add your improvements
3. Submit a PR

## License

MIT