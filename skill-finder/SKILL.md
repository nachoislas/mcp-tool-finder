---
name: skill-finder
description: Find agent skills from the public catalog and local installation. Use when user asks "find skill for X", "what skills exist for testing", "skill for React", "how do I do X with skills", or wants to discover available agent skills.
---

# Skill: Skill Finder

Find agent skills from the open agent skills ecosystem using `npx skills`.

## When to Use This Skill

- User asks "find skill for X" or "skill for [task]"
- User needs help with specific domain (testing, React, deployment)
- User wants to discover what skills exist in the ecosystem
- User wants to know which skills are already installed
- User asks "how do I do X with skills"

## Available Tools

### Find Skills (Public Catalog)

```bash
npx skills find [query]
```

Examples:
- `npx skills find react`
- `npx skills find testing`
- `npx skills find docker`

### List Installed Skills

```bash
npx skills list
```

### Get Skill Details

Visit https://skills.sh/{owner}/{repo}/{skill-name}

## Usage Examples

| Task | Command |
|------|---------|
| Find React skills | `npx skills find react` |
| Find testing skills | `npx skills find testing` |
| Find deployment skills | `npx skills find deploy` |
| List installed | `npx skills list` |

## Workflow

1. User describes what they need help with
2. Run `npx skills find [keywords]`
3. Present top 3-5 results with:
   - Skill name (@owner/skill-name)
   - Install count
   - Brief description
4. Offer to install: `npx skills add <owner/repo@skill> -g -y`

## Notes

- Search is fuzzy - partial matches work
- Higher install count = generally better tested
- Official repos (anthropics, vercel-labs) more reliable