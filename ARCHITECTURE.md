# Architecture

Waylou ACE CLI is a monorepo-based, multi-provider AI coding assistant that
runs in the terminal. This document describes the high-level architecture,
component relationships, and data flow.

## High-Level Overview

```
┌─────────────────────────────────────────────────────────────┐
│                         CLI Layer                             │
│  ┌─────────────────┐  ┌──────────────────────────────────┐  │
│  │  Terminal UI     │  │  Headless / Script Mode           │  │
│  │  (Ink + React)   │  │  (JSON / stream-json output)     │  │
│  └────────┬────────┘  └────────────────┬─────────────────┘  │
└───────────┼────────────────────────────┼────────────────────┘
            │                            │
┌───────────┼────────────────────────────┼────────────────────┐
│           │           Core Engine       │                     │
│  ┌────────▼────────────────────────────▼───────────────┐    │
│  │                  Agent / Session                      │    │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────────────┐   │    │
│  │  │ Prompts  │  │  Tools   │  │  History / Memory │   │    │
│  │  └──────────┘  └──────────┘  └──────────────────┘   │    │
│  └──────────────────────┬───────────────────────────────┘    │
│                         │                                     │
│  ┌──────────────────────▼───────────────────────────────┐    │
│  │                  Provider Layer                        │    │
│  │  ┌─────────┐ ┌──────────┐ ┌───────────┐ ┌─────────┐ │    │
│  │  │ Gemini  │ │ OpenAI   │ │ Anthropic │ │ Ollama  │ │    │
│  │  └─────────┘ └──────────┘ └───────────┘ └─────────┘ │    │
│  └──────────────────────────────────────────────────────┘    │
│                                                               │
│  ┌──────────────────────────────────────────────────────┐    │
│  │        ACE Specification & Validation                 │    │
│  │  CORE ◄── STANDARD ◄── ENTERPRISE                    │    │
│  └──────────────────────────────────────────────────────┘    │
└───────────────────────────────────────────────────────────────┘
```

## Package Architecture

```
packages/
├── cli/                    # Terminal UI & CLI entry point
│   ├── src/
│   │   ├── ui/             # Ink/React components
│   │   ├── config/         # Settings & auth configuration
│   │   └── branding/       # Brand assets (Waylou)
│   └── index.ts            # Binary entry point
│
├── core/                   # Core agent logic
│   ├── src/
│   │   ├── core/           # Agent loop, chat, prompts
│   │   ├── tools/          # Built-in tools (files, shell, web)
│   │   ├── config/         # Configuration & storage
│   │   ├── hooks/          # Extensibility hooks
│   │   └── utils/          # Common utilities
│   └── index.ts            # Barrel export
│
├── provider/               # Multi-AI provider abstraction
│   ├── src/
│   │   ├── byok.ts         # Bring Your Own Key support
│   │   ├── orchestrator.ts # Multi-model team orchestration
│   │   └── registry.ts     # Provider registry
│   └── index.ts
│
├── ace-spec/               # ACE specification & validation
│   ├── src/
│   │   ├── types.ts        # Type definitions
│   │   ├── specification.ts # CORE/STANDARD/ENTERPRISE rules
│   │   └── validator.ts    # Compliance validation engine
│   └── index.ts
│
├── autonomous-engine/      # Headless/autonomous operation
├── context-engine/         # Vector & AST semantic search
├── sandbox/                # Secure execution environment
├── sdk/                    # Public SDK for extensions
├── devtools/               # Developer tooling
└── test-utils/             # Shared test utilities
```

## Data Flow

```
User Input
    │
    ▼
┌──────────┐     ┌──────────┐     ┌──────────┐     ┌──────────────┐
│   CLI    │────▶│   Core   │────▶│ Provider │────▶│ AI API       │
│ (Ink UI) │     │ (Agent)  │     │ (Router) │     │ (Gemini etc) │
└──────────┘     └──────────┘     └──────────┘     └──────────────┘
    ▲                  │                                    │
    │                  ▼                                    │
    │           ┌──────────┐                               │
    │           │  Tools   │◄──────────────────────────────┘
    │           │ (Shell,  │    Tool calls from AI response
    │           │  FS, Web)│
    │           └──────────┘
    │                  │
    │                  ▼
    └──────────────────┘
         Response streamed back to UI
```

### Request Flow

1. **CLI** receives user input and sends it to the Core engine.
2. **Core** builds the prompt, attaches context (GEMINI.md, project files,
   conversation history), and selects the appropriate provider.
3. **Provider** routes the request to the configured AI API, handling
   authentication and response parsing.
4. **AI API** returns a response — either text or structured tool calls.
5. **Core** processes the response: if it contains tool calls, executes them
   via the Tool system and feeds results back for another turn.
6. **CLI** renders the final output in the terminal.

## Provider System

The provider layer is the key differentiator of Waylou ACE CLI. It abstracts
away the differences between AI APIs and provides a unified interface.

### Supported Providers

| Provider | Models | Authentication |
|----------|--------|----------------|
| Google Gemini | Gemini 2.5, 3.0 | OAuth / API Key / Vertex AI |
| OpenAI | GPT-4, GPT-4o | API Key |
| Anthropic | Claude 3.5, Claude 4 | API Key |
| Ollama | Llama, Mistral, Gemma (local) | None (localhost) |
| DeepSeek | DeepSeek V3, R1 | API Key |

### BYOK (Bring Your Own Key)

Users bring their own API keys for any provider. Keys are stored locally and
never sent to any server. The core system does not proxy or log API calls.

### Team Orchestration

The Orchestrator can form teams of multiple models with different roles
(architect, coder, reviewer) and capabilities (coding, reasoning, speed,
creativity). Tasks are routed to the best model for the job using configurable
strategies (capability-best, round-robin, parallel-vote).

## ACE Specification

The Agentic Coding Environment (ACE) specification defines three compliance
levels that standardize agent behavior:

- **CORE**: Basic agent capabilities — file operations, shell commands,
  web fetching, code reading and editing.
- **STANDARD**: Enhanced capabilities — MCP integration, conversation
  checkpointing, sandboxed execution, memory management.
- **ENTERPRISE**: Production-grade features — policy engine, audit logging,
  team orchestration, multi-tenancy, compliance reporting.

Agents self-assess their capabilities against the ACE spec and report their
compliance level.

## Sandbox

The sandbox package provides isolated execution environments:

- **macOS**: Apple Seatbelt (built-in sandbox)
- **Linux**: Docker or Podman containers
- **Cross-platform**: child_process with restricted permissions

## Context Engine

The context engine enables semantic understanding of codebases:

- **Vector search**: SQLite-vec for embedding-based similarity search over
  code and documentation.
- **AST analysis**: Tree-sitter for structural code understanding across
  multiple languages.
- **Hybrid retrieval**: Combines vector distance with AST relevance for
  precise context selection.

## Technology Stack

| Component | Technology |
|-----------|------------|
| Runtime | Node.js 20+ |
| Language | TypeScript |
| Terminal UI | Ink (React for CLI) |
| Package Manager | npm (workspaces) |
| Build | esbuild + TypeScript compiler |
| Testing | Vitest |
| Linting | ESLint + Prettier |
| Git Hooks | Husky + lint-staged |
| Monorepo | npm workspaces |