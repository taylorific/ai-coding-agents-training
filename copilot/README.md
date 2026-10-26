# Working with GitHub Copilot CLI

The GitHub Copilot CLI presentation from
[Working with AI Coding Agents](../README.md): how coding agents work, working
with one day to day, agent trust as a system design problem, then GitHub Copilot CLI
itself and its trust layers.

Online: <https://taylorific.github.io/ai-coding-agents-training/copilot/>

## Present the slides

Run these from the repository root, not this directory.

With Docker:

```bash
docker run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev copilot.md --remote

# Visit <http://localhost:3030/>
```

With Apple's [container](https://github.com/apple/container) CLI (macOS):

```bash
container system start   # once per boot

container run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev copilot.md --remote

# Visit <http://localhost:3030/>
```

Edit [copilot-slides.md](./copilot-slides.md) and
[copilot-trust-slides.md](./copilot-trust-slides.md) to see the changes. The
deck itself is [copilot.md](../copilot.md).

## Install GitHub Copilot CLI

| Platform | Command |
| --- | --- |
| macOS, Linux | `curl -fsSL https://gh.io/copilot-install \| bash` |
| Homebrew (macOS, Linux) | `brew install --cask copilot-cli` |
| WinGet (Windows) | `winget install GitHub.Copilot` |
| npm (Node.js 22+) | `npm install -g @github/copilot` |

Needs an active GitHub Copilot plan.

## Get started

```bash
cd my-project
copilot           # answer the trust prompt, then /login
```

The slides cover the rest: instructions files, permissions, everyday commands
and scripting.
