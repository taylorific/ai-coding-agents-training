# Working with OpenCode

The OpenCode presentation from
[Working with AI Coding Agents](../README.md): how coding agents work, working
with one day to day, agent trust as a system design problem, then OpenCode
itself and its trust layers.

Online: <https://taylorific.github.io/ai-coding-agents-training/opencode/>

## Present the slides

Run these from the repository root, not this directory.

With Docker:

```bash
docker run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev opencode.md --remote

# Visit <http://localhost:3030/>
```

With Apple's [container](https://github.com/apple/container) CLI (macOS):

```bash
container system start   # once per boot

container run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev opencode.md --remote

# Visit <http://localhost:3030/>
```

Edit [opencode-slides.md](./opencode-slides.md) and
[opencode-trust-slides.md](./opencode-trust-slides.md) to see the changes. The
deck itself is [opencode.md](../opencode.md).

## Install OpenCode

| Platform | Command |
| --- | --- |
| macOS, Linux | `curl -fsSL https://opencode.ai/install \| bash` |
| Homebrew (macOS, Linux) | `brew install anomalyco/tap/opencode` |
| npm | `npm install -g opencode-ai` |
| Windows | WSL recommended; natively `scoop install opencode` or `choco install opencode` |

Works with many model providers; add one with `/connect`.

## Get started

```bash
cd my-project
opencode          # then /connect, /models, /init
```

The slides cover the rest: instructions files, permissions, everyday commands
and scripting.
