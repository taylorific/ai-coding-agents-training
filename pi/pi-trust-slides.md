---
layout: section
level: 2
---

# Pi: trust layers

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
level: 2
class: compact-table
---

# The three layers in Pi

| Layer | Pi mechanism | Where |
| --- | --- | --- |
| 1. What it can do | None built in: containment, credentials, an optional gate extension | A container or VM, the repository host |
| 2. How it writes code | Instructions | `AGENTS.md`, `SYSTEM.md` |
| 3. How it thinks | Design docs, stage checklists, skills, prompt templates | `design/`, `agent-constraints/`, skills |
| The gate | On the remote: protected branches and required reviews | The repository host |

Rule of thumb: undoable with `git checkout` → **allow**. Leaves the working tree → **ask**.

---
hideInToc: true
level: 2
---

# Layer 1 is yours to build

Pi has no permission system. It "runs with the permissions of the user and process that launched it." So Layer 1 moves out of the agent:

1. **Run it in a container or micro-VM** with only the repository mounted. Pi's docs cover Docker and a VM extension
2. **Give it only the credentials the task needs**: no cloud logins; a Git token that can push branches but not merge
3. **Protect the remote**: branch protection with required reviews on `main`
4. **Optionally, a gate extension**: Pi ships a `permission-gate` example extension that asks before matching commands

<!--
The example extensions (permission-gate.ts, protected-paths.ts) are in the earendil-works/pi repository under packages/coding-agent/examples/extensions.
-->

---
hideInToc: true
level: 2
---

# Why it's built this way

- **Pi's bet**: prompts don't make an agent safe, they make you tired. That's the article's starting point too
- **The allow half is free**: inside a git repository in a container, everything local can be reset
- **The ask half has to be structural**: if the agent can't reach the remote's merge button or the cloud, the "leaves the working tree" actions are gated whatever it runs
- **Visibility instead of prompts**: sessions are saved as trees (`/tree`), so you can see and branch exactly what it did

**Know the limits**

- On your own laptop, with your SSH keys and cloud logins, Pi can do anything you can. Don't run it there on unfamiliar code
- A gate extension is a convenience, not a boundary; the container and credentials are the boundary

---
hideInToc: true
level: 2
---

# Layers 2, 3 and the gate

**Layer 2**: `AGENTS.md` at the repo root. Pi's small core means your conventions carry more of the load, so make the reasons explicit.

**Layer 3**:

- Design docs and stage checklists referenced from `AGENTS.md`
- A prompt template per stage, run as `/triage`, `/plan`, `/review`
- Skills for domain knowledge, loaded when relevant

**The gate**: a pull request that needs a human review before it merges. The agent can open it; it can't land it.
