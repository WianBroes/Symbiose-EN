# Commands & Triggers — Symbiose

> Everything is said in natural language. This page lists the recognized keywords and what they trigger.

---

## Startup

| What you say | What happens |
|--------------|--------------|
| `yo` | Full startup — ASCII art + validation + greeting |
| `hi`, `hey`, `hello` | Quiet startup — no ASCII art, but same logic |

---

## Closing

| What you say | What happens |
|--------------|--------------|
| `close` | Closure skill — macro-scan, profile update, TRANSFERT, snapshot |
| `we're done` | Same |
| `closure` | Same |

---

## Skills

| Trigger | Skill loaded | Effect |
|---------|--------------|--------|
| "import", "index", "process inbox" | `import` | Converts and indexes files from `00_📥Inbox/` |
| "export", "backup", "prepare for GitHub" | `export` | Exports profile + framework, prepares migration |
| "do a dream", "consolidate observations" | `dream` | Compacts `observations.md` — also called auto every 10 closures |
| "new project", "add a folder" | `new-project` | Creates a project folder following vault conventions |

---

## Profile & memory

| What you say | What happens |
|--------------|--------------|
| "analyse my traits" | Immediate micro-scan — updates `🧬 Traits` in the profile |
| "take stock" | Same |
| "what do you know about me" | Displays the active profile (traits + skills) |

---

## Modes

| What you say | Effect |
|--------------|--------|
| "switch to autonomous" | AUTONOMOUS mode — AI executes then documents |
| "switch to secure" | SECURE mode — summarize → validate → execute |
| "switch to critical" | CRITICAL mode — challenge → validate → execute |

Modes are also auto-detected from session signals (open files, task type).

---

## Automatic scans

- **Micro-scan** — every 10 messages (kernel) → updates traits/skills if signal detected
- **Macro-scan** — at every `close` → global analysis of the session
- **Dream** — every 10 closures → compacts accumulated observations
