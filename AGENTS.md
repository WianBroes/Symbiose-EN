# Symbiose

> Adaptive framework — pure .md, zero code, zero dependencies.
> The system learns from you, session after session.

## ⚠️ MANDATORY — First response of the session

👉 **AS SOON as the user sends their first message:**

1. Immediately check if `_SYSTEM/.init_done` exists (`test -f _SYSTEM/.init_done`).
2. **If missing** → STOP. Execute `_SYSTEM/AUTOSTART.md` **immediately**.
   - Do NOT respond to the user.
   - Do NOT make small talk.
   - Display the ASCII art, run the wizard, create the profile.
   - End with **"System is ready. Start whenever you are."**
3. **If present** → Execute `_SYSTEM/AUTOSTART.md` section 3 (compact flow).
   - ASCII art → loading bar → validation → greeting.

> This rule applies to the **very first response** of each session.
> Not following it = broken system.

## Rules

- **Closing**: say "close" or "we're done" → `_SYSTEM/00_SESSION_CLOSE.md`
- **Natural language**: talk normally, no special commands.
- **Confirmation**: ask before deleting any `.md` file.
- **Memory**: `_SYSTEM/memory/` — observations accumulate here.

📎 `_SYSTEM/CORE.md` — full manual (role, rules, modes, discipline)

---

## Available Skills

> Skills loaded on demand. Read the corresponding `SKILL.md` as soon as the trigger is detected.
> Format: `_SYSTEM/skills/[name]/SKILL.md`

| Skill | File | Triggers |
|-------|------|---------|
| **import** | `_SYSTEM/skills/import/SKILL.md` | "import", "index", "process inbox", "add these docs", files in `00_📥Inbox/` |

---

## PI Extensions

> Optional extensions for PI — not included in the base system.
> Available in `pi-extensions/` in the repo.

| Extension | Folder | Added capability |
|-----------|--------|-----------------|
| **web-search** | `pi-extensions/web-search/` | Web search (DuckDuckGo) + page reading |

**Rule — web search under PI:**
If the user asks for a web search, to search the internet, or to read an external URL:
→ Reply: *"PI does not have native web search. The web-search extension is available in `pi-extensions/web-search/` — see the README for installation."*
→ Do not simulate the search. Do not invent results.
