---
name: viraui-explore
description: >-
  Use when the user explicitly asks to explore divergent UI directions, show
  multiple variants behind a picker, prototype several versions of one piece,
  riff around a chosen direction, or promote a picked explore variant. Triggers
  include "explore 3 directions", "show variants", "flip through options",
  "prototype picker", keep/riff after an explore run. Never auto-load on
  ordinary compose (viraui-design), data stress (viraui-breakui), or motion-only
  work (viraui-motion).
license: MIT
metadata:
  author: Vira Software
  version: '2026.11.11'
disable-model-invocation: true
---

# viraui-explore

Divergent **design exploration** for one ViraUI piece. Build 3–5 genuinely different directions behind visual picker; user picks; promote only winner.

**Explicit invoke only** (`disable-model-invocation`). Ordinary compose → **viraui-design**. Read hub + **one** sibling ref — not whole folder.

## When to load

- User names this skill, or asks directions / variants / explore / prototype picker
- Follow-up `riff` / `keep` / `keep … leave the picker` after explore run

## When not to load

- Ordinary compose, prop choice, layout → **viraui-design**
- Worst-case data stress → **viraui-breakui**
- Motion tokens without explore ask → **viraui-motion**
- APG audit → **viraui-a11y**
- Bootstrap → **viraui-setup**
- “Load all explore refs first” → hub + **one** matching ref

## Action router

| Need | Read |
| --- | --- |
| Narrow brief + Vira recon | [scope.md](scope.md) |
| Name directions before code | [axes.md](axes.md) |
| Isolated route / files | [harness.md](harness.md) |
| Picker DOM / CSS / JS | [picker.md](picker.md) |
| `keep` / `riff` / cleanup | [promote.md](promote.md) |
| Build each variant’s UI | **viraui-design** (discovery → composition → layout) |
| Motion quality inside a variant | **viraui-motion** (hub + one ref) |
| After promote | design [verify.md](../viraui-design/verify.md) |

## Explore contract

1. **Never touch production** during exploration — only `/prototypes/<slug>` (or standalone HTML).
2. **Named axis per variant** — layout / density / personality / motion / interaction. Tint-only ≠ divergence.
3. **Every variant fully works** — real interactions, realistic copy (no lorem). Content: [breakui catalog](../viraui-breakui/catalog.md) when available.
4. **Picker is harness chrome** — [picker.md](picker.md) verbatim; never project-themed.
5. **Variant swap instant**; picker highlight may slide. Product motion → **viraui-motion**.
6. **Vira-native variants** — theme tokens, Stack-first, public props/parts before inventing CSS.
7. **Stop for user choice**; promote only on ask; delete harness unless leave-picker.

## Red flags — STOP

| Excuse | Reality |
| --- | --- |
| “Auto-explore every new screen” | Explicit ask only |
| “Three accent tints count” | Replace with real axis split |
| “Theme the picker to match brand” | Verbatim chrome — [picker.md](picker.md) |
| “Animate the variant crossfade” | Instant swap |
| “Edit the real route now” | Promote only after `keep` |
| “Read all explore refs first” | Hub + one ref |

## Rationalization counters

- **“Faster to edit prod in place”** → isolation is the point — [harness.md](harness.md).
- **“Raw ms easing is fine in variants”** → **viraui-motion** tokens.
- **“Skip verify after keep”** → [verify.md](../viraui-design/verify.md) still required.

## Out of scope

Monorepo component impl, data stress catalogs, APG audits, inventing Vira APIs, ambient redesign without explore ask.

## Next skill

Compose/API while building variants → **viraui-design**. Motion inside variants → **viraui-motion**. After promote → [verify.md](../viraui-design/verify.md). Data stress on winner → **viraui-breakui**.
