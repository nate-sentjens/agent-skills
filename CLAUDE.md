# CLAUDE.md — Agent Governance for this Repository

This file governs how any agent should behave when operating on this
repository. It exists because this repo is public, and agents working on it
must respect both its philosophy and its security posture.

Read this file before touching anything else.

---

## What This Repo Is

A personal library of agent skills, MCP configurations, and prompt templates.
Skills here are deliberately generic and context-free. That constraint is the
highest-order requirement when creating or editing anything in this repo.

---

## Access Rules

### The agent MAY read
- All `SKILL.md` files
- All `README.md` files
- `CLAUDE.md` (this file)
- `*.example.json` files in `mcp/`
- `*.md` files in `prompts/`
- `.gitignore`, `LICENSE`, `CONTRIBUTING.md`
- `.github/workflows/` files
- `.claude/settings.local.json.example`

### The agent MUST NOT read
- `.env` or any `.env.*` variant
- `.agent-secrets` or any file matching `*secret*`, `*credential*`,
  `*token*`, `*apikey*`, `*.pem`, `*.key`
- Any file in `_draft/`, `private/`, or `local/`
- `*.local.md` files (local skill overrides, not for publication)
- `.claude/settings.local.json` (contains real local config, not the example)
- Git history diffs on any of the above paths

### The agent MUST NOT
- Commit or propose changes containing project-specific context: client names,
  domain names, service URLs, account identifiers, or anything revealing what
  the author is actually working on
- Add hardcoded values where `.example` placeholders belong
- Modify or disable the secrets-scanning CI workflow
- Modify the access rules in this file without explicit human instruction
- Push anything without explicit human approval

---

## Pre-Publication Checklist

Before marking any skill, prompt, or config as ready for this repo, apply
every check below. If any check fails, the content is not ready.

**Generality.** Could someone with a completely different tech stack, employer,
and set of projects use this? If not, abstract further.

**Auditability.** Can a human read and fully understand this in under five
minutes? If not, split it.

**Portability.** Does it reference platform-specific paths, tool versions, or
machine-specific config that would prevent it working elsewhere? Flag and
parameterise these.

**Disclosure.** Does the content, examples, or metadata reveal anything about
the author's specific work, clients, infrastructure, or projects? If yes, not
ready.

**Infrastructure extra pass.** Skills in `infrastructure/` carry higher
disclosure risk than other domains. Apply the disclosure check twice, and
specifically scan for: hostnames, subdomain patterns, account or zone IDs,
IP addresses, ARNs, region-specific assumptions, and certificate or key
material. When uncertain, omit rather than publish.

---

## What Belongs Here vs. Elsewhere

| Content | Here? | Where instead |
|---|---|---|
| Generic, reusable skills | ✅ | — |
| Project-specific skills | ❌ | Project's `.claude/skills/` |
| Business-context prompts | ❌ | Private repo or local only |
| MCP config templates (`.example.json`) | ✅ | — |
| MCP configs with real values | ❌ | `~/.claude/claude.json` locally |
| NanoClaw operational config | ❌ | On-machine, never public |
| Skills used by NanoClaw agents | ✅ | Here, once scrubbed |
| Operational runbooks | ❌ | Private repo or internal docs |
| Works-in-progress not yet scrubbed | ❌ | `_draft/` (gitignored) |
| Local skill overrides (`*.local.md`) | ❌ | Gitignored automatically |

If uncertain whether something belongs here, default to keeping it out and
flagging for human review.

---

## Skill Quality Standards

**`status` field** must be set honestly:
- `stable` — used regularly, well-tested, unlikely to change structurally
- `experimental` — in active iteration; others should expect churn
- `deprecated` — superseded; kept for reference only

**`scope` field** must be set accurately:
- `general` — clean for any context
- `personal` — personal workflow patterns; others should review before reuse
- `business-safe` — explicitly vetted for professional or client contexts

Do not set `stable` or `business-safe` without deliberate review. Default new
skills to `experimental` and `personal` until they've earned otherwise.

---

## Commit Conventions

```
<type>(<domain>): <short description>

Types:   add | update | fix | remove | refactor | docs
Domains: coding | infrastructure | research | writing | agents | mcp | prompts
```

Examples:
```
add(coding/go): error wrapping patterns for multi-layer services
update(infrastructure/aws-iam): broaden least-privilege role examples
docs(mcp/context-hub): clarify annotation persistence behaviour
```

Propose commits in this format. Do not push without explicit human approval.

---

## NanoClaw and This Repo

Skills in this repo are installable into NanoClaw agent containers using the
same `SKILL.md` format — no modification needed. The deployment pattern for
NanoClaw is to mount specific skill folders into the relevant container at
startup, rather than the full repo. A research agent gets research skills; a
coding agent gets coding skills. This is intentional: least-privilege applies
to agent capabilities, not just filesystem access.

What never appears here: NanoClaw's operational configuration — which groups
or channels it is connected to, what scheduled tasks it runs, and what memory
or context it holds. That configuration lives on-machine and is never public.

---

## A Note on This File

`CLAUDE.md` is itself a portfolio artifact. Its presence, specificity, and
coverage signal that agent governance is a first-class concern — not a
retrofit. It should remain legible to a human reader, not just an agent.
