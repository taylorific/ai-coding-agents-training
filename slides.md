---
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
hideInToc: true
title: "Working with AI Coding Agents"
author: "Mischa Taylor"
info: |
  ## Working with AI Coding Agents
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
themeConfig:
  paginationX: r
  paginationY: t
  paginationPagesDisabled: [1]
---

# Working with AI Coding Agents

##### Mischa Taylor | 📧 <taylor@linux.com>

<div @click="$slidev.nav.next" class="mt-12 py-1" hover:bg="white op-10">
  Press Space for next page <carbon:arrow-right />
</div>

<div class="abs-br m-6 text-xl">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="slidev-icon-btn">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
hideInToc: true
routeAlias: toc
---

# Table of Contents

<Toc columns="2" maxDepth="1"/>

---
hideInToc: true
---

# One presentation per agent

Each agent has its own presentation, specific to that agent:

- How coding agents work, and how to work with one day to day
- Installing it on macOS, Linux and Windows, and getting started
- Its instructions file, permissions and everyday commands
- Agent trust as a system design problem, in that agent's own settings

Pick yours from the table of contents, or read on for a one-slide summary of each.

---
layout: section
---

# Claude Code

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# Claude Code at a glance

| | |
| --- | --- |
| **From** | Anthropic |
| **Start it** | `claude` |
| **Install** (macOS, Linux) | `curl -fsSL https://claude.ai/install.sh \| bash` |
| **Instructions file** | `CLAUDE.md` |
| **Permissions** | Allow, ask and deny rules in `settings.json` |

<div class="mt-8 text-xl">

[Open the Claude Code presentation →](https://taylorific.github.io/ai-coding-agents-training/claude-code/)

</div>

---
layout: section
---

# Codex

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# Codex at a glance

| | |
| --- | --- |
| **From** | OpenAI |
| **Start it** | `codex` |
| **Install** (macOS, Linux) | `npm install -g @openai/codex` |
| **Instructions file** | `AGENTS.md` |
| **Permissions** | A sandbox for the repository, plus rules for specific commands |

<div class="mt-8 text-xl">

[Open the Codex presentation →](https://taylorific.github.io/ai-coding-agents-training/codex/)

</div>

---
layout: section
---

# Gemini CLI

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# Gemini CLI at a glance

| | |
| --- | --- |
| **From** | Google |
| **Start it** | `gemini` |
| **Install** (macOS, Linux) | `npm install -g @google/gemini-cli` |
| **Instructions file** | `GEMINI.md` |
| **Permissions** | Policy-engine rules: allow, ask, deny |

<div class="mt-8 text-xl">

[Open the Gemini CLI presentation →](https://taylorific.github.io/ai-coding-agents-training/gemini-cli/)

</div>

---
layout: section
---

# Antigravity

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# Antigravity at a glance

| | |
| --- | --- |
| **From** | Google |
| **Start it** | `agy` |
| **Install** (macOS, Linux) | `curl -fsSL https://antigravity.google/cli/install.sh \| bash` |
| **Instructions file** | `AGENTS.md`, `GEMINI.md` |
| **Permissions** | Allow, ask and deny rules in `settings.json` |

<div class="mt-8 text-xl">

[Open the Antigravity presentation →](https://taylorific.github.io/ai-coding-agents-training/antigravity/)

</div>

---
layout: section
---

# Cursor

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# Cursor at a glance

| | |
| --- | --- |
| **From** | Anysphere |
| **Start it** | `agent` |
| **Install** (macOS, Linux) | `curl https://cursor.com/install -fsS \| bash` |
| **Instructions file** | `AGENTS.md`, `.cursor/rules/` |
| **Permissions** | Allow and deny lists; anything unlisted asks |

<div class="mt-8 text-xl">

[Open the Cursor presentation →](https://taylorific.github.io/ai-coding-agents-training/cursor/)

</div>

---
layout: section
---

# GitHub Copilot CLI

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# GitHub Copilot CLI at a glance

| | |
| --- | --- |
| **From** | GitHub |
| **Start it** | `copilot` |
| **Install** (macOS, Linux) | `npm install -g @github/copilot` |
| **Instructions file** | `AGENTS.md`, `.github/copilot-instructions.md` |
| **Permissions** | Allow and deny flags; anything unlisted asks |

<div class="mt-8 text-xl">

[Open the GitHub Copilot CLI presentation →](https://taylorific.github.io/ai-coding-agents-training/copilot/)

</div>

---
layout: section
---

# Amp

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# Amp at a glance

| | |
| --- | --- |
| **From** | Amp |
| **Start it** | `amp` |
| **Install** (macOS, Linux) | `curl -fsSL https://ampcode.com/install.sh \| bash` |
| **Instructions file** | `AGENTS.md` |
| **Permissions** | No prompts by default; plugins and the remote do the gating |

<div class="mt-8 text-xl">

[Open the Amp presentation →](https://taylorific.github.io/ai-coding-agents-training/amp/)

</div>

---
layout: section
---

# Kiro

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# Kiro at a glance

| | |
| --- | --- |
| **From** | AWS |
| **Start it** | `kiro-cli` |
| **Install** (macOS, Linux) | `curl -fsSL https://cli.kiro.dev/install \| bash` |
| **Instructions file** | `AGENTS.md`, `.kiro/steering/` |
| **Permissions** | Allow, ask and deny rules in `permissions.yaml` |

<div class="mt-8 text-xl">

[Open the Kiro presentation →](https://taylorific.github.io/ai-coding-agents-training/kiro/)

</div>

---
layout: section
---

# OpenCode

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# OpenCode at a glance

| | |
| --- | --- |
| **From** | Anomaly |
| **Start it** | `opencode` |
| **Install** (macOS, Linux) | `curl -fsSL https://opencode.ai/install \| bash` |
| **Instructions file** | `AGENTS.md` |
| **Permissions** | Allow, ask and deny patterns in `opencode.json` |

<div class="mt-8 text-xl">

[Open the OpenCode presentation →](https://taylorific.github.io/ai-coding-agents-training/opencode/)

</div>

---
layout: section
---

# Pi

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
class: compact-table
---

# Pi at a glance

| | |
| --- | --- |
| **From** | Earendil |
| **Start it** | `pi` |
| **Install** (macOS, Linux) | `curl -fsSL https://pi.dev/install.sh \| sh` |
| **Instructions file** | `AGENTS.md` |
| **Permissions** | None by design; contain it and gate on the remote |

<div class="mt-8 text-xl">

[Open the Pi presentation →](https://taylorific.github.io/ai-coding-agents-training/pi/)

</div>

---
src: ./comparison/comparison-slides.md
---
