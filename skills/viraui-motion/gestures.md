**When to read:** Drag, swipe, fling, hold-to-confirm, sheet/drawer feel, mobile/PWA touch, or “doesn’t follow my finger”.

# Gestures

Direct manipulation: while pointer is down, UI **is** finger; on lift, settle with tokens. Prefer shipped `@viraui/react` overlays (`Dialog.Sheet`, Popover/Menu sheets — see **viraui-design** composition + specs) over hand-rolled drawers. Do **not** default to Vaul / Framer Motion.

Duration / easing for non-track settle: [speed.md](speed.md) / [timing.md](timing.md). Whether to animate at all: [principles.md](principles.md).

## Checklist

| Phase | Rule |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Track (pointer down) | Position 1:1 — no easing, no duration, no spring. `transition-duration: 0s` (or swipe-strength at `0`) while dragging |
| Release (pointer up) | Settle with `--duration-*` + `--easing-*` (or WAAPI from foundation nested). Exit shorter than enter |
| Dismiss | Distance **or** velocity — flick over short travel still dismisses |
| Linked values | Overlay opacity / backdrop scale derive from drag progress — one source of truth |
| Interrupt | User can catch mid-close and drag back — prefer transitions / retargetable motion over `@keyframes` on gesture surfaces |
| Spatial | Dismiss along same axis surface entered |

## Defaults

| Situation | Default |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| Product sheet / drawer | Compose Vira overlay parts; open specs before inventing drag chrome |
| Small floating panel | Shorter travel tokens (`--duration-fast` / `--duration-instant`) than full-bleed edge sheet (`--duration-normal`) |
| Hold-to-confirm | Linear fill while held (time is honest); cancel snaps with `--easing-exit` + short duration |
| Rubber-band past edge | Resistance, not hard stop — keep subtle |
| Bounce on release | Only after drag applied force; button-close → no bounce / no elastic |
| Snap-back under threshold | Fast — [speed.md](speed.md) exit bias |

```css
.sheet[data-dragging] {
  transition-duration: 0s;
}

.sheet:not([data-dragging]) {
  transition:
    transform var(--duration-normal) var(--easing-entrance),
    opacity var(--duration-fast) var(--easing-entrance);
}

.sheet[data-ending-style] {
  transition-duration: var(--duration-instant);
  transition-timing-function: var(--easing-exit);
}
```

Write `transform` on dragged element. Do **not** drive child motion from inheritable CSS var on parent (recalc tax on long lists).

## Mobile / PWA

- Test on **real device** (LAN IP) — trackpad and 60Hz desktop hide roughness.
- Hit targets ≥ **44×44** CSS px (invisible hitbox ok).
- Set `touch-action` so browser does not steal drag axis.
- Gate hover chrome: `@media (hover: hover) and (pointer: fine)`.
- Prefer `transform` / `opacity` only — [performance.md](performance.md).

## Reduced motion

Preflight / authored rules still kill decorative transitions ([principles.md](principles.md)). **Tracking stays** (user produces motion). On release under `prefers-reduced-motion: reduce`, jump or short settle to final position — no bounce / elastic / fling spectacle.

## Gotchas

- Vaul / Motion drag APIs as required stack → wrong; Vira sheets + specs first.
- Spring or transition during track → syrup lag.
- React state per `pointermove` → jank; write styles / motion values off render path.
- Keyframes on interruptible gesture surfaces → jumps when retargeted.
- Do not load whole motion folder — this file + tokens refs only if picking settle curves next.

## Validation

- Track is 1:1; release uses tokens
- Overlay linkage follows drag progress
- Mobile checklist considered for PWA / touch
- Reduced-motion: track ok; decorative settle killed or instant
