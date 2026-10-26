---
layout: section
---

# Side by side

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
level: 2
class: text-sm compact-table
---

# Same ideas, different names (1 of 2)

| | Start | Instructions | Permission rules | Script it |
| --- | --- | --- | --- | --- |
| **Claude Code** | `claude` | `CLAUDE.md` | `~/.claude/settings.json` allow / ask / deny | `claude -p` |
| **Codex** | `codex` | `AGENTS.md` | Sandbox + `~/.codex/rules/*.rules` | `codex exec` |
| **Gemini CLI** | `gemini` | `GEMINI.md` | `~/.gemini/policies/*.toml` | `gemini -p` |
| **Antigravity** | `agy` | `AGENTS.md`, `GEMINI.md` | `antigravity-cli/settings.json` allow / ask / deny | `agy -p` |
| **Cursor** | `agent` | `AGENTS.md`, `.cursor/rules/` | `cli-config.json` allow / deny | `agent -p` |

---
hideInToc: true
level: 2
class: text-sm compact-table
---

# Same ideas, different names (2 of 2)

| | Start | Instructions | Permission rules | Script it |
| --- | --- | --- | --- | --- |
| **Copilot CLI** | `copilot` | `AGENTS.md`, `.github/copilot-instructions.md` | `--allow-tool` / `--deny-tool` | `copilot -p` |
| **Amp** | `amp` | `AGENTS.md` | None by default; plugins | `amp -x` |
| **Kiro** | `kiro-cli` | `AGENTS.md`, `.kiro/steering/` | `~/.kiro/settings/permissions.yaml` | `kiro-cli chat --no-interactive` |
| **OpenCode** | `opencode` | `AGENTS.md` | `opencode.json` allow / ask / deny | `opencode run` |
| **Pi** | `pi` | `AGENTS.md` | None by design; contain it | `pi -p` |

`AGENTS.md` is read by nine of the ten, directly or as an option.

---
hideInToc: true
level: 2
---

# One instructions file for every agent

Keep the real content in `AGENTS.md`, and point the rest at it:

| Agent | How |
| --- | --- |
| Codex, Cursor, Copilot, Amp, Kiro, OpenCode, Pi, Antigravity | Read `AGENTS.md` already |
| Claude Code | `CLAUDE.md` containing `@AGENTS.md` |
| Gemini CLI | `"context": { "fileName": ["AGENTS.md"] }` in `.gemini/settings.json` |

Skills follow the same pattern: `.agents/skills/<name>/SKILL.md` is read by Codex, Gemini CLI, Copilot, Amp and OpenCode; Claude Code uses `.claude/skills/`.

A team can then use whichever agent each person prefers, with the same project knowledge.

---
hideInToc: true
level: 2
---

# How each one handles "ask"

| Approach | Agents | What it means for the trust model |
| --- | --- | --- |
| Allow, **ask** and deny lists | Claude Code, Antigravity, Kiro, OpenCode, Gemini CLI | The model maps directly |
| A sandbox plus rules | Codex | The sandbox draws the line; rules catch what it can't see |
| Allow and deny only; unlisted asks | Cursor, Copilot CLI | "Ask" means "leave it off the allow list" |
| No prompts | Amp (by default), Pi | Contain it, and put the gate on the remote |

Whatever the agent, the strongest gate is the one it can't reach: protected branches, required reviews, and credentials scoped to the task.

---
hideInToc: true
level: 2
---

# Picking one

- **Use what your organization has approved and pays for.** The data-handling terms matter more than benchmark scores
- They're all good enough that **how you use them** matters more than which one you pick
- Things that do differ:
  - how much control you get over prompts (see the previous slide)
  - which models you can use: one vendor's, or any provider (OpenCode, Pi, Kiro, Amp)
  - open source: Codex, Gemini CLI, OpenCode and Pi are
- Try the same real task in two of them. You'll learn more than from any comparison table

<!--
Keep this slide fair and short; it dates fastest. Update it before each delivery.
-->
