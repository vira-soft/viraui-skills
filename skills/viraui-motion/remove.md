**When to read:** App feels slow / over-animated — subtract motion only. Never add/retune curves (→ [improve.md](improve.md) / [build.md](build.md)).

# Remove

Burden of proof reversed: motion stays only if it passes gate. Counterpart to [opportunities.md](opportunities.md).

## Gate

```
Keyboard-triggered (shortcut, command palette, focus jump)?
└── Yes → DELETE

Seen 100+/day (core nav, tab switch, dense list rows)?
└── Yes → DELETE

On functional data the user reads/acts on (tables, charts) without a real value change?
└── Yes → DELETE

Purpose named (feedback / spatial / state / anti-jank / explanation)?
├── No → rare first-time delight? KEEP : DELETE
└── Yes → tens/day?
          ├── Yes → REDUCE to near-imperceptible tokens
          └── No → over budget vs [speed.md](speed.md)? REDUCE : KEEP
```

Marketing gets more latitude for one hero explanation; repeated section scroll reveals still fail.

## Reducing (same motion, smaller)

| Today | Reduce toward |
| ----------------------------------- | ------------------------------------------------------------ |
| Hover scale / lift / shadow | Color/opacity only, `--duration-instant` / `--duration-fast` |
| Slide/scale on frequent surface | Opacity only + fast tokens |
| UI longer than `--duration-normal` | Drop to fast/normal family |
| Long stagger | Cap or delete — [choreography.md](choreography.md) |
| Infinite pulse on persistent chrome | Once, or static end state |

If reduced motion no longer carries purpose → delete.

## Hunt list

- Shortcut-opened overlays with enter/exit
- Tab / segment / sidebar route crossfades inside app shell
- Hover transforms on dense rows
- Every-section scroll reveal (`whileInView`, IO class toggles, AOS utilities)
- Persistent infinite loops (non-loading)
- Staggered lists opened many times/day
- Evocative elastic on tables/errors

## Removal hazards

Check before delete:

- Element left at `opacity: 0` / off-screen transform with no final-state rule
- Exit animation required for unmount timing — switch to instant unmount + clean state
- Orphaned keyframes, unused CSS vars, dead Motion imports — clean up
- Shared utility used by justified motion — narrow change

Ask before removing lockfile motion dependency.

## Vira cleanup

Prefer editing consumer CSS modules / local styles. Do not strip theme `--duration-*` / `--easing-*` definitions. Overlay behavior: confirm parts still meet specs after removing custom chrome.

## Gotchas

- Deleting bridging toast/sheet motion that prevents teleport → disorienting; KEEP if purpose holds.
- “Gentler” under reduced-motion as replacement for delete → wrong; reduced-motion kill is [principles.md](principles.md).
- Do not load whole motion folder.

## Validation

- Only subtractive edits
- Gate branch recorded per removal
- Hazards checked; tokens theme intact
