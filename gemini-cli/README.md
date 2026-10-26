# Working with Gemini CLI

The Gemini CLI presentation from
[Working with AI Coding Agents](../README.md): how coding agents work, working
with one day to day, agent trust as a system design problem, then Gemini CLI
itself and its trust layers.

Online: <https://taylorific.github.io/ai-coding-agents-training/gemini-cli/>

## Present the slides

Run these from the repository root, not this directory.

With Docker:

```bash
docker run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev gemini-cli.md --remote

# Visit <http://localhost:3030/>
```

With Apple's [container](https://github.com/apple/container) CLI (macOS):

```bash
container system start   # once per boot

container run -it --rm \
  --mount type=bind,source="$(pwd)",target="/slidev" \
  --publish 3030:3030 \
  docker.io/boxcutter/slidev gemini-cli.md --remote

# Visit <http://localhost:3030/>
```

Edit [gemini-cli-slides.md](./gemini-cli-slides.md) and
[gemini-cli-trust-slides.md](./gemini-cli-trust-slides.md) to see the changes. The
deck itself is [gemini-cli.md](../gemini-cli.md).

## Install Gemini CLI

| Platform | Command |
| --- | --- |
| npm (Node.js 20+) | `npm install -g @google/gemini-cli` |
| Homebrew (macOS, Linux) | `brew install gemini-cli` |
| MacPorts (macOS) | `sudo port install gemini-cli` |

Since June 18, 2026, free and Google One accounts use Antigravity instead; Gemini CLI remains for API keys, Vertex AI and paid Code Assist licenses.

## Get started

```bash
cd my-project
gemini            # pick a sign-in method on first run
gemini -p "Explain the architecture of this codebase"
```

The slides cover the rest: instructions files, permissions, everyday commands
and scripting.
