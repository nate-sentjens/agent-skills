# mcp/context-hub/

CLI-driven tool (`chub`) for fetching curated, versioned API documentation
into agent context. Distinctive features over Context7: all content is
inspectable open markdown, agents can persist session discoveries as
annotations that survive across sessions, and private or niche docs can be
authored and served via the bring-your-own-docs path.

## Setup

```bash
# Install the CLI globally
npm install -g @aisuite/chub

# Install the Claude Code skill (wires chub into agent sessions globally)
mkdir -p ~/.claude/skills/get-api-docs
cp $(npm root -g)/@aisuite/chub/skills/get-api-docs/SKILL.md \
   ~/.claude/skills/get-api-docs/SKILL.md

# Optional: merge config.example.json into ~/.claude/claude.json to use
# chub via MCP rather than CLI+skill mode.
```

## Usage

```bash
chub search "stripe"              # Find available docs
chub get stripe/api               # Fetch doc (auto-detects language)
chub get stripe/api --lang py     # Fetch Python variant
chub get openai/chat --version 2  # Fetch specific version

# Persistent annotations — survive across sessions
chub annotate stripe/api "Webhook verification requires raw body"

# Community feedback
chub feedback stripe/api up
```

Prompt the agent to use it:

```
Use chub to fetch the latest App Store Connect API docs before proceeding.
```

## Private / Niche Docs (BYOD)

For APIs not in the public registry (e.g. App Store Connect, internal
services), author docs locally and point your config at the build output:

```yaml
# ~/.chub/config.yaml
sources:
  - name: community
    url: https://cdn.aichub.org/v1
  - name: private
    path: /path/to/local/docs/dist
```

See the [context-hub content guide](https://github.com/andrewyng/context-hub/blob/main/docs/content-guide.md)
for authoring conventions.
