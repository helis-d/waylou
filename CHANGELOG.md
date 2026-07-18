# Changelog

All notable changes to the Waylou ACE CLI project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

> **Note:** This file serves as the project-level changelog. Detailed,
> versioned release notes are maintained in the
> [`docs/changelogs/`](docs/changelogs/) directory. For the full release
> history, see the [Release Notes Index](docs/changelogs/index.md) and
> [GitHub Releases](https://github.com/helis-d/waylou/releases).

## Release Channels

| Channel | Description | Changelog |
|---------|-------------|-----------|
| **Stable** | Recommended for general use | [`latest.md`](docs/changelogs/latest.md) |
| **Preview** | Experimental features for early feedback | [`preview.md`](docs/changelogs/preview.md) |
| **Nightly** | Built from `main`, most recent changes | — |

## [Unreleased]

### Added
- Multi-provider support layer (OpenAI, Anthropic, Ollama, DeepSeek)
- ACE (Agentic Coding Environment) specification framework
- Autonomous engine for headless operation
- Context engine with vector and AST-based semantic code search
- Sandboxed execution environment
- MCP (Model Context Protocol) integration
- VS Code IDE companion extension

### Changed
- Rebranded from Google Gemini CLI to Waylou ACE CLI
- Updated package structure and naming conventions

### Fixed
- N/A (initial fork release)

[unreleased]: https://github.com/helis-d/waylou/compare/v0.1.0...HEAD