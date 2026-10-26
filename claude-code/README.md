# Working with Claude Code

The Claude Code presentation from
[Working with AI Coding Agents](../README.md): how coding agents work, working
with one day to day, agent trust as a system design problem, then Claude Code
itself and its trust layers.

Online: <https://taylorific.github.io/ai-coding-agents-training/claude-code/>

## Present the slides

Run these from the repository root, not this directory.

With Docker:

```bash
docker run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev claude-code.md --remote

# Visit <http://localhost:3030/>
```

With Apple's [container](https://github.com/apple/container) CLI (macOS):

```bash
container system start   # once per boot

container run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev claude-code.md --remote

# Visit <http://localhost:3030/>
```

Edit [claude-code-slides.md](./claude-code-slides.md) and
[claude-code-trust-slides.md](./claude-code-trust-slides.md) to see the changes. The
deck itself is [claude-code.md](../claude-code.md).

## Install Claude Code

| Platform | Command |
| --- | --- |
| macOS, Linux, WSL | `curl -fsSL https://claude.ai/install.sh \| bash` |
| Windows PowerShell | `irm https://claude.ai/install.ps1 \| iex` |
| Homebrew (macOS) | `brew install --cask claude-code` |
| WinGet (Windows) | `winget install Anthropic.ClaudeCode` |

Needs a Pro, Max, Team or Enterprise plan, or an Anthropic Console account. On Windows, also install Git for Windows.

## Get started

```bash
cd my-project
claude            # sign in on first run
claude doctor     # check the install
```

The slides cover the rest: instructions files, permissions, everyday commands
and scripting.
