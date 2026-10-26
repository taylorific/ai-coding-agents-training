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

# Sections

Each section is its own file, so a deck can use any of them on its own or in
any order. Each agent has two files: its own slides, and its trust slides.

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
| [comparison](./comparison/comparison-slides.md) | All ten side by side, one shared `AGENTS.md` |
| [next-steps](./next-steps/next-steps-slides.md) | What to do next, and why the Swamp Training deck follows |

[slides.md](./slides.md) pulls them in with `src:`:

```markdown
---
src: ./claude-code/claude-code-slides.md
---
```

Each section slide links back to the table of contents, so a deck that imports
one needs a slide with `routeAlias: toc`.

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
