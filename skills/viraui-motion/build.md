**When to read:** Building one interaction’s motion end-to-end (implement, not audit).

# Build

Ordered construction. Gate first — zero lines of motion can success. Tokens only: [speed.md](speed.md) / [timing.md](timing.md). Style pick: [animations.md](animations.md). Multi-element: [choreography.md](choreography.md). Gestures: [gestures.md](gestures.md).

## Sequence

### 1. Should it animate?

| Frequency | Decision |
| ---------------------------------------------- | -------------------------------------------------------------------------- |
| 100+/day (keyboard shortcuts, command palette) | **No motion.** Stop |
| Tens/day (hover, list nav) | Near-imperceptible — `--duration-instant` / `--duration-fast` — or nothing |
| Occasional (modals, sheets, toasts) | Standard functional tokens |
| Rare / first-time | Delight budget — evocative allowed per [animations.md](animations.md) |

Keyboard-initiated actions → no enter/exit motion. Fail gate → offer instant state / static affordance.

### 2. Purpose (name one)

Feedback · spatial consistency · state indication · prevent jarring change · explanation (marketing/onboarding) · delight (rare tier only).

Cannot name it → do not build. Dense data user reads/acts on → no decorative motion.

### 3. Tool ladder (cheapest first)

| Need | Tool |
| ----------------------------------------- | ----------------------------------------------------------------- |
| Hover / press / class or data-attr toggle | CSS `transition` + tokens |
| Enter on mount without JS state | `@starting-style` |
| Predetermined motion under load | CSS `animation` |
| Programmatic, no library | WAAPI + foundation nested durations |
| Scroll / stagger / size morph | **viraui-design** [styling.md](../viraui-design/styling.md) first |
| Overlay / sheet / toast / menu | Compose `@viraui/react` parts — do not hand-roll focus traps |

Do not install motion library for fade. Framer/GSAP only if CSS/WAAPI cannot express behavior **and** user accepts dependency.

### 4. Properties

- Prefer `transform` + `opacity` ([performance.md](performance.md)).
- Never start from `scale(0)` — use ~`0.9–0.97` + opacity `0`.
- Trigger-anchored popovers/menus: origin at trigger (part/docs); centered dialogs stay centered.
- Prefer `%` in `translate()` over magic px.
- Set `transform` on element — not via inheritable parent CSS vars.

### 5. Duration + easing

Map to [speed.md](speed.md) / [timing.md](timing.md). Exit shorter than enter. No raw `cubic-bezier` / ms tables.

### 6. Interrupt + exit

Rapid / reversible UI → transitions (retargetable), not keyframes. Gesture surfaces → [gestures.md](gestures.md). Always ship reduced-motion with animation ([principles.md](principles.md)).

### 7. Hover gate

`@media (hover: hover) and (pointer: fine)` for hover-only chrome.

## Recipe pointers (Vira)

| Surface | Start from |
| --------------------------- | ------------------------------------------------------------- |
| Overlay appear | [animations.md](animations.md) functional popup sample |
| Disclosure / tabs indicator | Same file — indicator sample |
| Dialog / Popover sheet | Specs + composition; travel `--duration-normal`, exit shorter |
| Toast / banner | Evocative tokens only when attention is intentional |
| Accordion height | design `styling.md` size paths; tokens on transition |

## Gotchas

- Approximating curves “because familiar” → defect; use theme tokens.
- Parallel token systems (`--ease-out` forks) → defect.
- Reduced-motion / hover gate as follow-up → ship together.
- Do not load whole motion folder.

## Validation

- Frequency + purpose recorded
- Tokens only; reduced-motion present
- Cheapest tool that works; Vira parts before custom overlay chrome
