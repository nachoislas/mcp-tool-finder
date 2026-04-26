# Capability Tagger

Auto-tag MCP tools with capabilities for discovery.

## Trigger

- "tag capabilities"
- "analyze tool"
- During registry update

## What It Does

1. **Fetch** tool metadata from npm/github
2. **Analyze** package description
3. **Extract** capabilities
4. **Tag** in registry
5. **Update** search index

## Capability Taxonomy

```
Capability Categories:
├── database
│   ├── postgres
│   ├── mysql
│   ├── sqlite
│   ├── mongodb
│   └── universal
├── api
│   ├── rest
│   ├── graphql
│   └── webhook
├── filesystem
│   ├── read
│   ├── write
│   └── watch
├── browser
│   ├── automation
│   └── scraping
├── communication
│   ├── slack
│   ├── discord
│   └── email
├── cloud
│   ├── aws
│   ├── gcp
│   └── azure
└── devops
    ├── docker
    ├── kubernetes
    └── ci-cd
```

## Tagging Rules

### From package.json
```json
{
  "keywords": ["postgresql", "database", "sql"],
  "description": "PostgreSQL database integration"
}
```
→ Tags: `database:postgres`, `database:sql`

### From repository
- Readme → extract keywords
- Code → analyze exports
- Issues → identify use cases

## Auto-Detection

```python
def detect_capabilities(package):
    keywords = package.keywords + parse_description(package.description)
    capabilities = []
    
    for keyword in keywords:
        if keyword in CAPABILITY_MAP:
            capabilities.append(CAPABILITY_MAP[keyword])
    
    return capabilities
```

## Boundaries

- Update tags on registry update
- Validate tags manually periodically
- No guess - require evidence