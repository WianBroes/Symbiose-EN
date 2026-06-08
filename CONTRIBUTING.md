# Contributing to Symbiose

## 🐛 Report a bug

Open a [GitHub issue](https://github.com/WianBroes/Symbiose-EN/issues) with:
- The affected file
- What happens vs what should happen
- If possible, the command or message that triggered it

## 💡 Suggest an improvement

1. **Fork** the repo
2. **Create a branch**: `git checkout -b feature/my-change`
3. **Edit** the relevant files
4. **Commit and push**: `git commit -m "clear description" && git push origin feature/my-change`
5. **Open a Pull Request** with a description of what you changed and why

## 📐 Rules

- **Structure**: respect `_SYSTEM/` organization (CORE.md, modes/, memory/, profile/)
- **.md files**: comment your changes (why this change)
- **Behavior**: don't break the startup sequence (AUTOSTART.md → CORE.md)
- **Memory**: don't touch `_SYSTEM/memory/` in PRs — it's user-specific

## 📝 Style

- **Language**: English (system source files are in English)
- **Format**: readable Markdown, no excessive formatting
- **AGENTS.md**: stay agnostic — no tool-specific references

---

*Thanks for contributing 🙌*
