# Working with Cursor

The Cursor presentation from
[Working with AI Coding Agents](../README.md): how coding agents work, working
with one day to day, agent trust as a system design problem, then Cursor
itself and its trust layers.

Online: <https://taylorific.github.io/ai-coding-agents-training/cursor/>

## Present the slides

Run these from the repository root, not this directory.

With Docker:

```bash
docker run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev cursor.md --remote

# Visit <http://localhost:3030/>
```

With Apple's [container](https://github.com/apple/container) CLI (macOS):

```bash
container system start   # once per boot

container run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev cursor.md --remote

# Visit <http://localhost:3030/>
```

Edit [cursor-slides.md](./cursor-slides.md) and
[cursor-trust-slides.md](./cursor-trust-slides.md) to see the changes. The
deck itself is [cursor.md](../cursor.md).

## Install Cursor

| Platform | Command |
| --- | --- |
| macOS, Linux, WSL | `curl https://cursor.com/install -fsS \| bash` |
| Windows PowerShell | `irm 'https://cursor.com/install?win32=true' \| iex` |

These install the Cursor CLI (`agent`). The editor installs from cursor.com.

## Get started

```bash
agent login
cd my-project
agent             # Shift+Tab cycles Agent / Plan / Ask
```

The slides cover the rest: instructions files, permissions, everyday commands
and scripting.
