# Working with AI Coding Agents

To start the slide show, with either Docker or Apple's
[container](https://github.com/apple/container) CLI:

## Docker

```bash
docker run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev

# Visit <http://localhost:3030/>
```

## Apple container (macOS)

```bash
container system start   # once per boot

container run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev

# Visit <http://localhost:3030/>
```

Edit the [slides.md](./slides.md) to see the changes.

Learn more about Slidev at the [documentation](https://sli.dev/).

# Presentations

There's one presentation per agent, each specific to that agent, plus an index:

| Presentation | Source | Online |
| --- | --- | --- |
| Index: one slide per agent, and all ten side by side | [slides.md](./slides.md) | [/](https://taylorific.github.io/ai-coding-agents-training/) |
| Working with Claude Code | [claude-code.md](./claude-code.md) | [/claude-code/](https://taylorific.github.io/ai-coding-agents-training/claude-code/) |
| Working with Codex | [codex.md](./codex.md) | [/codex/](https://taylorific.github.io/ai-coding-agents-training/codex/) |
| Working with Gemini CLI | [gemini-cli.md](./gemini-cli.md) | [/gemini-cli/](https://taylorific.github.io/ai-coding-agents-training/gemini-cli/) |
| Working with Antigravity | [antigravity.md](./antigravity.md) | [/antigravity/](https://taylorific.github.io/ai-coding-agents-training/antigravity/) |
| Working with Cursor | [cursor.md](./cursor.md) | [/cursor/](https://taylorific.github.io/ai-coding-agents-training/cursor/) |
| Working with GitHub Copilot CLI | [copilot.md](./copilot.md) | [/copilot/](https://taylorific.github.io/ai-coding-agents-training/copilot/) |
| Working with Amp | [amp.md](./amp.md) | [/amp/](https://taylorific.github.io/ai-coding-agents-training/amp/) |
| Working with Kiro | [kiro.md](./kiro.md) | [/kiro/](https://taylorific.github.io/ai-coding-agents-training/kiro/) |
| Working with OpenCode | [opencode.md](./opencode.md) | [/opencode/](https://taylorific.github.io/ai-coding-agents-training/opencode/) |
| Working with Pi | [pi.md](./pi.md) | [/pi/](https://taylorific.github.io/ai-coding-agents-training/pi/) |

Each agent's directory has a README with its own commands to present the deck,
and how to install and start the agent.

Every agent presentation has the same outline, in three groups: coding agents
(how they work, working with one day to day, agent trust as a system design
problem), then the agent itself (getting started, and its trust layers), and
next steps.

To present one agent's deck locally, name its file after the image:

```bash
docker run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev claude-code.md --remote
```

Use `container run` the same way with Apple's container CLI. The deck files
stay in the repository root so they share `style.css` and `components/`.

# Sections

Each section is its own file, so a deck can use any of them on its own or in
any order. Each agent has two files: its own slides, and its trust slides.
The sections other than an agent's own never name a specific agent, so every
agent presentation can share them.

| Directory | Covers |
| --- | --- |
| [fundamentals](./fundamentals/fundamentals-slides.md) | The agent loop, context, instruction files, permissions, extending an agent |
| [practices](./practices/practices-slides.md) | Writing tasks, plan then build, verification, git, review, security |
| [trust](./trust/trust-slides.md) | Agent trust as a system design problem (after [Paul Stack](https://stack72.dev/agent-trust-is-a-system-design-problem/)) |
| [claude-code](./claude-code/) | Claude Code: install on macOS, Linux and Windows, getting started, daily use (`claude-code-slides.md`); the trust layers in its own settings (`claude-code-trust-slides.md`) |
| [codex](./codex/) | OpenAI Codex CLI: install on macOS, Linux and Windows, getting started, daily use (`codex-slides.md`); the trust layers in its own settings (`codex-trust-slides.md`) |
| [gemini-cli](./gemini-cli/) | Google Gemini CLI: install on macOS, Linux and Windows, getting started, daily use (`gemini-cli-slides.md`); the trust layers in its own settings (`gemini-cli-trust-slides.md`) |
| [antigravity](./antigravity/) | Google Antigravity: install on macOS, Linux and Windows, getting started, daily use (`antigravity-slides.md`); the trust layers in its own settings (`antigravity-trust-slides.md`) |
| [cursor](./cursor/) | Cursor CLI: install on macOS, Linux and Windows, getting started, daily use (`cursor-slides.md`); the trust layers in its own settings (`cursor-trust-slides.md`) |
| [copilot](./copilot/) | GitHub Copilot CLI: install on macOS, Linux and Windows, getting started, daily use (`copilot-slides.md`); the trust layers in its own settings (`copilot-trust-slides.md`) |
| [amp](./amp/) | Amp: install on macOS, Linux and Windows, getting started, daily use (`amp-slides.md`); the trust layers in its own settings (`amp-trust-slides.md`) |
| [kiro](./kiro/) | Kiro: install on macOS, Linux and Windows, getting started, daily use (`kiro-slides.md`); the trust layers in its own settings (`kiro-trust-slides.md`) |
| [opencode](./opencode/) | OpenCode: install on macOS, Linux and Windows, getting started, daily use (`opencode-slides.md`); the trust layers in its own settings (`opencode-trust-slides.md`) |
| [pi](./pi/) | Pi: install on macOS, Linux and Windows, getting started, daily use (`pi-slides.md`); the trust layers in its own settings (`pi-trust-slides.md`) |
| [comparison](./comparison/comparison-slides.md) | All ten side by side, one shared `AGENTS.md` (index only) |
| [next-steps](./next-steps/next-steps-slides.md) | What to do next, and why the Swamp Training deck follows |

The deck files pull them in with `src:`:

```markdown
---
src: ./claude-code/claude-code-slides.md
---
```

Each section slide links back to the table of contents, so a deck that imports
one needs a slide with `routeAlias: toc`.

## Table of contents levels

The table of contents is two levels deep. The deck files add the top-level
group slides ("Coding agents", the agent's name, and "Agents" in the index),
and the section slides they import have `level: 2`, so `<Toc/>` indents them
under their group. Next steps and Side by side stay at the top level.

Give every `hideInToc: true` slide in a section file `level: 2` as well. A
hidden slide left at the default level 1 becomes the parent of the next
section, which then disappears from the table of contents along with it.

# Update dependencies

## Docker

To see what is out of date:

```bash
docker run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --entrypoint npm \
  docker.io/boxcutter/slidev outdated
```

To upgrade Slidev and the themes to their latest versions:

```bash
docker run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --entrypoint npm \
  docker.io/boxcutter/slidev \
    install @slidev/cli@latest @slidev/theme-default@latest @slidev/theme-seriph@latest
```

## Apple container (macOS)

To see what is out of date:

```bash
container run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --entrypoint npm \
  docker.io/boxcutter/slidev outdated
```

To upgrade Slidev and the themes to their latest versions:

```bash
container run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --entrypoint npm \
  docker.io/boxcutter/slidev \
    install @slidev/cli@latest @slidev/theme-default@latest @slidev/theme-seriph@latest
```

Then, on the host:

```bash
git add package.json package-lock.json
git commit -m "Sync npm lockfile"
git push
```

# Attributions

The following projects were used for inspiration and some code was
reused for the slideware:

- https://sli.dev/ - Slidev slideware
- https://github.com/alexanderdavide/slidev-theme-academic  Pagination  - Alexander Eble
- https://github.com/jpetazzo/container.training - Idea of using markdown slideware for training - Jérôme Petazzoni
