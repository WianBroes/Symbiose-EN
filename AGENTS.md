# Symbiose

> Adaptive framework — pure .md, zero code, zero dependencies.
> The system learns from you, session after session.

## ⚠️ IMPERATIVE — First response of the session

👉 **AS SOON as the user sends their first message:**

1. Immediately check if `_SYSTEM/.init_done` exists (`test -f _SYSTEM/.init_done`).
2. **If missing** → STOP. Run `_SYSTEM/AUTOSTART.md` **immediately**.
   - Do NOT respond to the user.
   - Do NOT make small talk.
   - Display ASCII art, run the wizard, create profile.
   - End with **"System is ready. Start whenever you are."**
3. **If present** → Run `_SYSTEM/AUTOSTART.md` section 3 (compact flow).
   - ASCII art → loading bar → validation → greeting.

> This rule applies to the **very first response** of each session.
> Not following it = broken system.

## Rules

- **Closing**: say "close" or "we're done" → `_SYSTEM/00_SESSION_CLOSE.md`
- **Natural language**: speak normally, no special commands.
- **Confirmation**: ask before deleting any `.md` file.
- **Memory**: `_SYSTEM/memory/` — observations accumulate here.

📎 `_SYSTEM/CORE.md` — full manual (role, rules, modes, discipline)
