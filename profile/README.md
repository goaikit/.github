[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

# AIKIT

**Multi-agent template package manager and CLI** for `aikit.toml` packages (install from **GitHub or a local path**), project scaffolding, publishing, and **`aikit run`** for supported coding-agent CLIs. **[aikit-sdk](https://github.com/goaikit/aikit/tree/main/aikit-sdk)** (Rust) and **[aikit-py](https://github.com/goaikit/aikit/tree/main/aikit-py)** (Python) are the programmatic gateway: same catalog, paths, deploy, detection, and run/event APIs.

**Full documentation** (Newton template, `aikit run` options, NDJSON, Windows notes): [github.com/goaikit/aikit/blob/main/README.md](https://github.com/goaikit/aikit/blob/main/README.md)

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

## Quick Start

### Create a package and deploy to Cursor and Claude

```bash
# 1. Create a new package (defines aikit.toml and template layout)
aikit package init my-tools --description "My AI commands"

# 2. Enter the package and add your templates (rules, skills, prompts)
cd my-tools
# Edit aikit.toml and add files under templates/ as needed

# 3. Build the package (produces dist/ or agent-specific zips)
aikit package build

# 4. Publish to GitHub (creates release and uploads assets)
aikit package publish username/my-tools
# Or: push repo first, then aikit release v1.0.0

# 5. Install the package for Cursor (in a project that uses Cursor)
cd /path/to/your-project
aikit install username/my-tools --ai cursor

# 6. Install the same package for Claude (e.g. in another project or --ai claude)
aikit install username/my-tools --ai claude

# 7. Verify: list installed packages and check available agents
aikit list
aikit check
```

### Use an existing project with an AI assistant

```bash
# Create a new template project with Claude templates
aikit init my-project --ai claude

# Or set up in the current directory for Cursor
aikit init --here --ai cursor

# Install a package from GitHub (owner/repo) or a local directory
aikit install username/package-name
aikit list
```

## Commands

| Command | Description |
|---------|-------------|
| `aikit init [name]` | Initialize a project with AI assistant templates |
| `aikit install <source>` | Install packages from GitHub (owner/repo) or local directory |
| `aikit list` | Show installed packages (optional: `--author`, `--detailed`) |
| `aikit update <pkg>` | Update a package to latest version (optional: `--breaking`) |
| `aikit remove <pkg>` | Uninstall a package (optional: `--force`) |
| `aikit check` | Check git, VS Code, and AI agent CLIs availability |
| `aikit run` | Run a supported coding-agent CLI (`--agent` required; optional `--events` NDJSON) |
| `aikit version` | Show version |
| `aikit package init <name>` | Create a new package with aikit.toml |
| `aikit package build` | Build distributable package (output: dist/ or .genreleases/) |
| `aikit package publish <owner/repo>` | Publish package to GitHub (release and assets) |
| `aikit release <version>` | Create GitHub release from .genreleases/ (e.g. v1.0.0) |

## Creating and publishing packages

```bash
# Create package
aikit package init my-tools --description "AI dev tools" --package-version 0.1.0

# Add templates and edit aikit.toml, then build
aikit package build

# Publish (creates GitHub release and uploads)
aikit package publish username/my-tools

# If you use a flow that produces zips in .genreleases/, create the release with:
# aikit release v1.0.0 --notes-file release_notes.md
```

## Configuration

- **GitHub auth:** Set `GITHUB_TOKEN` or `GH_TOKEN` in `.env` or use `--token` / `--github-token` on install, init, or release.
- **Package manifest:** Each package has an `aikit.toml` (name, version, description). Required for local installs and for publish.

Example `.env`:

```bash
GITHUB_TOKEN=your_github_token_here
```

## Supported AI assistants

The catalog lists **18** coding assistants for install/template mapping. **`aikit run`** supports: `codex`, `claude`, `gemini`, `opencode`, `agent`.

**CLI-based:** Claude, Gemini, Qwen, OpenCode, Codex, Auggie, CodeBuddy, Qoder, Q, Amp, Shai

**IDE-based:** GitHub Copilot, Cursor, Windsurf, KiloCode, Roo, Bob

Run `aikit check` to see which are installed on your system (git and VS Code are also checked).

## License

Apache License 2.0 - See [LICENSE](LICENSE)

Need help? [Open an issue](https://github.com/goaikit/aikit/issues)
