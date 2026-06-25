# CHANGELOG — Symbiose EN

---

## 2026-06-25

### v1.2 — Full parity with Symbiose-FR

**Kernel v2 — multi-tool support**
- Atomic increment: `kernel.sh` uses `mkdir` lock (Linux, macOS, Windows git-bash)
- `scan-check.sh`: scan logic extracted into dedicated script — single source of truth
- `.scan_interval`: configurable interval (default 10), shared across all tools
- Claude Code: `UserPromptSubmit` hook wired to kernel scripts (created by wizard)
- PI: extension updated to delegate to `scan-check.sh`

**Cross-platform**
- `kernel.sh`: `flock` (Linux) → `mkdir` lock (universal)
- `backup.sh`: `date -Iseconds` → `date +%Y-%m-%dT%H:%M:%S` (universal)
- Wizard machine scan: adapted commands for Linux / macOS / Windows

**Architecture (aligned with FR v1.2)**
- `01_Profil/` as user data bundle (OKF v0.1 compliant)
- Traits + Skills system with adaptive scan
- Full modes directory (LAB, STRUCTURAL, CREATION, DOSSIER, META, COMBINATIONS)
- Skills: closure, dream, export added
- Alpha pipeline: PROCESS.md + INDEX
- `analyse.md`: full adaptive scan protocol
- `CLAUDE.md` tracked — included in distribution

---

## 2026-06-08

### v1.1 — Initial English translation

- Full EN translation of all system files
- PATCH-001: renamed `00_📥 Inbox` → `00_📥Inbox`
- PATCH-002: fixed CLAUDECODE detection variable
- PATCH-003: wizard creates CLAUDE.md for Claude Code
- PATCH-004: pi-extensions/web-search added
