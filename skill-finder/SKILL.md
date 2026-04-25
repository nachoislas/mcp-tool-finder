---
name: skill-finder
description: Find agent skills from the public catalog and local installation. Use when user asks "find skill for X", "what skills exist for testing", "skill for React", "how do I do X with skills", or wants to discover available agent skills.
---

# Skill: Skill Finder

Find agent skills from the open agent skills ecosystem using `npx skills`.

**Fast path**: Check `reference/top-skills.md` first. If the user's domain matches a listed skill, use that directly — no search needed.

## When to Use

- User asks "find skill for X" or "skill for [task]"
- User needs help with a specific domain (testing, React, deployment)
- User wants to discover what skills exist in the ecosystem
- User wants to know which skills are already installed
- User asks "how do I do X with skills"

## When NOT to Use

- User needs an external tool or API integration — use `mcp-finder` instead
- User already knows which skill they want and just wants to install it
- User is asking about MCP servers, not agent skills
- Task requires code execution, file access, or browser control (those are MCP servers, not skills)

## Workflow

### Step 1: Fast-path lookup

Check `reference/top-skills.md`. If the user's domain matches, present that skill directly.

### Step 2: Search the catalog

```bash
npx skills find [keyword]
```

Examples:
- `npx skills find react`
- `npx skills find testing`
- `npx skills find docker`

### Step 3: Handle no results

If search returns 0 results:
1. Try a broader keyword (e.g. `"test"` instead of `"integration-testing"`)
2. Check `reference/top-skills.md` for the closest match
3. Browse https://skills.sh for the full catalog

### Step 4: Present results

Show top 3–5 results with:
- Skill name (`@owner/skill-name`)
- Install count (higher = better tested and maintained)
- Brief description

### Step 5: Offer to install

```bash
npx skills add <owner/repo@skill-name> -g -y
```

### Step 6: Verify installed skills

```bash
npx skills list
```

## Quick Reference

| Task | Command |
|------|---------|
| Find React skills | `npx skills find react` |
| Find testing skills | `npx skills find testing` |
| Find deployment skills | `npx skills find deploy` |
| List installed | `npx skills list` |
| Get skill details | https://skills.sh/{owner}/{repo}/{skill-name} |

## Notes

- Search is fuzzy — partial matches work
- Higher install count = generally better tested and maintained
- Official repos (anthropics, vercel-labs) are more reliable
- Skills provide **instructions** (how-to); for external tools use MCP servers via `mcp-finder`