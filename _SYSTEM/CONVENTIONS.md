# CONVENTIONS — Vault architecture

> Organization rules for the Symbiose vault.
> The system is agnostic, but these conventions are optimized for **Obsidian** (explorer sorting, emoji rendering, internal links).
> They remain valid in terminal or any other tool.

---

## Root folders

Format: `XX_emoji Name`

| Component | Rule |
|-----------|------|
| `XX_` | Two digits + underscore — controls order in Obsidian explorer and `ls` |
| `emoji` | One thematic emoji right after the underscore — readable at a glance |
| `Name` | PascalCase or kebab-case |

**Reserved:**
- `00_` → system only (`00_📥Inbox`)
- `_` (leading underscore) → hidden folders in Obsidian (`_SYSTEM`, `_Templates`)

**New projects:** list the root, take the next free number starting from `01_`.

**Emoji by domain:**
| Domain | Emoji |
|--------|-------|
| Legal / dispute | ⚖️ |
| Code / development | 💻 |
| Life project | 🌱 |
| Research / study | 📚 |
| Finance | 💰 |
| Creative / design | 🎨 |
| Personal | 🧑 |

Examples: `01_⚖️Legal-Case`, `02_💻MyApp`, `03_🌱Garden`.

---

## Files

- Names in `UPPERCASE.md` for structural project files (`README`, `TIMELINE`, `ACTORS`, `OPEN_POINTS`).
- Names in `kebab-case.md` for regular notes.
- No spaces in file names — Obsidian links work but it's fragile in terminal.

---

## System folders

| Folder | Role |
|--------|------|
| `_SYSTEM/` | System core — do not modify without reason |
| `_Templates/` | File and project templates |
| `_Meta/` | Non-content root files: README, LICENSE, CONTRIBUTING |
| `00_📥Inbox/` | Entry point: TRANSFERT, files waiting to be sorted |

**Hard-locked files at root** (do not move):
- `AGENTS.md` — universal entry point for all AI tools
- `CLAUDE.md` — required by Claude Code

---

## Obsidian graph

`_` folders are excluded from the graph by default via `.obsidian/graph.json`:
```
-path:"_SYSTEM" -path:"_Templates" -path:"_Meta"
```

The graph only shows projects and their real connections — actors, locations, structural files. Working notes in `notes/` appear; system files do not.

**Graph-friendly writing:**
- People → `[[First Last]]`
- Locations / key entities → `[[Name]]`
- Structural project files → linked from README (`Linked to: [[TIMELINE]] · [[ACTORS]]…`)
- Dates → plain text, no links
