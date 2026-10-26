---
layout: section
level: 2
---

# Getting started with Amp

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
level: 2
class: compact-table
---

# Install Amp

| Platform | Command |
| --- | --- |
| macOS, Linux | `curl -fsSL https://ampcode.com/install.sh \| bash` |
| Windows | Run the same command inside WSL |

- Updates itself; `amp update` to force it, `amp version` to check
- `amp login` signs in; scripts use `AMP_API_KEY` (a token from Settings, starting `sgamp_`)
- Editors: VS Code, Cursor, Windsurf, Zed and Neovim. Run `amp` in the editor's terminal, press `Ctrl+O`, choose `ide connect`
- Pricing: a free tier, then paid plans and usage credits at the model providers' prices

---
hideInToc: true
level: 2
---

# Getting started

```bash
amp login

cd my-project
amp                          # interactive
```

Then, inside the session:

1. Ask Amp to write an `AGENTS.md` for the repository. Read it and trim it
2. Ask a question first: *"Explain how requests flow through this service"*
3. Ask for a plan before a change: *"Plan this, don't edit yet"*
4. Let it implement and run the tests
5. Review with `git diff` before you commit

Pick how hard Amp works per task with its mode dial: `low`, `medium`, `high`, `ultra`.

---
hideInToc: true
level: 2
---

# AGENTS.md

- Project: `AGENTS.md` in the current directory and every parent up to `$HOME`
- Subtrees: an `AGENTS.md` deeper in the tree is added when Amp reads files there
- Falls back to `AGENT.md` or `CLAUDE.md` in a directory without an `AGENTS.md`
- Global: `~/.config/amp/AGENTS.md`
- `@path` includes another file; `globs:` frontmatter limits a file to matching paths

`AMP_IGNORE_GUIDANCE_FILES` skips files by glob (`'*'` turns them all off).

---
hideInToc: true
level: 2
---

# Settings and permissions

`~/.config/amp/settings.json` (you) or `.amp/settings.json` (the workspace). `amp config edit` opens it.

```json
{
  "amp.tools.disable": ["builtin:web_search"],
  "amp.mcpServers": {
    "context7": { "command": "npx", "args": ["-y", "@upstash/context7-mcp"] }
  }
}
```

- **By default, Amp doesn't ask before running tools.** That's a design choice: it works best in a repository you can reset
- `amp.tools.disable` turns tools off entirely
- Approval rules for specific tools come from a **plugin** (`.amp/plugins/`), not a setting
- `amp.mcpPermissions` allows or rejects MCP servers

---
hideInToc: true
level: 2
class: compact-table
---

# Scripting and extending

```bash
amp -x "Which files in this folder are Markdown? Print only the names."
echo "Summarize this diff" | amp -x
git diff | amp -x "Write a commit message for this diff"
```

| Feature | Where |
| --- | --- |
| MCP servers | `amp mcp add context7 -- npx -y @upstash/context7-mcp` |
| Skills | `.agents/skills/<name>/SKILL.md`, `~/.config/amp/skills/` |
| Subagents | Amp delegates to `Task` subagents on its own, mostly in `medium` mode |
| Plugins | `.amp/plugins/*.ts`: custom modes, subagents, tool approval |
| Cloud | `amp -ox` runs the task on Amp's servers and prints the thread URL |
