# mcp/context7/

Fetches up-to-date, version-specific library documentation directly into the
agent's context. Eliminates hallucinated APIs and outdated code generation for
standard open-source libraries.

## Setup

```bash
# Merge config.example.json into ~/.claude/claude.json under mcpServers.
# No API key required for basic use; get a free key at context7.com/dashboard
# for higher rate limits and add it as an environment variable:

# In your local config (not committed):
# "env": { "CONTEXT7_API_KEY": "YOUR_API_KEY_HERE" }
```

## Usage

Add `use context7` to any prompt involving a library or framework. The agent
resolves the library, fetches current docs, and injects them into context.

```
Implement JWT middleware for a Go HTTP server. use context7
```

To target a specific library directly, use its Context7 ID:

```
Set up Supabase auth. use library /supabase/supabase
```

## Coverage

Community-maintained index covering most major open-source libraries. For
niche or private APIs not in the index, use context-hub instead.
