# 🚀 Quick Start — Symbiose

**You just cloned the repo. Here's how to get started in 2 minutes.**

---

## 1. Launch your AI tool

Open a terminal in the project folder and type:

| Tool | Command |
|------|---------|
| **PI** | `pi` |
| **Claude Code** | `claude` |
| **Codex CLI** | `codex` |
| **Cursor** | `cursor .` |
| **Continue.dev** | Open the folder in VS Code with the extension |
| **Other** | Launch your tool in this folder |

---

## 2. Say "yo"

The system detects it's your first session and:

```
1. Asks your language preference
2. Scans your machine (OS, RAM, CPU)
3. Identifies your tool (PI, Claude Code…)
4. Welcomes you
5. Asks your name and profile
6. Creates your profile
7. Marks initialization as done
→ System ready
```

Then, talk to it **naturally**, in plain language.

---

## 3. Use the system

Nothing to learn. Give instructions like you would to a human:

- *"Analyze this file"*
- *"Create a Python script that does X"*
- *"Explain this folder structure"*
- *"Find all recently modified markdown files"*

The AI announces each action before executing it. You validate or correct.

Project templates are available in `_Templates/`.

---

## 4. Close the session

At the end of a session, say:

```
close
```

or

```
we're done
```

The system automatically saves context in `00_TRANSFERT.md` for the next session.
**Without closing, the system doesn't learn — it stagnates.**

---

## 💡 Good to know

- **Everything is in the files.** Open any `.md` in `_SYSTEM/` to understand or modify behavior.
- **The system learns.** The more you use it, the more relevant the AI becomes for you.
- **You stay in control.** The AI does nothing without validation (SECURE mode by default).
- **No dependencies for the base system.** Just markdown files. Optional extensions (e.g. web-search for PI) have their own dependencies — the wizard offers automatic installation.
- **Automatic backup at each closure.** Each session close saves system state locally — nothing is sent online. If something breaks, just tell your AI *"something isn't working, restore the system to its previous state"* — it handles the rest.

---

## 🚨 Troubleshooting

| Problem | Solution |
|---------|----------|
| AI doesn't respond at startup | Make sure you're in the Symbiose folder |
| "Missing file" error | Check that all `_SYSTEM/` files are present (CORE.md, AUTOSTART.md, 00_SESSION_CLOSE.md) — `ENV.md` is generated at first startup |
| System doesn't remember me | Check that `_SYSTEM/.init_done` exists (otherwise it reinitializes) |
| I want to start over | Delete `_SYSTEM/.init_done` and `_SYSTEM/memory/observations.md` |

---

**You're ready. 🤝**
