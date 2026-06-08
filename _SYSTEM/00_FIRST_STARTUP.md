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

Save the preference to `_SYSTEM/profile/language.md`.

### 2. Machine scan

Fill `_SYSTEM/ENV.md`:

```
hostname, OS (cat /etc/os-release), kernel (uname -a),
CPU (lscpu → model + cores), RAM (free -h), shell ($SHELL)
```

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

**If `CLAUDECODE=1` detected AND `CLAUDE.md` absent at root → offer:**

```
Claude Code detected. Create the auto-start file (CLAUDE.md)?
  1. Yes (recommended)
  2. No
```

- **If yes** → create `CLAUDE.md` at root:
  ```markdown
  # Symbiose — Claude Code

  Read `AGENTS.md` before responding to any message.
  ```
- **If no** → continue without, note in `ENV.md` that auto-start is disabled.

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

### 5. User profile

Ask:
1. **Name or nickname**
2. **Short description** — who you are, what you do, tech interests

Create `_SYSTEM/profile/README.md` with the collected info.
Create `_SYSTEM/profile/language.md` with the language preference.

### 6. Obsidian configuration

If the vault is open in Obsidian, `.obsidian/` already exists. Otherwise, create it.

Create or update `.obsidian/graph.json` to exclude system folders from the graph:

```json
{
  "collapse-filter": true,
  "search": "-path:\"_SYSTEM\" -path:\"_Templates\" -path:\"_Meta\"",
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

> If `.obsidian/graph.json` already exists: update only the `"search"` field without touching the rest.

### 7. Finalization

Create the following files (gitignored — not tracked):
- `_SYSTEM/memory/observations.md` — title `# Observations` + line *"No observations yet."*
- `_SYSTEM/memory/modes.md` — title `# Work modes` + line *"No sessions recorded."*
- `_SYSTEM/profile/traits.md` — empty table: `| Trait | When it activates | Rule for the AI |`

Then:
- Write the marker: `_SYSTEM/.init_done` (empty file)
- Update `00_📥Inbox/00_TRANSFERT.md`: "Initialization session — system ready"

> Note: the final messages "Yo [name], système prêt." + "System is ready. Start whenever you are." are handled by AUTOSTART.md after this wizard ends.
