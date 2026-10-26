---
layout: section
---

# Pi

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
---

# What Pi is

A deliberately minimal, open source (MIT) terminal coding agent, from pi.dev.

- **Small core**: read, search, edit and run commands; everything else is an extension
- **Any model**: Anthropic, OpenAI, Google, Bedrock, Azure, Mistral, Groq, OpenRouter, Ollama and more
- **No permission prompts, by design**: it runs with your user's permissions. Contain it yourself
- **Extensible in TypeScript**: tools, commands, keybindings, a permission gate if you want one

Good for people who want to see and control exactly what their agent does.

---
hideInToc: true
class: compact-table
---

# Install Pi

| Platform | Command |
| --- | --- |
| macOS, Linux | `curl -fsSL https://pi.dev/install.sh \| sh` |
| Windows PowerShell | `powershell -c "irm https://pi.dev/install.ps1 \| iex"` |
| npm (Node.js 22.19+) | `npm install -g --ignore-scripts @earendil-works/pi-coding-agent` |
| Nix | `nix profile add github:earendil-works/pi/stable` |

- The installers bring Node.js if needed and pin dependencies; update with `pi update`
- Config, credentials and sessions live in `~/.pi/agent/`

---
hideInToc: true
---

# Getting started

```bash
pi --version

cd my-project
pi
```

Then, inside the session:

1. `/login`: pick a provider; use a subscription or paste an API key
2. `/model` (or `Ctrl+L`): pick a model
3. Ask a question first: *"Explain how requests flow through this service"*
4. Ask for a small change; press `Enter` while it works to steer it, `Esc` to stop
5. Review with `git diff` before you commit

Pi doesn't ask before acting. Start it in a git repository you can reset.

---
hideInToc: true
---

# Instructions and sessions

- `AGENTS.md` is loaded from `~/.pi/agent/`, parent directories and the current directory
- `SYSTEM.md` in a project replaces or extends the default system prompt
- Prompt templates are Markdown files you run as `/name`

| Input | Does |
| --- | --- |
| `!git status` / `!!git status` | Runs a command and sends / doesn't send the output to the model |
| `/new`, `/resume`, `/tree`, `/fork` | Sessions are saved as trees you can branch |
| `/compact`, `/export`, `/share` | Context and sharing |
| `/settings`, `/hotkeys` | Configuration |

---
hideInToc: true
---

# Scripting and extending

```bash
pi -p "Summarize what changed on this branch"
pi --mode json -p "List the TODOs in src/"    # an event stream for tools
pi --continue                                  # resume the last session here
```

- RPC over stdin/stdout and an SDK for embedding Pi in your own tools
- Packages: `pi install npm:<package>` or `pi install git:<repo>`
- Extensions add tools, commands and gates; skills and prompt templates are built in
- No built-in subagents or plan mode: run several Pi sessions (e.g. in tmux), or add an extension
