---
layout: section
---

# Amp: trust layers

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# The three layers in Amp

| Layer | Amp mechanism | Where |
| --- | --- | --- |
| 1. What it can do | No prompts by default: a plugin, disabled tools, and the remote's own rules | `.amp/plugins/`, `amp.tools.disable`, GitHub settings |
| 2. How it writes code | Guidance files | `AGENTS.md` |
| 3. How it thinks | Design docs, stage checklists, skills | `design/`, `agent-constraints/`, `.agents/skills/` |
| The gate | A plugin that asks before `gh pr create`, backed by branch protection | `.amp/plugins/`, the repository host |

Rule of thumb: undoable with `git checkout` → **allow**. Leaves the working tree → **ask**.

---
hideInToc: true
---

# Layer 1 starts from "allow everything"

Amp runs tools without asking. The "allow" half of the rule is already done; what's missing is the "ask" half. Three ways to add it, strongest last:

1. **A tool-approval plugin** in `.amp/plugins/`: inspect each shell command and ask before the destructive and publishing ones (see Amp's plugin docs for the permissions example)
2. **Disable what it never needs**: `"amp.tools.disable": [...]` removes tools entirely
3. **Move the gate to the remote**, where no local setting can skip it:
   - branch protection on `main` with required reviews
   - a token for the agent that can push branches but not merge, and no cloud credentials in its environment

<!--
Amp's docs describe permissions through plugins rather than a settings key; the plugin API is documented at ampcode.com/docs/customize/plugins. Check it before presenting.
-->

---
hideInToc: true
---

# Why it's built this way

- **Amp trades prompts for speed.** That's a reasonable default inside a git repository, where every local change can be undone
- **What it can't undo is outside the working tree**: pushes, PRs, cloud resources. Those need a gate somewhere
- **A remote-side gate is stronger than a prompt**: branch protection holds whatever the agent runs, however the command is spelled
- **Credentials are permissions**: if the shell has `aws` credentials, the agent does too. Give it an environment with only what the task needs

**Know the limits**

- Without a plugin there's no human prompt before `gh pr create`; review PRs before merge, not before creation
- Use a container or a disposable VM for unfamiliar repositories

---
hideInToc: true
---

# Layers 2, 3 and the gate

**Layer 2**: `AGENTS.md` at the repo root, shared with other agents. Use `globs:` frontmatter in nested files for rules that only apply to part of the tree:

```markdown
---
globs: ["src/cli/**"]
---
The CLI never imports from src/internal: it keeps the CLI decoupled from internals.
```

**Layer 3**: design docs and stage checklists referenced from `AGENTS.md`; domain knowledge in `.agents/skills/<name>/SKILL.md`.

**The gate**: your plugin's prompt if you have one, and always the required review on the remote.
