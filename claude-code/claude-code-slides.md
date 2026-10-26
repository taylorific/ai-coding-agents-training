---
layout: section
---

# Claude Code

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
---

# Install and sign in

```bash
# Native installer (macOS, Linux, WSL)
curl -fsSL https://claude.ai/install.sh | bash

# or Homebrew
brew install --cask claude-code
```

```bash
cd my-project
claude            # first run opens a browser to sign in
claude doctor     # check the install
```

Sign in with a Claude subscription (Pro, Max, Team, Enterprise) or an Anthropic Console API key. Enterprises can also run it through Amazon Bedrock, Google Vertex AI or Microsoft Foundry.

Also available as a desktop app, in VS Code and JetBrains, and on the web at claude.ai/code.

---
hideInToc: true
---

# CLAUDE.md

| File | Scope |
| --- | --- |
| `~/.claude/CLAUDE.md` | You, in every project |
| `./CLAUDE.md` or `./.claude/CLAUDE.md` | The project; commit it |
| `subdir/CLAUDE.md` | Read when Claude works in that directory |

- `/init` drafts one from your repository
- `/memory` opens the files for editing
- `@path/to/file.md` inside CLAUDE.md imports another file
- Want one file for every agent? Keep `AGENTS.md` and put `@AGENTS.md` in `CLAUDE.md`

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

`/permissions` shows and edits the allow and deny rules.

---
hideInToc: true
---

# Settings and allow-lists

| File | Scope |
| --- | --- |
| `~/.claude/settings.json` | You, everywhere |
| `.claude/settings.json` | The project, shared through git |
| `.claude/settings.local.json` | You, in this project; git-ignored |

```json
{
  "permissions": {
    "allow": ["Bash(npm run test:*)", "Bash(git diff:*)"],
    "deny": ["Read(./.env)", "Bash(git push:*)"]
  }
}
```

Allow narrow command patterns, and deny reading secret files outright.

---
hideInToc: true
class: compact-table
---

# In the session

| Input | Does |
| --- | --- |
| `@src/app.ts` | Adds a file to the prompt |
| `!npm test` | Runs a shell command yourself; output goes into context |
| `Esc` | Interrupts Claude |
| `Esc` `Esc` | Rewinds to an earlier message, and optionally the code |
| `/clear` | Starts a fresh conversation |
| `/compact` | Summarizes the conversation to free context |
| `/model`, `/effort` | Changes model or reasoning effort |
| `/review` | Reviews your current changes |
| `claude -c` / `claude -r` | Continues the last session / picks one to resume |

---
hideInToc: true
---

# Extending Claude Code

| Mechanism | Where |
| --- | --- |
| MCP servers | `claude mcp add <name> -- <command>`; project servers in `.mcp.json` |
| Skills | `.claude/skills/<name>/SKILL.md`, loaded when relevant or run as `/<name>` |
| Subagents | `.claude/agents/<name>.md`; manage with `/agents` |
| Hooks | `hooks` in settings.json: scripts on `PreToolUse`, `PostToolUse`, `Stop`, ... |
| Plugins | Bundles of the above: `/plugin` to browse and install |

```bash
claude mcp add github -- npx -y @modelcontextprotocol/server-github
claude mcp list
```

---
hideInToc: true
---

# Scripting and parallel work

```bash
# Non-interactive: print the answer and exit
claude -p "Summarize what changed on this branch" --output-format json

# Only the tools you allow
claude -p "Fix the lint errors" --allowedTools "Edit" "Bash(npm run lint:*)"

# Its own git worktree, so it doesn't collide with your checkout
claude -w fix-login
```

- `--bg` starts a session in the background; `claude agents` lists them
- `claude --cloud "<task>"` runs it in a cloud sandbox instead of on your machine
- The Agent SDK and the GitHub Action run the same agent from your own code and CI
