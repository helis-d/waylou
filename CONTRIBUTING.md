# Contributing to Waylou ACE CLI

Thank you for your interest in contributing. This guide covers everything
you need to get started.

## Project Status (Honest Assessment)

Waylou ACE CLI is a fork of Google Gemini CLI. We are actively developing
it, and some areas are more mature than others.

### Where We Need Help Most

**Provider layer** (`packages/provider`) — the biggest development need.

The provider layer handles:
- Unified interface across multiple AI APIs
- BYOK (Bring Your Own Key) authentication
- Provider orchestration and model routing

Known gaps:
- Test coverage is minimal
- New provider integrations needed (Azure, AWS Bedrock, LM Studio, llama.cpp)
- Streaming response stability varies by provider
- Fallback mechanisms need improvement when a provider returns errors

If you have experience with AI APIs, SDKs, or provider integrations, **you
are exactly who we need**.

### CLI Layer

The CLI (`packages/cli`) works but is **open for new features**:
- New slash commands (`/explain`, `/fix`, `/refactor`)
- Theme system enhancements
- Multi-session management
- Better error messages and user feedback

We want the CLI to be feature-rich. Creative ideas are welcome.

### Other Areas

- **Documentation**: Getting started guides, API references, examples
- **Testing**: Unit tests, integration tests, eval suite
- **ACE Specification**: Refining CORE, STANDARD, ENTERPRISE levels

## Development Setup

### Prerequisites
- Node.js 20.19.0 or later
- npm 9 or later

### Getting Started

```bash
# Clone the repository
git clone https://github.com/helis-d/waylou.git
cd waylou

# Install dependencies
npm install

# Build all packages
npm run build

# Run in development mode
node run.js
```

### Useful Commands

| Command | Description |
|---------|-------------|
| `npm run build` | Build all packages |
| `npm test` | Run all tests |
| `npm run lint` | Run ESLint and Prettier checks |
| `npm run typecheck` | Run TypeScript type checking |
| `node run.js` | Start the CLI in development mode |

## Repository Workflow

### Branch Strategy

| Branch | Purpose |
|--------|---------|
| `main` | Production branch. Always deployable. |
| `develop` | Integration branch for features. |
| `feature/*` | New features. Branch from `develop`. |
| `fix/*` | Bug fixes. Branch from `main`. |
| `release/*` | Release preparation. Branch from `develop`. |
| `hotfix/*` | Critical production fixes. Branch from `main`. |
| `docs/*` | Documentation-only changes. |

### Conventional Commits

All commits must follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

**Types:** `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`,
`build`, `ci`, `chore`, `revert`

**Scopes:** `cli`, `core`, `provider`, `ace-spec`, `autonomous-engine`,
`context-engine`, `sandbox`, `sdk`, `docs`, `ci`, `deps`

**Examples:**
```
feat(provider): add Anthropic streaming support
fix(cli): resolve crash in headless mode on Windows
docs(readme): update installation instructions
test(provider): add unit tests for orchestrator
refactor(core): simplify token counting logic
ci: add multi-platform build workflow
```

### Pull Request Process

1. **Open an issue first** — Describe what you want to change. This prevents
   wasted effort.
2. **Fork the repository** and create a feature branch.
3. **Make your changes** — Keep PRs focused and reasonably sized.
4. **Add tests** — New features must include tests.
5. **Run the full suite**: `npm run lint && npm test`
6. **Submit a PR** against the `develop` branch.
7. **Respond to review feedback** — Be open to suggestions.

### PR Requirements

- [ ] Follows [Conventional Commits](./CONTRIBUTING.md#conventional-commits)
- [ ] Includes tests for new functionality
- [ ] Updates documentation if needed
- [ ] Passes `npm run lint` with no errors
- [ ] Passes `npm test` with no failures
- [ ] Describes what the change does and why

## Code Standards

### TypeScript
- Use strict TypeScript. Avoid `any` — use `unknown` or proper types.
- Prefer `interface` over `type` for object shapes.
- Export types alongside implementations.

### Formatting
We use **Prettier** and **ESLint**. Formatting is enforced via a pre-commit
hook (Husky + lint-staged). Run manually with:

```bash
npm run lint
```

Key rules:
- 2-space indentation
- Single quotes
- Trailing commas in multi-line expressions
- Maximum 80 characters per line
- Semicolons required

### Naming Conventions
- **Files**: `kebab-case.ts` for modules, `PascalCase.tsx` for React components
- **Variables & functions**: `camelCase`
- **Classes & interfaces**: `PascalCase`
- **Constants**: `UPPER_SNAKE_CASE`
- **Types**: `PascalCase`, prefixed with `T` only if disambiguation needed

### Testing
- Use **Vitest** for all tests.
- Test files live next to their source: `foo.test.ts` alongside `foo.ts`.
- Aim for meaningful coverage — test behavior, not implementation.
- Run specific tests: `npx vitest path/to/test.test.ts`

## Issue Guidelines

### Bug Reports
Use the [Bug Report template](https://github.com/helis-d/waylou/issues/new?template=bug_report.yml).
Include:
- Steps to reproduce
- Expected vs actual behavior
- Environment details (OS, Node version, provider)

### Feature Requests
Use the [Feature Request template](https://github.com/helis-d/waylou/issues/new?template=feature_request.yml).
Describe:
- The problem you're trying to solve
- Your proposed solution
- Alternatives you've considered

## Release Process

Releases follow [Semantic Versioning](https://semver.org/).

| Channel | Frequency | Stability |
|---------|-----------|-----------|
| Nightly | Daily at 00:00 UTC | Experimental |
| Preview | Weekly on Tuesday 23:59 UTC | Pre-release |
| Stable | Weekly on Tuesday 20:00 UTC | Production |

The release workflow is automated via GitHub Actions. See
`.github/workflows/release-*.yml` for details.

## Code Review

All PRs require at least one review before merging. Reviewers look for:
- Correctness and edge-case handling
- Test coverage
- Code style and readability
- Performance implications
- Security considerations

## License

By contributing, you agree that your contributions will be licensed under
the Apache License 2.0. See [LICENSE](./LICENSE) for the full text.