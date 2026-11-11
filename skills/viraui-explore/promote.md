# Promote / riff

**When to read:** after the user picks a winner, asks to riff, or asks to keep/leave the picker.

## Wait state (before promote)

Present the set honestly — no pre-picked favorite:

| #   | Variant   | Axis                                 | When it's the right choice | Its cost            |
| --- | --------- | ------------------------------------ | -------------------------- | ------------------- |
| 1   | Quiet     | Minimal motion, borders over shadows | Daily-use tool             | Least memorable     |
| 2   | Editorial | Large type, generous whitespace      | Moment needs weight        | Eats vertical space |

Close with harness URL/path and keys (`1–N`, arrows, `R`).

If two variants converged while building, cut one and say so.

## Invocation variants

| Invocation                         | Behavior                                                                    |
| ---------------------------------- | --------------------------------------------------------------------------- |
| `keep <variant>`                   | Promote into the app; **delete** prototype surface                          |
| `keep <variant>, leave the picker` | Promote; **keep** harness                                                   |
| `riff <variant>`                   | Keep harness; new axis set around that direction ([axes.md](axes.md) again) |

## Promote steps

1. Move the winning variant into the real app tree (project file layout, naming, tokens).
2. Follow **viraui-design**: props/parts before custom CSS; Stack-first; index-first specs — do not invent APIs.
3. Motion that ships → meet **viraui-motion** (tokens + reduced-motion). Picker chrome rules do **not** apply to product UI.
4. Delete `/prototypes/<slug>` (or standalone file) unless the user said leave the picker.
5. Hand off to design [verify.md](../viraui-design/verify.md) (CSS rewrite leftovers = 0 + ship report).
6. If the winner changed keyboard/APG surface and the user wants an audit → **viraui-a11y**.

## Riff

Keep the harness. Run Phase 3 again ([axes.md](axes.md)) diverging **around** the gravitated direction. Rebuild variants; same picker contract.

## Motion bar (variants, not picker)

Product motion inside variants uses **viraui-motion** — hub + one ref. Do not paste raw ms / cubic-bezier tables here. Variant swap stays instant regardless.
