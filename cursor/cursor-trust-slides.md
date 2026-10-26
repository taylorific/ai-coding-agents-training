---
layout: section
---

# Cursor: trust layers

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# The three layers in Cursor

| Layer | Cursor mechanism | File |
| --- | --- | --- |
| 1. What it can do | `permissions.allow` / `deny`; anything unlisted prompts | `~/.cursor/cli-config.json` |
| 2. How it writes code | Rules | `AGENTS.md`, `.cursor/rules/*.mdc` |
| 3. How it thinks | Design docs, stage checklists, skills | `design/`, `agent-constraints/`, skills |
| The gate | Leave `gh` and `git` unlisted so they prompt | `~/.cursor/cli-config.json` |

Rule of thumb: undoable with `git checkout` → **allow**. Leaves the working tree → **ask**.

---
hideInToc: true
---

# Layer 1: ~/.cursor/cli-config.json

```json
{
  "version": 1,
  "permissions": {
    "allow": [
      "Read(**)", "Write(**)",
      "Shell(ls)", "Shell(cat)", "Shell(grep)", "Shell(find)",
      "Shell(npm)", "Shell(node)", "Shell(make)", "Shell(go)", "Shell(cargo)"
    ],
    "deny": ["Shell(sudo)", "Read(.env*)", "Write(**/*.key)"]
  }
}
```

`git`, `gh`, `rm`, `aws`, `gcloud` and `az` are deliberately **not** listed, so each use prompts.

---
hideInToc: true
---

# Why it's built this way

- **Cursor has no `ask` list.** A command is allowed, denied, or (if unlisted) prompted. "Ask" means "leave it out of `allow`"
- **`Shell(...)` matches the first word only.** `Shell(git)` would allow `git status` *and* `git push --force`, so you can't allow `git` and still be asked about force pushes
- **The trade-off**: either allow `git` and lose the prompt on destructive git, or leave it unlisted and approve every `git` command. Start unlisted; it's cheap to say `y`
- **`--force` / `--yolo` runs everything not denied.** Only the `deny` list survives it, so put the things that must never run there

**Know the limits**

- Turn on the sandbox (`/sandbox`, `--sandbox enabled`) for a hard boundary on files and network
- Project `.cursor/cli.json` can only set permissions; keep the trust model in your user config

<!--
The docs mention a command:args form (e.g. Shell(curl:*)) for matching arguments with globs. Its exact behavior for subcommands isn't documented; test before relying on it.
-->

---
hideInToc: true
---

# Layers 2, 3 and the gate

**Layer 2**: `AGENTS.md` at the repo root (shared with other agents). Add `.cursor/rules/*.mdc` for rules that only apply to some files, using `globs`.

**Layer 3**: reference the design docs and stage checklists from `AGENTS.md`, or as an "Apply Intelligently" rule:

```markdown
---
description: Before changing a subsystem, read its design doc
---
Read design/<area>.md before changing that area. Follow agent-constraints/*.md in order.
```

**The gate**: because `gh` is unlisted, `gh pr create` stops for approval. In headless runs (`agent -p`) nothing is applied without `--force`, so keep publication out of scripts.
