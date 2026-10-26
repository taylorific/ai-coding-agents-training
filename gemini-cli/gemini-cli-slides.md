---
layout: section
---

# Gemini CLI

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
---

# Gemini CLI or Antigravity CLI?

- Since June 18, 2026, Google's free tier and Google One plans use **Antigravity CLI** instead of Gemini CLI
- Gemini CLI remains for **Gemini API keys**, **Vertex AI** and paid Code Assist licenses
- It's open source (Apache 2.0): github.com/google-gemini/gemini-cli

The ideas in this section (context files, approval modes, sandboxing, MCP) carry over. Check which one your account gets before the class.

<!--
Verify this slide before presenting: Google has been moving quickly here. The notice is on the Gemini CLI README and docs (geminicli.com/docs).
-->

---
hideInToc: true
class: compact-table
---

# Install and sign in

```bash
npm install -g @google/gemini-cli
# or
brew install gemini-cli
# or run it without installing
npx @google/gemini-cli
```

| Sign-in | Set up |
| --- | --- |
| Google account | Run `gemini`, choose "Sign in with Google"; Workspace accounts also need `GOOGLE_CLOUD_PROJECT` |
| Gemini API key | `export GEMINI_API_KEY=...` |
| Vertex AI | `gcloud auth application-default login`, plus `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` |

Environment variables can also live in `~/.gemini/.env` or the project's `.gemini/.env`.

---
hideInToc: true
---

# GEMINI.md

- Global: `~/.gemini/GEMINI.md`
- Project: `GEMINI.md` in the workspace and its parent directories
- Subdirectories: picked up when a tool touches files there
- All found files are joined and sent with every prompt
- `@./docs/conventions.md` inside a file imports another one
- `/init` drafts one; `/memory show` displays what's loaded

Read `AGENTS.md` instead, or as well, from `settings.json`:

```json
{ "context": { "fileName": ["AGENTS.md", "GEMINI.md"] } }
```

---
hideInToc: true
class: compact-table
---

# Approval modes and sandbox

| Approval mode | Behavior |
| --- | --- |
| `default` | Asks before edits and commands |
| `auto_edit` | File edits go through; commands still ask |
| `plan` | Read-only |
| `yolo` | No prompts. Command line only: `--yolo` |

Sandbox the tools with `-s` / `--sandbox`, or `"tools": { "sandbox": "docker" }` in settings:

- macOS: Seatbelt (`sandbox-exec`) profiles
- Docker or Podman: `ghcr.io/google/gemini-cli` image; network off by default
- Linux: gVisor (`runsc`) and LXC also supported

`security.disableYoloMode` lets an admin turn YOLO off entirely.

---
hideInToc: true
---

# settings.json

`~/.gemini/settings.json` for you; `.gemini/settings.json` in the project wins.

```json
{
  "general": {
    "defaultApprovalMode": "auto_edit",
    "checkpointing": { "enabled": true }
  },
  "tools": { "sandbox": "docker" },
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"]
    }
  }
}
```

`/settings` edits it from inside a session. `gemini mcp add` adds servers from the shell.

---
hideInToc: true
class: compact-table
---

# In the session

| Input | Does |
| --- | --- |
| `@src/` | Adds a file or directory to the prompt |
| `!git status` | Runs a shell command; `!` alone toggles shell mode |
| `/memory` | Shows or reloads the context files |
| `/tools`, `/mcp` | Lists built-in and MCP tools |
| `/chat save <tag>`, `/resume` | Saves and resumes conversations |
| `/compress` | Summarizes the conversation to free context |
| `/restore` | Undoes file changes back to a checkpoint |
| `Esc` `Esc` | Rewinds the conversation |
| `/stats` | Token use and quota |

With checkpointing on, every file-changing tool call is snapshotted first, so `/restore` can undo it.

---
hideInToc: true
---

# Scripting

```bash
# Non-interactive
gemini -p "Explain the architecture of this codebase"

# Structured output for scripts and CI
gemini -p "List the TODOs in src/" --output-format json

# Pipe input in
git diff | gemini -p "Write a commit message for this diff"

# Sandboxed
gemini -s -p "Run the test suite and summarize failures"
```

`--output-format stream-json` emits one JSON event per line. Exit codes: `0` success, `1` error, `42` bad input, `53` turn limit reached.
