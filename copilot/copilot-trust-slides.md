---
layout: section
---

# Copilot CLI: trust layers

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# The three layers in Copilot CLI

| Layer | Copilot mechanism | Where |
| --- | --- | --- |
| 1. What it can do | `--allow-tool` / `--deny-tool`; anything unlisted that changes things asks | Launch flags (wrap them in a script or alias) |
| 2. How it writes code | Custom instructions | `AGENTS.md`, `.github/copilot-instructions.md` |
| 3. How it thinks | Design docs, stage checklists, skills, custom agents | `design/`, `.github/skills/`, `.github/agents/` |
| The gate | Leave `gh pr create` unlisted so it asks | Launch flags |

Rule of thumb: undoable with `git checkout` → **allow**. Leaves the working tree → **ask**.

---
hideInToc: true
---

# Layer 1: a launch wrapper

```bash
# ~/bin/cop: Copilot CLI with the team's trust model
exec copilot \
  --allow-tool='write' \
  --allow-tool='shell(npm:*)' --allow-tool='shell(node:*)' --allow-tool='shell(make:*)' \
  --allow-tool='shell(git status)' --allow-tool='shell(git diff:*)' \
  --allow-tool='shell(git add:*)' --allow-tool='shell(git commit:*)' \
  --allow-tool='shell(gh pr view:*)' --allow-tool='shell(gh pr checks:*)' \
  --deny-tool='shell(sudo)' --deny-tool='shell(git push --force)' \
  "$@"
```

Everything else (`git push`, `git reset`, `rm`, `gh pr create`, `gh api`, `aws`, `gcloud`, `az`) isn't allowed, so it **asks**.

---
hideInToc: true
---

# Why it's built this way

- **Copilot has allow and deny, but no "ask" list.** Unlisted commands that change your system prompt, so "ask" means "don't allow it"
- **Allow narrowly**: `shell(git:*)` would allow `git reset --hard` too. List the git subcommands that are undoable, and let the rest ask
- **Deny is absolute**: a `--deny-tool` holds even under `--allow-all`. Use it for things the agent should never do, like `sudo`
- **Flags are per session**, hence the wrapper: one script everyone runs is your single, readable trust model

**Know the limits**

- "Yes, and approve for the rest of the session" quietly widens the model; prefer approving once
- Saved approvals live in `~/.copilot/permissions-config.json`; review it now and then
- Programmatic runs (`-p`) need `--allow-all-tools`, which drops every prompt. Keep publication out of them

---
hideInToc: true
---

# Layers 2, 3 and the gate

**Layer 2**: `AGENTS.md` at the repo root (shared with other agents), or `.github/copilot-instructions.md`. Path-specific conventions go in `.github/instructions/*.instructions.md` with `applyTo:`.

**Layer 3**:

- Design docs and stage checklists referenced from `AGENTS.md`
- Skills in `.github/skills/<name>/SKILL.md` (or `.agents/skills/`)
- A custom agent per stage, such as `.github/agents/triage.agent.md`, run with `/agent`

**The gate**: `gh pr create` isn't allowed, so it asks. On GitHub, add **branch protection with required reviews** too: even a PR the agent opens can't merge without a human.
