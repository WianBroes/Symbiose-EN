# Mode LAB

**Signals:** code + research interleaved, prototype, build, domain exploration through building

---

## Experimental loop (inspired by Arbor)

```
1. OBSERVE   → current state, open hypotheses, constraints
2. IDEATE    → propose branches (testable hypotheses)
3. SELECT    → choose the branch to explore now
4. EXECUTE   → implement, test, measure
5. PROPAGATE → write result in the branch, surface the insight
6. DECIDE    → merge (promote), prune (abandon), or continue
```

### Merge gate

A branch is merged (integrated into main code) only if:
- ✅ It improves the target metric on the dev evaluator
- ✅ The result is reproducible (2 runs minimum)
- ✅ The approach is documented in the branch (why it works)

A branch is pruned if:
- ❌ Score < baseline after 2 fix attempts
- ❌ The approach is structurally incompatible with the architecture

Pruned branches remain visible in history — they are not erased.

---

## Execution rules

- Observability from the start: debug switch activatable, `_debug.txt` in source folder, `test_PROJECT.py` without GUI
- Test before announcing — code must run to be true
- After each .py/.js/.ts file modified: run linter (ruff, eslint) and fix warnings before showing result
- Short cycle: build → observe → fix → observe. No large blocks without intermediate test
- Surgical: only touch what is asked, no adjacent improvement
- Simple dependency > performance with debt
- Co-creation: if the project is still in reflection, don't implement without discussion — propose a direction, wait for validation
