# Env Manager

Manage environment variables for MCP servers across projects.

## Trigger

- "set env var"
- "configure environment"
- "env config"
- During provisioning phase

## What It Does

1. **Collect** required env vars from MCP servers
2. **Prompt** user for missing values
3. **Validate** env var format
4. **Store** securely (not in git)
5. **Load** at runtime

## Env Var Schema

```json
{
  "required": {
    "DATABASE_URL": {
      "type": "string",
      "pattern": "postgres://.*",
      "description": "PostgreSQL connection string",
      "required": true
    },
    "GITHUB_TOKEN": {
      "type": "string", 
      "description": "GitHub personal access token",
      "required": true
    }
  },
  "optional": {
    "LOG_LEVEL": {
      "type": "string",
      "default": "info",
      "values": ["debug", "info", "warn", "error"]
    }
  }
}
```

## Storage

Store in `.env.local` (gitignored):

```
.env.local
.env.project
.env.secrets (encrypted)
```

## Loading Priority

1. Process environment
2. `.env.secrets` (encrypted)
3. `.env.project` 
4. `.env.local`
5. Default values

## Validation

- Required vars must be present
- Pattern matching for URLs
- Enum validation for choices
- Type checking

## Commands

```bash
# Set env var
/gsd-env set DATABASE_URL=postgres://localhost/mydb

# List env vars (masked)
/gsd-env list

# Validate current config
/gsd-env validate
```

## Boundaries

- Never commit secrets
- Encrypt sensitive data
- Require confirmation for destructive changes