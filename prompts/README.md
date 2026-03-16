# prompts/

Standalone system prompts that configure an agent's persona or operating mode
for an extended session.

---

## Prompts vs. Skills

This distinction matters and is worth stating explicitly:

**A skill** (`SKILL.md`) is an on-demand capability loaded when a specific
task arises. The agent pulls it in as needed, uses it, and moves on.

**A prompt** (this directory) is a persistent persona or mode that frames an
entire session. You set it once at the start — via `--system-prompt`, a
project's `CLAUDE.md` import, or by pasting it — and it shapes everything
the agent does from there. A Go code reviewer, an AWS ops assistant, a
technical writing editor: these are roles, not tasks.

If you're writing something the agent invokes once for a specific job, it's
a skill. If you're writing something that changes how the agent behaves
across an entire session, it's a prompt.

---

## Convention

Each prompt is a single `.md` file with minimal frontmatter:

```yaml
---
name: prompt-name
description: What persona or mode this establishes, and when to use it
scope: general       # general | personal | business-safe
status: stable       # stable | experimental | deprecated
---
```

Followed by the system prompt content itself, written directly for the model
— no preamble, no meta-commentary. Concise and specific beats comprehensive
and vague.

---

## Prompts

*(Empty at initialisation — added as stable patterns emerge.)*
