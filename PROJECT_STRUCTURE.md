# Project Structure

This document describes the complete folder structure of the Waylou ACE CLI
monorepo.

```
waylou/
├── .allstar/                   # Allstar security policy configuration
├── .gemini/                    # Gemini CLI configuration
│   ├── commands/               # Custom slash commands
│   ├── skills/                 # Custom skill definitions
│   ├── config.yaml             # Gemini config
│   └── settings.json           # User settings
├── .github/                    # GitHub configuration
│   ├── actions/                # Reusable GitHub Actions
│   │   ├── npm-auth-token/     # NPM authentication
│   │   ├── publish-release/    # Release publishing
│   │   ├── push-docker/        # Docker image push
│   │   ├── push-sandbox/       # Sandbox image push
│   │   ├── tag-npm-release/    # NPM release tagging
│   │   └── verify-release/     # Release verification
│   ├── ISSUE_TEMPLATE/         # Issue templates
│   │   ├── bug_report.yml      # Bug report form
│   │   ├── feature_request.yml # Feature request form
│   │   └── config.yml          # Issue template configuration
│   ├── scripts/                # GitHub automation scripts
│   ├── workflows/              # CI/CD pipelines (40+ workflows)
│   ├── CODEOWNERS              # Default code owners
│   ├── PULL_REQUEST_TEMPLATE.md # PR template
│   └── dependabot.yml          # Dependabot configuration
├── .husky/                     # Git hooks (Husky)
│   └── pre-commit              # Pre-commit hook script
├── .vscode/                    # VS Code workspace settings
│   ├── settings.json           # Editor settings
│   ├── launch.json             # Debug configurations
│   └── extensions.json        # Recommended extensions
├── bundle/                     # Bundled production output
├── docs/                       # Project documentation
│   ├── admin/                  # Admin & enterprise docs
│   ├── assets/                 # Images & static assets
│   ├── changelogs/             # Version changelogs
│   ├── cli/                    # CLI feature docs
│   ├── core/                   # Core library docs
│   ├── examples/               # Usage examples
│   ├── extensions/             # Extension development docs
│   ├── get-started/            # Getting started guides
│   ├── hooks/                  # Hooks documentation
│   ├── ide-integration/        # IDE integration docs
│   ├── mermaid/                # Mermaid diagram sources
│   ├── reference/              # API reference
│   ├── resources/              # Additional resources
│   └── tools/                  # Built-in tools docs
├── evals/                      # Evaluation test suite
│   ├── *.eval.ts               # Individual evaluation specs
│   └── README.md               # Evals documentation
├── integration-tests/          # Integration tests
├── memory-tests/               # Memory usage benchmarks
├── packages/                   # Monorepo packages (npm workspaces)
│   ├── ace-spec/               # ACE specification & validation
│   ├── autonomous-engine/      # Autonomous/headless engine
│   ├── cli/                    # Terminal UI & CLI binary
│   ├── context-engine/         # Vector/AST semantic search
│   ├── core/                   # Core agent logic library
│   ├── devtools/               # Developer tooling
│   ├── provider/               # Multi-AI provider layer
│   ├── sandbox/                # Secure execution environment
│   ├── sdk/                    # Public SDK for extensions
│   └── test-utils/             # Shared test utilities
├── perf-tests/                 # Performance benchmarks
├── schemas/                    # JSON schemas
├── scripts/                    # Build, dev & utility scripts
│   ├── pre-commit.js           # Lint-staged runner
│   ├── generate-settings-doc.ts # Settings doc generator
│   └── ...                     # Other utility scripts
├── sea/                        # Single Executable Application launcher
├── third_party/                # Vendored third-party code
└── tools/                      # Development tools & caretaker agents
│   ├── caretaker-agent/        # Automated issue triage agent
│   └── gemini-cli-bot/         # GitHub bot

Root files:
├── .editorconfig               # Editor configuration
├── .gitattributes              # Git attributes (LFS, line endings)
├── .gitignore                  # Git ignore rules
├── .lycheeignore               # Link checker ignore rules
├── .npmrc                      # npm configuration
├── .nvmrc                      # Node.js version requirement
├── .prettierignore             # Prettier ignore rules
├── .prettierrc.json            # Prettier configuration
├── .waylouignore               # Waylou ignore rules
├── .yamllint.yml               # YAML lint configuration
├── ARCHITECTURE.md             # Architecture documentation
├── CHANGELOG.md                # Project changelog
├── CODE_OF_CONDUCT.md          # Code of Conduct
├── CONTRIBUTING.md             # Contributing guide
├── Dockerfile                  # Docker build definition
├── FAQ.md                      # Frequently asked questions
├── GEMINI.md                   # Legacy project context file
├── IDEA.md                     # Brand transformation plan
├── LICENSE                     # Apache 2.0 license
├── Makefile                    # Make build targets
├── PROJECT_STRUCTURE.md        # This file
├── README.md                   # Project README
├── ROADMAP.md                  # Project roadmap
├── SECURITY.md                 # Security policy
├── SUPPORT.md                  # Support information
├── WAYLOU.md                   # Waylou project context
├── esbuild.config.js           # esbuild bundler config
├── eslint.config.js            # ESLint configuration
├── implementation_plan.md      # Implementation plan
├── package.json                # Root package manifest
├── package-lock.json           # Dependency lock file
├── run.js                      # Development runner script
├── tsconfig.json               # TypeScript configuration
└── vitest.workspace.ts         # Vitest workspace config (if present)
```

## Key Packages

### `cli` (`@waylou/cli`)
Terminal UI built with Ink (React for CLI). Provides the `waylou` binary.
Handles interactive mode, slash commands, authentication dialogs, and
provider selection UI.

### `core` (`@waylou/cli-core`)
The brain of the operation. Manages the agent loop, prompt construction,
tool execution, conversation history, configuration, and extensibility hooks.

### `provider` (`@waylou/cli-provider`)
Multi-provider abstraction layer. Defines a unified interface for all AI
providers (Gemini, OpenAI, Anthropic, Ollama, DeepSeek). Supports BYOK
(Bring Your Own Key) and team orchestration.

### `ace-spec` (`@waylou/ace-spec`)
Agentic Coding Environment specification. Defines CORE, STANDARD, and
ENTERPRISE compliance levels with associated capabilities and validation
rules. Used for self-assessment and compliance reporting.

### `autonomous-engine` (`@waylou/autonomous-engine`)
Runs the agent without a TUI — headless mode for scripts, CI/CD, and
automated workflows. Also provides the A2A (Agent-to-Agent) server.

### `context-engine` (`@waylou/context-engine`)
Semantic code understanding. Uses SQLite-vec for vector search and
Tree-sitter for AST analysis. Provides hybrid retrieval for precise
context selection.

### `sandbox` (`@waylou/sandbox`)
Secure execution environment. Supports macOS Seatbelt, Docker, Podman,
and restricted child_process modes.

### `sdk` (`@waylou/cli-sdk`)
Public SDK for building extensions and integrations with Waylou ACE CLI.

### `devtools` (`@waylou/cli-devtools`)
Internal development tools for the Waylou team.

### `test-utils` (`@waylou/cli-test-utils`)
Shared test utilities used across packages.