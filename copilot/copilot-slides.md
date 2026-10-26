---
layout: section
level: 2
---

# Getting started with GitHub Copilot CLI

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
level: 2
class: compact-table
---

# Install Copilot CLI

| Platform | Command |
| --- | --- |
| macOS, Linux (script) | `curl -fsSL https://gh.io/copilot-install \| bash` |
| Homebrew (macOS, Linux) | `brew install --cask copilot-cli` |
| WinGet (Windows) | `winget install GitHub.Copilot` |
| npm (Node.js 22+) | `npm install -g @github/copilot` |

- Needs an active GitHub Copilot plan
- Windows: PowerShell 6 or later
- Binaries are also on the github/copilot-cli releases page
- For scripts: `COPILOT_GITHUB_TOKEN` (or `GH_TOKEN`) with a fine-grained token that has the **Copilot Requests** permission

---
hideInToc: true
level: 2
---

# Getting started

```bash
cd my-project
copilot                      # answer the trust prompt, then /login if asked
```

Then, inside the session:

1. `/init`: creates repository instructions. Read them and trim them
2. Ask a question first: *"Explain how requests flow through this service"*
3. `/plan` (or `Shift+Tab`) and ask for a small change
4. Approve each tool as it asks: once, or for the rest of the session
5. `/diff` to see the changes; review with `git diff` before committing

`/model` picks a model; `/usage` shows what you've used.

---
hideInToc: true
level: 2
---

# Custom instructions

| File | Scope |
| --- | --- |
| `~/.copilot/copilot-instructions.md` | You, in every repository |
| `.github/copilot-instructions.md` | The repository |
| `.github/instructions/**/*.instructions.md` | Paths matching `applyTo:` in the frontmatter |
| `AGENTS.md`, `CLAUDE.md`, `GEMINI.md` | Also read, if present |

- All found files are combined; none overrides another
- `/instructions` lists them and turns them on or off
- Changes apply in a new session (`/new`)

---
hideInToc: true
level: 2
class: compact-table
---

# Trust and tool approval

On first run in a folder: trust it for this session, remember it, or leave.

| Flag | Does |
| --- | --- |
| `--allow-tool='shell(git:*)'` | Allows every `git` command |
| `--deny-tool='shell(git push)'` | Blocks `git push`, even with `--allow-all` |
| `--allow-tool=shell` | Allows all shell commands |
| `--allow-all-paths`, `--allow-url=...` | File access outside the folder, URLs |
| `--allow-all` (`--yolo`) | Everything not denied |

- Read-only actions run without asking; anything that changes your system asks
- Flags last for one session; approvals you save go to `~/.copilot/permissions-config.json`
- `/permissions` shows and changes them in a session

---
hideInToc: true
level: 2
class: compact-table
---

# In the session and scripting

| Input | Does |
| --- | --- |
| `@file`, `#123` | Adds a file / an issue or PR |
| `!git status` | Runs a shell command yourself |
| `/plan`, `/model`, `/context`, `/compact` | Plan, model, context |
| `/agent`, `/mcp`, `/add-dir` | Custom agents, MCP servers, extra folders |
| `/delegate` | Hands the task to Copilot's cloud agent as a PR |

```bash
copilot -p "Summarize what changed on this branch" --allow-all-tools
copilot --continue           # resume the last session here
copilot --resume             # pick a session
```

MCP: the GitHub MCP server is built in; add others with `copilot mcp add` (stored in `~/.copilot/mcp-config.json`, or `.mcp.json` in the repo).
