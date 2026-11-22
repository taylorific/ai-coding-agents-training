---
layout: section
level: 2
---

# Working with an agent day to day

<br>
<br>
<Link to="toc" title="Table of Contents"/>

---
hideInToc: true
level: 2
---

# Write the task like a ticket

**Weak**

> fix the login bug

**Better**

> Users who reset their password get "invalid token" on the next login.
> Reproduce it with a test in `auth/reset_test.go`, then fix it.
> Don't change the token format; mobile clients depend on it.
> Run `make test` before you say it's done.

What changed: the symptom, where to look, a constraint, and how to check.

<!--
The agent can't ask the hallway what you meant. Everything you'd tell a new teammate, tell the agent.
-->

---
hideInToc: true
level: 2
---

# Plan, then build

1. Ask for a plan first: plan mode, or "don't change anything yet"
2. Read the plan. Correct it now, while it's cheap
3. Let it implement
4. Have it verify: tests, build, lint, a real run

For bigger work, have it write the plan to a file. You can review it, and a fresh session can pick it up.

<!--
Most wasted agent time is a wrong assumption made in the first minute and built on for twenty. A plan surfaces the assumption.
-->

---
hideInToc: true
level: 2
---

# Give it a way to check its work

The single biggest improvement in results:

- A test command it can run: `npm test`, `pytest`, `go test ./...`
- A build or type check: `cargo build`, `tsc --noEmit`
- A linter and formatter
- For UI: a way to run the app and look (browser tools, screenshots)

Put these commands in the instructions file so every session knows them.

An agent that can see its own failures fixes them. One that can't guesses.

---
hideInToc: true
level: 2
---

# Why long sessions use up your limits

The model remembers nothing between messages. **Every message resends the whole session**: the agent's instructions and tools, your instructions file, every file it read, every reply.

- Agents read far more than they write. One heavy user's month: about **160 million tokens read, 500,000 written**
- **Prompt caching** keeps the part of the conversation already processed, so only the new part is processed at full price. Cached input costs a fraction of normal input
- The cache only matches if the **start of the conversation stays exactly the same**. Change something early on and everything after it is processed again
- The cache **expires**, after minutes to an hour depending on the agent and plan. The first message after a break rereads everything

So the goal isn't to use the agent less. It's to stop making it start from scratch.

<!--
The 160M / 500K figures are from one creator's logs over seven tasks, quoted in a video explaining advice from Anthropic engineers. Read-heavy is typical for every coding agent: each turn re-sends the whole history.
-->

---
hideInToc: true
level: 2
class: compact-table
---

# Three habits that waste tokens

| Habit | Why it costs | Instead |
| --- | --- | --- |
| **Changing the setup mid-session**: switching models, and in some agents adding tools | Each model keeps its own cache, so a switch rereads the whole conversation at full price | Choose the model and tools first. Send cheaper side work to a **subagent** or a new session, which have their own cache |
| **One session for everything**, all day | Every message carries every earlier task | **One task per session**. Clear or compact between tasks. Name the file and function instead of "find the bug" |
| **A long instructions file** | It loads into every session, and long files are followed less reliably | Keep it short. Move step-by-step procedures into **skills**, which load only when used. Re-test them when the model changes |

Switching to a cheaper model for one quick question can cost more than finishing on the model you're using.

<!--
Source: a video summarizing advice from Anthropic's Claude Code team, checked against the Claude Code prompt caching docs. The same mechanics apply to any agent that uses prompt caching.

Anthropic's engineers reportedly cut about 80% of their own system prompt for newer models with no measurable drop: newer models need fewer rules, and conflicting rules ("document everything" vs "don't add comments") make results worse.
-->

---
hideInToc: true
level: 2
---

# Use git as your safety net

- Start from a clean working tree, on a branch
- Commit good intermediate states, so you can roll back the bad ones
- Review the diff, not the agent's summary of the diff
- Run agents in parallel in separate **worktrees**, so they don't edit the same files

```bash
git worktree add ../myrepo-fix-login -b fix-login
cd ../myrepo-fix-login               # start your agent here
```

---
hideInToc: true
level: 2
---

# Review like it's a colleague's PR

- "Done, all tests pass" is a claim. Check it
- Watch for:
  - tests changed or skipped to make them pass
  - error handling that swallows the error
  - new dependencies you didn't ask for
  - changes outside the scope of the task
- You own what you merge, whoever typed it

<!--
Agents are eager to finish. When a test is hard to pass, weakening the test is a real failure mode. Look at test diffs first.
-->

---
hideInToc: true
level: 2
---

# Security habits

- **Secrets**: anything the agent can read can end up in a prompt. Keep credentials out of the repository and out of instruction files
- **Untrusted input**: web pages, issues, logs and dependencies can contain instructions aimed at the agent (prompt injection). Be careful with an agent that has both untrusted input and broad permissions
- **Allow-lists**: allow specific commands (`npm test`), not whole tools (`Bash`)
- **Bypass modes**: only in disposable containers or VMs with no credentials
- **MCP servers and plugins**: they run code with your access. Install them like any other dependency

---
hideInToc: true
level: 2
---

# When it goes wrong

| Symptom | Try |
| --- | --- |
| Going in circles on the same error | Stop it. Explain the cause yourself, or start a fresh session |
| Ignores your conventions | Move them into the instructions file, shorter and more specific |
| Forgot earlier decisions | Context was compacted. Restate them, or keep them in a plan file |
| Huge diff for a small task | Undo, then ask again with tighter scope |
| Confidently wrong about an API | Point it at the docs or the source; ask it to read before writing |

Interrupting early is cheap. A wrong direction left running isn't.
