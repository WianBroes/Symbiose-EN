# 00_FIRST_STARTUP — First startup wizard

> Runs ONCE during the very first session.
> Configures the environment, detects tooling, creates the user profile.

---

### 1. Machine scan

Fill `_SYSTEM/ENV.md`:

```
hostname, OS (cat /etc/os-release), kernel (uname -a),
CPU (lscpu → model + cores), RAM (free -h), shell ($SHELL)
```

### 2. Tool detection

Identify the active tool:

```bash
echo "PI_CODING_AGENT=${PI_CODING_AGENT:-not detected}"
echo "CLAUDE_CODE=${CLAUDE_CODE:-not detected}"
```

### 3. Welcome

> **Welcome to Symbiose.**
>
> This is an **adaptive framework** — it learns from you, your sessions,
> your choices. The more you use it, the more it adapts to your way of working.
>
> **Ground rules:**
> - Speak naturally, as you would to a human.
> - Stay lucid and critical: I am a tool, not a truth.
> - At the end of each session, say **"close"** or **"we're done"**.
> - Core idea: **you build your own system**. I provide the frame, you fill the content.

### 4. User profile

Ask:
1. **Name or handle**
2. **Short description** — who you are, what you do, tech interests

Create `_SYSTEM/profile/README.md` with the collected info.

### 5. Finalization

Create the following files (gitignored — not tracked):
- `_SYSTEM/memory/observations.md` — title + *"No observations yet."*
- `_SYSTEM/memory/modes.md` — title + *"No sessions recorded."*
- `_SYSTEM/profile/traits.md` — empty table: `| Trait | When it activates | Rule for AI |`

Then:
- Write the marker: `_SYSTEM/.init_done` (empty file)
- Update `00_📥 Inbox/00_TRANSFERT.md`: "Initialization session — system ready"

> Note: final message "Yo [name], system ready." is handled by AUTOSTART.md after this wizard ends.
