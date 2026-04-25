# Domain → Recommended Skill + MCP Pairs

Use this table to answer "I need to build X" instantly, without searching.

## Web & Browser

| Task | Skill | MCP Server | Install |
|------|-------|-----------|---------|
| E2E browser testing | `testing` | `@anthropic/mcp-server-puppeteer` | `npx skills find testing` + `npm i -g @anthropic/mcp-server-puppeteer` |
| Web scraping | `web-scraper` | `@modelcontextprotocol/server-fetch` | `npx skills find scraping` + `npm i -g @modelcontextprotocol/server-fetch` |
| Screenshot / visual testing | `webapp-testing` | `@anthropic/mcp-server-puppeteer` | `npx skills find webapp-testing` + `npm i -g @anthropic/mcp-server-puppeteer` |

## Database & Backend

| Task | Skill | MCP Server | Install |
|------|-------|-----------|---------|
| PostgreSQL app | `database` | `@modelcontextprotocol/server-postgres` | `npx skills find database` + `npm i -g @modelcontextprotocol/server-postgres` |
| SQLite app | `database` | `@modelcontextprotocol/server-sqlite` | `npx skills find database` + `npm i -g @modelcontextprotocol/server-sqlite` |
| API backend | `backend-architect` | `@modelcontextprotocol/server-filesystem` | `npx skills find backend` |

## GitHub & DevOps

| Task | Skill | MCP Server | Install |
|------|-------|-----------|---------|
| GitHub automation | `github` | `@modelcontextprotocol/server-github` | `npx skills find github` + `npm i -g @modelcontextprotocol/server-github` |
| CI/CD pipeline | `github-actions-templates` | `@modelcontextprotocol/server-github` | `npx skills find cicd` + `npm i -g @modelcontextprotocol/server-github` |
| Docker / containers | `docker-expert` | `@modelcontextprotocol/server-filesystem` | `npx skills find docker` |

## AI & Agents

| Task | Skill | MCP Server | Install |
|------|-------|-----------|---------|
| Build AI agent | `ai-agents-architect` | `@modelcontextprotocol/server-memory` | `npx skills find agents` + `npm i -g @modelcontextprotocol/server-memory` |
| RAG / vector search | `rag-engineer` | `@modelcontextprotocol/server-memory` | `npx skills find rag` + `npm i -g @modelcontextprotocol/server-memory` |
| LLM app | `llm-app-patterns` | `@modelcontextprotocol/server-fetch` | `npx skills find llm` |

## Search & Web Research

| Task | Skill | MCP Server | Install |
|------|-------|-----------|---------|
| Web search | `search-specialist` | `@modelcontextprotocol/server-brave-search` | `npx skills find search` + `npm i -g @modelcontextprotocol/server-brave-search` |
| HTTP requests | `api-patterns` | `@modelcontextprotocol/server-fetch` | `npm i -g @modelcontextprotocol/server-fetch` |

## File & Filesystem

| Task | Skill | MCP Server | Install |
|------|-------|-----------|---------|
| File operations | `bash-linux` | `@modelcontextprotocol/server-filesystem` | `npm i -g @modelcontextprotocol/server-filesystem` |
| File organization | `file-organizer` | `@modelcontextprotocol/server-filesystem` | `npx skills find file-organizer` + `npm i -g @modelcontextprotocol/server-filesystem` |

## Notes

- Always check env vars before recommending an MCP server (e.g. `BRAVE_API_KEY`, `GITHUB_TOKEN`)
- If a skill is not listed here, fall back to `npx skills find [keyword]`
- If an MCP server is not listed, fall back to searching https://glama.ai/mcp/servers
