**When to read:** Naming a motion effect from a vague description (“what’s it called when…”). Not for building — then [build.md](build.md).

# Vocabulary

Return the best glossary term first; 1–2 alternates if close. Keep answers short. After naming, point builders to the matching motion router row (tokens still [speed.md](speed.md) / [timing.md](timing.md)).

## Entrances & exits

- **Fade in / Fade out** — Opacity appear or disappear.
- **Slide in** — Enter by sliding from an edge.
- **Scale in** — Grow from smaller to full size, often with fade.
- **Pop in** — Appear with slight overshoot.
- **Reveal** — Uncover via clip-path or mask.
- **Enter / Exit** — Motion when added to or removed from the tree.

## Sequencing

- **Stagger** — Cascade with small delays between items → [choreography.md](choreography.md).
- **Orchestration** — Coordinated multi-element timing.
- **Delay / Duration / Fill mode / Keyframes / Interpolation** — Timing primitives; Vira durations are `--duration-*`.
- **Stepped animation** — Discrete steps (e.g. countdown).

## Transforms

- **Translate / Scale / Rotate / Skew** — Transform axes.
- **3D tilt / Flip / Perspective** — Depth; keep vestibular-safe ([principles.md](principles.md)).
- **Transform origin** — Anchor for scale/rotate.
- **Origin-aware animation** — Grows from trigger (popover/menu), not center.

## State & navigation

- **Crossfade** — Out + in in the same spot.
- **Morph** — One shape becomes another.
- **Shared element transition** — Element travels and transforms across states.
- **Layout animation** — Size/position change animates instead of snapping.
- **Accordion / Collapse** — Height expand/collapse.
- **Direction-aware transition** — Forward vs back slide direction.

## Scroll

- **Scroll reveal / Scroll-driven animation / Parallax / Page transition / View transition** — Prefer CSS timelines first (**viraui-design** [styling.md](../viraui-design/styling.md)).

## Feedback

- **Hover effect / Press feedback / Hold to confirm / Drag / Drag to reorder / Swipe to dismiss / Rubber-banding** → [gestures.md](gestures.md) when pointer-driven.
- **Shake / Wiggle** — Error jitter; Vira: `--easing-wiggle` only when appropriate ([animations.md](animations.md)).
- **Ripple** — Expanding tap confirmation (rare in Vira product UI).

## Easing language → tokens

| Spoken                 | Prefer                                      |
| ---------------------- | ------------------------------------------- |
| Ease-out entrance/exit | `--easing-entrance` / `--easing-exit`       |
| On-screen move         | `--easing-standard`                         |
| Elastic / overshoot    | `--easing-elastic` (evocative / press only) |
| Wiggle                 | `--easing-wiggle`                           |
| Linear                 | Constant motion only (spinners, hold fill)  |

Do not invent parallel `--ease-*` forks. Authority: [timing.md](timing.md).

## Spring language

Springs are physics metaphors. On ViraUI screens prefer token CSS/WAAPI; gesture release may need velocity-aware settle ([gestures.md](gestures.md)) without mandating a spring library.

## Performance words

**Jank / Dropped frame / Compositing / will-change / Layout thrashing** → [performance.md](performance.md).

## Principles words

**Purposeful animation / Frequency of use / Spatial consistency / Reduced motion** → [principles.md](principles.md). Reduced motion on Vira = kill transitions/animations (preflight + authored), not “gentler bounce”.

## Gotchas

- Naming ≠ implementing; after the term, stop unless asked to build.
- Do not load the whole motion folder.

## Validation

- Glossary term first; tokens cited if user asks how to build next
