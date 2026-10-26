---
layout: section
level: 2
---

# Getting started with Gemini CLI

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
level: 2
---

# Gemini CLI or Antigravity CLI?

- Since June 18, 2026, Google's free tier and Google One plans use **Antigravity CLI** (`agy`) instead of Gemini CLI
- Gemini CLI remains for **Gemini API keys**, **Vertex AI** and paid Code Assist licenses, and isn't tuned for the newest Gemini models
- It's open source (Apache 2.0): github.com/google-gemini/gemini-cli

If you're on a free or Google One account, you'll be using Antigravity instead. The ideas carry over.

<!--
Verify this slide before presenting: Google has been moving quickly here. The notice is on the Gemini CLI README and docs (geminicli.com/docs).
-->

---
hideInToc: true
level: 2
class: compact-table
---

# Install Gemini CLI

| Platform | Command |
| --- | --- |
| npm (Node.js 20+; macOS, Linux, Windows) | `npm install -g @google/gemini-cli` |
| Homebrew (macOS, Linux) | `brew install gemini-cli` |
| MacPorts (macOS) | `sudo port install gemini-cli` |
| Try without installing | `npx @google/gemini-cli` |

| Sign-in | Set up |
| --- | --- |
| Google account | Run `gemini`, choose "Sign in with Google"; Workspace accounts also need `GOOGLE_CLOUD_PROJECT` |
| Gemini API key | `export GEMINI_API_KEY=...` |
| Vertex AI | `gcloud auth application-default login`, plus `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` |

<!--
On Windows, run it from PowerShell (Windows 11 24H2 or later recommended).
-->

---
hideInToc: true
level: 2
---

# Getting started

```bash
gemini --version

cd my-project
gemini                       # pick a sign-in method on first run
```

Then, inside the session:

1. `/init`: drafts a `GEMINI.md` from your repository. Read it and trim it
2. Ask a question first, pointing at files with `@`: *"Explain @src/server.ts"*
3. `/plan` and ask for a small change; read the plan
4. Let it implement in the default mode, approving each edit
5. `/restore` undoes a change if checkpointing is on; review with `git diff`

---
hideInToc: true
level: 2
---

# GEMINI.md

- Global: `~/.gemini/GEMINI.md`
- Project: `GEMINI.md` in the workspace and its parent directories
- Subdirectories: picked up when a tool touches files there
- `@./docs/conventions.md` inside a file imports another one
- `/memory show` displays what's loaded

Read `AGENTS.md` instead, or as well, from `settings.json`:

```json
{ "context": { "fileName": ["AGENTS.md", "GEMINI.md"] } }
```

---
hideInToc: true
level: 2
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

Per-command rules live in the **policy engine**: `~/.gemini/policies/*.toml`.

---
hideInToc: true
level: 2
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
level: 2
class: compact-table
---

# In the session

| Input | Does |
| --- | --- |
| `@src/` | Adds a file or directory to the prompt |
| `!git status` | Runs a shell command; `!` alone toggles shell mode |
| `/memory` | Shows or reloads the context files |
| `/tools`, `/mcp`, `/skills` | Built-in tools, MCP tools, skills |
| `/chat save <tag>`, `/resume` | Saves and resumes conversations |
| `/compress` | Summarizes the conversation to free context |
| `/restore` | Undoes file changes back to a checkpoint |
| `Esc` `Esc` | Rewinds the conversation |
| `/stats` | Token use and quota |

---
hideInToc: true
level: 2
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
