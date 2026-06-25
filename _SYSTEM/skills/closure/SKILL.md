---
name: closure
description: Session closure ritual. Macro-scan, TRANSFERT, snapshot. Triggered by "close", "we're done", "closure ritual".
trigger: close|we're done|closure|closure ritual
---

# Closure — Session end ritual

> **Read this file in full.** Do not skip steps. Do not improvise.
> Closure is the only moment the system learns from the session.
> Without it, the system stagnates.

---

## 0. Check — new content (MANDATORY)

**Never answer "already done" without checking.**

1. What was the **last message analysed** by the last micro-scan?
2. Are there **more recent** exchanges in this session?
3. If yes → scan is MANDATORY
4. If no → proceed

> The last exchanges are the richest — the user re-reads, questions, insists.

---

## 1. Macro-scan — full analysis

### 1a. Re-read the entire session

From memory, scan the session looking for:

- **Question structure**: anticipator? reactive? root cause or symptom?
- **Relationship to error**: insists or lets it slide?
- **Abstraction level**: systemic? practical? alternates?
- **Decision style**: validates quickly? compares multiple options?
- **Meta-position**: observes themselves?

### 1b. Trait signals

| Look for this | Trait |
|---------------|-------|
| Spontaneous decision ("yeah go", "ok direct") | `direct +1` |
| Hesitation / reversal ("actually no", "wait...") | `precise +1` |
| Positive reaction ("nice", "perfect") | satisfaction |
| Negative reaction ("too long", "not clear") | dissatisfaction → adjust |
| Code request ("give me the code") | `technical +1` |
| Explanation request ("explain the concept") | `pedagogical +1` |
| Recurring phrasing ("basically", "simply") | language register |
| Exploration ("could we also...?") | `explorer +1` |
| Redirection ("no that's not it") | `directive +1` |

### 1c. Skill signals

| Look for this | Action |
|---------------|--------|
| Technical jargon ("k8s cluster", "Promise.all") | Skill +1 XP |
| Precise instruction ("make a docker compose with 3 services") | Skill +1 XP |
| Exploratory question ("how does a vector store work?") | Emerging skill +1 XP |
| Corrects the AI ("no that's not how it works") | Skill +1 XP bonus |
| Cites a tool/framework ("I use Astro") | Skill tool +1 XP |

**Rules:**
- Max +2 XP per skill per scan
- AI correction: +1 XP additional
- New skill: create entry, XP=1, choose an emoji icon

### 1d. Apply accumulation

```
Score = total_cumulated_signals / nb_active_sessions
```

### 1e. Update files

- `01_Profil/profil.md` (🧬 Traits) — update scores
- `01_Profil/profil.md` (🎯 Skills) — add/increment XP
- `01_Profil/memory/observations.md` — **raw append** (no selection, no rephrasing)

### 1f. Notify significant changes

- Skill level-up → notify
- New trait → notify
- Significantly modified trait → notify

---

## 2. Dominant mode

Write to `01_Profil/memory/modes.md`:

```
[DATE] [PROJECT] — [description: what we did, signals, dominant mode]
```

Check last 5 entries — if pattern ≥ 2 → propose graduation.

---

## 3. Display summary

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔬 Symbiose Diagnostic
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📊 Traits:
  [trait]  [+/-score]  [description]

⚔️ Skills:
  [icon] [name]  Lv.[n]  +[n] XP  [description]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📋 Mode: [mode]
Session: [short/medium/long] — [👍/👎/🤝]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## 4. Kernel cleanup

```bash
echo 0 > _SYSTEM/kernel/.msg_count
```

---

## 5. Profile — propose, don't impose

Ask: *"I have [N] observation(s) that could enrich the profile: [list]. Want me to prepare them?"*

If yes → show changes before writing.
If no → don't insist.

---

## 6. TRANSFERT — update

Read `00_📥Inbox/00_TRANSFERT.md` → merge current state:
- **Resolved** → remove
- **Progressed** → update
- **New** → add
- **Unchanged** → keep

**Constraint:** max 5 items in "In progress". "Nothing — session wrapped" if empty.

---

## 7. Alpha pipeline — automatic review

**Mandatory.** The pipeline lives or dies here.

1. Read `_SYSTEM/alpha/00_INDEX.md`
2. For each feature in 🔬 ALPHA / 🧪 BETA / 🚦 PRERELEASE:
   - Check if `_SYSTEM/alpha/.used_[name]` exists → feature **used** this session
   - Check with `00_TRANSFERT.md` if files were modified → feature **modified**
3. **Counter rules:**
   - If **modified** → reset counter to 0
   - If **used** (flag present) → increment counter (+1) + delete the flag
   - If **neither** → counter unchanged
4. **Promotion thresholds:**
   - 🔬 ALPHA → 🧪 BETA: 3 usage sessions without bug
   - 🧪 BETA → 🚦 PRERELEASE: 5 usage sessions without bug
   - 🚦 PRERELEASE → ✅ RELEASE: propose to user
5. **Abandon:** if a feature hasn't been used in 5+ sessions → propose abandonment
6. Update `00_INDEX.md` + clean `.used_*` flags
7. Notify: *"Alpha pipeline: [X] promoted, [Y] proposed for abandonment."*

---

## 8. Closure counter

```bash
bash _SYSTEM/kernel/closure.sh
```

Every 10 closures, the counter sets `.dream_requested` → AI runs a consolidation dream at next startup.

---

## 9. Snapshot

```bash
git add "00_📥Inbox/00_TRANSFERT.md" [modified files] && git commit -m "session close YYYY-MM-DD" --quiet
git add 01_Profil/ && git commit -m "profile snapshot YYYY-MM-DD" --quiet
```

> If no git → silent skip.
