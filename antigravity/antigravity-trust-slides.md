---
layout: section
---

# Antigravity: trust layers

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# The three layers in Antigravity

| Layer | Antigravity mechanism | File |
| --- | --- | --- |
| 1. What it can do | `permissions` allow / ask / deny | `~/.gemini/antigravity-cli/settings.json` |
| 2. How it writes code | Rules | `AGENTS.md` (or `GEMINI.md`), `.agents/rules/` |
| 3. How it thinks | Design docs, stage checklists, skills, plan artifacts | `design/`, `agent-constraints/`, `SKILL.md` skills |
| The gate | An `ask` rule on `gh pr create` | `~/.gemini/antigravity-cli/settings.json` |

Rule of thumb: undoable with `git checkout` → **allow**. Leaves the working tree → **ask**.

---
hideInToc: true
---

# Layer 1: ~/.gemini/antigravity-cli/settings.json

```json
{
  "permissions": {
    "allow": ["command(*)", "read_file(*)", "write_file(*)"],
    "ask": [
      "command(git push --force)", "command(git push -f)", "command(git reset --hard)",
      "command(git clean -f)", "command(git branch -D)", "command(rm -rf)",
      "command(gh pr create)", "command(gh pr merge)", "command(gh issue close)",
      "command(gh api)", "command(aws)", "command(gcloud)", "command(az)"
    ],
    "deny": ["command(sudo)"]
  }
}
```

---
hideInToc: true
---

# Why it's built this way

- **Deny > ask > allow**: the broad `command(*)` allow can't override the specific asks
- **`command(...)` matches word by word**, so `command(git push --force)` doesn't catch plain `git push`. Use `regex:` inside the rule when spelling varies
- **`sudo` is denied outright**: run privileged commands yourself
- **The plan is an artifact**: Antigravity writes an implementation plan you review (`Ctrl+R`) before it builds. That's Layer 3's "human approves the plan" step, built in

**Know the limits**

- `auto` mode and the `always-proceed` preset skip prompts entirely, including the gate. Keep `default` or `accept-edits` when the gate matters
- For a hard boundary, turn on the terminal sandbox (`--sandbox`, `enableTerminalSandbox`)

<!--
Antigravity's docs are new and changing quickly. Re-check the permissions syntax with /permissions before presenting.
-->

---
hideInToc: true
---

# Layers 2, 3 and the gate

**Layer 2**: `AGENTS.md` at the repo root (shared with other agents), plus `.agents/rules/*.md` for rules that only apply to some files:

```markdown
---
trigger: glob
globs: src/cli/**
---
The CLI never imports from src/internal: it keeps the CLI decoupled from internals.
```

**Layer 3**: design docs and stage checklists referenced from `AGENTS.md`; domain knowledge as skills (`/skills`).

**The gate**: the `ask` on `gh pr create`. Compare the diff with the plan artifact before you say yes.
