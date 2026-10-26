---
layout: section
---

# Side by side

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: text-sm compact-table
---

# Same ideas, different names

| | Claude Code | Codex | Gemini CLI |
| --- | --- | --- | --- |
| **Start** | `claude` | `codex` | `gemini` |
| **Instructions** | `CLAUDE.md` | `AGENTS.md` | `GEMINI.md` |
| **Settings** | `.claude/settings.json` | `.codex/config.toml` | `.gemini/settings.json` |
| **Read-only** | `plan` mode | `--sandbox read-only` | `plan` mode |
| **Auto-edit** | `acceptEdits` | `workspace-write` | `auto_edit` |
| **No limits** | `--dangerously-skip-permissions` | `--yolo` | `--yolo` |
| **Script it** | `claude -p` | `codex exec` | `gemini -p` |
| **Resume** | `claude -c` / `-r` | `codex resume` | `/resume` |
| **Add MCP** | `claude mcp add` | `codex mcp add` | `gemini mcp add` |
| **Free context** | `/compact` | `/compact` | `/compress` |

---
hideInToc: true
---

# One instructions file for every agent

Keep the real content in `AGENTS.md`, and point the others at it:

```bash
# Claude Code: import it
echo '@AGENTS.md' > CLAUDE.md
```

```json
// Gemini CLI: .gemini/settings.json
{ "context": { "fileName": ["AGENTS.md"] } }
```

Codex reads `AGENTS.md` already.

A team can then use whichever agent each person prefers, with the same project knowledge.

---
hideInToc: true
---

# Picking one

- **Use what your organization has approved and pays for.** The data-handling terms matter more than benchmark scores
- All three are good enough that **how you use them** matters more than which one you pick
- Differences worth knowing:
  - Sandboxing: Codex and Gemini CLI sandbox commands by default or with one flag; Claude Code leans on permission rules and its own sandbox setting
  - Open source: Codex and Gemini CLI are; Claude Code isn't
- Try the same real task in two of them. You'll learn more than from any comparison table

<!--
Keep this slide fair and short; it dates fastest. Update it before each delivery.
-->
