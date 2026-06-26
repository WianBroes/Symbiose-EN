# Security

## Automatic checks

Every update to the repo automatically goes through:

- **ShellCheck** — verifies that shell scripts do not contain dangerous patterns
- **Semgrep** — detects hidden network calls, dynamic executions, and known security patterns
- **detect-secrets** — scans all files for API keys, tokens, or credentials accidentally committed

The status of these checks is visible in the **Actions** tab of the GitHub repo.

## Reporting an issue

If you identify a security issue in this repo:

→ Open a **private issue** or contact the maintainer directly before making it public.

## Philosophy

Symbiose is a pure `.md` framework. The only executable files are the scripts in `_SYSTEM/kernel/` — their role is documented and their code is readable.
