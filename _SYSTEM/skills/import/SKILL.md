---
name: import
description: Import and index documents into a Symbiose project. Creates a mirrored structure with originals and AI-readable markdown versions. Use when files are present in 00_📥Inbox/, or when the user says "import", "index", "process inbox", "add these docs", "convert these files", or any variant asking to bring documents into a project.
---

# Import — Document indexing

Imports files into a Symbiose project by creating a mirror structure:
originals preserved + markdown versions for the AI.

## Symbiose detection

**First of all**, scan `00_📥Inbox/` for folders whose name starts with `@user_`.

```bash
ls 00_📥Inbox/ | grep "^@user_"
```

Format: `@user_[hostname]_[date]`

If detected → **this is a Symbiose user export**, not an ordinary document.
Announce: **"Symbiose user export detected — from [hostname] ([date]). Import?"**

### `@user_` import

Merge into `01_🧠Profil/`:

**`profile/`** — file by file:
- Absent locally → direct copy
- Present on both sides → show diff, ask: keep local / take import / merge manually

**`memory/`**:
- `observations.md` → **append** (observations accumulate, do not overwrite)
- `modes.md` → **append**

Clean up inbox after successful import.

---

## Symbiose content detection

Scan `00_📥Inbox/` for folders whose name follows the pattern `XX_*` (ex: `01_MyProject`, `02_Archive`).

```bash
ls 00_📥Inbox/ | grep -E "^[0-9]{2}_"
```

If detected → **this is a Symbiose project folder**.
Announce: **"Symbiose project folder detected — [name]. Integrate at root?"**

### `XX_` import

- Check that a folder with the same name does not already exist at root
  - If yes → ask: replace / rename / cancel
- Move from `00_📥Inbox/[name]/` → project root
- No conversion — content is already in Symbiose format

Clean up inbox after successful import.

---

## Target structure (document import)

```
[Project]/import/[import-name]/
├── Originals/        ← source files, preserved tree
└── import MD/        ← .md mirror, same tree
```

## Steps

### 1. Identify

Scan `00_📥Inbox/` for unprocessed files (excluding already processed Symbiose packages).
List and present to user for confirmation.

### 2. Destination project

List existing `XX_*/` folders at root.
Ask: **"Which destination project?"** or offer to create a new one.

### 3. Conversion mode

Ask: **"Import mode?"**

Briefly explain: full mode creates two folders — `Originals/` (intact files) + `import MD/` (text versions readable by AI, same tree). Originals-only mode skips conversion.

| Type | Action |
|------|--------|
| `.pdf` | `pdftotext file.pdf -` or `pandoc` → `.md` |
| `.docx` `.doc` `.odt` | `pandoc -t markdown` → `.md` |
| `.txt` `.md` | Direct copy |
| `.jpg` `.png` `.pptx` | Not convertible — `.md` stub only |

Options (present in this order):
1. **Full — Originals + import MD** ← default, propose first
2. **Selective — choose which files to convert**
3. **Originals only — no conversion**

> **Invariant:** if conversion, the `.md` files are always transformed copies — the original in `Originals/` is never modified. Both versions always coexist.

### 4. Create the structure

```bash
mkdir -p "[Project]/import/[import-name]/Originals"
mkdir -p "[Project]/import/[import-name]/import MD"
```

> Single file (not a folder) → import-name = file name without extension.

### 5. Move originals

Move from `00_📥Inbox/[import-name]/` → `[Project]/import/[import-name]/Originals/`.
Preserve exact internal tree.

### 6. Convert and create .md files

For each file, create the mirror in `import MD/` at the same relative path.

Frontmatter to add systematically:

```yaml
---
source: Originals/[relative-path]
date: [extracted from name if DD-MM-YY or YYYY format, otherwise ~]
acteurs: []
type: [mail | letter | legal | report | draft | personal-notes | annex]
statut: [converted | empty | image]
---
```

Non-convertible files → stub:
```markdown
---
source: Originals/file.jpg
statut: image
---
> Non-convertible file — see Originals/
```

### 7. Clean up Inbox

- Delete the processed folder in `00_📥Inbox/`
- Update `00_📥Inbox/00_TRANSFERT.md`

## Rules

- **Forward-only** — never reorganize what already exists in the project
- The tree is **never flattened** — reproduced identically
- Later reorganization = user initiative, not system
