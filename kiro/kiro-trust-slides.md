---
layout: section
---

# Kiro: trust layers

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# The three layers in Kiro

| Layer | Kiro mechanism | File |
| --- | --- | --- |
| 1. What it can do | Capability rules: `allow`, `ask`, `deny` | `~/.kiro/settings/permissions.yaml` |
| 2. How it writes code | Steering files | `AGENTS.md`, `.kiro/steering/*.md` |
| 3. How it thinks | Specs, design docs, stage checklists, skills | `.kiro/specs/`, `design/`, `.kiro/skills/` |
| The gate | An `ask` rule on `gh pr create` | `~/.kiro/settings/permissions.yaml` |

Rule of thumb: undoable with `git checkout` → **allow**. Leaves the working tree → **ask**.

---
hideInToc: true
---

# Layer 1: ~/.kiro/settings/permissions.yaml

```yaml
rules:
  - capability: shell
    match: ["*"]
    effect: allow
  - capability: shell
    match: ["git push --force*", "git push -f*", "git reset --hard*",
            "git clean -f*", "git branch -D*", "rm -rf *",
            "gh pr create*", "gh pr merge*", "gh issue close*", "gh api *",
            "aws *", "gcloud *", "az *"]
    effect: ask
  - capability: shell
    match: ["sudo *"]
    effect: deny
```

---
hideInToc: true
---

# Why it's built this way

- **Deny > ask > allow**, whatever the order: the broad `*` allow can't override the specific asks
- **Compound commands are split**, so `make && git push --force` still hits the ask rule
- **Permissions can't live in the repository.** The workspace file is stored per user, outside the repo, so a cloned repository can't grant itself permissions. Share the trust model as a documented file people copy, or push it to `~/.kiro` with device management

**Know the limits**

- Shell patterns only support `*`: `rm -fr` doesn't match `rm -rf *`
- `--trust-all-tools` and autopilot skip the prompts, including the gate
- Start with `match: ["git *", "npm *", ...]` instead of `"*"` if you're new to this, and widen it

---
hideInToc: true
---

# Layers 2, 3 and the gate

**Layer 2**: `AGENTS.md` plus steering in `.kiro/steering/`. `structure.md` is a natural home for "the CLI never imports internals, because...".

**Layer 3**: Kiro builds part of it in. A **spec** is a plan you approve before code is written:

| Spec file | Matches the article's stage |
| --- | --- |
| `requirements.md` | Triage: what's actually wrong or wanted |
| `design.md` | Planning: architecture, docs and test impact |
| `tasks.md` | Implementation, run task by task |

Add the adversarial review as a hook or a custom agent; domain knowledge goes in `.kiro/skills/`.

**The gate**: the `ask` on `gh pr create`.
