---
layout: section
level: 2
---

# Codex: trust layers

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
level: 2
class: compact-table
---

# The three layers in Codex

| Layer | Codex mechanism | File |
| --- | --- | --- |
| 1. What it can do | Sandbox + approvals, then **rules** for specific commands | `~/.codex/config.toml`, `~/.codex/rules/default.rules` |
| 2. How it writes code | Project instructions | `AGENTS.md` |
| 3. How it thinks | Design docs, stage checklists, skills | `design/`, `agent-constraints/`, `.agents/skills/` |
| The gate | A `prompt` rule on `gh pr create` | `~/.codex/rules/default.rules` |

Rule of thumb: undoable with `git checkout` → **allow**. Leaves the working tree → **ask**.

---
hideInToc: true
level: 2
---

# Layer 1, part 1: the sandbox already draws the line

```toml
# ~/.codex/config.toml
sandbox_mode = "workspace-write"     # edit and run freely inside the repository
approval_policy = "on-request"       # ask before going beyond it

[sandbox_workspace_write]
network_access = false               # remotes, PRs and clouds need approval
```

- `workspace-write` is the "undoable with `git checkout`" half: edits and local commands inside the repo run without prompts
- With the network off, `git push`, `gh pr create`, `aws`, `gcloud` and `az` can't reach anything without asking. That's the "leaves the working tree" half
- This is the default for a git repository, so most of Layer 1 is already there

---
hideInToc: true
level: 2
---

# Layer 1, part 2: rules for what the sandbox can't see

The sandbox can't tell `git reset --hard` from `git status`; both stay inside the repo. Rules can.

```python
# ~/.codex/rules/default.rules
prefix_rule(pattern = ["git", "push", ["--force", "-f"]], decision = "prompt")
prefix_rule(pattern = ["git", "reset", "--hard"], decision = "prompt")
prefix_rule(pattern = ["git", "clean", "-f"], decision = "prompt")
prefix_rule(pattern = ["git", "branch", "-D"], decision = "prompt")
prefix_rule(pattern = ["rm", "-rf"], decision = "prompt")
prefix_rule(pattern = ["sudo"], decision = "forbidden",
            justification = "Run privileged commands yourself")
prefix_rule(pattern = ["gh", "pr", ["create", "merge"]], decision = "prompt")
prefix_rule(pattern = ["gh", "api"], decision = "prompt")
```

Test a rule before trusting it: `codex execpolicy check --pretty --rules ~/.codex/rules/default.rules -- git push -f origin main`

<!--
Rules are documented as experimental. When several rules match, the most restrictive decision wins (forbidden > prompt > allow). Rules only match commands written as plain && / || / ; / | chains; anything more complex is matched as one command.
-->

---
hideInToc: true
level: 2
---

# Layers 2, 3 and the gate

**Layer 2**: `AGENTS.md` at the repo root. One page of conventions with reasons, ending with "change only what the task needs." Nested `AGENTS.md` files refine it per directory.

**Layer 3**: point at it from `AGENTS.md`:

```markdown
## Before you change anything
- Read the design doc for the area: design/<area>.md
- Follow agent-constraints/triage.md, then planning.md, review.md, implementation.md
```

Domain knowledge goes in skills: `.agents/skills/<name>/SKILL.md` (repo) or `~/.agents/skills/` (you).

**The gate**: the `gh pr create` rule, plus the network being off, means the only interruption is when work is about to go public.
