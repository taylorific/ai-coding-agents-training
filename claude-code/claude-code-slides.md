---
layout: section
---

# Claude Code

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# Install Claude Code

| Platform | Command |
| --- | --- |
| macOS, Linux, WSL | `curl -fsSL https://claude.ai/install.sh \| bash` |
| Windows PowerShell | `irm https://claude.ai/install.ps1 \| iex` |
| Homebrew (macOS) | `brew install --cask claude-code` |
| WinGet (Windows) | `winget install Anthropic.ClaudeCode` |
| npm (Node.js 22+) | `npm install -g @anthropic-ai/claude-code` |

- Windows: also install Git for Windows (for Git Bash); use WSL 2 if you want sandboxing
- Needs a Pro, Max, Team or Enterprise plan, or an Anthropic Console account

<!--
Windows CMD: curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
The native installer updates itself; Homebrew, WinGet and npm installs don't.
Claude Code is also a desktop app, VS Code and JetBrains extensions, and on the web at claude.ai/code.
-->

---
hideInToc: true
---

# Getting started

```bash
claude --version
claude doctor                # check the install and settings

cd my-project
claude                       # first run opens a browser to sign in
```

Then, inside the session:

1. `/init`: drafts a `CLAUDE.md` from your repository. Read it and trim it
2. Ask a question first: *"Explain how requests flow through this service"*
3. Switch to plan mode (`Shift+Tab`) and ask for a small change
4. Approve the plan, let it edit, and have it run the tests
5. Review with `git diff` before you commit

---
hideInToc: true
---

# CLAUDE.md

| File | Scope |
| --- | --- |
| `~/.claude/CLAUDE.md` | You, in every project |
| `./CLAUDE.md` or `./.claude/CLAUDE.md` | The project; commit it |
| `subdir/CLAUDE.md` | Read when Claude works in that directory |

- `/memory` opens the files for editing
- `@path/to/file.md` inside CLAUDE.md imports another file
- Already have an `AGENTS.md`? Put `@AGENTS.md` in `CLAUDE.md` instead of copying it

<!--
Claude Code also keeps an automatic memory per project, where it saves things it learned across sessions. /memory shows that too.
-->

---
hideInToc: true
class: compact-table
---

# Permission modes

`Shift+Tab` cycles modes during a session; `--permission-mode` sets one at start.

| Mode | Behavior |
| --- | --- |
| `manual` | Asks before edits and commands |
| `acceptEdits` | File edits go through; commands still ask |
| `plan` | Read-only: researches and proposes a plan |
| `auto` | A classifier approves safe actions and asks about risky ones |
| `dontAsk` | Denies anything not already allowed, without asking |
| `bypassPermissions` | No checks. Disposable sandboxes only |

`/permissions` shows and edits the allow, ask and deny rules.

---
hideInToc: true
---

# Settings

| File | Scope |
| --- | --- |
| `~/.claude/settings.json` | You, everywhere |
| `.claude/settings.json` | The project, shared through git |
| `.claude/settings.local.json` | You, in this project; git-ignored |

```json
{
  "permissions": {
    "allow": ["Bash(npm run test *)", "Bash(git diff *)"],
    "ask": ["Bash(git push *)"],
    "deny": ["Read(./.env)"]
  }
}
```

Rules are checked deny first, then ask, then allow.

---
hideInToc: true
class: compact-table
---

# In the session

| Input | Does |
| --- | --- |
| `@src/app.ts` | Adds a file to the prompt |
| `!npm test` | Runs a shell command yourself; output goes into context |
| `Esc` / `Esc` `Esc` | Interrupts / rewinds to an earlier message, optionally the code |
| `/clear`, `/compact` | Fresh conversation / summarize to free context |
| `/model`, `/effort` | Changes model or reasoning effort |
| `/review` | Reviews your current changes |
| `/mcp`, `/agents`, `/hooks` | MCP servers, subagents, hooks |
| `claude -c` / `claude -r` | Continues the last session / picks one to resume |

Extend it with MCP (`claude mcp add`), skills (`.claude/skills/<name>/SKILL.md`), subagents (`.claude/agents/`), hooks and plugins (`/plugin`).

---
hideInToc: true
---

# Scripting and parallel work

```bash
# Non-interactive: print the answer and exit
claude -p "Summarize what changed on this branch" --output-format json

# Only the tools you allow
claude -p "Fix the lint errors" --allowedTools "Edit" "Bash(npm run lint *)"

# Its own git worktree, so it doesn't collide with your checkout
claude -w fix-login
```

- `--bg` starts a session in the background; `claude agents` lists them
- `claude --cloud "<task>"` runs it in a cloud sandbox
- The Agent SDK and the GitHub Action run the same agent from your code and CI
