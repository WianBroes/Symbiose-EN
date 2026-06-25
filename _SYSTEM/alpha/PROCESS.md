# ⚙️ Alpha Pipeline — Process

**Context:** any modification of the Symbiose metasystem (rules, extensions, scripts, vault structure, new tools) goes through this lifecycle. This avoids:
- Features that die after one session
- Silent bugs that contaminate the system
- Undocumented decisions

---

## Lifecycle

```
💡 IDEA → 🔬 ALPHA → 🧪 BETA → 🚦 PRERELEASE → ✅ RELEASE → 🏁 ARCHIVE
                                  ↓                        ↓
                               ❌ ABANDONED             🔄 REPLACED

🔧 QUICK FIX → implemented directly (no cycle)
```

**QUICK FIX:** isolated change, <30 lines, no dependency on other features. Does not go through the ALPHA→RELEASE cycle. Noted in `00_INDEX.md` section "Quick fixes" for traceability.

| Stage | Entry criteria | Risk | Action at closure |
|-------|----------------|------|-------------------|
| **💡 IDEA** | User says "we should" | None | Nothing — stays in list |
| **🔬 ALPHA** | Code/script/extension exists and runs | Probable bugs | Check: bugs encountered? If yes, fix or ❌ ABANDON |
| **🧪 BETA** | 3 sessions without bug in ALPHA | Rare bugs | Check: 3 sessions without bug → promote |
| **🚦 PRERELEASE** | 5 sessions without bug in BETA | Stable | Check: 5 sessions without bug → promote |
| **✅ RELEASE** | Adopted as standard | None (normal tech debt) | Document in CORE.md if relevant |
| **❌ ABANDONED** | Blocked, too risky, obsolete | — | Move to archive |
| **🔄 REPLACED** | Replaced by better solution | — | Archive old, reference new |

---

## Rules

### Entry into pipeline

1. User says "add to alpha" → create entry in `00_INDEX.md` with `💡 IDEA`
2. Describe the feature in one line — enough to know what it is in 3 months

### Promotion

1. At each **session closure**, `00_INDEX.md` is reviewed
2. AI examines each ALPHA/BETA/PRERELEASE feature: bugs encountered this session?
3. If no bug entry since last promotion: count +1 session
4. At threshold: propose promotion to user → "Promote X to Y?"
5. User decides. No promotion without explicit validation.

### Abandonment

1. A feature can be abandoned at any time
2. Move to ❌ ABANDONED in `00_INDEX.md`
3. If code exists: move to archive with reference

### Entry content

```
| [name] | [current stage] | [stage entry date] | [sessions without bug] |
```
