# CHANGELOG — Symbiose

---

## 2026-06-08

### PATCH-001 — Removed space in `00_📥 Inbox`

**Problem:** the `00_📥 Inbox` folder contained a space → forced `\ ` in bash commands → triggered "backslash-escaped whitespace" warnings.

**Fix:** renamed to `00_📥Inbox`. All references updated in `README.md`, `AUTOSTART.md`, `00_FIRST_STARTUP.md`, `00_SESSION_CLOSE.md`, `CORE.md`.

---

### PATCH-002 — Claude Code detection variable

**Problem:** `00_FIRST_STARTUP.md` used `CLAUDE_CODE` → correct variable is `CLAUDECODE`.

**Fix:** variable corrected in the tool detection section.

---

### PATCH-003 — CLAUDE.md added to wizard

**Problem:** `CLAUDE.md` absent at root → Claude Code did not load `AGENTS.md` automatically.

**Fix:** wizard now offers to create `CLAUDE.md` if Claude Code is detected. `CLAUDE.md` added to `.gitignore`.

---

### PATCH-004 — PI extensions

**Added:** `pi-extensions/web-search/` folder — DuckDuckGo search + page reading for PI. Wizard offers installation if PI is detected. Documented in `AGENTS.md`, `CORE.md`, `README.md`.
