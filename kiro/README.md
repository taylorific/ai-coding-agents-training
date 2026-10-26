# Working with Kiro

The Kiro presentation from
[Working with AI Coding Agents](../README.md): how coding agents work, working
with one day to day, agent trust as a system design problem, then Kiro
itself and its trust layers.

Online: <https://taylorific.github.io/ai-coding-agents-training/kiro/>

## Present the slides

Run these from the repository root, not this directory.

With Docker:

```bash
docker run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev kiro.md --remote

# Visit <http://localhost:3030/>
```

With Apple's [container](https://github.com/apple/container) CLI (macOS):

```bash
container system start   # once per boot

container run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev kiro.md --remote

# Visit <http://localhost:3030/>
```

Edit [kiro-slides.md](./kiro-slides.md) and
[kiro-trust-slides.md](./kiro-trust-slides.md) to see the changes. The
deck itself is [kiro.md](../kiro.md).

## Install Kiro

| Platform | Command |
| --- | --- |
| CLI: macOS, Linux | `curl -fsSL https://cli.kiro.dev/install \| bash` |
| IDE, and the CLI on Windows | Download from [kiro.dev/downloads](https://kiro.dev/downloads/) |

Sign in with GitHub, Google, AWS Builder ID or your organization.

## Get started

```bash
kiro-cli login
cd my-project
kiro-cli          # trust the workspace when asked
```

The slides cover the rest: instructions files, permissions, everyday commands
and scripting.
