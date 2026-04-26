# Semantic Search

Search tools/codebase via vector embeddings for semantic similarity.

## Trigger

- "find similar tools"
- "search by meaning"
- "semantic search"
- During discovery phase

## What It Does

1. **Embed** query text
2. **Search** vector index
3. **Rank** by similarity
4. **Return** top matches with scores

## Vector Store

Uses Supabase pgvector or in-memory:

```sql
CREATE TABLE tool_embeddings (
  id SERIAL PRIMARY KEY,
  tool_name TEXT NOT NULL,
  description TEXT,
  capabilities TEXT[],
  embedding vector(1536)
);
```

## Search Query

```sql
SELECT tool_name, description,
  1 - (embedding <=> query_embedding) as similarity
FROM tool_embeddings
ORDER BY embedding <=> query_embedding
LIMIT 5;
```

## Capabilities Taxonomy

```
database:postgres
database:mysql  
database:sqlite
api:rest
api:graphql
filesystem:read
filesystem:write
browser:automation
web scraping
```

## Rank Formula

```
score = (semantic_similarity * 0.5) + 
       (popularity * 0.2) + 
       (recency * 0.15) + 
       (success_rate * 0.15)
```

## Indexing

1. Scrape MCP registry
2. Generate embeddings for each tool
3. Store in vector DB
4. Update periodically

## Boundaries

- Re-index on new tools
- Validate embeddings periodically
- Return top-5 with scores