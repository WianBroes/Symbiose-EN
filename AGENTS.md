# Symbiose

> Adaptive framework — pure .md, zero code, zero dependencies.
> The system learns from you, session after session.

## ⚠️ IMPERATIVE — First response of the session

👉 **AS SOON AS the user sends their first message:**

1. Immediately check if `01_🧠Profil/👤profil.md` exists (`test -f 01_🧠Profil/👤profil.md`).
2. **If missing** → STOP. Execute `_SYSTEM/AUTOSTART.md` **immediately**.
   - Do NOT respond to the user.
   - Do NOT make small talk.
   - Display the ASCII art, launch the wizard, create the profile.
   - End with **"System is ready. Start whenever you are."**
3. **If it exists** → Execute `_SYSTEM/AUTOSTART.md` section 3 (compact flow).
   - ASCII art → validation → greeting.

> This rule applies to the **very first response** of each session.
> Not following it = broken system.

## ⚠️ IMPERATIVE — Periodic scan

👉 **At every message**, before responding:

Check if `[scan]` is present in context (system-reminder or hook output).
**If yes → load and execute `_SYSTEM/skills/scan/SKILL.md` IMMEDIATELY, before any response.**

> Do not defer. Do not merge with the response. Do not ignore.
> `[scan]` = mandatory scan, not a suggestion.

---

## ⚠️ IMPERATIVE — Command descriptions

👉 **For every bash command submitted for validation:**

The description MUST:
- Be in **plain English**
- Explain **what it does concretely** — not how it works technically
- Be readable by someone who does not code
- Allow validation **without reading the raw command**

Examples:
- ❌ `"Fetch and check commits behind"`
- ✅ `"Check if updates are available on GitHub"`
- ❌ `"Rebase local commits on top of origin/master"`
- ✅ `"Integrate the GitHub update while keeping local changes"`

> The user sees the raw command (with flags, options) but may not understand it.
> The description is the only thing they can rely on to decide whether to validate or not.

---

## Rules

- **Closing**: say "close" or "we're done" → `_SYSTEM/skills/closure/SKILL.md`
- **Natural language**: speak normally, no special commands.
- **Confirmation**: ask before deleting a `.md` file.
- **Memory**: `01_🧠Profil/memory/` — observations accumulate here.

📎 `_SYSTEM/CORE.md` — full manual (role, rules, modes, discipline)

---

## Available skills

> Skills loaded on demand. Read the corresponding `SKILL.md` as soon as the trigger is detected.
> Format: `_SYSTEM/skills/[name]/SKILL.md`

| Skill | File | Triggers |
|-------|------|---------|
| **scan** | `_SYSTEM/skills/scan/SKILL.md` | `[scan]` detected in system-reminder — **automatic, maximum priority** |
| **import** | `_SYSTEM/skills/import/SKILL.md` | "import", "index", "process inbox", "add these docs", files in `00_📥Inbox/` |
| **export** | `_SYSTEM/skills/export/SKILL.md` | "export", "export framework", "export profile", "backup", "prepare for GitHub", migration to new machine |
| **closure** | `_SYSTEM/skills/closure/SKILL.md` | "close", "closure", "we're done", "closure ritual" |
| **dream** | `_SYSTEM/skills/dream/SKILL.md` | "do a dream", "consolidate observations", "clean memory" |
| **new-project** | `_SYSTEM/skills/new-project/SKILL.md` | "new project", "add a folder", "create a project", "new folder" |
| **update** | `_SYSTEM/skills/update/SKILL.md` | "update", "check update" |
| **mirror** | `_SYSTEM/skills/mirror/SKILL.md` | "mirror", "mirror check", "mirror [file]", "sync EN", "translate [file]" |

---

## Pi extensions

> Optional extensions for PI — not included in the base system.
> Available in `_SYSTEM/pi-extensions/` of the repo.

| Extension | Folder | Added capability |
|-----------|--------|-----------------|
| **web-search** | `_SYSTEM/pi-extensions/web-search/` | Web search (DuckDuckGo) + page reading |

**Rule — web search under PI:**
If the user asks for a web search, to search the internet, or to read an external URL:
→ Reply: *"PI does not have native web search. The web-search extension is available in `_SYSTEM/pi-extensions/web-search/` — see the README for installation."*
→ Do not simulate the search. Do not invent results.
