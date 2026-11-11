**When to read:** “What could animate here?” / “make it feel more alive” — read-only hunt. Do not implement; hand build to [build.md](build.md).

# Opportunities

Restraint first. Short high-conviction list beats a wishlist. Cap **5–7** suggestions per app (fewer per view). Order by leverage.

## Gate (every candidate)

1. **Frequency** — 100+/day or keyboard → reject. Tens/day → near-imperceptible only or reject. Occasional / rare → eligible.
2. **Purpose** — Must name: feedback, spatial consistency, state indication, prevent jarring change, explanation, or delight (rare only).
3. **Budget** — Must fit [speed.md](speed.md) tokens (functional UI inside instant/fast/normal). If it “only works” as slow spectacle → reject.
4. **Function** — Dense data / charts the user reads → reject decorative motion.

Fail any step → put in **Rejected** with the reason.

## Where to hunt

| Seam                                              | Typical purpose                |
| ------------------------------------------------- | ------------------------------ |
| Overlay open/close (Dialog, Popover, Menu, Sheet) | Spatial + prevent jarring      |
| Expand/collapse disclosure                        | State indication               |
| Toast / banner enter-exit same edge               | Spatial consistency            |
| Press / toggle feedback                           | Feedback                       |
| Tab / segmented indicator travel                  | State indication               |
| Empty → first content                             | Prevent jarring / rare delight |
| Destructive confirm                               | Feedback (functional only)     |

Skip: command palette / shortcut chrome, every-section scroll reveal, hover scale on dense tables, infinite pulse on persistent chrome.

## Output format

```
### Suggestions
1. [surface] — purpose: … — tokens: --duration-* / --easing-* — notes: …
…

### Rejected
- [surface] — reason: frequency | purpose | budget | function
```

No code edits. If user asks to implement one item → [build.md](build.md) (hub + that ref only).

## Gotchas

- Suggesting Motion/Vaul/Sonner stacks → wrong; Vira parts + tokens.
- Hardcoded ms in proposals → map to `--duration-*`.
- Do not load the whole motion folder.

## Validation

- ≤7 suggestions; every row passed the gate
- Rejected list present when candidates failed
- Read-only
