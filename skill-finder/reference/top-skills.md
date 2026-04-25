# Top Skills by Domain

Use this as a fast-path when `npx skills find` returns no results or the user needs an instant recommendation.

## Frontend

| Skill | What it does | Install |
|-------|-------------|---------|
| `react-patterns` | Modern React hooks, composition, TypeScript | `npx skills add anthropics/skills@react-patterns -g -y` |
| `nextjs-best-practices` | Next.js App Router, SSR, data fetching | `npx skills add anthropics/skills@nextjs-best-practices -g -y` |
| `tailwind-patterns` | Tailwind CSS v4, design tokens | `npx skills add anthropics/skills@tailwind-patterns -g -y` |

## Backend

| Skill | What it does | Install |
|-------|-------------|---------|
| `backend-architect` | API design, microservices, distributed systems | `npx skills add anthropics/skills@backend-architect -g -y` |
| `database` | SQL, NoSQL, migrations, optimization | `npx skills add anthropics/skills@database -g -y` |
| `api-patterns` | REST vs GraphQL, versioning, pagination | `npx skills add anthropics/skills@api-patterns -g -y` |

## Testing

| Skill | What it does | Install |
|-------|-------------|---------|
| `tdd-workflow` | TDD red-green-refactor cycle | `npx skills add anthropics/skills@tdd-workflow -g -y` |
| `webapp-testing` | Playwright-based web app testing | `npx skills add anthropics/skills@webapp-testing -g -y` |

## DevOps & Cloud

| Skill | What it does | Install |
|-------|-------------|---------|
| `github-actions-templates` | CI/CD pipeline patterns | `npx skills add anthropics/skills@github-actions-templates -g -y` |
| `docker-expert` | Dockerfile, Compose, containers | `npx skills add anthropics/skills@docker-expert -g -y` |
| `terraform-skill` | Infrastructure as code | `npx skills add anthropics/skills@terraform-skill -g -y` |

## AI & Agents

| Skill | What it does | Install |
|-------|-------------|---------|
| `llm-app-patterns` | LLM application development | `npx skills add anthropics/skills@llm-app-patterns -g -y` |
| `rag-engineer` | RAG pipelines, vector search | `npx skills add anthropics/skills@rag-engineer -g -y` |
| `gemini-api-dev` | Gemini API integration | `npx skills add anthropics/skills@gemini-api-dev -g -y` |

## Fallback Path

If `npx skills find [keyword]` returns 0 results:

1. Try a broader keyword (e.g. "test" instead of "integration-test")
2. Check this file for a close match
3. Visit https://skills.sh to browse the full catalog
4. Suggest the user install manually: `npx skills add <owner/repo@skill> -g -y`
