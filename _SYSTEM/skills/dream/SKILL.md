---
name: dream
description: Observation consolidation + long-term pattern detection. Triggered automatically every 10 closures.
trigger: auto (dream_requested flag) | manual ("dream", "consolidate observations", "clean memory")
---

# Dream — Consolidation & pattern detection

> The dream has two objectives: (1) compact observations, (2) detect patterns
> that only emerge after multiple sessions.

---

## Triggers

| Mode | Condition |
|------|-----------|
| **Automatic (closure)** | Every 10 closures, via `_SYSTEM/kernel/closure.sh` → `.dream_requested` |
| **Manual** | User says "dream", "consolidate", "clean memory" |

---

## Procedure

> 🚩 At dream start: `touch _SYSTEM/alpha/.used_dream`

### Phase 1 — Read existing

1. Read `01_Profil/memory/observations.md` — hypothesis tree 🌳 + raw observations
2. Read `01_Profil/profil.md` — section 🧬 Traits, current scores
3. Read `01_Profil/memory/modes.md` — mode history

### Phase 1b — Update hypothesis tree

The tree (`## 🌳 Hypothesis tree`) is the consolidated structure. After reading raw observations:

1. **New branches**: an observation appearing 2+ sessions → create H[N] with status `🔬 testing`
2. **Branches to promote**: `🔬 testing` + new confirming signal → move to `✅ confirmed` + add insight
3. **Branches to disprove**: contradicted by evidence → move to `❌ disproved` (keep branch, add reason)
4. **Branches to merge**: two H pointing to the same conclusion → merge keeping sub-branches
5. **Dormant branches**: `✅ confirmed` but not observed in 5+ sessions → propose `💤 dormant` (don't apply alone)

Branch format:
```
### H[ID]: [Title] · [status]
- **B[ID].[N]** · [description] → [result] ([proof])
- **→ Insight**: [actionable lesson for the AI]
```

### Phase 2 — Weak signals & long-term patterns

Search across ALL observations (not just recent):

**A. Missed traits** — behavior appearing in 3+ sessions but never noted as a trait

**B. Reasoning patterns (meta-analysis)** — repeated question structure, same reaction to error, dominant abstraction level

**C. Trait confirmation / disproval** — trait not observed in N sessions → notify

**D. Weak signal convergence** — two separate observations pointing to the same conclusion

### Phase 3 — Consolidation (compact)

1. Group redundant observations (same idea, different phrasing)
2. Remove strict duplicates (word for word)
3. Compact phrasing: one line per observation, max 200 characters
4. Convert relative dates to absolute dates
5. Lossless: result must contain AT LEAST as much information as the original

### Phase 4 — Update & notification

1. Mark dream date in `01_Profil/memory/observations.md`:
   ```
   > Last dream: YYYY-MM-DD
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
| **Never decide alone** | Pattern detected? Report it, don't apply it. Unless confirmed 3×. |
| **Lossless** | Dream never removes unique information. Fewer words, not less meaning. |
| **Absolute dates** | Always convert relative dates. "Last week" is unreadable in 3 months. |
| **No creative rephrasing** | No "so the user tends to be X". Lexical compaction only. |
