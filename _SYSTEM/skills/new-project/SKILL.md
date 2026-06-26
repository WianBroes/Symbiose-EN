# Skill — new-project

> Create a new project folder in the vault following Symbiose conventions.
> Triggered by: "new project", "add a folder", "create a project", "new folder".

---

## 1. Find the next available number

```bash
ls -d [0-9][0-9]_* 2>/dev/null | sort | tail -1
```

Take the next number. `00_` and `01_` are system-reserved.

---

## 2. Choose the emoji

Ask if the domain is not obvious. Reference in `_SYSTEM/CONVENTIONS.md`:

| Domain | Emoji |
|--------|-------|
| Code / development | 💻 |
| Life project | 🌱 |
| Finance | 💰 |
| Research / study | 📚 |
| Creative / design | 🎨 |
| Personal | 🧑 |
| Legal / litigation | ⚖️ |

If the domain is not in the list → suggest a coherent emoji and validate with the user. Then add it to `CONVENTIONS.md`.

---

## 3. Create the structure

**Case A — category folder (placeholder or broad domain):**

```
XX_EmojiName/
└── PROJET.md      ← based on _SYSTEM/_Templates/Projet.md, status: dormant
```

**Case B — concrete project within an existing category:**

```
XX_EmojiCategory/
└── 🧬ProjectName/     ← thematic emoji + PascalCase name
    └── PROJET.md      ← based on _SYSTEM/_Templates/Master Project.md if tech, otherwise Projet.md
```

Rule: if the project has a stack / architecture → `Master Project.md`. Otherwise → `Projet.md`.

---

## 4. Fill in PROJET.md

Required fields:
- `nom` — short name
- `statut` — `actif | dormant | archive`
- `type` — `code | dossier | vie`
- `derniere_activite` — today's date

Optional fields depending on context:
- `stack` — if tech project
- `dependances` — if linked to other projects
- `tags` — free keywords

---

## 5. Icon on key files (optional)

If the user wants a visually identifiable file in the explorer:
→ Suggest 3-4 emojis coherent with the domain
→ Rename the file: `👤profil.md`, `🧬Symbiose/`, etc.
→ Update all references with `sed -i`

---

## 6. Update the parent category PROJET.md

If the project is nested in a category (Case B), update the `## Structure` section of the parent `PROJET.md` to reflect the new sub-project.

---

## 7. Confirm

Display the final folder tree of the created folder.
