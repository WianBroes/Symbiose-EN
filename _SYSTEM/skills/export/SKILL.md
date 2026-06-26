---
name: export
description: Export Symbiose framework or user data. Use when the user says "export", "export framework", "export profile", "backup", "prepare for GitHub", or wants to migrate to a new machine or share the framework.
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
_SYSTEM/AUTOSTART.md
_SYSTEM/CORE.md
_SYSTEM/CONVENTIONS.md
_SYSTEM/00_FIRST_STARTUP.md
_SYSTEM/QUICK_START.md
_SYSTEM/startup_ascii.md
_SYSTEM/analyse.md
_SYSTEM/skills/
_SYSTEM/_Templates/
_SYSTEM/modes/
_SYSTEM/pi-extensions/
.gitignore
```

**What is NOT copied:**
- `01_🧠Profil/` (personal data)
- `00_📥Inbox/` (content)
- Project folders (`XX_*/`)
- `.obsidian/`, `.claude/`, `CLAUDE.md`

**Created:** `00_📥Inbox/00_TRANSFERT.md` empty (startup template)

**Destination naming:** `Symbiose-framework-YYYY-MM-DD/`

---

### Mode B — User data

Exports `01_🧠Profil/` for migration to a new machine or tool.

**What is copied:**
```
01_🧠Profil/
  👤profil.md
  memory/
    observations.md
    modes.md
  profile/
    (all files)
```

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

Retrieve hostname: `hostname`
Retrieve date: `date +%Y-%m-%d`

### 3. Copy

**Mode A — Framework:**
```bash
DEST=~/Desktop/Symbiose-framework-$(date +%Y-%m-%d)
mkdir -p "$DEST/_SYSTEM" "$DEST/00_📥Inbox"

cp AGENTS.md "$DEST/"
cp .gitignore "$DEST/"
cp _SYSTEM/AUTOSTART.md _SYSTEM/CORE.md _SYSTEM/CONVENTIONS.md \
   _SYSTEM/00_FIRST_STARTUP.md _SYSTEM/QUICK_START.md \
   _SYSTEM/startup_ascii.md _SYSTEM/analyse.md "$DEST/_SYSTEM/"
cp -r _SYSTEM/skills "$DEST/_SYSTEM/"
cp -r _SYSTEM/_Templates "$DEST/_SYSTEM/"
cp -r _SYSTEM/modes "$DEST/_SYSTEM/"
cp -r _SYSTEM/pi-extensions "$DEST/_SYSTEM/"
```

Create empty TRANSFERT:
```bash
echo "# TRANSFERT" > "$DEST/00_📥Inbox/00_TRANSFERT.md"
```

**Mode B — User data:**
```bash
HOST=$(hostname)
DATE=$(date +%Y-%m-%d)
DEST=~/Desktop/@user_${HOST}_${DATE}

cp -r 01_🧠Profil/. "$DEST"
```

### 4. Validate

Display the created tree:
```bash
find "$DEST" -not -path '*/.git/*' | sort
```

Confirm: **"Export complete → `[path]`"**

---

## Rules

- Never include `01_🧠Profil/` in a framework export
- Never modify source files — copy only
- If destination already exists → ask for confirmation before overwriting
