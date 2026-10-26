---
layout: section
---

# Codex

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
---

# Install and sign in

```bash
npm install -g @openai/codex
# or
brew install --cask codex
# or the standalone installer (macOS, Linux)
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

```bash
cd my-project
codex            # choose "Sign in with ChatGPT"
```

- Included with ChatGPT Plus, Pro, Business, Edu and Enterprise plans
- An API key works too; scripts can set `CODEX_API_KEY`
- Also an IDE extension (VS Code, Cursor, Windsurf), a desktop app (`codex app`) and Codex Cloud (`codex cloud`)

---
hideInToc: true
---

# AGENTS.md

- Global: `~/.codex/AGENTS.md`
- Project: one `AGENTS.md` per directory, from the repository root down to where you started Codex
- Files are joined root first, so the closest file has the last word
- `AGENTS.override.md` in a directory replaces that directory's `AGENTS.md`
- Capped at 32 KiB by default (`project_doc_max_bytes`)
- `/init` writes a first draft

`AGENTS.md` is an open convention. Other tools read it too, which makes it a good choice for the shared file.

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
network_access = true

[mcp_servers.context7]
command = "npx"
args = ["-y", "@upstash/context7-mcp"]
```

- `codex -c key=value` overrides a setting for one run
- `--profile <name>` loads `~/.codex/<name>.config.toml` on top

---
hideInToc: true
class: compact-table
---

# In the session

| Command | Does |
| --- | --- |
| `/init` | Writes an `AGENTS.md` |
| `/status` | Model, sandbox, approvals and token use |
| `/permissions` | Changes sandbox and approval mode |
| `/model` | Changes model and reasoning effort |
| `/review` | Reviews uncommitted changes, a commit, or against a base branch |
| `/diff` | Shows the changes made so far |
| `/compact` | Summarizes the conversation to free context |
| `/new`, `/resume`, `/fork` | Fresh conversation, pick up an old one, branch one |
| `/mcp` | Lists MCP servers and their tools |

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

Progress goes to stderr and the final answer to stdout, so it pipes cleanly. The GitHub Action and the Codex SDK run the same agent in CI and your own code.
