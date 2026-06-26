---
name: closure
description: Session closure ritual. Macro-scan, TRANSFERT, snapshot. Triggered by "close", "closure", "we're done", "closure ritual".
trigger: close|closure|we're done|closure ritual
---

# Closure — End-of-session ritual

> **Read this file in full.** Do not skip steps. Do not improvise.
> Closure is the only moment when the system learns from the session.
> Without it, the system stagnates.

---

## 0. Verification — new content (MANDATORY)

**Never say "already done" without checking.**

1. What was the **last message analyzed** by the last micro-scan?
2. Are there **more recent** exchanges in this session?
3. If yes → scan is MANDATORY
4. If no → proceed

> The last exchanges are the richest — the user re-reads, questions, insists.

---

## 1. Macro-scan — full analysis

### 1a. Re-read the full session

In my memory, go through the session and look for:

- **Question structure**: anticipator? reactive? root cause or symptom?
- **Relationship to error**: insists or lets it go?
- **Abstraction level**: systemic? practical? alternates?
- **Decision style**: validates quickly? compares multiple options?
- **Meta-position**: observes themselves?

### 1b. Trait signals

| Look for | Trait |
|----------|-------|
| Spontaneous decision ("yes go ahead", "ok direct") | `direct +1` |
| Hesitation / reversal ("actually no", "in the end...") | `precis +1` |
| Positive reaction ("ah cool", "perfect") | satisfaction |
| Negative reaction ("too long", "not clear") | dissatisfaction → adjust |
| Code request ("give the code", "do this") | `technique +1` |
| Explanation request ("explain the concept") | `pédagogue +1` |
| Recurring formulation ("basically", "simply") | language register |
| Exploration ("could we also...?") | `explorateur +1` |
| Redirection ("no that's not it") | `directif +1` |
| Brings lived experience as proof (travel, field, past) | `observateur +1` |
| Reframes at a higher level of abstraction, sees limit of a response | `systémique +1` |
| Spontaneously connects two unrelated domains | `systémique +1` |
| Reaches a synthesis or action plan without being asked | `synthétiseur +1` |

> **Off-project sessions (conversation, daily life, curiosity):** cognitive traits appear more clearly here than in work sessions. Scan with the same rigor — often richer.

### 1c. Skill signals

| Look for | Action |
|----------|--------|
| Technical jargon ("k8s cluster", "Promise.all") | Skill +1 XP |
| Precise instruction ("make a docker compose with 3 services") | Skill +1 XP |
| Exploratory question ("how does a vector store work?") | Emerging skill +1 XP |
| Corrects the AI ("no that's not how it works") | Skill +1 XP bonus |
| Cites a tool/framework ("I use Astro") | Tool skill +1 XP |
| Combo two domains ("my Rust API in a container") | Rust + Docker combo |

**Rules:**
- Max +2 XP per skill per scan
- AI correction: +1 XP additional
- New skill: create entry, XP=1, choose an emoji icon

### 1d. Apply accumulation

```
Score = total_cumulative_signals / nb_active_sessions
```

Each signal detected in session is added to the trait's cumulative total.
The score is the per-session average — stable, differentiated, without artificial convergence.

### 1e. Update files

- `01_🧠Profil/👤profil.md` (🧬 Traits) — update scores
- `01_🧠Profil/👤profil.md` (🎯 Skills) — add/increment XP
- `01_🧠Profil/👤profil.md` (🔭 En émergence) — increment sessions, add new signals
- `01_🧠Profil/👤profil.md` (🧠 Modes de pensée) — promote if ≥ 3 sessions
- `01_🧠Profil/👤profil.md` (⚡ Synergies) — add or increment
- `01_🧠Profil/memory/observations.md` — **raw append** (no selection, no reformulation)

### 1f. Discovery scan — reasoning pattern

> This scan looks for **how** they think, not what they know. Fill in only if signal observed — do not force.

| Signal observed | Action |
|-----------------|--------|
| Structures ideas in branches/sub-categories spontaneously | `🔭 arborescente +1` |
| Starts from a concrete example to reach a general rule | `🔭 inductive +1` |
| Starts from a principle to descend to concrete cases | `🔭 déductive +1` |
| Connects two domains through a common mechanism (analogy) | `🔭 analogique +1` |
| Uses knowledge from one domain to solve a problem in another | `🔭 transversale +1` |
| Looks for patterns, recurrences, invariants | `🔭 pattern-matching +1` |
| Identifies exceptions, what doesn't fit the rule | `🔭 critique +1` |
| Reformulates the problem differently before answering | `🔭 recadrage +1` |

**Promotion rule:**
- Signal in `🔭 En émergence` ≥ 3 distinct sessions → suggest promotion to `🧠 Modes de pensée`
- Never promote based on user declaration — observation only

### 1g. Free question — what did I learn about them?

Ask **one single question, no imposed format:**

> *"What did I learn about this person this session?"*

Answer freely — no table, no category, no signal to check. What the session revealed about who they are, how they think, what matters to them. Things that wouldn't have appeared in a mechanical scan.

Write the answer in `memory/observations.md` — raw, as is, without reformatting.
Attribute the source: `[symbiose]` if it emerges from the interaction, `[IA]` if it's a projection to verify.

> It's the AI that analyzes, not the user. The value comes from this asymmetry.

### 1h. Synergy scan

> After scanning traits, skills, and thinking modes separately — look at combinations.
> Do not force. Only if a combination points to something the elements alone don't show.

**Question:** *"Are there 2-3 elements from different dimensions that reinforce each other and point in the same direction?"*

**If yes:**
1. Name the pattern (a short phrase, not a label)
2. List the elements that compose it
3. Formulate the direction — a direction, not a conclusion
4. Add to `⚡ Synergies` in the profile

**Promotion rule:**
- Synergy observed in 1 session → note in `⚡ Synergies` (Sessions: 1)
- Confirmed in 2+ distinct sessions → **active** direction (indicate in Direction column)
- Contradicted by new elements → mark `❌ infirmé` + reason (do not delete — trace remains)

**Example combinations to watch:**

| Combination | Possible direction |
|-------------|-------------------|
| `observateur` + `analogique` + `systémique` | Knowledge translator — draws laws from reality, transfers them across domains |
| `direct` + `synthétiseur` + `arborescente` | Solution architect — structures fast, decides without losing nuance |
| `explorateur` + `transversale` + `inductive` | Learns by connecting — not by accumulating |
| `precis` + `systémique` + `recadrage` | Critical thinker — sees the limit of a model before others |

> These examples are prompts, not rules. The system builds its own combinations from the real elements observed.

### 1i. Notify significant changes

- Skill level-up → notify
- New trait → notify
- Trait significantly modified → notify

---

## 2. Dominant mode

Write in `01_🧠Profil/memory/modes.md`:

```
[DATE] [PROJECT] — [description: what we did, signals, dominant mode]
```

Check the last 5 entries — if pattern ≥ 2 → suggest graduation.

---

## 3. Display summary

Mandatory format — no variation:

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

## 5. Profile — suggest (do not impose)

Ask: *"I have [N] observation(s) that could enrich the profile: [list]. Shall I prepare them?"*

If yes → show changes before writing.
If no → do not insist.

---

## 6. TRANSFERT — update

Read `00_📥Inbox/00_TRANSFERT.md` → merge current state:
- **Resolved** → delete
- **Advanced** → update
- **New** → add
- **Unchanged** → keep

**Constraint:** max 5 items in "In progress". "Nothing — session complete" if empty.

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
   - If **neither modified nor used** → counter unchanged
4. **Promotion thresholds:**
   - 🔬 ALPHA → 🧪 BETA: 3 usage sessions without bug
   - 🧪 BETA → 🚦 PRERELEASE: 5 usage sessions without bug (cumulative BETA)
   - 🚦 PRERELEASE → ✅ RELEASE: suggest to the maintainer
5. **Abandonment:** if a feature has not been used in 5+ sessions → suggest abandonment
   - If counter 0 and sessions ≥ 3 without usage or modification → suggest abandonment
6. Update `00_INDEX.md` + clean up `.used_*` flags
7. Notify: *"Alpha pipeline: [X] promoted, [Y] suggested for abandonment."*

> Each feature sets its own flag when it executes: `touch _SYSTEM/alpha/.used_[name]`
> Closure reads the flags, increments, then deletes them. Automatic, no questions.

---

## 8. Closure counter

```bash
bash _SYSTEM/kernel/closure.sh
```

> Increments `.closure_count`. Every 10 closures, sets `.dream_requested` for the next startup.

Every 10 closures, `.dream_requested` is set → the AI launches a consolidation dream at next startup.

---

## 9. Snapshot

```bash
git add [modified _SYSTEM/ files]
git diff --cached --quiet || git commit -m "session close YYYY-MM-DD" --quiet
```

> `.claude/` and `01_🧠Profil/` are gitignored — do not include them.
> If no git → silent skip.
