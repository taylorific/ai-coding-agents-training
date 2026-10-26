# Working with Antigravity

The Antigravity presentation from
[Working with AI Coding Agents](../README.md): how coding agents work, working
with one day to day, agent trust as a system design problem, then Antigravity
itself and its trust layers.

Online: <https://taylorific.github.io/ai-coding-agents-training/antigravity/>

## Present the slides

Run these from the repository root, not this directory.

With Docker:

```bash
docker run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev antigravity.md --remote

# Visit <http://localhost:3030/>
```

With Apple's [container](https://github.com/apple/container) CLI (macOS):

```bash
container system start   # once per boot

container run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev antigravity.md --remote

# Visit <http://localhost:3030/>
```

Edit [antigravity-slides.md](./antigravity-slides.md) and
[antigravity-trust-slides.md](./antigravity-trust-slides.md) to see the changes. The
deck itself is [antigravity.md](../antigravity.md).

## Install Antigravity

| Platform | Command |
| --- | --- |
| macOS, Linux | `curl -fsSL https://antigravity.google/cli/install.sh \| bash` |
| Windows PowerShell | `irm https://antigravity.google/cli/install.ps1 \| iex` |
| Windows CMD | `curl -fsSL https://antigravity.google/cli/install.cmd -o install.cmd && install.cmd && del install.cmd` |

The IDE and desktop app install from antigravity.google/download.

## Get started

```bash
cd my-project
agy               # trust the folder and sign in on first run
agy -p "Summarize what changed on this branch"
```

The slides cover the rest: instructions files, permissions, everyday commands
and scripting.
