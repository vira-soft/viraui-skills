**When to read:** Deciding whether to animate, skip, or honor `prefers-reduced-motion` on composed screen.

# Principles

Motion supports task. Same tokens for `@viraui/react` **and** custom consumer CSS. Load from **viraui-design** compose — hub + **one** motion ref, not whole folder.

## Checklist

Before any animation:

| Check | Fail = skip or simplify |
| ---------- | ----------------------------------------------- |
| Frequency | 100+/day or keyboard-initiated? → **no motion** |
| Purpose | Necessary, or decoration? |
| Value | Helps orientation, feedback, or continuity? |
| Efficiency | Stalls task or hurts performance? |

Frequency gate:

| Frequency | Decision |
| ------------------------------------- | ----------------------------------------------- |
| 100+/day (shortcuts, command palette) | No enter/exit motion |
| Tens/day (hover, list nav) | Near-imperceptible tokens or nothing |
| Occasional (modals, sheets, toasts) | Standard functional tokens |
| Rare / first-time | Delight budget — [animations.md](animations.md) |

Then:

1. Functional hover/press/focus/expand/overlay → animate with tokens unless reduced-motion.
2. Pair motion with text, chip, focus, or `aria-*` — never meaning by motion alone (see **viraui-design** [accessibility.md](../viraui-design/accessibility.md)).
3. Every authored animation includes reduced-motion path (or relies on preflight kill — see below).
4. Building end-to-end → [build.md](build.md). Subtracting excess → [remove.md](remove.md).

## Defaults

| Situation | Default |
| --------------------------------- | ---------------------------------------------------------------------------------- |
| Hover, press, expand, overlay | Functional tokens (`--duration-fast` / instant) |
| Toast / celebration | Evocative — [animations.md](animations.md) |
| Error, destructive, dense data | Functional only — no elastic/wiggle |
| Keyboard / 100+/day chrome | Instant state — no enter/exit animation |
| Custom sidebar / card / table CSS | Same contract as Vira components |
| Duration / easing | `--duration-*` / `--easing-*` only — [speed.md](speed.md) / [timing.md](timing.md) |

## Reduced motion

Preflight kills motion globally on `*` with `animation: none !important` and `transition: none !important` so it beats later layers. Component CSS needs extra reduced-motion rules only when behavior must change beyond killing motion (instant final opacity/transform, hide decorative effects).

```css
/* Preflight already kills transition/animation — add only when final state must change */
@media (prefers-reduced-motion: reduce) {
  .overlay[data-starting-style],
  .overlay[data-ending-style] {
    opacity: 1;
    transform: none;
  }
}
```

JS motion (count-up, typewriter): `matchMedia('(prefers-reduced-motion: reduce)')` → jump to final state.

Vestibular-safe: pointer-drag 1:1 (`transition-duration: 0s` while dragging) — detail in [gestures.md](gestures.md); no exaggerated z-depth; prefer fade over slide when unsure; no autoplay without controls; no blink/flash; no multi-axis chaos.

## Gotchas

- **Tokens only** — no raw `ms`, `ease`, Framer/GSAP for standard UI feedback.
- **`prefers-reduced-motion` is non-negotiable** — preflight covers kill; still handle JS and final-state overrides. Do **not** keep “gentler” bounce under reduce.
- **Do not skip custom CSS** — “Vira already animates” ≠ exemption for consumer chrome.
- **Do not load whole motion folder** — hub router → one sibling ref.
- Instant show/hide is still motion choice; expand/collapse gets functional tokens unless reduced-motion or frequency gate fails.
- Elastic/wiggle = brand personality on press/toast — not errors or data tables.

## Validation

Stop if:

- Hardcoded `200ms` / `ease-in-out` / invented `--spring`
- Custom CSS left unanimated “for later” while Vira parts move
- Motion is only “saved” / “new” signal
- Keyboard / 100+/day chrome still has enter/exit motion
- All motion refs loaded “to be safe”
