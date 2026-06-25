---
name: export
description: Export Symbiose framework or user data. Use when the user says "export framework", "export profile", "backup", "prepare for GitHub", or wants to migrate to a new machine or share the framework.
---

# Export — Framework & user data

Two modes: export the bare framework (GitHub-ready) or personal data (migration/backup).

## Modes

### Mode A — Framework

Produces a blank Symbiose ready to be cloned or pushed to GitHub.
Contains no personal data.

**What is copied:**
```
AGENTS.md
CLAUDE.md
_SYSTEM/AUTOSTART.md
_SYSTEM/CORE.md
_SYSTEM/CONVENTIONS.md
_SYSTEM/00_FIRST_STARTUP.md
_SYSTEM/00_SESSION_CLOSE.md
_SYSTEM/QUICK_START.md
_SYSTEM/startup_ascii.md
_SYSTEM/analyse.md
_SYSTEM/backup.sh
_SYSTEM/kernel/
_SYSTEM/modes/
_SYSTEM/skills/
_Templates/
pi-extensions/
.gitignore
README.md
LICENSE
CHANGELOG.md
CONTRIBUTING.md
```

**What is NOT copied:**
- `01_Profil/` (personal data)
- `00_📥Inbox/` (content)
- Project folders (`XX_*/`)
- `.obsidian/`, `.claude/`

**Created:** `00_📥Inbox/00_TRANSFERT.md` empty (startup template)

**Destination naming:** `Symbiose-framework-YYYY-MM-DD/`

---

### Mode B — User data

Exports `01_Profil/` for migration to a new machine or tool.

**Destination naming:** `@user_[hostname]_YYYY-MM-DD/`
The `@` prefix identifies a Symbiose user export at import.

---

## Steps

### 1. Identify mode

Ask if not specified:
```
Export framework (GitHub / sharing) or user data (migration / backup)?
  1. Framework
  2. User data
```

### 2. Destination

Ask for destination path or propose default:
- Framework: `~/Desktop/Symbiose-framework-YYYY-MM-DD/`
- User data: `~/Desktop/@user_[hostname]_YYYY-MM-DD/`

### 3. Copy

Use `git archive` if in a git repo (cleanest, respects .gitignore):
```bash
git archive --format=zip HEAD -o ~/Desktop/Symbiose-$(date +%Y-%m-%d).zip
```

Or manual copy for a directory export.

For user data:
```bash
HOST=$(hostname)
DATE=$(date +%Y-%m-%d)
DEST=~/Desktop/@user_${HOST}_${DATE}
cp -r 01_Profil/. "$DEST"
```

### 4. Validate

Display the created tree:
```bash
find "$DEST" -not -path '*/.git/*' | sort
```

Confirm: **"Export complete → `[path]`"**

---

## Rules

- Never include `01_Profil/` in a framework export
- Never modify source files — copy only
- If destination already exists → ask for confirmation before overwriting
