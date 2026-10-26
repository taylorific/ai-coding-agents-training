---
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
hideInToc: true
title: "Working with OpenCode"
author: "Mischa Taylor"
info: |
  ## Working with OpenCode
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

# Working with OpenCode

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

<Toc/>

---
layout: section
---

# Coding agents

<br>
<br>
<Link to="toc" title="Table of Contents"/>

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
layout: section
---

# OpenCode

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
src: ./opencode/opencode-slides.md
---

---
src: ./opencode/opencode-trust-slides.md
---

---
src: ./next-steps/next-steps-slides.md
---
