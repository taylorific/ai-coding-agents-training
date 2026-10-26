# Working with Codex

The Codex presentation from
[Working with AI Coding Agents](../README.md): how coding agents work, working
with one day to day, agent trust as a system design problem, then Codex
itself and its trust layers.

Online: <https://taylorific.github.io/ai-coding-agents-training/codex/>

## Present the slides

Run these from the repository root, not this directory.

With Docker:

```bash
docker run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev codex.md --remote

# Visit <http://localhost:3030/>
```

With Apple's [container](https://github.com/apple/container) CLI (macOS):

```bash
container system start   # once per boot

container run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev codex.md --remote

# Visit <http://localhost:3030/>
```

Edit [codex-slides.md](./codex-slides.md) and
[codex-trust-slides.md](./codex-trust-slides.md) to see the changes. The
deck itself is [codex.md](../codex.md).

## Install Codex

| Platform | Command |
| --- | --- |
| macOS, Linux | `curl -fsSL https://chatgpt.com/codex/install.sh \| sh` |
| Windows PowerShell | `powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 \| iex"` |
| Homebrew (macOS) | `brew install --cask codex` |
| npm | `npm install -g @openai/codex` |

Sign in with a ChatGPT plan or an API key.

## Get started

```bash
cd my-project
codex             # choose "Sign in with ChatGPT"
codex exec "Summarize what changed on this branch"
```

The slides cover the rest: instructions files, permissions, everyday commands
and scripting.
