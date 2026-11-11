**When to read:** Review diff / PR that adds or changes motion.

# Review

Diff review, not full codebase audit ([improve.md](improve.md)). Standards cite sibling refs — do not paste duplicate cubic-bezier / ms tables.

## Standards (pass/fail)

1. **Frequency** — Keyboard / 100+/day motion → fail ([principles.md](principles.md)).
2. **Purpose** — Named functional/evocative role ([animations.md](animations.md)).
3. **Tokens** — `--duration-*` / `--easing-*` only ([speed.md](speed.md) / [timing.md](timing.md)).
4. **Reduced motion** — Kill path present; not “gentler bounce” ([principles.md](principles.md)).
5. **Properties** — Prefer transform/opacity; no `transition: all` ([performance.md](performance.md)).
6. **Physicality** — No `scale(0)`; trigger-origin for anchored overlays.
7. **Interruptibility** — No keyframes on rapid/reversible or gesture surfaces ([gestures.md](gestures.md)).
8. **Choreography** — No dual entrance; no high-frequency stagger ([choreography.md](choreography.md)).
9. **Hover gate** — Fine-pointer media for hover-only effects.
10. **Whole interface** — Custom CSS in diff obeys same contract as Vira parts.

## Escalation

| Finding | Action |
| --------------------------------------------- | ---------------------------------------- |
| Missing reduced-motion / raw ms on shipped UI | **Block** |
| `transition: all` / layout thrash on hot path | **Block** |
| Evocative on dense/error UI | **Block** or require functional retarget |
| Missing hover gate / weak origin | **Should fix** |
| Naming / comment clarity | **Nice** |

Remedial order: delete unjustified motion → token swap → property/engine fix → choreography cut.

## Output

```
| Result | File | Standard # | Note |
| ------ | ---- | ---------- | ---- |
```

End with **Block** or **Approve** (Approve only if zero Blocks). Optional Before|After for worst offender.

## Gotchas

- Approving Framer/Vaul defaults on Vira screens → fail; require tokens + design-spec overlays.
- Loading every motion ref to review one hover → fail; hub + this ref (+ one cited sibling).
- Do not re-audit unrelated files (→ [improve.md](improve.md)).

## Validation

- Every Block cites standard number
- Token guidance → speed/timing, not invented curves
