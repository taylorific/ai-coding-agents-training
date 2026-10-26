# Working with Pi

The Pi presentation from
[Working with AI Coding Agents](../README.md): how coding agents work, working
with one day to day, agent trust as a system design problem, then Pi
itself and its trust layers.

Online: <https://taylorific.github.io/ai-coding-agents-training/pi/>

## Present the slides

Run these from the repository root, not this directory.

With Docker:

```bash
docker run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev pi.md --remote

# Visit <http://localhost:3030/>
```

With Apple's [container](https://github.com/apple/container) CLI (macOS):

```bash
container system start   # once per boot

container run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev pi.md --remote

# Visit <http://localhost:3030/>
```

Edit [pi-slides.md](./pi-slides.md) and
[pi-trust-slides.md](./pi-trust-slides.md) to see the changes. The
deck itself is [pi.md](../pi.md).

## Install Pi

| Platform | Command |
| --- | --- |
| macOS, Linux | `curl -fsSL https://pi.dev/install.sh \| sh` |
| Windows PowerShell | `powershell -c "irm https://pi.dev/install.ps1 \| iex"` |
| npm (Node.js 22.19+) | `npm install -g --ignore-scripts @earendil-works/pi-coding-agent` |

Pi doesn't ask before acting; run it in a container or a repository you can reset.

## Get started

```bash
cd my-project
pi                # then /login and /model
```

The slides cover the rest: instructions files, permissions, everyday commands
and scripting.
