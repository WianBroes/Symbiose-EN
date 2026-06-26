---
name: update
description: Update _SYSTEM/ from the git repo. Checks for available updates, applies if confirmed, handles migration if necessary.
trigger: "update", "check update"
---

# Skill — update

> Updates `_SYSTEM/` from the git origin repo.
> Triggered manually or from the startup notification.

---

## 1. Check context

```bash
git -C . rev-parse --is-inside-work-tree 2>/dev/null
```

- **Not a git repo** → display:
  > *"This vault is not a git repo. To update, download the latest version from GitHub and replace the `_SYSTEM/` folder manually."*
  → Stop here.

- **Git repo** → continue.

---

## 2. Silent fetch

```bash
git fetch origin 2>/dev/null
BEHIND=$(git rev-list HEAD..origin/master --count 2>/dev/null)
```

- `BEHIND=0` → display: *"Already up to date."* → stop.
- `BEHIND>0` → continue.

---

## 3. Display CHANGELOG diff

```bash
git diff HEAD origin/master -- CHANGELOG.md 2>/dev/null | grep "^+" | grep -v "^+++" | head -20
```

Display added lines from CHANGELOG since the current version.
If CHANGELOG empty or unavailable → display: *"`BEHIND` commit(s) available."*

---

## 4. Confirm

```
X commit(s) available. Apply the update?
  1. Yes
  2. No
```

---

## 5. Apply

```bash
git pull origin master
```

If conflict in `_SYSTEM/` → display the conflicting file and ask what to do (keep local / take origin).

---

## 6. Migration (if necessary)

Check if any vault folders are still tracked (old pre-v1.1 setups):

```bash
git ls-files | grep -E "^0[2-7]_|^00_📥Inbox/" 2>/dev/null
```

If non-empty result:
```bash
git rm -r --cached 00_📥Inbox/ 02_* 03_* 04_* 05_* 06_* 07_* 2>/dev/null
git commit -m "chore: untrack personal vault (v1.1 migration)"
```

Confirm: *"Migration applied — personal vault untracked from repo."*

---

## 7. Confirm

Display: *"Update applied. Restart the session for changes to take effect."*
