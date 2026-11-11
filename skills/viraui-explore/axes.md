# Directions (axes)

**When to read:** Phase 3 — name divergent directions **before** writing variant code.

## Defaults

- **3** variants by default.
- Up to **5** when the user asks (`x5`) or the design space is genuinely wide.
- More than 5 dilutes comparison — refuse and cut.

## Naming

Each variant gets:

1. A **direction name** — Quiet, Editorial, Dense, Playful — never Option A/B/C.
2. A **named axis** in one phrase — layout, density, personality, motion story, interaction model.

**Completion criterion:** every variant has a name + axis; no two share the same axis position.

## Anti-convergence

Sharing product tokens is **not** convergence — variants should feel native to the product.

These **are** convergence (replace one):

- Tint / accent swap only
- Copy-only difference
- Same layout + same interaction + same motion with a different border radius

Real alternatives: different layout structure, different interaction model, different density/spacing rhythm, different motion story (still **viraui-motion** tokens).

## Vira-native divergence

Every direction must be defendable as shippable with:

- Theme semantic tokens (no raw hex skin as the “idea”)
- Public `@viraui/react` parts/props first (**viraui-design**)
- Stack-first layout; container spacing from the design spacing floor

List the set for the user **before** coding. If two proposed directions collapse, cut one and say so.

## Next

Build harness → [harness.md](harness.md). Build each variant’s UI via **viraui-design** (hub + one matching ref). Motion inside a variant → **viraui-motion** (hub + one ref).
