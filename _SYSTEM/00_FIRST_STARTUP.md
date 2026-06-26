# 00_FIRST_STARTUP — First startup wizard

> Runs ONCE during the very first session.
> Configures the environment, detects the tooling, creates the user profile.

---

### 1. Language preference

```
Welcome to Symbiose! 🌍
Choose your language:
  1. English (default)
  2. Français
```

Save the preference to `01_Profil/profil.md` (field `**Language**` in the 👤 User section).

### 2. Machine scan

Fill `01_Profil/profil.md` (section 🖥️ Machine). Run **one command at a time** — do not group.

```bash
uname -s
```
→ Linux / Darwin / MINGW* → adapt the following commands accordingly.

**Linux:**
```bash
cat /etc/os-release | grep PRETTY_NAME
uname -r
cat /proc/cpuinfo | grep "model name" | head -1 | cut -d':' -f2 | xargs
free -h | awk '/^Mem:/{print $2}'
echo $SHELL
```

**macOS:**
```bash
sw_vers -productName
sw_vers -productVersion
uname -r
sysctl -n machdep.cpu.brand_string
echo "$(( $(sysctl -n hw.memsize) / 1073741824 )) GiB"
echo $SHELL
```

**Windows (git-bash):**
```bash
uname -o
uname -r
wmic cpu get name 2>/dev/null || echo "N/A"
wmic computersystem get TotalPhysicalMemory 2>/dev/null || echo "N/A"
echo $SHELL
```

> Rule: one command per call. If a command fails, continue with the next — do not block.

### 3. Tool detection

Identify the tool:

```bash
echo "PI_CODING_AGENT=${PI_CODING_AGENT:-not detected}"
echo "CLAUDECODE=${CLAUDECODE:-not detected}"
```

| Variable          | Expected value | Tool        |
|-------------------|----------------|-------------|
| `PI_CODING_AGENT` | any value      | PI          |
| `CLAUDECODE`      | `1`            | Claude Code |

**If `CLAUDECODE=1` detected → offer:**

```
Claude Code detected. Activate the kernel (automatic micro-scans)?
  1. Yes (recommended)
  2. No
```

- **If yes** → get the absolute project path (`pwd`), then create `.claude/settings.local.json`:
  ```bash
  PROJ=$(pwd)
  mkdir -p .claude
  cat > .claude/settings.local.json << EOF
  {
    "hooks": {
      "UserPromptSubmit": [
        {
          "matcher": "*",
          "hooks": [
            {
              "type": "command",
              "command": "bash '$PROJ/_SYSTEM/kernel/kernel.sh' && bash '$PROJ/_SYSTEM/kernel/scan-check.sh'",
              "timeout": 5
            }
          ]
        }
      ]
    }
  }
  EOF
  ```
  Confirm: *"Kernel activated — micro-scans every 10 messages."*
- **If no** → continue without. The system works, scans happen only at closure.

**If `PI_CODING_AGENT` detected → offer:**

```
PI detected. Web-search extension available (DuckDuckGo search + page reading).
Install now?
  1. Yes
  2. No
```

- **If yes** → execute:
  ```bash
  mkdir -p ~/.pi/agent/extensions
  cp -r pi-extensions/web-search ~/.pi/agent/extensions/web-search
  pip install duckduckgo-search
  cd ~/.pi/agent/extensions && npm install
  ```
  Confirm: *"Web-search extension installed. Restart PI to activate it."*
- **If no** → continue without. Reminder: available at any time in `pi-extensions/web-search/`.

### 4. Welcome

> **Welcome to Symbiose.**
>
> This is an **adaptive framework** — it learns from you, your sessions,
> your choices. The more you use it, the more it adapts to your way of working.
>
> **Ground rules:**
> - Speak naturally, as you would to a human.
> - Stay lucid and critical: I am a tool, not a source of truth.
> - At the end of each session, say **"close"** or **"we're done"**.
> - Core idea: **you are building your own system**. I provide the framework, you fill in the content.
>
> **Nothing is fixed.**
> The structure you see — folders, names, categories, rules — is a starting point, not a constraint.
> Everything can be renamed, reorganized, removed or enriched. Just say so.
> The system adapts to you, not the other way around.

### 5. User profile

Ask:
1. **Name or nickname**
2. **Short description** — who you are, what you do, tech interests

Add collected info to `01_Profil/profil.md` (section `## 👤 User`).

### 6. Obsidian configuration

If the vault is open in Obsidian, `.obsidian/` already exists. Otherwise, create it.

Create or update `.obsidian/graph.json` to exclude system folders from the graph:

```json
{
  "collapse-filter": true,
  "search": "-path:\"_SYSTEM\"",
  "showTags": false,
  "showAttachments": false,
  "hideUnresolved": false,
  "showOrphans": true,
  "collapse-color-groups": true,
  "colorGroups": [],
  "collapse-display": true,
  "showArrow": false,
  "textFadeMultiplier": 0,
  "nodeSizeMultiplier": 1,
  "lineSizeMultiplier": 1,
  "collapse-forces": true,
  "centerStrength": 0.518713248970312,
  "repelStrength": 10,
  "linkStrength": 1,
  "linkDistance": 250,
  "scale": 0.6666666666666666,
  "close": false
}
```

> If `.obsidian/graph.json` already exists: update only the `"search"` field, leave the rest unchanged.

### 7. Finalization

Create the following files (gitignored — not tracked):

- `01_Profil/index.md` — OKF bundle summary listing concepts
- `01_Profil/log.md` — change history (OKF §7)
- `01_Profil/profil.md` — sections 🖥️ Machine, 👤 User, 🧬 Traits, 🎯 Skills (single file, created at step 2) — with OKF frontmatter (`type: Symbiose.Profile`)
- `01_Profil/memory/observations.md` — OKF frontmatter (`type: Symbiose.Memory`), content *"No observations yet."*
- `01_Profil/memory/modes.md` — OKF frontmatter (`type: Symbiose.ModeHistory`), content *"No sessions recorded."*

Create vault folders (gitignored — not tracked) with their `PROJET.md`:

| Folder | name | type | status | description |
|--------|------|------|--------|-------------|
| `02_Symbiose/` | Symbiose | code | active | Adaptive AI framework — pure .md, zero dependency |
| `03_Dev/` | Dev | code | dormant | Development projects and code |
| `04_Life/` | Life | life | dormant | Life projects and personal development |
| `05_Finances/` | Finances | dossier | dormant | Financial tracking and assets |
| `06_Research/` | Research | dossier | dormant | Research, studies, learning |
| `07_Creative/` | Creative | dossier | dormant | Creative projects and design |

Each `PROJET.md` is generated from `_SYSTEM/_Templates/Projet.md` by replacing `{{NAME}}`, `{{DESCRIPTION}}`, `type`, `status` and `last_activity` (today's date). `{{TREE}}` = minimal folder tree. `{{STATUS_NOTES}}` = "No active project." except for Symbiose ("Active — admin: [username].").

> These folders are a starting point — the user can rename, delete, or add via the `new-project` skill.

Then:
- Create `00_📥Inbox/` and `00_📥Inbox/00_TRANSFERT.md` with the initial content:
  ```
  ---
  type: Symbiose.Transfert
  updated: [today's date]
  ---

  # TRANSFERT

  ## En chantier

  *(empty)*

  ## Résolu cette session

  - Initialization session — system ready ✓
  ```

> Then display the welcome message directly:
> ```
> Yo [name], system ready.
> System is ready. Start whenever you are.
> ```
