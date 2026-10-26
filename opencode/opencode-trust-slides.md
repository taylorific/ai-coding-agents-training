---
layout: section
level: 2
---

# OpenCode: trust layers

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
level: 2
class: compact-table
---

# The three layers in OpenCode

| Layer | OpenCode mechanism | File |
| --- | --- | --- |
| 1. What it can do | `permission` rules: `allow`, `ask`, `deny` | `~/.config/opencode/opencode.json` |
| 2. How it writes code | Instructions | `AGENTS.md`, `instructions` in `opencode.json` |
| 3. How it thinks | Plan agent, design docs, stage checklists, skills | `design/`, `agent-constraints/`, `.agents/skills/` |
| The gate | An `ask` pattern on `gh pr create` | `~/.config/opencode/opencode.json` |

Rule of thumb: undoable with `git checkout` → **allow**. Leaves the working tree → **ask**.

---
hideInToc: true
level: 2
---

# Layer 1: ~/.config/opencode/opencode.json

```json
{
  "permission": {
    "edit": "allow",
    "webfetch": "allow",
    "external_directory": "ask",
    "bash": {
      "*": "allow",
      "git push --force*": "ask", "git push -f*": "ask", "git reset --hard*": "ask",
      "git clean -f*": "ask", "git branch -D*": "ask", "rm -rf *": "ask",
      "gh pr create*": "ask", "gh pr merge*": "ask", "gh issue close*": "ask",
      "gh api *": "ask", "aws *": "ask", "gcloud *": "ask", "az *": "ask",
      "sudo *": "deny"
    }
  }
}
```

---
hideInToc: true
level: 2
---

# Why it's built this way

- **Order matters: the last matching rule wins.** `"*": "allow"` goes first so every specific rule after it can override it. Put it last and it would allow everything
- **`external_directory` asks**: touching files outside the project is the "directory tree" case in the rule
- **One global file**: project `opencode.json` files merge on top, so a repository can tighten rules for itself; keep your baseline in `~/.config/opencode/`
- **The Plan agent** can't edit files, which makes "plan, then approve, then build" a `Tab` away

**Know the limits**

- Patterns match the command text: `git -C . push --force` doesn't match `git push --force*`
- `--auto` approves everything not denied, including the gate
- Start with `"*": "ask"` and allow specific commands if you're new to this

---
hideInToc: true
level: 2
---

# Layers 2, 3 and the gate

**Layer 2**: `AGENTS.md` at the repo root. Pull existing convention files in instead of copying them:

```json
{ "instructions": ["CONTRIBUTING.md", "design/conventions.md"] }
```

**Layer 3**: design docs and stage checklists through `instructions` or `AGENTS.md`; skills in `.agents/skills/<name>/SKILL.md`; a custom agent per stage (`.opencode/agents/review.md`) with its own read-only `permission`.

**The gate**: the `ask` on `gh pr create`.
