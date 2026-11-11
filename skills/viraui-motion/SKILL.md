---
name: viraui-motion
description: >-
  Use when adding, skipping, auditing, reviewing, or removing transitions,
  hover or press feedback, overlay enter/exit, micro-interactions, drag/swipe
  or mobile PWA gesture feel, stagger/choreography, jank or animation
  performance, --duration-* / --easing-* tokens, or prefers-reduced-motion on a
  ViraUI screen — including custom consumer CSS, not only @viraui/react
  components. Use when naming a motion effect or hunting where motion should or
  should not exist. Use even if the user never names this skill or
  viraui-design.
license: MIT
metadata:
  author: Vira Software
  version: '2026.11.11'
---

# viraui-motion

Motion is **product, not polish**. Same tokens for `@viraui/react` **and** custom consumer CSS. Portable across Agent Skills hosts (Cursor, Claude Code, Codex, Gemini, …).

Load this hub when motion symptoms match (see description). Read **one** sibling ref from the router — not the whole folder.

This skill does **not** replace **viraui-design** for component choice or API. Compose/API → design; motion tokens/principles → here. **viraui-design** also routes here when composing screens with transitions.

## When to load

- Hover, press, focus, expand/collapse, overlay open/close on Vira or custom CSS
- Token choice (`--duration-*`, `--easing-*`) or `prefers-reduced-motion` behavior
- Replacing raw `ms`, `ease`, or animation libraries on UI feedback
- Drag / swipe / sheet feel, mobile or PWA touch, jank, stagger/choreography
- Audit, review, remove, or find motion opportunities; name a motion effect
- **viraui-design** is composing a screen and motion applies (add/skip/debug)

## When not to load

- Bootstrap, theme, preflight → **viraui-setup**
- Component/prop/layout choice without motion symptom → **viraui-design** only
- APG audit → **viraui-a11y**
- Data stress / worst-case fixtures → **viraui-breakui**
- Divergent variant picker (explicit) → **viraui-explore**
- Load all motion refs “to be safe” → hub + **one** matching ref only

## Action router

| Need                                          | Read                                 |
| --------------------------------------------- | ------------------------------------ |
| Whether to animate; reduced-motion; frequency | [principles.md](principles.md)       |
| Functional vs evocative                       | [animations.md](animations.md)       |
| Duration, exits, distance                     | [speed.md](speed.md)                 |
| Which easing                                  | [timing.md](timing.md)               |
| Touch / drag / swipe / mobile PWA             | [gestures.md](gestures.md)           |
| Jank / compositing / expensive props          | [performance.md](performance.md)     |
| Multi-element sequence / stagger intent       | [choreography.md](choreography.md)   |
| Build one interaction end-to-end              | [build.md](build.md)                 |
| Name the motion pattern                       | [vocabulary.md](vocabulary.md)       |
| Hunt where motion helps                       | [opportunities.md](opportunities.md) |
| Audit existing motion                         | [improve.md](improve.md)             |
| Review a motion diff                          | [review.md](review.md)               |
| Delete / reduce motion                        | [remove.md](remove.md)               |

## Motion contract

1. **Whole interface** — “Vira already animates” is not an exemption for custom CSS.
2. Hover, press, focus, expand/collapse, overlay open/close → **functional** motion unless `prefers-reduced-motion: reduce`.
3. Tokens only, e.g. `transition: transform var(--duration-fast) var(--easing-standard);`
   Duration: `--duration-instant` \| `--duration-fast` \| `--duration-normal` \| `--duration-slow` \| `--duration-slowest`.
   Easing: `--easing-standard` \| `--easing-entrance` \| `--easing-exit` \| `--easing-elastic` \| `--easing-wiggle`.
4. Every animation you add includes `@media (prefers-reduced-motion: reduce) { transition: none; }` (or equivalent). Motion never carries meaning alone.
5. Keyboard / 100+/day surfaces → no enter/exit motion ([principles.md](principles.md)).
6. Prefer `@viraui/react` overlays over hand-rolled drawers; no Vaul/Framer/Sonner as required defaults.

Theme group `motion` in `@viraui/react/specs/foundation/theme-topics.xml`. Full roles/principles/a11y + longer-than-slowest `calc(var(--duration-slowest) * n)`: `@viraui/react/specs/foundation/motion.xml`. Preset JS: `@viraui/foundation/<brand>/nested` (`duration.*`, `easing.*`) — see [speed.md](speed.md).

**Engine** (CSS vs JS): prefer modern CSS timelines / `sibling-index()` / `@starting-style` — see **viraui-design** [styling.md](../viraui-design/styling.md). This skill owns tokens and principles.

## Red flags — STOP

| Excuse                                   | Reality                                                      |
| ---------------------------------------- | ------------------------------------------------------------ |
| “Polish / next sprint / skip custom CSS” | Functional motion required                                   |
| “200ms ease-in-out is fine”              | `--duration-*` + `--easing-*`                                |
| “Framer/GSAP/Vaul for hover or sheets”   | Token CSS + Vira parts unless explicitly out of scope        |
| “IO / Framer for scroll reveal”          | CSS timelines first — **viraui-design** hub motion pointers  |
| “Gentler motion under reduced-motion”    | Kill transitions/animations — [principles.md](principles.md) |
| “Read all motion refs first”             | Hub + one ref from router                                    |
| “Only load if user said viraui-motion”   | Description symptoms are enough — load on match              |

## Rationalization counters

- **JS `180`/`480` literals** → foundation nested tokens — [speed.md](speed.md).
- **Blur/loop/bounce spectacle** → [animations.md](animations.md) evocative limits.
- **No reduced-motion** → [principles.md](principles.md) — non-negotiable.
- **Only Vira components animate** → custom sidebar/card CSS still covered.
- **Syrup drag / jump on release** → [gestures.md](gestures.md).

## Out of scope

Monorepo Vira component implementation, bootstrap, APG audit, inventing component APIs, data-stress harnesses, divergent explore pickers.

## Next skill

Compose and API → **viraui-design**. Structured a11y audit → **viraui-a11y**. Bootstrap → **viraui-setup**. Worst-case data → **viraui-breakui**. Explicit variants → **viraui-explore**.
