[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

# AIKIT

**One CLI + gateway for every coding-agent CLI on your machine.** Run,
package, share, and serve AI coding agents the same way regardless of
whether you're using Claude Code, Codex, Gemini CLI, OpenCode, the
built-in `aikit` agent, or any other entry in the catalog.

## Highlights

- **Run any agent uniformly** — `aikit agent run --agent <name> -p "…"`
  for Claude, Codex, Gemini, OpenCode, and the built-in `aikit` agent;
  optional NDJSON event stream for tooling.
- **Multi-turn HTTP API** — `aikit serve` exposes the agent runtime over
  HTTP with both SSE streaming and single-shot JSON responses, selected
  by the standard `Accept` header. Sessions are implicit; resume by id.
- **Templates and packages** — `aikit init` scaffolds a Spec-Driven
  Development project; `aikit install/update/remove/list` manage
  packaged commands, skills, and agent definitions from GitHub or a
  local path.
- **MCP config merge** — `aikit agent mcp add` registers one MCP server
  entry into whichever agent config file is appropriate (Cursor,
  Claude, Gemini, VS Code Copilot, OpenCode, Codex).
- **One LLM call** — `aikit llm` wraps any OpenAI-compatible endpoint.
- **Rust + Python gateways** —
  [`aikit-sdk`](https://github.com/goaikit/aikit/tree/main/aikit-sdk)
  (Rust) and
  [`aikit-py`](https://github.com/goaikit/aikit/tree/main/aikit-py)
  (Python) expose the same catalog, paths, deploy, detection, and
  run/event APIs.

**Full documentation:**
[github.com/goaikit/aikit/blob/main/README.md](https://github.com/goaikit/aikit/blob/main/README.md)
· [HTTP serve API reference](https://github.com/goaikit/aikit/blob/main/webdocs/serve.mdx)

## Installation

### Linux (GNU)
```bash
curl -L https://github.com/goaikit/aikit/releases/latest/download/aikit-x86_64-unknown-linux-gnu.tar.gz | tar xz
sudo mv aikit /usr/local/bin/
```

### Linux (MUSL/Universal)
```bash
curl -L https://github.com/goaikit/aikit/releases/latest/download/aikit-x86_64-unknown-linux-musl.tar.gz | tar xz
sudo mv aikit /usr/local/bin/
```

### Homebrew (Linux)
```bash
brew install goaikit/cli/aikit
```

### Scoop (Windows)
```powershell
scoop bucket add goaikit https://github.com/goaikit/scoop-bucket
scoop install aikit
```

### Windows
Download from [GitHub Releases](https://github.com/goaikit/aikit/releases/latest) and add to PATH.

## Quick taste

### Run a coding agent

```bash
echo "Add error handling to main.rs" | aikit agent run --agent claude
```

### Serve a multi-turn agent over HTTP

```bash
aikit serve --port 8787

# Single-shot JSON response
curl -s -H 'Accept: application/json' -H 'Content-Type: application/json' \
  -d '{"agent":"aikit","content":"Say hello."}' \
  http://127.0.0.1:8787/v1/messages | jq .
# → {"session_id":"…","content":"Hello, world!","exit_code":0}
```

### Build, publish, and install a package

```bash
aikit package init my-tools --description "My AI commands"
cd my-tools && aikit package build
aikit package publish username/my-tools

# In another project:
aikit install username/my-tools --ai claude
aikit list
```

## Commands

| Command | Description |
|---------|-------------|
| `aikit init [name]` | Initialize a project with AI assistant templates |
| `aikit install <source>` | Install packages from GitHub (owner/repo) or local directory |
| `aikit list` | Show installed packages |
| `aikit update <pkg>` | Update a package to latest version |
| `aikit remove <pkg>` | Uninstall a package |
| `aikit check` | Check git, VS Code, and AI agent CLIs availability |
| `aikit agent run` | Run a coding agent (`--agent` required; optional `--events` NDJSON) |
| `aikit agent list` | List project-scoped agent definitions |
| `aikit agent check` | Probe runnable agent CLIs only |
| `aikit agent mcp list` / `add` | Inspect or merge MCP server entries |
| `aikit serve` | HTTP server exposing the agent runtime (SSE or JSON via `Accept`) |
| `aikit llm` | One-shot OpenAI-compatible LLM call |
| `aikit package init/build/publish` | Author and ship packages |
| `aikit release <version>` | Create a GitHub release from `.genreleases/` |
| `aikit version` | Show version |

## Supported AI assistants

The catalog lists **19** assistants for install/template mapping.
Runnable via `aikit agent run`: `codex`, `claude`, `gemini`, `opencode`,
`cursor`, `pi`, `aikit`, `auto`.

**CLI-based:** Claude, Gemini, Qwen, OpenCode, Codex, Pi, Auggie, CodeBuddy,
Qoder, Q, Amp, Shai

**IDE-based:** GitHub Copilot, Cursor, Windsurf, KiloCode, Roo, Bob

Run `aikit check` to see which are installed on your system.

## License

Apache License 2.0 — see [LICENSE](https://github.com/goaikit/aikit/blob/main/LICENSE)

Need help? [Open an issue](https://github.com/goaikit/aikit/issues)
