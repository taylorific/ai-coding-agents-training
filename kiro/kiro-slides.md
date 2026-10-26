---
layout: section
---

# Kiro

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
---

# Kiro: IDE and CLI

| Form | What it is |
| --- | --- |
| **Kiro IDE** | AWS's agentic editor, built around **specs**: requirements, design and tasks before code |
| **Kiro CLI** (`kiro-cli`) | The same agent in your terminal |

Sign in with GitHub, Google, AWS Builder ID, or your organization (IAM Identity Center, Okta, Entra).

Plans: Free (50 credits a month), then Pro, Pro+, Pro Max and Power with more credits.

---
hideInToc: true
class: compact-table
---

# Install Kiro

| What | Platform | How |
| --- | --- | --- |
| IDE | macOS, Windows, Linux | Download the installer from kiro.dev/downloads |
| CLI | macOS, Linux | `curl -fsSL https://cli.kiro.dev/install \| bash` |
| CLI | Windows 11 | Supported in PowerShell; see kiro.dev/downloads for the installer |

```bash
kiro-cli doctor              # check the install
kiro-cli login               # browser sign-in; --use-device-flow on remote machines
```

The IDE runs on Windows 10/11 (x64, ARM64), macOS (Apple silicon, Intel), and Ubuntu 24+, Debian 13+, Fedora 40+, Arch and Mint 22+.

---
hideInToc: true
---

# Getting started

```bash
kiro-cli login

cd my-project
kiro-cli                     # trust the workspace when asked
```

Then, inside the session:

1. `/guide`: a tour of what Kiro can do
2. Ask a question first: *"Explain how requests flow through this service"*
3. `Shift+Tab` into plan mode and ask for a small change
4. Approve tools as it asks; `/tools trust <name>` stops asking for one
5. Review with `git diff` before you commit

In the IDE: open a folder and start a **spec** for anything bigger than a quick fix.

---
hideInToc: true
---

# Steering files

| File | Scope |
| --- | --- |
| `~/.kiro/steering/*.md` | You, in every project |
| `.kiro/steering/*.md` | The project: start with `product.md`, `tech.md`, `structure.md` |
| `AGENTS.md` | Also read, always included |

```markdown
---
inclusion: fileMatch
fileMatchPattern: "src/api/**"
---
Every handler validates its input with the shared schema.
```

`inclusion` is `always` (default), `fileMatch`, `manual` (use with `#name`) or `auto` (Kiro decides from `name` and `description`).

---
hideInToc: true
class: compact-table
---

# Specs, hooks and permissions

| Feature | What it does |
| --- | --- |
| **Specs** | `requirements.md` → `design.md` → `tasks.md`, then runs the tasks in order |
| **Hooks** | `.kiro/hooks/*.json`: run a command or an agent on events like `PostFileSave`, `PreToolUse` |
| **Autopilot / Supervised** | IDE setting: act freely, or stop for review |
| **Permissions** | `~/.kiro/settings/permissions.yaml`: `allow`, `ask` or `deny` per capability |

```yaml
rules:
  - capability: shell
    match: ["git *", "npm *", "npx *"]
    effect: allow
```

Anything without a rule asks. `--trust-all-tools` turns prompts off: disposable environments only.

---
hideInToc: true
---

# Scripting and extending

```bash
kiro-cli chat --no-interactive "Summarize what changed on this branch"

kiro-cli chat --no-interactive --trust-tools=read_file,grep_search \
  "Find every TODO in src/"

kiro-cli chat --resume       # pick up the last conversation here
```

- MCP servers: `.kiro/settings/mcp.json` (project) or `~/.kiro/settings/mcp.json`; `kiro-cli mcp add`
- Custom agents: `.kiro/agents/<name>.json`; switch with `/agent`
- Skills: `.kiro/skills/<name>/SKILL.md`
