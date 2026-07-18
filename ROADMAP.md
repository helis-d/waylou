# Roadmap

Waylou ACE CLI is under active development. This roadmap outlines planned
features and areas of focus. Priorities may shift based on community
feedback and contributions.

## Guiding Principles

- **Provider freedom**: Users should never be locked into a single AI provider.
- **Terminal-first**: The CLI experience should be fast, responsive, and delightful.
- **Open by default**: Everything is open source. No proprietary features hidden behind licenses.
- **ACE compliance**: All features should map to one of the three ACE levels.

## Current Focus (Q3 2026)

### Provider Layer
- [ ] Improve test coverage to >80%
- [ ] Add Azure OpenAI provider
- [ ] Add AWS Bedrock provider
- [ ] Improve streaming stability across all providers
- [ ] Implement automatic fallback on provider errors
- [ ] Add provider health monitoring and metrics

### CLI Features
- [ ] `/explain` — Explain selected code
- [ ] `/fix` — Fix lint errors or bugs in context
- [ ] `/refactor` — Suggest refactoring improvements
- [ ] Theme system: user-customizable color schemes
- [ ] Multi-session / tabbed conversations
- [ ] Better onboarding wizard for first-time users

### ACE Specification
- [ ] Standardize compliance validation tooling
- [ ] Add self-assessment reporter (`waylou --ace-report`)
- [ ] Publish spec as standalone document
- [ ] Community review of ENTERPRISE level requirements

## Upcoming (Q4 2026)

### Provider Orchestration
- [ ] Dynamic team formation based on task analysis
- [ ] Cost-aware routing (auto-select cheapest capable model)
- [ ] Parallel execution with result merging
- [ ] Provider benchmarking suite

### Context Engine
- [ ] Incremental indexing (watch mode for changing codebases)
- [ ] Expanded language support via Tree-sitter grammars
- [ ] Embedding model selection (local, API-based)

### Sandbox
- [ ] Kubernetes executor support
- [ ] Resource limits and quotas
- [ ] Network policy configuration

### MCP Ecosystem
- [ ] MCP server marketplace / registry
- [ ] One-click MCP server installation
- [ ] MCP server testing utilities

## Future (2027+)

### Enterprise
- [ ] SSO / OIDC authentication
- [ ] Team management and collaboration
- [ ] Usage analytics dashboard
- [ ] Audit and compliance reporting

### Platform
- [ ] Web UI companion
- [ ] Mobile companion app
- [ ] IDE plugins (VS Code, JetBrains, Neovim)
- [ ] REST API for headless integration

### Community
- [ ] Contribution ladder (good first issue → core contributor)
- [ ] RFC process for major changes
- [ ] Community calls
- [ ] Documentation translations

## How to Influence the Roadmap

1. **Open an issue** with the `enhancement` label describing your idea.
2. **Upvote existing issues** with 👍 reactions to show demand.
3. **Submit a PR** — working code is the best way to move something forward.
4. **Join the discussion** on relevant issues.

## Completed

- [x] Multi-provider abstraction layer (Gemini, OpenAI, Anthropic, Ollama, DeepSeek)
- [x] BYOK (Bring Your Own Key) authentication model
- [x] Provider orchestration framework
- [x] ACE specification with CORE, STANDARD, ENTERPRISE levels
- [x] Autonomous engine for headless operation
- [x] Context engine with vector + AST search
- [x] Sandboxed execution (Seatbelt, Docker, Podman)
- [x] MCP (Model Context Protocol) support
- [x] VS Code companion extension
- [x] CI/CD pipeline with 40+ workflows

---

_Last updated: July 2026. This roadmap is a living document and reflects
current intentions, not commitments._