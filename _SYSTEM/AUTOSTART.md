# AUTOSTART — Startup sequence

> Runs at the beginning of **every session**, triggered by the first user message.
> The user saying **"yo"** is the canonical startup signal.

---

### 1. Check

- `01_🧠Profil/👤profil.md` exists? → **Yes** → proceed to **Compact flow (section 3)**
- `01_🧠Profil/👤profil.md` exists? → **No** → proceed to **First startup (section 2)**

---

### 2. First startup 👶

1. **Display** `_SYSTEM/startup_ascii.md`
2. Run **`_SYSTEM/00_FIRST_STARTUP.md`** which:
   - Asks language preference (English / Français)
   - Scans the machine (OS, CPU, RAM, shell)
   - Asks name and short description
   - Creates user profile in `01_🧠Profil/`
   - `01_🧠Profil/👤profil.md` now serves as init marker
   - Updates `00_📥Inbox/00_TRANSFERT.md`
3. **Immediately follow with compact validation** — in the same response, without interruption:
   ```
   ✓ CORE · ENV · memory · TRANSFERT · TRAITS · SKILLS | [name]
   ```
   > Do not wait for a new message. The wizard and validation form a continuous sequence.
4. **Finish with:**
   ```
   Yo [name], système prêt.
   System is ready. Start whenever you are.
   ```

---

### 3. Subsequent sessions — compact flow 🔁

Triggered when `👤profil.md` exists.

1. **Display** `_SYSTEM/startup_ascii.md`
2. **Detect harness** (session only — not persisted):
   - `PI_CODING_AGENT=true` → PI
   - `CLAUDECODE=1` → Claude Code
   - otherwise → Unknown
3. **Check dream**: if `_SYSTEM/kernel/.dream_requested` exists → load and execute `_SYSTEM/skills/dream/SKILL.md` before applying the profile.
4. **Read & validate** silently:
   - `_SYSTEM/CORE.md` (section 0 — identity & project)
   - `01_🧠Profil/👤profil.md` ← machine, user, language, traits, skills
   - `01_🧠Profil/memory/observations.md`
   - `00_📥Inbox/00_TRANSFERT.md`
5. **Read & apply profile** (cf. CORE.md section 2b):
   - `01_🧠Profil/👤profil.md` (section 🧬 Traits) ← generate behavioral rules
   - `01_🧠Profil/👤profil.md` (section 🎯 Skills) ← adjust depth per domain
6. **Output** — compact validation:
   ```
   ✓ CORE · ENV · memory · TRANSFERT · TRAITS · SKILLS | [name]
   FR: Yo [name], système prêt.  |  EN: Yo [name], system ready.
   ```
7. **Check update** (silent):
   ```bash
   git -C . rev-parse --is-inside-work-tree 2>/dev/null && \
   git fetch origin 2>/dev/null
   BEHIND=$(git rev-list HEAD..origin/master --count 2>/dev/null)
   AHEAD=$(git rev-list origin/master..HEAD --count 2>/dev/null)
   ```
   - If `BEHIND` > 0 → display below greeting: `⬆️ Update available — say "update" to apply it.`
   - If `AHEAD` > 0 → display below greeting: `⬆️ You have [N] unpushed local commit(s) on GitHub.`
   - If both at 0 or error (no git, no network) → silent skip, no message.
8. **Display** TRANSFERT content visibly (below the greeting — shows current session context inline)
9. Wait for instructions — with profile rules active

---

### 4. Greeting handler 🖐️

Applies **regardless** of startup type when the user's first message is a greeting.

| User says | Behavior |
|-----------|----------|
| **"yo"** | Full startup flow (ASCII + greeting) **always** — whether first or subsequent session |
| "hi", "hey", "hello", etc. | Casual greeting → normal response (no ASCII art), then proceed with startup logic |

> **Note:** "yo" is the canonical startup word. It triggers the full branded greeting every time.
> Other greetings are treated as casual conversation starter without ceremony.
