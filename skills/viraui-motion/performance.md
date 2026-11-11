**When to read:** Jank, dropped frames, choppy shadow/blur, laggy drag, or choosing properties for cost.

# Performance

Question is “does each frame finish in time?” — not easing taste ([timing.md](timing.md)) or whether to animate ([principles.md](principles.md)). Prefer CSS / WAAPI for predetermined motion; JS only when interruptible / gesture-driven. Engine ladders for scroll/stagger: **viraui-design** [styling.md](../viraui-design/styling.md).

## Checklist

1. Name the cause before changing code — never “added `will-change`, seems smoother”.
2. Default animate **`transform` + `opacity`**. Other properties need a reason.
3. Never `transition: all` — list exact properties.
4. Do not conclude “fine” from a fast laptop — mid-range phone / 120Hz is the bar.
5. Tokens still apply — [speed.md](speed.md) / [timing.md](timing.md); raw ms is not a perf fix.

## Symptom → cause

| Problem                             | First fix                                                                           |
| ----------------------------------- | ----------------------------------------------------------------------------------- |
| Stutters while moving               | Prefer `translate` / `scale` / `opacity` over `width` / `height` / `top` / `margin` |
| Choppy shadow                       | Prefer `filter: drop-shadow()` over animating `box-shadow`                          |
| Jank only under load / navigation   | Move predetermined motion to CSS or WAAPI (off main-thread when possible)           |
| React hand-rolled loop drops frames | Write `ref.current.style`, not React state per frame                                |
| Drag slower as list grows           | Stop driving child transforms via inheritable CSS vars on a parent                  |
| Blur lag (esp. Safari)              | Keep animated `blur()` small; prefer fade                                           |
| Extra properties animate            | Replace `transition: all`                                                           |
| 1px jump when motion starts/ends    | `will-change: transform` **last**, only after you see the jump                      |

## Property tiers

| Tier      | Examples                                                          | Cost               |
| --------- | ----------------------------------------------------------------- | ------------------ |
| Composite | `transform`, `opacity` (and some `filter` / `clip-path` — verify) | Cheapest           |
| Paint     | `box-shadow`, `border-radius`, `color`                            | Redraw each frame  |
| Layout    | `width`, `height`, `padding`, `margin`, `top`, `left`             | Relayout neighbors |

Swap down: grow with `scale()`, move with `translate()`, show/hide with `opacity`. Accordion height is a documented exception when no transform equivalent — still prefer modern size animation paths in **viraui-design** [styling.md](../viraui-design/styling.md).

## Frame budget

~16.7ms at 60Hz; ~8ms at 120Hz. Layout thrash on complex pages can eat dozens of frames — pick composite properties first.

## `will-change`

Last resort after property choice and main-thread diagnosis. Promote only the animating element; remove when idle if the layer is long-lived and costly.

## Gotchas

- Framer / GSAP / Motion version drama as first answer → wrong; CSS/WAAPI + tokens first.
- Inherited CSS custom props driving many children’s transforms → list lag.
- `will-change` sprayed on every card → memory / layer tax.
- Do not load the whole motion folder.

## Validation

- Cause named; property tier justified
- No `transition: all`
- Gesture track still writes transform on the element ([gestures.md](gestures.md))
- Reduced-motion path unchanged ([principles.md](principles.md))
