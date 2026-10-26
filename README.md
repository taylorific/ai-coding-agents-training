# Working with AI Coding Agents

To start the slide show:

```
docker run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev

# Visit <http://localhost:3030/>
```

Edit the [slides.md](./slides.md) to see the changes.

Learn more about Slidev at the [documentation](https://sli.dev/).

# Sections

Each section is its own file, so a deck can use any of them on its own or in
any order:

| Directory | Covers |
| --- | --- |
| [fundamentals](./fundamentals/fundamentals-slides.md) | The agent loop, context, instruction files, permissions, extending an agent |
| [practices](./practices/practices-slides.md) | Writing tasks, plan then build, verification, git, review, security |
| [claude-code](./claude-code/claude-code-slides.md) | Claude Code |
| [codex](./codex/codex-slides.md) | OpenAI Codex CLI |
| [gemini-cli](./gemini-cli/gemini-cli-slides.md) | Google Gemini CLI |
| [comparison](./comparison/comparison-slides.md) | The three side by side, one shared `AGENTS.md` |

[slides.md](./slides.md) pulls them in with `src:`:

```markdown
---
src: ./claude-code/claude-code-slides.md
---
```

Each section slide links back to the table of contents, so a deck that imports
one needs a slide with `routeAlias: toc`.

# Update dependencies

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

# on the host
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
