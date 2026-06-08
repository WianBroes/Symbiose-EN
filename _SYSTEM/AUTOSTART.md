# AUTOSTART — Startup sequence

> Runs at the beginning of **every session**, triggered by the first user message.
> The user saying **"yo"** is the canonical startup signal.

---

### 1. Check

- `_SYSTEM/.init_done` exists? → **Yes** → proceed to **Compact flow (section 3)**
- `_SYSTEM/.init_done` exists? → **No** → proceed to **First startup (section 2)**

---

### 2. First startup 👶

The greeting (ASCII + loading bar) comes **first**, then the wizard.

1. **Display** `_SYSTEM/startup_ascii.md`
2. **Loading bar:**
   ```
   ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓  100%
   ✓ CORE · ENV · memory · TRANSFERT
   ```
3. Run **`_SYSTEM/00_FIRST_STARTUP.md`** which:
   - Asks language preference (English / Français)
   - Scans the machine (OS, CPU, RAM, shell)
   - Detects the tool (PI, Claude Code, Codex CLI…)
   - Asks name and short description
   - Creates user profile in `_SYSTEM/profile/`
   - Writes `_SYSTEM/.init_done` marker
   - Updates `00_📥Inbox/00_TRANSFERT.md`
4. **Finish with:**
   ```
   Yo [name], système prêt.
   System is ready. Start whenever you are.
   ```

---

### 3. Subsequent sessions — compact flow 🔁

Triggered when `.init_done` exists.

1. **Display** `_SYSTEM/startup_ascii.md`
2. **Read & validate** silently:
   - `_SYSTEM/profile/language.md` ← determines greeting language
   - `_SYSTEM/CORE.md` (section 0 — identity & project)
   - `_SYSTEM/ENV.md`
   - `_SYSTEM/memory/observations.md`
   - `00_📥Inbox/00_TRANSFERT.md`
3. **Output** — loading bar + compact validation:
   ```
   ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓  100%
   ✓ CORE · ENV · memory · TRANSFERT | [name]
   FR: Yo [name], système prêt.  |  EN: Yo [name], system ready.
   ```
4. **Display** TRANSFERT content visibly (below the greeting — shows current session context inline)
5. Wait for instructions

---

### 4. Greeting handler 🖐️

Applies **regardless** of startup type when the user's first message is a greeting.

| User says     | Behavior |
|---------------|----------|
| **"yo"**     | Full startup flow (ASCII + loading bar + "Yo [name], system ready.") **always** — whether first or subsequent session |
| "hey", "hi", "hello", etc. | Casual greeting → normal response (no ASCII art), then proceed with startup logic |

> **Note:** "yo" is the canonical startup word. It triggers the full branded greeting every time.
> Other greetings are treated as casual conversation starters without ceremony.
