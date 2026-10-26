---
layout: section
---

# OpenCode

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# Install OpenCode

| Platform | Command |
| --- | --- |
| macOS, Linux | `curl -fsSL https://opencode.ai/install \| bash` |
| Homebrew (macOS, Linux) | `brew install anomalyco/tap/opencode` |
| npm (any platform) | `npm install -g opencode-ai` |
| Windows | WSL recommended; natively `scoop install opencode` or `choco install opencode` |
| Arch Linux | `paru -S opencode-bin` |

- Open source; works with 75+ model providers
- Also a desktop app, IDE extension and a web UI (`opencode web`)

<!--
OpenCode 1 and 2 both install as "opencode" and can't sit side by side. Plain `brew install opencode` and `pacman -S opencode` now give version 2; the commands on this slide (script, npm, the anomalyco tap, the AUR package) give version 1. Check which one the class should use.
-->

---
hideInToc: true
---

# Getting started

```bash
cd my-project
opencode
```

Then, inside the session:

1. `/connect`: add a provider (an API key, OpenCode Zen, or a GitHub Copilot or ChatGPT subscription)
2. `/models`: pick a model
3. `/init`: writes an `AGENTS.md` from your repository. Read it and trim it
4. Press `Tab` to switch to the **Plan** agent, ask for a small change, read the plan
5. `Tab` back to **Build** to implement; `/undo` and `/redo` step through changes

---
hideInToc: true
---

# AGENTS.md

| File | Scope |
| --- | --- |
| `~/.config/opencode/AGENTS.md` | You, in every project |
| `AGENTS.md` | The project; commit it |
| `CLAUDE.md`, `~/.claude/CLAUDE.md` | Used when there's no `AGENTS.md` |

Pull in more files with `instructions` in `opencode.json`:

```json
{ "instructions": ["CONTRIBUTING.md", "docs/guidelines.md", "docs/conventions/*.md"] }
```

---
hideInToc: true
---

# Agents and permissions

- **Build** (default) has every tool; **Plan** can't edit files. `Tab` switches
- Subagents: `@general` for side tasks, `@explore` for read-only searching

`opencode.json` in the project (or `~/.config/opencode/opencode.json`):

```json
{
  "permission": {
    "edit": "allow",
    "webfetch": "ask",
    "bash": { "*": "ask", "git status": "allow", "npm test": "allow" }
  }
}
```

Values are `allow`, `ask` or `deny`; for patterns, **the last matching rule wins**. Most permissions default to `allow`.

---
hideInToc: true
class: compact-table
---

# In the session and scripting

| Input | Does |
| --- | --- |
| `@file`, `!cmd` | Adds a file / runs a shell command |
| `/undo`, `/redo` | Steps changes back and forward (needs git) |
| `/sessions`, `/new`, `/compact` | Conversations and context |
| `/models`, `/connect` | Models and providers |

```bash
opencode run "Summarize what changed on this branch"
opencode run --format json "List the TODOs in src/"
opencode --continue          # resume the last session
opencode serve               # headless server; opencode run --attach <url>
```

MCP servers go under `mcp` in `opencode.json`; skills in `.opencode/skills/` or `.agents/skills/`.
