<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="/docs/assets/waylou-banner.png">
    <img alt="Waylou ACE CLI Banner" src="/docs/assets/waylou-banner.png" width="800">
  </picture>
</p>

<p align="center">
  <strong>Your terminal. Your models. Your rules.</strong>
</p>

<p align="center">
  <a href="https://github.com/helis-d/waylou/actions"><img alt="CI" src="https://github.com/helis-d/waylou/actions/workflows/ci.yml/badge.svg"></a>
  <a href="https://www.npmjs.com/package/@waylou/cli"><img alt="npm version" src="https://img.shields.io/npm/v/@waylou/cli"></a>
  <a href="./LICENSE"><img alt="License" src="https://img.shields.io/github/license/helis-d/waylou"></a>
  <a href="https://github.com/helis-d/waylou"><img alt="GitHub Repo stars" src="https://img.shields.io/github/stars/helis-d/waylou"></a>
</p>

---

**Waylou ACE CLI** is an open-source AI coding assistant that runs directly
in your terminal. It connects to multiple AI models — Gemini, OpenAI,
Anthropic, Ollama, DeepSeek — through a single, unified interface.

Forked from Google Gemini CLI, Waylou extends the foundation with
multi-provider support, autonomous operation, and an architecture designed
for extensibility.

> **Status:** Active development. Core functionality works. Provider layer
> and CLI features are under heavy development. Contributions welcome.

## Why Waylou?

| Capability | Waylou ACE CLI | Gemini CLI |
|------------|:---:|:---:|
| Multi-provider (Gemini, OpenAI, Claude, local) | ✅ | ❌ |
| BYOK — Bring Your Own Key | ✅ | ❌ |
| Provider orchestration & team routing | ✅ | ❌ |
| Headless / autonomous mode | ✅ | ✅ |
| MCP (Model Context Protocol) | ✅ | ✅ |
| ACE compliance specification | ✅ | ❌ |
| VS Code companion | ✅ | ❌ |
| Apache 2.0 open source | ✅ | ✅ |

## Quick Start

```bash
# Install globally
npm install -g @waylou/cli

# Or run instantly
npx @waylou/cli

# Launch
waylou
```

## Features

### Multi-Provider AI
Use any model, any provider. Swap mid-session. Route tasks to the right
model based on capability, speed, or cost.

**Supported providers:**
- **Google Gemini** — Gemini 2.5, 3.0 (1M token context)
- **OpenAI** — GPT-4, GPT-4o
- **Anthropic** — Claude 3.5, Claude 4
- **Ollama** — Local models (Llama, Mistral, Gemma)
- **DeepSeek** — DeepSeek V3, R1

### Provider Orchestration
Form teams of models with different roles — architect, coder, reviewer.
The orchestrator distributes tasks using configurable strategies
(capability-best, round-robin, parallel-vote).

### ACE Specification
The **Agentic Coding Environment** specification standardizes agent
behavior across three compliance levels:

- **CORE** — File operations, shell commands, web fetch
- **STANDARD** — MCP integration, checkpointing, sandbox, memory
- **ENTERPRISE** — Policy engine, audit logging, team orchestration

### Headless & Autonomous
Run in CI/CD pipelines, scripts, and automated workflows:

```bash
waylou -p "Review this PR and summarize the changes" --output-format json
```

### Context Engine
Semantic code search combining vector embeddings (SQLite-vec) with AST
analysis (Tree-sitter) for precise, relevant context retrieval.

### Sandbox
Secure execution via macOS Seatbelt, Docker, or Podman.

## Installation

### Prerequisites
- Node.js 20+
- npm 9+

### Quick Install

```bash
npm install -g @waylou/cli
```

### From Source

```bash
git clone https://github.com/helis-d/waylou.git
cd waylou
npm install
npm run build
node run.js
```

## Configuration

Set your provider API keys:

```bash
export GEMINI_API_KEY="your-key"      # Google Gemini
export OPENAI_API_KEY="your-key"      # OpenAI
export ANTHROPIC_API_KEY="your-key"   # Anthropic
export DEEPSEEK_API_KEY="your-key"    # DeepSeek
```

For local models, install [Ollama](https://ollama.com) and run:

```bash
waylou --provider ollama
```

## Architecture

```
CLI (Ink/React UI)
    │
    ▼
Core Engine (Agent Loop, Tools, Prompts)
    │
    ▼
Provider Layer (Gemini | OpenAI | Anthropic | Ollama | DeepSeek)
    │
    ▼
AI APIs
```

See [ARCHITECTURE.md](./ARCHITECTURE.md) for the full system design.

## Packages

| Package | Description |
|---------|-------------|
| `@waylou/cli` | Terminal UI & CLI binary |
| `@waylou/cli-core` | Core agent logic, tools, prompts |
| `@waylou/cli-provider` | Multi-AI provider abstraction |
| `@waylou/ace-spec` | ACE specification & validation |
| `@waylou/autonomous-engine` | Headless / autonomous operation |
| `@waylou/context-engine` | Vector & AST semantic search |
| `@waylou/sandbox` | Secure execution environment |
| `@waylou/cli-sdk` | Public SDK for extensions |

## Documentation

- [Architecture](./ARCHITECTURE.md)
- [Project Structure](./PROJECT_STRUCTURE.md)
- [FAQ](./FAQ.md)
- [Changelog](./CHANGELOG.md)
- [Roadmap](./ROADMAP.md)
- [Contributing](./CONTRIBUTING.md)
- [Security](./SECURITY.md)
- [Support](./SUPPORT.md)

## Roadmap

See [ROADMAP.md](./ROADMAP.md) for planned features and priorities.

## Contributing

Contributions are welcome — especially for the **provider layer**, which is
the project's biggest development need. If you have experience with AI APIs,
SDKs, or model integrations, we'd love your help.

See [CONTRIBUTING.md](./CONTRIBUTING.md) for the full guide.

## Community

- [GitHub Issues](https://github.com/helis-d/waylou/issues)
- [GitHub Discussions](https://github.com/helis-d/waylou/discussions)
- Read the [Code of Conduct](./CODE_OF_CONDUCT.md)

## Acknowledgments

This project is forked from
[Google Gemini CLI](https://github.com/google-gemini/gemini-cli). We are
grateful to the original authors and contributors for building an
exceptional foundation.

## License

Apache License 2.0 — See [LICENSE](./LICENSE) for details.