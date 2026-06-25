# Analyse — Adaptive scan protocol

> Defines the two analysis levels: micro (periodic) and macro (closure).
> Analysis is done by the AI in the conversation — no external LLM.

---

## 1. Micro-scan — periodic (every N messages)

**Call chain:**
1. The `.pi/extensions/symbiose-kernel.ts` extension listens to the `input` event
2. It calls `bash _SYSTEM/kernel/kernel.sh` before the AI responds
3. kernel.sh increments `.msg_count`
4. The extension reads `.msg_count`, if `count % interval == 0` → injects a `symbiose-scan` message
5. **At the start of each response**, the AI looks for a `customType === "symbiose-scan"` message
6. If found → execute the micro-scan (procedure below)

> **Rule:** The AI does not look for a file — it looks for a message in its context.

**Trigger:** `symbiose-scan` message (or `[scan]` in hook output) present in context

**Procedure:**
1. Look for `[scan]` in messages. If found → run the scan. Otherwise → do nothing.
2. Re-read the last ~5 exchanges (in session memory)
3. Look for trait and skill signals (see tables below)
4. Write detections directly to files
5. **If level-up detected → apply immediately + notify:**
   - Ex: 🐍 Python goes Apprentice → Adept → jargon OK from next response

### Trait signals (behavior)

| Look for this | Example | Trait |
|---------------|---------|-------|
| Spontaneous decision | "yeah go for it", "ok direct" | `direct +1` |
| Hesitation / reversal | "actually no", "wait..." | `precise +1` |
| Positive reaction | "nice", "perfect" | satisfaction |
| Negative reaction | "too long", "not clear" | dissatisfaction → adjust |
| Code request | "give me the code", "do this" | `technical +1` |
| Explanation request | "explain the concept" | `pedagogical +1` |
| Recurring phrasing | "basically", "simply" | language register |
| Exploration | "could we also...?" | `explorer +1` |
| Redirection | "no that's not it" | `directive +1` |

### Skill signals (competency)

| Look for this | Example | Action |
|---------------|---------|--------|
| Technical jargon | "k8s cluster", "Promise.all" | Skill domain +1 XP |
| Precise instruction | "make a docker compose with 3 services" | Skill domain +1 XP |
| Exploratory question | "how does a vector store work?" | Emerging skill +1 XP |
| Corrects the AI | "no that's not how it works" | Skill +1 XP bonus |
| Cites a tool/framework | "I use Astro", "on NixOS" | Skill tool +1 XP |
| Two-domain combo | "my Rust API in a container" | Rust + Docker combo |

### Skill increment rules
- Max **+2 XP** per skill per micro-scan
- AI correction: **+1 XP additional** (even if already at +2)
- New skill: create entry, XP=1, choose a representative emoji icon

### Feedback in response

If something was detected → one line at the start of the response:
```
📊 direct +1 · technical +1
⚔️ 🐍 Python +1 XP
🎉 🐍 Python → Adept! (Lv.3) ← applied immediately
```

If nothing → no feedback.

---

## 2. Macro-scan — session closure

**Trigger:** "close", "we're done"

**Procedure:**
1. **Re-read the entire session** — not just the end, not the micro-scans
2. Look for **global patterns** no micro-scan captures:
   - Behavioral evolution during the session
   - Mode alternation (e.g. fast execution → reflection)
   - Non-obvious dominant topics
   - Actual autonomy level (how often did validation need to happen?)
3. Consolidate with micro-scans already written to files
4. Update scores

### 2a. Traits — simple accumulation

Each trait has a score = total cumulated signals / number of active sessions.

**Session signal (for each detected trait):**

| Intensity | When |
|-----------|------|
| **+2** | Strong signal, repeated, explicit |
| **+1** | Signal present but moderate |
| **0** | Neutral |
| **-1** | Weak inverse signal |
| **-2** | Strong inverse signal |

**Accumulation:**
```
Score = total_signals / nb_sessions
```

### 2b. Skills — cumulative XP

Skills **do not decrease** between sessions.

**Levels:**

| Level | Title | XP required |
|-------|-------|-------------|
| ⭐ | Novice | 1 |
| ⭐⭐ | Apprentice | 3 |
| ⭐⭐⭐ | Adept | 6 |
| ⭐⭐⭐⭐ | Expert | 10 |
| ⭐⭐⭐⭐⭐ | Master | 15 |
| 👑 | Grandmaster | 21 |

```
level = floor((sqrt(1 + 8 × XP) - 1) / 2)
```

### 2c. Active rules

Rules are generated from traits + skills and **applied immediately** (micro-scan) or at next session startup (macro-scan).

### 2d. Meta-analysis — reasoning patterns

> Separate step from traits and skills. Looks at HOW the user thinks, not WHAT they do.

Look for across the entire session:
1. **Question structure** — "what if" before implementing? Corrective questions after? Root cause or symptom?
2. **Relationship to error** — lets it slide or insists? Turns incidents into system improvements?
3. **Abstraction level** — systemic / practical / alternates?
4. **Decision style** — validates quickly? Needs to compare options?
5. **Meta-position** — observes themselves and communicates their patterns?

**If a pattern confirms across ≥2 sessions** → propose a new trait or adjust an existing one.

### 2e. Closure summary

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔬 Symbiose Diagnostic
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📊 Traits:
  direct        +1.4 ↑   Short responses, direct
  technical     +1.4 ↑   Code, commands, jargon
  precise       +1.1 ↑   Verifies before proceeding

⚔️ Skills:
  🐍 Python         Lv.3 ⭐⭐⭐  +1 XP   Jargon OK

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📋 Active rules: 3 traits · 1 skill
Session: Kernel AI — short — 👍
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## 3. Applying rules in session

At each session startup (AUTOSTART.md section 3), I read `profil.md` (🧬 Traits + 🎯 Skills) and generate active rules.

**Startup procedure:**
1. Read `01_Profil/profil.md` — section 🧬 Traits, extract traits with score > |0.3|
2. Read `01_Profil/profil.md` — section 🎯 Skills, extract skills with level ≥ 2
3. Generate rules according to the mapping in CORE.md section 2b
4. **Apply them for the entire session**

## 4. On-demand scan

The user can request an analysis at any time:
- *"Analyse my traits"* — runs immediate macro-scan
- *"Check my skills"* — reads and displays current state
