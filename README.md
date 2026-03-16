# agent-skills

Dotfiles for AI execution. A curated, public-safe collection of agent skills,
MCP configurations, and prompt templates that power my daily workflows across
coding, infrastructure, and research. Built primarily for
[Claude Code](https://claude.ai/code) and compatible with any agent platform
that reads the `SKILL.md` format.

---

## Philosophy

**Skills should be composable, not monolithic.** A skill that does one thing
well is more useful than one that tries to do everything. Narrow skills
compose; bloated ones don't.

**Skills should be auditable.** Every skill in this repo fits in a single
sitting. If you can't read and fully understand a skill in a few minutes,
it's doing too much or explaining itself poorly.

**Skills should be portable.** Nothing here is tied to a specific project,
client, or context. Where project-specific knowledge is necessary to author a
skill, that knowledge is abstracted away before publication. The goal is
reusable patterns, not operational runbooks.

**Configuration is an artifact.** These skills, prompts, and MCP configs are
first-class versioned artifacts — the same way dotfiles configure a machine,
these configure how I work with agents. They evolve deliberately, not
haphazardly.

---

## Structure

Skills are organized by domain. The tool a skill runs on is an implementation
detail; what it *does* is what matters for discoverability.

```
agent-skills/
│
├── coding/           # Language-specific and development workflow skills
│   ├── swift/        # Swift idioms, concurrency, SPM, testing
│   ├── go/           # Go error handling, modules, build patterns
│   └── app-store-connect/  # Release ops, provisioning, TestFlight
│
├── infrastructure/   # Cloud ops, self-hosted services, networking, security
│   ├── aws-iam/      # Role hygiene and least-privilege patterns
│   ├── aws-ops/      # EC2, Route 53, certbot — generic operational patterns
│   └── self-hosted/  # Generic self-hosted service skills
│
├── research/         # Gathering, synthesis, and monitoring workflows
├── writing/          # Writing, editing, and communication workflows
├── agents/           # Agent orchestration, delegation, and swarm patterns
│
├── mcp/              # MCP server configurations and wrappers
│   ├── context7/     # Up-to-date library docs via Context7 MCP
│   ├── context-hub/  # Curated versioned docs + persistent annotations (chub)
│   └── aws/          # AWS MCP suite
│
└── prompts/          # Standalone system prompts that configure agent personas
```

`mcp/` and `prompts/` are top-level rather than nested under domains because
they're consumed differently. MCP configs are installed into tool-specific
locations; prompts configure extended agent sessions rather than on-demand
capabilities. Each has its own `README.md` with conventions specific to that
type.

`research/`, `writing/`, and `agents/` are intentionally sparse at present.
They exist to signal intent and grow as stable patterns emerge — particularly
`agents/`, which will develop alongside [NanoClaw](https://nanoclaw.dev/)
usage. Premature population is worse than honest emptiness.

---

## Skill Frontmatter

Every `SKILL.md` includes the following YAML frontmatter:

```yaml
---
name: skill-name
description: What this skill does and when to use it
status: stable       # stable | experimental | deprecated
scope: general       # general | personal | business-safe
---
```

**`status`** lets you distinguish well-tested skills from ones still being
refined. Prefer `experimental` for anything in active iteration.

**`scope`** signals where a skill is safe to use:
- `general` — clean enough for any context, personal or professional
- `personal` — patterns specific to personal workflows; review before reuse
- `business-safe` — explicitly vetted for use in professional/client contexts

---

## Context7 vs. context-hub

Both tools live in `mcp/` and solve the same root problem — agents
hallucinating outdated or deprecated APIs — but from different angles.

**Context7** is an MCP server that resolves and fetches live documentation
from a community-maintained index. Zero friction, broad coverage of standard
open-source libraries. Invoke it by adding `use context7` to a prompt.

**context-hub** (`chub`) is a CLI-driven tool by Andrew Ng's team. Its
distinguishing features: all content is inspectable open markdown; agents can
persist session discoveries as annotations that survive across sessions; and
it supports private or niche docs via a bring-your-own-docs path. The last
point matters for APIs like App Store Connect that Context7 doesn't cover.

In practice: Context7 for standard libraries, context-hub for anything niche,
private, or where persistent agent annotations add value.

---

## Using These Skills

**With Claude Code — global (available across all projects):**
```bash
git clone https://github.com/YOUR_HANDLE/agent-skills ~/.agent-skills

# Symlink a single skill
ln -s ~/.agent-skills/coding/go ~/.claude/skills/go

# Or symlink an entire domain
ln -s ~/.agent-skills/coding ~/.claude/skills/coding
```

**With Claude Code — per project:**
```bash
cp -r ~/.agent-skills/coding/go .claude/skills/
```

**With GitHub Copilot:**
```bash
cp -r ~/.agent-skills/coding/go .github/skills/
```

**With context-hub:** Skills in `mcp/context-hub/` include the `chub`
`SKILL.md` that wires the CLI into Claude Code. Install it once globally and
`chub get` becomes available across all agent sessions.

The `SKILL.md` format is an [open standard](https://github.com/anthropics/skills)
supported by Claude Code, GitHub Copilot, Cursor, Windsurf, and others.

---

## What's Deliberately Absent

Project-specific context, business-sensitive details, and anything that would
reveal what I'm actually working on are kept out by design. Skills are
published only when abstracted into genuinely reusable patterns.

This is enforced by:
1. **[`CLAUDE.md`](./CLAUDE.md)** — governs agent behaviour when operating on
   this repo, including explicit file access restrictions and a pre-publication
   disclosure checklist.
2. **[`settings.local.json.example`](./.claude/settings.local.json.example)**
   — a template for local Claude Code deny rules that enforce access
   restrictions at the tool level, not just advisorily.
3. **CI secrets scanning** — every push is checked by
   [trufflehog](https://github.com/trufflesecurity/trufflehog) via
   `.github/workflows/secrets-scan.yml`.

If you notice a skill that inadvertently contains specific operational detail,
opening an issue is welcome.

---

## Contributing

This is a personal repo. Curation is the point, so I don't accept PRs for new
skills. Issues flagging errors, outdated content, or unintended information
disclosure are welcome and acted on promptly.

---

## License

MIT. Fork, adapt, and use freely. Attribution appreciated but not required.
