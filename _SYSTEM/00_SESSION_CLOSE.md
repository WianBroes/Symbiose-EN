# 00_SESSION_CLOSE — Closure ritual

> **Single reference for closing a session.** Execute all steps silently, display one block at end.

---

## 0. Display

Final block : checklist → what was built → what remains → observations → profile suggestion.

```
## ✅ Closure checklist
- [ ] Sections 1-3 filled
- [ ] Dominant mode noted in _SYSTEM/memory/modes.md
- [ ] Self-improvement for active mode(s)
- [ ] Observations: X new
- [ ] Profile update suggested (section 3a)
- [ ] Profile updated (if confirmed)
- [ ] 00_TRANSFERT.md updated
- [ ] Local snapshot (`git add "00_📥 Inbox/00_TRANSFERT.md" [+ _SYSTEM/*.md if modified] && git commit -m "session close YYYY-MM-DD" --quiet`)
```

## 0b. Dominant mode (required)

Write to `_SYSTEM/memory/modes.md` :
```
[DATE] [PROJECT] — [raw description: what we did, signals, what dominated]
```

**New mode detection:** read last 5 entries → pattern ≥2x → candidate. 3 confirmations → propose graduation → the mode is documented in `_SYSTEM/memory/modes.md` with its suggested autonomy.

---

## 1. Trigger

User says **"close"**, **"we're done"**, or **"closure ritual"**.

## 2. Template

```markdown
# Session close {{DATE}} — {{TOPIC}}

**Agent:** {{ACTIVE AI}}
**Mode:** {{detected mode}}
**Triggered by:** user

---

## 1. 🔧 What was built

> Exact file paths, technical decisions, concrete results.

-

## 2. 🔶 What remains in progress

> Unresolved, known bugs, priorities (P1/P2/P3).

-

## 3. 🧠 Observations on user

> 3-5 max, only what's NEW. Format: `[observed]` / source: `[user]` `[symbiose]` `[AI]`.
> No psychologizing. Check `_SYSTEM/profile/` before writing.
> If you think there's nothing to observe → don't conclude alone. Ask the user.

-
```

## 3. After closure

### 3a. Profile — suggest, don't assume

Ask: *"I have [N] observation(s) that could enrich the profile: [list]. Want me to prepare them?"*

If user says yes → update `_SYSTEM/profile/` and `CORE.md` section 2 if actionable rule changes. Show changes before writing.

### 3b. Transfer merge (required)

Read existing `00_📥 Inbox/00_TRANSFERT.md` → merge current state :
- **Resolved** → remove
- **Progressed** → update
- **New** → add
- **Unchanged** → keep

Format :
```markdown
# TRANSFER — {{DATE}}

**Session:** {{TOPIC}}

---

## 🔶 In progress

> 3-5 items max, prioritized. "Nothing — session wrapped" if empty.

-

## 📁 Modified files

> Exact paths.

-

## 🧠 System changes

> New rules, created/deleted files.

-
```
