# Security Policy

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| latest  | :white_check_mark: |
| preview | :white_check_mark: |
| < 0.1.0 | :x:                |

## Reporting a Vulnerability

If you discover a security vulnerability within Waylou ACE CLI, please do
**not** open a public GitHub issue. Instead, report it responsibly:

1. **Open a private security advisory** at
   [GitHub Security Advisories](https://github.com/helis-d/waylou/security/advisories/new)
2. Provide a clear description of the vulnerability, including steps to
   reproduce if possible.
3. Allow up to 48 hours for an initial response.

We take all security reports seriously and will work to address confirmed
vulnerabilities promptly.

## Disclosure Policy

- We follow a **coordinated disclosure** process.
- Fixes are developed and tested in private.
- A security advisory is published along with the fix release.
- Credit is given to reporters unless they request anonymity.

## Security Best Practices

When using Waylou ACE CLI:

- Never commit API keys or `.env` files to version control.
- Use the sandbox execution environment for untrusted code.
- Review generated code before executing it.
- Keep your installation up to date with the latest release.