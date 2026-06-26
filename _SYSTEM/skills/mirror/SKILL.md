---
name: mirror
description: FR→EN synchronization. Detects missing or outdated files, translates on demand, updates MIRROR_STATUS.
trigger: "mirror", "mirror check", "mirror [file]", "sync EN", "translate [file]"
---

# Skill — mirror

> Synchronizes Symbiose-EN from Symbiose-FR.
> Claude translates. User validates. MIRROR_STATUS is the source of truth.

---

## Prerequisite — local EN repo

```bash
FR_ROOT=$(git rev-parse --show-toplevel)
EN_ROOT="${FR_ROOT/Symbiose-FR/Symbiose-EN}"
```

If `$EN_ROOT` does not exist:
```bash
gh repo clone WianBroes/Symbiose-EN "$EN_ROOT"
```
Confirm: *"EN repo cloned into `$EN_ROOT`."*

---

## Command: `mirror check`

**Goal:** display what is missing or outdated in EN.

### 1. Read MIRROR_STATUS

Load `_SYSTEM/MIRROR_STATUS.md` — list of all tracked files.

### 2. For each row in the table

```bash
CURRENT_HASH=$(git log -1 --format="%h" -- "[FR path]")
```

Compare `CURRENT_HASH` with the hash stored in MIRROR_STATUS:

| Condition | Status displayed |
|-----------|-----------------|
| Status = `✗ —` | `✗ missing` |
| Status = `⚠️ ~` | `⚠️ untracked — verification required` |
| Stored hash ≠ CURRENT_HASH | `⚠️ outdated (FR: CURRENT_HASH / EN: stored hash)` |
| Stored hash = CURRENT_HASH | `✓ up to date` |

### 3. Display the report

```
── Mirror check ──────────────────
✗ missing (4)
  · SECURITY.md
  · _SYSTEM/skills/scan/SKILL.md
  · _SYSTEM/skills/update/SKILL.md
  · _SYSTEM/skills/new-project/SKILL.md

⚠️ untracked (16)
  · README.md
  · AGENTS.md
  · ...

✓ up to date (0)
──────────────────────────────────
Say "mirror [file]" to translate.
```

---

## Command: `mirror [file]`

**Goal:** translate a file FR → EN, validate, write, update status.

Accepts: short name (`CORE.md`), FR path (`_SYSTEM/CORE.md`), or EN path (`_SYSTEM/COMMANDS.md`).
Resolve via MIRROR_STATUS if path is ambiguous.

### 1. Read the FR file

```bash
cat "$FR_ROOT/[FR path]"
```

### 2. Translate

- Translate all content to English
- Keep the structure identical (frontmatter, headings, tables, code blocks)
- Keep system proper nouns as-is: trait names (`direct`, `systémique`...), file names, bash commands, paths
- Adapt cultural references if necessary

### 3. Display the translation

Display the full translated content for validation.

```
── Translation: [file] ────────
[translated content]
──────────────────────────────────
OK to write to EN? (yes / corrections)
```

### 4. Write if validated

If user says "yes" or equivalent:

```bash
# Create folder if needed
mkdir -p "$EN_ROOT/$(dirname "[EN path]")"
# Write the file
# (write translated content to $EN_ROOT/[EN path])
```

### 5. Update MIRROR_STATUS

Get the current hash of the FR file:
```bash
NEW_HASH=$(git log -1 --format="%h" -- "[FR path]")
```

Update the corresponding row in `_SYSTEM/MIRROR_STATUS.md`:
- Replace the hash with `NEW_HASH`
- Replace the status with `✓ NEW_HASH`

### 6. Commit to EN

```bash
cd "$EN_ROOT"
git add "[EN path]"
git commit -m "mirror: translate [EN path] from FR [NEW_HASH]"
```

Confirm: *"[file] translated and committed to EN."*

---

## Command: `mirror push`

Push EN commits to GitHub:

```bash
cd "$EN_ROOT"
git push origin master
```

---

## Notes

- Never overwrite an EN file without displaying the translation and getting confirmation.
- If the existing EN file differs from the translation → display both and let the user choose.
- MIRROR_STATUS lives in FR — it is the source of truth for tracking.
- Personal data files (profile, memory, observations, TRANSFERT) are never mirrored.
