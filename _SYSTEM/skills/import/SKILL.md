---
name: import
description: Import and index documents into a Symbiose project. Creates a mirrored structure with originals and AI-readable markdown versions. Use when files are present in 00_📥Inbox/, or when the user says "import", "index", "process inbox", "add these docs", "convert these files", or any variant asking to bring documents into a project.
---

# Import — Document indexing

Imports files into a Symbiose project by creating a mirror structure:
originals preserved + markdown versions for the AI.

## Target structure

```
[Project]/import/[import-name]/
├── Originals/        ← source files, preserved hierarchy
└── import MD/        ← .md mirror, same hierarchy
```

## Steps

### 1. Identify

Scan `00_📥Inbox/` for unprocessed files.
List and present to the user for confirmation.

### 2. Destination project

List existing `XX_*/` folders at the root.
Ask: **"Which destination project?"** or offer to create a new one.

### 3. Conversion mode

Ask: **"Import mode?"**

Brief explanation: full mode creates two folders — `Originals/` (intact files) + `import MD/` (text versions readable by the AI, same hierarchy). Originals-only mode skips conversion.

| Type | Action |
|------|--------|
| `.pdf` | `pdftotext file.pdf -` or `pandoc` → `.md` |
| `.docx` `.doc` `.odt` | `pandoc -t markdown` → `.md` |
| `.txt` `.md` | Direct copy |
| `.jpg` `.png` `.pptx` | Not convertible — `.md` stub only |

Options (present in this order):
1. **Full — Originals + import MD** ← default, present first
2. **Selective — choose which files to convert**
3. **Originals only — no conversion**

> **Invariant:** if converting, `.md` files are always transformed copies — the original in `Originals/` is never modified. Both versions always coexist.

### 4. Create the structure

```bash
mkdir -p "[Project]/import/[import-name]/Originals"
mkdir -p "[Project]/import/[import-name]/import MD"
```

> Single file (not a folder) → import-name = filename without extension.

### 5. Move originals

Move from `00_📥Inbox/[import-name]/` → `[Project]/import/[import-name]/Originals/`.
Preserve exact internal hierarchy.

### 6. Convert and create .md files

For each file, create the mirror in `import MD/` at the same relative path.

Frontmatter to add systematically:

```yaml
---
source: Originals/[relative-path]
date: [extracted from name if DD-MM-YY or YYYY format, otherwise ~]
actors: []
type: [mail | letter | legal | report | draft | personal-notes | annex]
status: [converted | empty | image]
---
```

Non-convertible files → stub:
```markdown
---
source: Originals/file.jpg
status: image
---
> Non-convertible file — see Originals/
```

### 7. Clean the Inbox

- Delete the processed folder in `00_📥Inbox/`
- Update `00_📥Inbox/00_TRANSFERT.md`

## Rules

- **Forward-only** — never reorganize what already exists in the project
- Hierarchy is **never flattened** — reproduced identically
- Later reorganization = user initiative, not the system's
