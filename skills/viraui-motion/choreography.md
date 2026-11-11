**When to read:** Two or more elements move on the same event — stagger, sequence, crossfade, “feels mechanical” / “too much going on”.

# Choreography

Own **relationships** between motions: cast, overlap, stillness. Single-element curves → [animations.md](animations.md) / [speed.md](speed.md) / [timing.md](timing.md). CSS stagger / view timelines / `sibling-index()` **engine** → **viraui-design** [styling.md](../viraui-design/styling.md).

## Checklist

1. Cast every mover as Lead / Support / Decoration / Static **before** timing.
2. Prefer **parallel** over sequence; sequence only when order carries meaning or overlap looks broken.
3. **One entrance per container** — panel slides in ⇒ content already present (no parent enter + child stagger).
4. Never stagger high-frequency or keyboard-triggered UI (menus, tabs, command palettes, dense lists).
5. Uniform identical delay/distance/easing across items → forbidden (metronome).
6. Visible ⇒ interactive; delayed items must not block a ready control.
7. Survive interruption — mid-flight reverse must not break order.

## Cast

| Role       | Treatment                                               |
| ---------- | ------------------------------------------------------- |
| Lead       | Moves first, farthest, longest on screen                |
| Support    | Shorter / smaller follow                                |
| Decoration | Fade only — or nothing                                  |
| Static     | Does not animate (incl. containers whose children move) |

More than one Lead ⇒ hierarchy problem; say so. Most groups shrink here.

## Relationships

| Relation | When                                                       |
| -------- | ---------------------------------------------------------- |
| Together | Same object / same moment — shared timing family           |
| Overlap  | Stagger — second starts while first still moves            |
| Sequence | Overlap would clash (two rich views, cause→effect drawing) |
| Carry    | Animate parent; children come along                        |

**Together defaults:** exiting element leaves layout immediately so siblings close the gap **while** it fades; view swap in one container = crossfade, not full wait; sub-parts of one component share one duration/easing family ([speed.md](speed.md) / [timing.md](timing.md)).

**Overlap (product UI):** keep total group inside functional duration tokens — typically finish within `--duration-normal` or less; stagger only the first handful of a long list. Marketing / first-run may use slower evocative tokens ([animations.md](animations.md)). Vary delay **and** treatment by importance; order by importance / reading direction / cause, not blind DOM index.

**Sequence:** slightly overlap the handoff so it reads as one gesture, not a queue.

## Gotchas

- Framer `staggerChildren` / `layoutId` as required APIs → express intent here; implement with Vira tokens + design `styling.md` CSS first.
- Hardcoded `30ms` / `80ms` / `300ms` literals → map to `--duration-*` and calculated delays from those tokens.
- Do not load the whole motion folder.

## Validation

- Cast recorded; one Lead
- No dual entrance; no high-frequency stagger
- Tokens for all durations/easings
- Engine deferred to design `styling.md` when writing CSS timelines
