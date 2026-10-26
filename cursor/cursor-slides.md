---
layout: section
---

# Cursor

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
---

# Cursor: editor and CLI

| Form | What it is |
| --- | --- |
| **Cursor** | A VS Code-based editor with an agent built in (Agent, Plan and Ask modes) |
| **Cursor CLI** (`agent`) | The same agent in your terminal, sharing your rules and MCP servers |

Both sign in with your Cursor account; the CLI also takes an API key (`CURSOR_API_KEY`) for scripts.

The editor installs from cursor.com for macOS, Windows and Linux. The rest of this section is about the CLI, because it works the same way as the other agents here.

---
hideInToc: true
class: compact-table
---

# Install the Cursor CLI

| Platform | Command |
| --- | --- |
| macOS, Linux, WSL | `curl https://cursor.com/install -fsS \| bash` |
| Windows PowerShell | `irm 'https://cursor.com/install?win32=true' \| iex` |

If `agent` isn't found afterwards, add `~/.local/bin` to your `PATH`:

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc   # or ~/.bashrc
source ~/.zshrc
```

- `agent --version` checks the install; it updates itself (`agent update` to force it)
- `agent login` signs in through the browser; `agent status` shows who you are

---
hideInToc: true
---

# Getting started

```bash
agent login

cd my-project
agent                        # interactive; Shift+Tab cycles Agent / Plan / Ask
```

Then, inside the session:

1. `/ask` and ask a question first: *"Explain how requests flow through this service"*
2. `/plan` and ask for a small change; read the plan
3. Switch back to Agent mode and let it implement, approving commands as it asks (`y` / `n`)
4. `Ctrl+R` reviews the changes; `/rewind` steps back
5. Review with `git diff` before you commit

---
hideInToc: true
---

# Rules

| File | Scope |
| --- | --- |
| `.cursor/rules/*.mdc` | Project rules with frontmatter; folders allowed |
| `AGENTS.md`, `CLAUDE.md` | Plain Markdown at the root (and nested `AGENTS.md`); read as rules |
| User and Team rules | Set in the editor and the Cursor dashboard |

```markdown
---
description: React component conventions
globs: src/components/**/*.tsx
alwaysApply: false
---
Components are function components with named exports.
```

`alwaysApply: true` = every request; `globs` = matching files; only `description` = the agent decides; none = only when you `@`-mention it. A plain `.md` in `.cursor/rules` is ignored.

---
hideInToc: true
class: compact-table
---

# Permissions

`~/.cursor/cli-config.json` (you) or `.cursor/cli.json` (the project):

```json
{
  "permissions": {
    "allow": ["Shell(ls)", "Shell(npm)", "Read(src/**)", "Write(src/**)"],
    "deny": ["Shell(sudo)", "Read(.env*)", "Write(**/*.key)"]
  }
}
```

| Token | Matches |
| --- | --- |
| `Shell(git)` | The first word of the command: **every** `git` subcommand |
| `Read(glob)`, `Write(glob)` | Paths; relative to the workspace |
| `WebFetch(domain)`, `Mcp(server:tool)` | Domains and MCP tools |

Deny beats allow. Anything not allowed prompts for approval. `--force` (alias `--yolo`) runs everything not denied.

---
hideInToc: true
class: compact-table
---

# In the session and scripting

| Input | Does |
| --- | --- |
| `@file` | Adds a file or folder |
| `/plan`, `/ask` | Switch mode |
| `/model`, `/mcp`, `/sandbox` | Model, MCP servers, sandbox |
| `/resume`, `/rewind`, `/summarize` | Conversations and context |
| `&` prefix | Sends the task to a Cursor cloud agent |

```bash
agent -p "Summarize what changed on this branch" --output-format json
agent -p --force "Fix the lint errors"     # without --force, changes are only proposed
agent --continue                            # resume the last chat
```

MCP servers: `.cursor/mcp.json` (project) or `~/.cursor/mcp.json`, shared with the editor.
