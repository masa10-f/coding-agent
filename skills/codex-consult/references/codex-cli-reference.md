# Codex CLI Reference

## Overview

Codex CLI is OpenAI's command-line interface for AI-powered code analysis and generation.

## Installation

```bash
# Install via npm
npm install -g @openai/codex

# Or via Homebrew
brew install openai-codex
```

## Authentication

```bash
codex login
```

## Main Commands

### `codex exec` - Non-interactive execution

Run Codex without interactive prompts. Best for scripting and automation.

```bash
codex exec [OPTIONS] [PROMPT]
```

**Key Options:**
| Option | Description |
|--------|-------------|
| `-m, --model <MODEL>` | Model to use; omit to use the Codex CLI default |
| `-s, --sandbox <MODE>` | Sandbox mode: read-only, workspace-write, danger-full-access |
| `-C, --cd <DIR>` | Working directory for the agent |
| `--search` | Enable web search |
| `-o, --output-last-message <FILE>` | Write final response to file |
| `-c, --config <key=value>` | Override configuration |

### `codex review` - Code review

Run automated code review on repository changes.

```bash
codex review [OPTIONS]
```

### `codex apply` - Apply diffs

Apply the latest diff produced by Codex agent.

```bash
codex apply
```

### `codex resume` - Continue session

Resume a previous interactive session.

```bash
codex resume --last
```

## Model Selection

Use the Codex CLI default model unless the user explicitly requests a model or the task has a known model requirement. If a model is needed, pass it with `-m` or `--model`.

## Sandbox Modes

| Mode | Description |
|------|-------------|
| `read-only` | No file modifications allowed (safest) |
| `workspace-write` | Can modify files in workspace |
| `danger-full-access` | Full system access (dangerous) |

## Configuration

Configuration file location: `~/.codex/config.toml`

```toml
# Optional default model
model = "your-preferred-model"

# Default sandbox mode
sandbox = "read-only"

# Enable web search by default
search = true
```

## Environment Variables

| Variable | Description |
|----------|-------------|
| `CODEX_MODEL` | Override default model |
| `OPENAI_API_KEY` | API key for authentication |

## Examples

### Basic query
```bash
codex exec "Explain the architecture of this project"
```

### With specific model and output
```bash
codex exec -m your-preferred-model -o result.md "Design a caching strategy"
```

### Scoped to directory
```bash
codex exec -C ./src "Review error handling patterns"
```

### With web search enabled
```bash
codex exec --search "What's the latest best practice for JWT authentication?"
```
