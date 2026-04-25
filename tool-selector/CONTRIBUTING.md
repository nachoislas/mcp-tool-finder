# Contributing to Tool Selector

Thanks for your interest!

## Ways to Contribute

1. **Improve skills** - Better descriptions, more examples
2. **Add categories** - New skill/MCP categories
3. **Fix bugs** - Wrong links, outdated info
4. **Add test cases** - More comprehensive evals

## How to Contribute

### Option 1: Edit Directly

1. Fork the repo
2. Edit the SKILL.md files
3. Submit a PR

### Option 2: Report Issues

1. Open an issue
2. Describe the problem
3. Suggest a fix

## Common Contributions

### Improve Trigger Descriptions

The most helpful change is making the `description` field better trigger. A good description:
- Has specific phrases users would say
- Is "pushy" - makes the skill want to be used

Example:
```yaml
# Before
description: Find skills

# After  
description: Find skills. Use when user asks "what skills exist for X" or needs to discover available skills.
```

### Add New Categories

Add to `references/categories.md`:
```markdown
| Category | Keywords | MCP Server |
|----------|----------|-----------|
| NewCat | new, cat | @owner/new-server |
```

## Review Process

1. PR submitted
2. Reviewed within 48h
3. Merged if looking good

## Questions?

Open an issue for discussion.