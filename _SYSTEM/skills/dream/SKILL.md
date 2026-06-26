---
name: dream
description: Observation consolidation + long-term pattern detection. Triggered automatically every 10 closures.
trigger: auto (dream_requested flag) | manual ("do a dream", "consolidate observations", "clean memory")
---

# Dream — Consolidation & pattern detection

> Inspired by OpenAI Dreaming V3, Claude Code AutoDream, and RecMem.
> The dream has two goals: (1) compact observations, (2) detect patterns
> that only emerge after multiple sessions.

---

## Triggers

| Mode | Condition |
|------|-----------|
| **Automatic (closure)** | Every 10 closures, via `_SYSTEM/kernel/closure.sh` → `.dream_requested` |
| **Manual** | User says "do a dream", "consolidate", "clean memory" |

---

## Procedure

### Phase 1 — Read existing data

> 🚩 `touch _SYSTEM/alpha/.used_dream` — signals usage to the alpha pipeline

1. Read `01_🧠Profil/memory/observations.md` — hypothesis tree 🌳 + raw observations
2. Read `01_🧠Profil/👤profil.md` — section 🧬 Traits, current scores
3. Read `01_🧠Profil/memory/modes.md` — mode history
4. Read `01_🧠Profil/👤profil.md` — section 🔭 En émergence (accumulated thinking mode signals)
5. Read `01_🧠Profil/👤profil.md` — section ⚡ Synergies (candidate synergies + sessions)

### Phase 1b — Update the hypothesis tree

The tree (`## 🌳 Arbre d'hypothèses`) is the consolidated structure. After reading raw observations:

1. **New branches**: an observation appearing in 2+ sessions → create H[N] with status `🔬 en test`
2. **Branches to promote**: `🔬 en test` + new confirming signal → move to `✅ confirmé` + add insight
3. **Branches to invalidate**: contradicted by evidence → move to `❌ infirmé` (keep the branch, add reason)
4. **Branches to merge**: two H pointing to the same conclusion → merge keeping sub-branches
5. **Dormant branches**: `✅ confirmé` but not observed in 5+ sessions → suggest `💤 dormant` (do not apply alone)

Branch format:
```
### H[ID]: [Title] · [status]
- **B[ID].[N]** · [description] → [result] ([proof])
- **→ Insight**: [actionable lesson for the AI]
```

### Phase 2 — Weak signals & long-term patterns

Search through ALL observations (not just recent ones):

**A. Missed traits**
- A behavior appearing in 3+ sessions but never noted as a trait
- Ex: if the user says "let's do X" in session 1, "we need to do X" in session 3, "X is important" in session 5 → `planificateur` trait undetected
- Action: create the trait in `👤profil.md` (🧬 Traits) with initial score 0.3 + notify

**B. Reasoning patterns (meta-analysis)**
- Same question structure repeated (ex: always "what if..." before implementing)
- Same reaction to errors (ex: always "that's not it" instead of "fix X")
- Same dominant abstraction level (always practical, rarely systemic)
- Action: add a pattern observation + adjust trait comment if relevant

**C. Trait confirmation / invalidation**
- A trait not observed in N sessions → notify
- Do not decide alone — notify: *"X has not been observed in 3 sessions. Keep the score as is?"*

**D. Convergence of weak signals**
- Two separate observations pointing to the same conclusion
- Ex: "prefers mechanical solutions" + "doesn't trust AI memory" → same `mécanicien` trait
- Action: merge observations, adjust trait accordingly

**E. Thinking modes — promotion from 🔭**
- Scan `🔭 En émergence`: any signal with Sessions ≥ 3 → suggest promotion to `🧠 Modes de pensée`
- Scan `🔭 En émergence`: signal present since previous dream without progress → note as persistent weak signal (do not delete)
- Never promote alone — suggest to user with proof (sessions, observations)

**F. Synergies — long-term validation**
- Scan `⚡ Synergies`: for each candidate synergie, search observations across all sessions for confirmation or contradiction
- Sessions ≥ 3 confirmed → mark as **active** synergy in `⚡`
- Contradicted by new elements → mark `❌ infirmé` + reason (do not delete — trace remains)
- Look for new emerging synergies not detected at closure: combinations of `🧬 Traits` + `🔭 En émergence` + `🎯 Skills` + `🧠 Modes de pensée` pointing coherently across multiple sessions

### Phase 3 — Consolidation (compact)

1. Group redundant observations (same idea, different formulations)
2. Remove strict duplicates (word for word)
3. Compact formulations: one line per observation, max 200 characters
4. Convert relative dates to absolute dates (ex: "last week" → "2026-06-11")
5. Lossless: the result must contain AT LEAST as much information as the original

### Phase 4 — Update & notification

1. Mark the dream date in `01_🧠Profil/memory/observations.md`:
   ```
   > Dernier dream : 2026-06-18
   ```
2. If traits updated → notify
3. If pattern detected → notify
4. If trait significantly modified → ask for confirmation

### Phase 5 — Cleanup

```bash
rm -f _SYSTEM/kernel/.dream_requested
echo 0 > _SYSTEM/kernel/.closure_count
```

---

## Rules

| Rule | Description |
|------|-------------|
| **Never decide alone** | Pattern detected? Report it, don't apply it. Unless the pattern is confirmed 3×. |
| **Lossless** | The dream never deletes unique information. Fewer words, not less meaning. |
| **Absolute dates** | Always convert relative dates. "Last week" → unreadable in 3 months. |
| **No creative reformulation** | No "so the user is rather X". Lexical compaction only. |
| **No more than one minute** | If it's long, you're overthinking. Cut fast, keep broad. |

---

## Long-term lifecycle

```
Session 1      raw observations
Session 2      raw observations
Session 3      raw observations
    ↓ (10 closures)
Dream #1       compact + patterns
    ↓
Session 11-20  new raw observations
    ↓ (10 closures)
Dream #2       compact + patterns + verification of dream #1 patterns
    ↓
... etc
```
