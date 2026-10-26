---
layout: section
---

# Next steps

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
---

# What you can do now

- Install an agent and run one real task end to end: question, plan, change, tests, review
- Write a one-page `AGENTS.md` for a repository you work in
- Set up Layer 1 for your agent: allow what `git checkout` can undo, ask about everything else
- Put the gate where it can't be skipped: required reviews on your main branch

---
hideInToc: true
---

# Next: Swamp Training

Everything in this deck makes **one agent session** safer and better. Three gaps remain:

| What you'd hope | What's actually true |
| --- | --- |
| The same request gets the same result next week | Agents aren't deterministic; each run can go differently |
| The instructions file makes the agent follow your process | Instructions are guidance; nothing enforces them |
| "Done, I restarted the device" means it restarted | The agent's report is a claim, not a record |

The **Swamp Training** deck picks up there: the agent drives typed, reusable automation instead of improvising each time, so the work is repeatable, enforced and recorded. It builds on everything here, and works with the agents you just met.

**taylorific.github.io/swamp-training**

<!--
Take the agent you set up today into the swamp deck; every exercise there assumes you can already run an agent with a sensible trust model.
-->
