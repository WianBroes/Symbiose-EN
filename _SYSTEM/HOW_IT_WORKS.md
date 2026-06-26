# How it works — Symbiose

> How the system works under the hood.

---

## Overview

```
User
    │
    ▼
AGENTS.md ──── universal entry point (PI, Claude Code, Cursor, Codex…)
    │
    ▼
AUTOSTART.md ── startup sequence
    │
    ├── 01_🧠Profil/👤profil.md exists?
    │       ├── No → wizard (00_FIRST_STARTUP.md)
    │       └── Yes → compact flow (ASCII → validation → greeting)
    │
    ▼
Active session
    │
    ├── Each message → kernel.sh (counter) + scan-check.sh
    │       └── every 10 messages → [scan] → profile micro-scan
    │
    ├── Skills loaded on demand (trigger detected → reads SKILL.md)
    │
    └── "close" → skills/closure/SKILL.md → macro-scan → TRANSFERT → snapshot
```

---

## Kernel

Pure bash mechanism — independent of the AI tool.

```
_SYSTEM/kernel/
├── kernel.sh       ← atomically increments .msg_count
├── scan-check.sh   ← reads .scan_interval, emits [scan] when it's time
├── .msg_count      ← shared counter (do not touch)
└── .scan_interval  ← interval in messages (default: 10)
```

Hooked via `UserPromptSubmit` hook (Claude Code) or `.pi` extension (PI).
The AI receives `[scan]` in context when it's time — it does not manage the counter.

---

## Adaptive profile

The profile emerges from usage — it is not filled in manually.

```
01_🧠Profil/
├── 👤profil.md        ← Machine + User + 🧬 Traits + 🎯 Skills
└── memory/
    ├── observations.md ← raw signals accumulated session after session
    └── modes.md        ← history of dominant modes per session
```

**Adaptation cycle:**
1. The AI observes signals during the session (style, domain, pace)
2. Micro-scan every 10 messages → writes to `observations.md`
3. Macro-scan at closure → consolidates into `👤profil.md` (Traits + Skills)
4. At next startup → the AI reads the profile and adapts its behavior

**Traits** — behavior (direct, technical, concise…) → modify tone and form
**Skills** — domains (code, law, finance…) → modify depth

---

## Skills

Procedure modules loaded on demand. *Progressive disclosure* principle — only descriptions are in permanent context, content is read when the trigger is detected.

```
_SYSTEM/skills/
├── _INDEX.md          ← descriptions permanently visible
├── import/SKILL.md
├── export/SKILL.md
├── closure/SKILL.md
├── dream/SKILL.md
└── new-project/SKILL.md
```

---

## Modes

Auto-detected from session signals. Each mode suggests a level of autonomy.

| Mode | Detected signal | Autonomy |
|------|----------------|----------|
| LAB | .py/.js/.ts files, shell, builds | AUTONOMOUS |
| STRUCTURAL | .md only, reorganization | SECURE |
| FOLDER | sources to cross-reference, analysis | SECURE |
| CREATION | design, free writing | AUTONOMOUS |
| META | questions about Symbiose itself | CRITICAL |

Modes combine. The user can override at any time.

---

## Alpha pipeline

Every system evolution follows a formalized lifecycle:

```
IDEA → ALPHA → BETA → PRERELEASE → RELEASE
```

Managed in `_SYSTEM/alpha/`. Prevents uncontrolled modifications to the system core.

---

## Reset

Delete `01_🧠Profil/👤profil.md` → the wizard restarts at the next session.
The system (skills, modes, kernel) survives. Only the user profile is recreated.
