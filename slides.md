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

<Toc columns="2"/>

---
src: ./fundamentals/fundamentals-slides.md
---

---
src: ./practices/practices-slides.md
---

---
src: ./trust/trust-slides.md
---

---
src: ./claude-code/claude-code-slides.md
---

---
src: ./claude-code/claude-code-trust-slides.md
---

---
src: ./codex/codex-slides.md
---

---
src: ./codex/codex-trust-slides.md
---

---
src: ./gemini-cli/gemini-cli-slides.md
---

---
src: ./gemini-cli/gemini-cli-trust-slides.md
---

---
src: ./antigravity/antigravity-slides.md
---

---
src: ./antigravity/antigravity-trust-slides.md
---

---
src: ./cursor/cursor-slides.md
---

---
src: ./cursor/cursor-trust-slides.md
---

---
src: ./copilot/copilot-slides.md
---

---
src: ./copilot/copilot-trust-slides.md
---

---
src: ./amp/amp-slides.md
---

---
src: ./amp/amp-trust-slides.md
---

---
src: ./kiro/kiro-slides.md
---

---
src: ./kiro/kiro-trust-slides.md
---

---
src: ./opencode/opencode-slides.md
---

---
src: ./opencode/opencode-trust-slides.md
---

---
src: ./pi/pi-slides.md
---

---
src: ./pi/pi-trust-slides.md
---

---
src: ./comparison/comparison-slides.md
---

---
src: ./next-steps/next-steps-slides.md
---
