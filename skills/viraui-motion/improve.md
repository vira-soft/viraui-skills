**When to read:** Audit existing motion in consumer app and prioritize fixes. Report in chat (optional user-asked markdown artifact). Do **not** invent `plans/` tree unless user asks.

# Improve

Read-only until user asks to apply fixes. Cite [principles.md](principles.md), [speed.md](speed.md), [timing.md](timing.md), [performance.md](performance.md), [gestures.md](gestures.md), [choreography.md](choreography.md) — do not restate full token tables here.

## Recon (Vira consumer)

- Theme loaded? `--duration-*` / `--easing-*` present?
- Motion in CSS modules / consumer CSS vs `@viraui/react` parts?
- Overlays via Dialog/Popover/Menu sheets or custom chrome?
- Framer / GSAP / WAAPI / rAF mixed in?

## Audit categories

| # | Category | Hunt | Target |
| --- | ------------------- | ---------------------------------------------------------- | ------------------------------------------------------------- |
| 1 | Purpose & frequency | Keyboard / 100+/day motion; decorative list hover | Delete or [remove.md](remove.md) gate |
| 2 | Duration & easing | Raw ms, `ease-in`, parallel `--ease-*` forks | [speed.md](speed.md) / [timing.md](timing.md) |
| 3 | Physicality | `scale(0)`; wrong transform-origin on trigger popups | Scale ≥ ~0.9; origin at trigger; dialogs centered |
| 4 | Interruptibility | `@keyframes` on toasts/toggles/drags | Transitions / retargetable motion; [gestures.md](gestures.md) |
| 5 | Performance | `transition: all`; layout props; parent CSS-var transforms | [performance.md](performance.md) |
| 6 | Choreography | Parent enter + child stagger; metronome delays | [choreography.md](choreography.md) |
| 7 | Reduced motion | Missing kill / JS ignores `matchMedia` | [principles.md](principles.md) — `none`, not gentler |
| 8 | Hover / touch | Hover without fine-pointer gate; tiny hit targets | Gate + 44×44 on gesture controls |

## Output

Prioritized findings (severity: Block / Should / Nice):

```
| Sev | Where | Issue | Fix pointer |
| --- | ----- | ----- | ----------- |
```

Self-contained enough that another agent can patch without re-auditing. When applying fixes → **viraui-design** for compose/CSS rewrite, then re-check motion tokens.

## Gotchas

- Replacing broken motion with second token system → defect.
- “Upgrade to Motion 14” as default fix → CSS/WAAPI + Vira first.
- Do not load whole motion folder — this ref + one cited sibling if needed.

## Validation

- Findings cite concrete files/selectors
- Every fix points at Vira token or sibling ref
- No forced plans directory
