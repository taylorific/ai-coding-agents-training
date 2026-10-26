# Working with Amp

The Amp presentation from
[Working with AI Coding Agents](../README.md): how coding agents work, working
with one day to day, agent trust as a system design problem, then Amp
itself and its trust layers.

Online: <https://taylorific.github.io/ai-coding-agents-training/amp/>

## Present the slides

Run these from the repository root, not this directory.

With Docker:

```bash
docker run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev amp.md --remote

# Visit <http://localhost:3030/>
```

With Apple's [container](https://github.com/apple/container) CLI (macOS):

```bash
container system start   # once per boot

container run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev amp.md --remote

# Visit <http://localhost:3030/>
```

Edit [amp-slides.md](./amp-slides.md) and
[amp-trust-slides.md](./amp-trust-slides.md) to see the changes. The
deck itself is [amp.md](../amp.md).

## Install Amp

| Platform | Command |
| --- | --- |
| macOS, Linux | `curl -fsSL https://ampcode.com/install.sh \| bash` |
| Windows | Run the macOS/Linux command inside WSL |

Amp doesn't ask before running tools; use it in a repository you can reset.

## Get started

```bash
amp login
cd my-project
amp
amp -x "Summarize this repository"
```

The slides cover the rest: instructions files, permissions, everyday commands
and scripting.
