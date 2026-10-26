---
layout: section
---

# Claude Code: trust layers

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# The three layers in Claude Code

| Layer | Claude Code mechanism | File |
| --- | --- | --- |
| 1. What it can do | `permissions.allow` / `ask` / `deny` | `~/.claude/settings.json` |
| 2. How it writes code | Project instructions | `CLAUDE.md` (or `@AGENTS.md`) |
| 3. How it thinks | Design docs, stage checklists, skills | `design/`, `agent-constraints/`, `.claude/skills/` |
| The gate | An `ask` rule on `gh pr create` | `~/.claude/settings.json` |

Claude Code is the agent the original article was written against, so it maps one to one.

Rule of thumb: undoable with `git checkout` → **allow**. Leaves the working tree → **ask**.

---
hideInToc: true
---

# Layer 1: ~/.claude/settings.json

```json
{
  "permissions": {
    "allow": [
      "Read", "Edit", "Write", "Glob", "Grep", "Bash", "WebFetch", "WebSearch",
      "Bash(gh pr view *)", "Bash(gh pr checks *)", "Bash(gh issue view *)"
    ],
    "ask": [
      "Bash(git push --force *)", "Bash(git push -f *)", "Bash(git reset --hard *)",
      "Bash(git clean -f *)", "Bash(git branch -D *)", "Bash(rm -rf *)", "Bash(sudo *)",
      "Bash(gh pr create *)", "Bash(gh pr merge *)", "Bash(gh issue close *)",
      "Bash(gh api *)", "Bash(aws *)", "Bash(gcloud *)", "Bash(az *)"
    ]
  }
}
```

---
hideInToc: true
---

# Why it's built this way

- **One global file**, not per-repo "always allow" clicks in `settings.local.json`
- **`ask` beats `allow`**: rules are checked deny → ask → allow
- **Read-only `gh` is allowed; `gh api` asks**: it can do anything the token can

**Know the limits**

- Prompts match the command as written: `git -C . push --force` or `sh -c 'rm -rf …'` slip past the pattern
- New to this? Start with scoped `Bash(...)` allows instead of bare `Bash`, and widen as you learn what the agent needs
- For a hard boundary, add the sandbox (`/sandbox`) or run in a container. Rules shape the workflow; the sandbox enforces it

---
hideInToc: true
---

# Layers 2, 3 and the gate

**Layer 2**: `CLAUDE.md` at the repo root. One page of conventions with reasons, ending with "change only what the task needs."

**Layer 3**: point at it from `CLAUDE.md`, so every session knows where to look:

```markdown
## Before you change anything
- Read the design doc for the area: design/<area>.md
- Follow agent-constraints/triage.md, then planning.md, review.md, implementation.md
```

Domain knowledge goes in skills: `.claude/skills/<name>/SKILL.md`, loaded only when relevant.

**The gate**: with this setup Claude triages, plans and implements without prompts, then stops at `gh pr create`. That prompt is where you compare the diff with the plan.
