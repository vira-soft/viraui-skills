# Directions (axes)

**When to read:** Phase 3 — name divergent directions **before** writing variant code.

## Defaults

- **3** variants default.
- Up to **5** when user asks (`x5`) or design space genuinely wide.
- >5 dilutes comparison — refuse + cut.

## Naming

Each variant gets:

1. **direction name** — Quiet, Editorial, Dense, Playful — never Option A/B/C.
2. **named axis** in one phrase — layout, density, personality, motion story, interaction model.

**Completion criterion:** every variant has name + axis; no two share same axis position.

## Anti-convergence

Sharing product tokens ≠ convergence — variants should feel native to product.

These **are** convergence (replace one):

- Tint / accent swap only
- Copy-only difference
- Same layout + same interaction + same motion w/ different border radius

Real alternatives: different layout structure, interaction model, density/spacing rhythm, motion story (still **viraui-motion** tokens).

## Vira-native divergence

Every direction must be defendable as shippable with:

- Theme semantic tokens (no raw hex skin as the “idea”)
- Public `@viraui/react` parts/props first (**viraui-design**)
- Stack-first layout; container spacing from design spacing floor

List set for user **before** coding. If two proposed directions collapse, cut one + say so.

## Next

Build harness → [harness.md](harness.md). Build each variant UI via **viraui-design** (hub + one matching ref). Motion inside variant → **viraui-motion** (hub + one ref).
