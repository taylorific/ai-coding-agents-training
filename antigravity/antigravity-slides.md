---
layout: section
---

# Antigravity

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
---

# What Antigravity is

Google's agent platform, in three forms:

| Form | What it is |
| --- | --- |
| **Antigravity CLI** (`agy`) | The terminal agent; replaced Gemini CLI for free and Google One accounts on June 18, 2026 |
| **Antigravity IDE** | A standalone editor with an Agent Manager for running several agents at once |
| **Antigravity App** | A desktop command center for agents |

Sign in with a personal Google account (free, AI Plus, Pro or Ultra plans), a business account through Google Cloud, Application Default Credentials, or a Gemini API key. `/usage` shows your quotas.

---
hideInToc: true
class: compact-table
---

# Install the Antigravity CLI

| Platform | Command |
| --- | --- |
| macOS, Linux | `curl -fsSL https://antigravity.google/cli/install.sh \| bash` |
| Windows PowerShell | `irm https://antigravity.google/cli/install.ps1 \| iex` |
| Windows CMD | `curl -fsSL https://antigravity.google/cli/install.cmd -o install.cmd && install.cmd && del install.cmd` |

- Installs `agy` to `~/.local/bin` (macOS, Linux) or `%LOCALAPPDATA%\agy\bin` (Windows)
- Needs macOS 12+, Windows 10 64-bit+, or Linux with glibc 2.28+
- The IDE and App: download the installer for your platform from antigravity.google/download

---
hideInToc: true
---

# Getting started

```bash
agy --version

cd my-project
agy                          # first run: theme, trust this folder, sign in
```

Then, inside the session:

1. Ask a question first: *"Explain how requests flow through this service"*
2. `/plan` (or `Shift+Tab` to plan mode) and ask for a small change
3. Review the plan artifact with `Ctrl+R`, then let it implement
4. `/rewind` if it goes wrong; review with `git diff` before committing
5. `Ctrl+D` or `/exit` to leave

In the IDE: open a folder, sign in, and open the Agent Manager with `Cmd+E` / `Ctrl+E`.

---
hideInToc: true
---

# Rules files

| File | Scope |
| --- | --- |
| `~/.gemini/AGENTS.md` or `~/.gemini/GEMINI.md` | You, in every project |
| `AGENTS.md` or `GEMINI.md` | The project; no frontmatter |
| `.agents/rules/*.md` | Extra project rules, with a `trigger:` frontmatter |

- `trigger:` is `always_on`, `model_decision` (needs `description`), `glob` (needs `globs`) or `manual`
- Rules add up rather than replace; the more specific directory wins a conflict
- Budget: 24,000 bytes per file, about 20,000 tokens for always-on rules

---
hideInToc: true
class: compact-table
---

# Modes and permissions

| Mode (`--mode`, `Shift+Tab`) | Behavior |
| --- | --- |
| `default` | Requests review before acting |
| `accept-edits` | File edits go through; commands still ask |
| `plan` | Read-only |
| `auto` | Proceeds inside the terminal sandbox (preview; personal accounts) |

Per-command rules in `~/.gemini/antigravity-cli/settings.json`:

```json
{ "permissions": {
    "allow": ["command(git status)", "command(npm test)"],
    "ask":   ["command(git push)"],
    "deny":  ["command(sudo)"] } }
```

Deny beats ask beats allow. `--dangerously-skip-permissions` turns prompts off: disposable environments only.

---
hideInToc: true
class: compact-table
---

# In the session and scripting

| Input | Does |
| --- | --- |
| `/plan`, `/goal` | Plan first / set a goal to work toward |
| `/permissions`, `/config` | Edit permissions and settings |
| `/mcp`, `/skills`, `/hooks`, `/agents` | Extensions |
| `/resume`, `/rewind` | Pick up a conversation / step back |
| `/usage` | Quotas |

```bash
agy -p "Summarize what changed on this branch" --output-format json
agy -c                       # continue the last conversation
agy --sandbox                # run commands in the terminal sandbox
```

MCP servers: `~/.gemini/config/mcp_config.json`, or `.agents/mcp_config.json` in the project.
