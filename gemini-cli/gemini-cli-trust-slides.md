---
layout: section
---

# Gemini CLI: trust layers

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# The three layers in Gemini CLI

| Layer | Gemini CLI mechanism | File |
| --- | --- | --- |
| 1. What it can do | Policy engine rules: `allow`, `ask_user`, `deny` | `~/.gemini/policies/*.toml` |
| 2. How it writes code | Context file | `GEMINI.md` (or `AGENTS.md` via `context.fileName`) |
| 3. How it thinks | Design docs, stage checklists, skills | `design/`, `agent-constraints/`, `.agents/skills/` |
| The gate | An `ask_user` rule on `gh pr create` | `~/.gemini/policies/trust.toml` |

Rule of thumb: undoable with `git checkout` → **allow**. Leaves the working tree → **ask**.

---
hideInToc: true
---

# Layer 1: ~/.gemini/policies/trust.toml

```toml
# Ask before anything destructive or public. Higher priority wins.
[[rule]]
toolName = "run_shell_command"
commandPrefix = [
  "git push --force", "git push -f", "git reset --hard", "git clean -f",
  "git branch -D", "rm -rf", "sudo",
  "gh pr create", "gh pr merge", "gh issue close", "gh api",
  "aws", "gcloud", "az",
]
decision = "ask_user"
priority = 500

# Everything else in the shell runs without a prompt.
[[rule]]
toolName = "run_shell_command"
decision = "allow"
priority = 100
```

---
hideInToc: true
---

# Why it's built this way

- **Priorities, not order**: the highest-priority matching rule wins, so the specific `ask_user` (500) beats the broad `allow` (100)
- **User-level on purpose**: workspace policy files (`.gemini/policies/`) are currently disabled, so a cloned repository can't loosen your rules. Keep the trust model in `~/.gemini/policies/`
- **Headless is stricter**: in `gemini -p`, `ask_user` becomes `deny`, so scripted runs simply can't publish

**Know the limits**

- `commandPrefix` is a string prefix: `rm -fr` isn't `rm -rf`. Use `commandRegex` where spelling varies
- Prefer starting narrower than "allow everything", and widen as you learn
- For a hard boundary, add the sandbox: `-s` or `"tools": { "sandbox": "docker" }`

---
hideInToc: true
---

# Layers 2, 3 and the gate

**Layer 2**: `GEMINI.md` at the repo root, or a shared `AGENTS.md`:

```json
{ "context": { "fileName": ["AGENTS.md", "GEMINI.md"] } }
```

**Layer 3**: point at the design docs and stage checklists from that file, and put domain knowledge in skills: `.agents/skills/<name>/SKILL.md` (or `.gemini/skills/`).

**The gate**: the `ask_user` rule on `gh pr create` is the one prompt in a normal run. Approve it after comparing the diff with the plan.
