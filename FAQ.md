# Frequently Asked Questions

## General

### What is Waylou ACE CLI?

Waylou ACE CLI is an open-source AI coding assistant that runs directly in
your terminal. It provides access to multiple AI models (Gemini, OpenAI,
Anthropic, Ollama, DeepSeek) through a single, unified interface. The
project was forked from Google Gemini CLI and extends it with multi-provider
support, autonomous operation, and a extensible architecture.

### How is it different from Google Gemini CLI?

Waylou ACE CLI builds on the foundation of Gemini CLI with these additions:

- **Multi-provider support**: Use any model you want, not just Gemini
- **Provider orchestration**: Route tasks to the best model for the job
- **ACE specification**: Standardized agent behavior with compliance levels
- **BYOK model**: Bring your own API keys for any provider
- **Autonomous engine**: Headless operation for CI/CD and scripts
- **Context engine**: Vector-based semantic code search
- **Active development**: New features and community contributions

### Is this project affiliated with Google?

No. Waylou ACE CLI is an independent fork of Google Gemini CLI, maintained
by the open-source community. It is not affiliated with or endorsed by
Google.

## Providers & Models

### Which AI providers are supported?

Currently supported providers:
- Google Gemini (Gemini 2.5, 3.0)
- OpenAI (GPT-4, GPT-4o)
- Anthropic (Claude 3.5, Claude 4)
- Ollama (local models: Llama, Mistral, Gemma)
- DeepSeek (DeepSeek V3, R1)

More providers are being added. See the
[CONTRIBUTING.md](CONTRIBUTING.md) if you'd like to help integrate a new one.

### How do I add my own API key?

```bash
# Gemini API Key
export GEMINI_API_KEY="your-key-here"

# OpenAI API Key
export OPENAI_API_KEY="your-key-here"

# Anthropic API Key
export ANTHROPIC_API_KEY="your-key-here"

# DeepSeek API Key
export DEEPSEEK_API_KEY="your-key-here"
```

You can also configure keys through the interactive setup when you first
run `waylou`.

### Can I use local models?

Yes. Install [Ollama](https://ollama.com), pull a model (`ollama pull
llama3`), and launch Waylou with:

```bash
waylou --provider ollama
```

### Is it free?

Yes, Waylou ACE CLI itself is free and open source (Apache 2.0). However,
the AI providers you connect to may have their own costs:

- **Google Gemini**: Free tier available (60 req/min, 1,000 req/day)
- **OpenAI**: Pay per token
- **Anthropic**: Pay per token
- **Ollama**: Free (runs locally on your hardware)
- **DeepSeek**: Pay per token

## Technical

### What are the system requirements?

- Node.js 20 or later
- npm 9 or later
- Operating system: macOS, Linux, or Windows (experimental)

### How do I install it?

```bash
npm install -g @waylou/cli
```

Or run without installation:

```bash
npx @waylou/cli
```

### How do I run it in headless mode?

```bash
waylou -p "Explain the architecture of this codebase"
```

For structured output:

```bash
waylou -p "List all TODO comments" --output-format json
```

### What is the ACE specification?

ACE stands for **Agentic Coding Environment**. It's a specification that defines
standardized agent behavior at three compliance levels:

- **CORE**: Basic file operations, shell commands, web fetch
- **STANDARD**: MCP integration, checkpointing, sandbox execution
- **ENTERPRISE**: Policy engine, audit logging, team orchestration

See [ARCHITECTURE.md](ARCHITECTURE.md) for more details.

### Does it support MCP servers?

Yes. Waylou ACE CLI supports the Model Context Protocol (MCP) for extending
its capabilities with custom tools. Configure MCP servers in
`~/.gemini/settings.json`.

## Contributing

### How can I contribute?

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full guide. The provider
layer is our biggest development need right now — if you have experience
with AI APIs, we'd love your help.

### What are the biggest areas that need help?

1. **Provider layer**: Adding new AI providers, improving existing ones
2. **CLI features**: New slash commands, UI improvements
3. **Documentation**: Better guides and examples
4. **Testing**: Increasing test coverage

### How do I report a bug?

Open a
[Bug Report](https://github.com/helis-d/waylou/issues/new?template=bug_report.yml)
on GitHub.

## Troubleshooting

### The CLI crashes on startup

1. Ensure Node.js 20+ is installed: `node --version`
2. Rebuild: `npm run build`
3. Check logs: `waylou --debug`

### My API key isn't working

1. Verify the environment variable is set: `echo $GEMINI_API_KEY`
2. Check the key at your provider's dashboard
3. Ensure the key has sufficient quota

### The terminal UI looks broken

1. Ensure your terminal supports Unicode and 256 colors
2. Try a different terminal (iTerm2, Windows Terminal, Kitty)
3. Set a simpler theme in settings