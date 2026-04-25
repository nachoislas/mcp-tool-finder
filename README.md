# 🔍 MCP Tool Finder

> A collection of Claude Code skills to help AI agents discover, install, and configure the right tools for any task — covering both agent skills and MCP servers.

---

## What is this?

When building AI agent workflows, two questions always come up:

1. **"What skills exist for X?"** — Agent skills provide *instructions* (how to think, plan, and act for a task)
2. **"What MCP server do I need for X?"** — MCP servers provide *tools* (browser access, databases, file systems, APIs)

This repo contains three Claude Code skills that answer both questions instantly:

| Skill | What it does |
|-------|-------------|
| [`skill-finder`](./skill-finder/) | Search the public skills catalog via `npx skills` |
| [`mcp-finder`](./mcp-finder/) | Search the MCP server ecosystem via glama.ai and awesome-mcp-servers |
| [`tool-selector`](./tool-selector/) | Orchestrator — run both and deliver a combined recommendation |

---

## Quick Start

### Install all three skills globally

```bash
npx skills add nachoislas/mcp-tool-finder@skill-finder -g -y
npx skills add nachoislas/mcp-tool-finder@mcp-finder -g -y
npx skills add nachoislas/mcp-tool-finder@tool-selector -g -y
```

### Use them

Just ask your AI agent:

- *"Find me a skill for React testing"*
- *"What MCP server do I need to access PostgreSQL?"*
- *"I need to build a GitHub automation bot — what tools exist?"*

The skills handle the discovery, ranking, and install commands for you.

---

## How it Works

```
User: "I need to build a browser scraper"
         │
         ▼
   tool-selector
   ┌──────────────────────────────────────┐
   │ 1. Check domain-pairs reference      │  ← fast path (no search needed)
   │ 2. Run skill-finder → web-scraper    │
   │ 3. Run mcp-finder → puppeteer        │
   │ 4. Combine + rank results            │
   │ 5. Present: skill + MCP + install    │
   └──────────────────────────────────────┘
```

Each skill has a **fast-path reference file** (curated top picks by domain) so common requests return instantly without network calls.

---

## Project Structure

```
mcp-tool-finder/
├── skill-finder/
│   ├── SKILL.md                    # Core skill instructions
│   └── reference/
│       └── top-skills.md           # Curated skills by domain
├── mcp-finder/
│   ├── SKILL.md
│   └── reference/
│       └── top-servers.md          # Curated MCP servers by domain
└── tool-selector/
    ├── SKILL.md
    └── reference/
        └── domain-pairs.md         # Domain → skill + MCP pairs table
```

---

## Contributing

**This project thrives on community contributions.** The curated reference files are only as good as the community keeps them — outdated packages, missing domains, and wrong env vars hurt everyone.

### Ways to contribute

#### 🗂️ Update reference files (easiest)

The most impactful contributions are keeping the reference tables accurate:

- Add a new domain or use-case to [`tool-selector/reference/domain-pairs.md`](./tool-selector/reference/domain-pairs.md)
- Add a top skill to [`skill-finder/reference/top-skills.md`](./skill-finder/reference/top-skills.md)
- Add/fix an MCP server in [`mcp-finder/reference/top-servers.md`](./mcp-finder/reference/top-servers.md)

#### 🐛 Fix stale data

- Deprecated npm packages
- Wrong env var names
- Broken install commands
- Outdated skill names

#### 💡 Improve the skills

- Stronger trigger descriptions (so Claude picks the right skill)
- Better fallback strategies
- New workflow steps
- More complete "When NOT to Use" guidance

#### 🌐 Add new domains

Missing a domain entirely? Add the full row to `domain-pairs.md`:

```markdown
| Task | Skill | MCP Server | Install |
|------|-------|-----------|---------|
| Your task | `skill-name` | `@scope/mcp-package` | install commands |
```

### How to submit

1. Fork the repo
2. Make your changes
3. Open a PR with a short description of what you changed and why
4. A maintainer will review within a few days

### Good first issues

Look for issues tagged `good first issue` — these are usually:
- Adding a missing domain to the reference tables
- Verifying that listed packages still exist on npm
- Fixing typos or unclear descriptions

---

## Design Philosophy

- **Fast path first** — curated reference files beat network search for common cases
- **Fallback always** — if search fails, there's always a next step
- **Verification included** — install recommendations always come with a verify command
- **Skills + MCP together** — most real workflows need both; this repo treats them as a pair

---

## License

MIT — see [LICENSE](./LICENSE) if present.

---

## Related

- [skills.sh](https://skills.sh) — Browse the full agent skills ecosystem
- [glama.ai/mcp/servers](https://glama.ai/mcp/servers) — Browse the full MCP server catalog
- [awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) — Community MCP server list
- [Model Context Protocol](https://modelcontextprotocol.io) — MCP specification
