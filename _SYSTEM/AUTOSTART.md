# AUTOSTART — Startup sequence

> Runs at the beginning of **every session**, triggered by the first user message.
> The user saying **"yo"** is the canonical startup signal.

---

### 1. Check

- `01_Profil/profil.md` exists? → **Yes** → proceed to **Compact flow (section 3)**
- `01_Profil/profil.md` exists? → **No** → proceed to **First startup (section 2)**

---

### 2. First startup 👶

1. **Display** `_SYSTEM/startup_ascii.md`
2. **Validation:**
   ```
   ✓ CORE · ENV · memory · TRANSFERT
   ```
3. Run **`_SYSTEM/00_FIRST_STARTUP.md`** which:
   - Asks language preference (English / Français)
   - Scans the machine (OS, CPU, RAM, shell)
   - Detects the tool (PI, Claude Code, Codex CLI…)
   - Asks name and short description
   - Creates user profile in `01_Profil/`
   - `01_Profil/profil.md` now serves as init marker
4. **Proceed directly to Compact flow (section 3)** immediately after wizard ends.
5. **Finish with:**
   ```
   Yo [name], system ready.
   System is ready. Start whenever you are.
   ```

---

### 3. Subsequent sessions — compact flow 🔁

1. **Display** `_SYSTEM/startup_ascii.md`
2. **Read & validate** silently:
   - `_SYSTEM/CORE.md` (section 0 — identity & project)
   - `01_Profil/profil.md` ← machine, user, language, traits, skills
   - `01_Profil/memory/observations.md`
   - `00_📥Inbox/00_TRANSFERT.md`

### 3a. Dream — observation consolidation

If `_SYSTEM/kernel/.dream_requested` exists → load and execute `_SYSTEM/skills/dream/SKILL.md` before applying the profile.

3. **Read & apply profile** (cf. CORE.md section 2b):
   - `01_Profil/profil.md` (section 🧬 Traits) ← generate behavioral rules
   - `01_Profil/profil.md` (section 🎯 Skills) ← adjust depth per domain
4. **Output** — compact validation:
   ```
   ✓ CORE · ENV · memory · TRANSFERT · TRAITS · SKILLS | [name]
   Yo [name], system ready.
   ```
5. **Display** TRANSFERT content visibly (below greeting)
6. Wait for instructions — with profile rules active

---

### 4. Greeting handler 🖐️

| User says | Behavior |
|-----------|----------|
| **"yo"** | Full startup flow (ASCII + "Yo [name], system ready.") **always** |
| "hi", "hey", "hello", etc. | Casual greeting → normal response, no ASCII art |
