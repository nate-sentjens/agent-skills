# mcp/

MCP server configurations for use with Claude Code and compatible agent tools.

---

## Convention

Every entry in this directory is a subfolder containing at minimum a
`config.example.json` — a template with all sensitive values replaced by
`YOUR_VALUE_HERE` placeholders. Real configs with actual keys, endpoints, or
credentials are never committed; they live in `~/.claude/claude.json` locally.

File naming: `config.example.json` (not `config.json.example`). This keeps
gitignore negation patterns reliable across directory depths.

```
mcp/
└── server-name/
    ├── config.example.json   # Template — committed
    └── README.md             # What this server does, setup notes
```

Install a config by copying the example, filling in your values, and merging
into your local `~/.claude/claude.json` under `mcpServers`.

---

## Servers

| Server | Purpose |
|---|---|
| [`context7/`](./context7/) | Live library docs via Context7 MCP — standard open-source libraries |
| [`context-hub/`](./context-hub/) | Curated versioned docs + persistent agent annotations via `chub` CLI |
| [`aws/`](./aws/) | AWS MCP suite for cloud resource interaction |

---

## Context7 vs. context-hub

Both solve agent hallucination of outdated APIs, from different angles.
See the [root README](../README.md#context7-vs-context-hub) for a full
comparison. Short version: Context7 for standard libraries, context-hub for
anything niche, private, or where cross-session annotation adds value.
