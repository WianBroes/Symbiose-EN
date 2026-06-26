---
name: scan
description: Periodic micro-scan — collects trait signals, skills, and reasoning patterns from the last 5 exchanges.
trigger: "[scan]" detected in a system-reminder (UserPromptSubmit hook)
---

# Scan — Periodic micro-scan

> **EXECUTE BEFORE RESPONDING TO THE USER.**
> Do not skip. Do not defer. Do not merge with the response.

---

## Procedure

1. Re-read the **last 5 exchanges** in session memory
2. Look for signals in the 3 tables below
3. Write detections to `01_🧠Profil/👤profil.md`
4. Display feedback at the **start of the response** if a signal is detected

---

## Trait signals (behavior)

| Look for | Trait |
|----------|-------|
| Spontaneous decision ("yes", "ok direct") | `direct +1` |
| Hesitation / reversal ("actually no") | `precis +1` |
| Redirection ("no that's not it") | `directif +1` |
| Exploration ("could we also...?") | `explorateur +1` |
| Brings lived experience as proof | `observateur +1` |
| Reframes at a higher level of abstraction | `systémique +1` |
| Connects two domains spontaneously | `systémique +1` |
| Reaches a synthesis without being asked | `synthétiseur +1` |

## Skill signals (competence)

| Look for | Action |
|----------|--------|
| Technical jargon | Domain skill +1 XP |
| Precise instruction | Domain skill +1 XP |
| Corrects the AI | Skill +1 XP bonus |
| Cites a tool/framework | Tool skill +1 XP |

Rules: max +2 XP per skill per scan. New skill → XP=1, emoji.

## Discovery signals (reasoning pattern)

| Look for | Action |
|----------|--------|
| Concrete example → general rule | `🔭 inductive +1` |
| Common mechanism between two domains | `🔭 analogique +1` |
| Spontaneously structures in branches | `🔭 arborescente +1` |
| Knowledge from one domain → problem in another | `🔭 transversale +1` |
| Reformulates the problem before answering | `🔭 recadrage +1` |
| Looks for patterns / invariants | `🔭 pattern-matching +1` |
| Identifies the exception to the rule | `🔭 critique +1` |
| Abstract principle → concrete case | `🔭 déductive +1` |

Rules: increment Sessions in `🔭 En émergence`. New signal → create entry (Sessions: 1 + raw observation).

---

## Feedback (start of response)

```
📊 direct +1 · systémique +1
⚔️ symbiose +1 XP
🔭 analogique +1
```

If nothing detected → no feedback, no mention of the scan.
