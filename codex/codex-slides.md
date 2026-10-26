---
layout: section
---

# Codex

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# Install Codex

| Platform | Command |
| --- | --- |
| macOS, Linux | `curl -fsSL https://chatgpt.com/codex/install.sh \| sh` |
| Windows PowerShell | `powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 \| iex"` |
| Homebrew (macOS) | `brew install --cask codex` |
| npm (any platform) | `npm install -g @openai/codex` |

- Prebuilt binaries are also on the GitHub releases page (openai/codex)
- Sign in with a ChatGPT plan (Plus, Pro, Business, Edu, Enterprise) or an API key
- Also: IDE extension (VS Code, Cursor, Windsurf), desktop app (`codex app`) and Codex Cloud (`codex cloud`)

---
hideInToc: true
---

# Getting started

```bash
codex --version

cd my-project                # a git repository
codex                        # choose "Sign in with ChatGPT"
```

Then, inside the session:

1. `/init`: writes an `AGENTS.md` from your repository. Read it and trim it
2. `/status`: check the sandbox and approval mode you're in
3. Ask a question first: *"Explain how requests flow through this service"*
4. Ask for a small change; approve anything it wants to run outside the sandbox
5. `/diff` to see what changed, `/review` for a second look, then commit

---
hideInToc: true
---

# AGENTS.md

- Global: `~/.codex/AGENTS.md`
- Project: one `AGENTS.md` per directory, from the repository root down to where you started Codex
- Files are joined root first, so the closest file has the last word
- `AGENTS.override.md` in a directory replaces that directory's `AGENTS.md`
- Capped at 32 KiB by default (`project_doc_max_bytes`)

`AGENTS.md` is an open convention that many tools read, so one file can serve everyone on the team, whatever they run.

<!--
project_doc_fallback_filenames in config.toml lets Codex read other names too, such as CLAUDE.md, if a repo already has one.
-->

---
hideInToc: true
class: compact-table
---

# Sandbox and approvals

Two separate controls:

| `--sandbox` (`-s`) | Commands can |
| --- | --- |
| `read-only` | Read files only |
| `workspace-write` | Write inside the project; network off by default |
| `danger-full-access` | Anything |

| `--ask-for-approval` (`-a`) | Codex asks |
| --- | --- |
| `on-request` | When it needs to go beyond the sandbox |
| `never` | Never; what the sandbox blocks just fails |

Git repositories default to `workspace-write` with `on-request`. `--yolo` turns off both. Disposable environments only.

---
hideInToc: true
---

# config.toml

`~/.codex/config.toml` for you; `.codex/config.toml` in a trusted project.

```toml
approval_policy = "on-request"
sandbox_mode = "workspace-write"

[sandbox_workspace_write]
network_access = false

[mcp_servers.context7]
command = "npx"
args = ["-y", "@upstash/context7-mcp"]
```

- `codex -c key=value` overrides a setting for one run
- `--profile <name>` loads `~/.codex/<name>.config.toml` on top
- `codex mcp add <name> -- <command>` adds an MCP server from the shell

---
hideInToc: true
class: compact-table
---

# In the session

| Command | Does |
| --- | --- |
| `/status` | Model, sandbox, approvals and token use |
| `/permissions` | Changes sandbox and approval mode |
| `/model` | Changes model and reasoning effort |
| `/review` | Reviews uncommitted changes, a commit, or against a base branch |
| `/diff` | Shows the changes made so far |
| `/compact` | Summarizes the conversation to free context |
| `/new`, `/resume`, `/fork` | Fresh conversation, pick up an old one, branch one |
| `/mcp`, `/skills` | MCP servers and skills |

`codex -i screenshot.png` attaches an image; `codex --search` lets it search the web.

---
hideInToc: true
---

# Scripting with codex exec

```bash
# Non-interactive; read-only unless you say otherwise
codex exec "Summarize what changed on this branch"

# Allowed to edit the workspace
codex exec --sandbox workspace-write "Fix the failing unit tests"

# Machine-readable events, and the final answer in a file
codex exec --json -o result.md "Write release notes from git log"

# Carry on from the last run
codex exec resume --last "Now update the changelog"
```

Progress goes to stderr and the final answer to stdout, so it pipes cleanly.
