# Harness

**When to read:** Phase 4 — isolated prototype surface + picker wiring. Never touch production routes here.

## Hard isolation

- Everything lives under an isolated surface. Production code does **not** import from it.
- Integration happens only on promote ([promote.md](promote.md)), and only for the chosen variant.

## Branches

### Project with a dev server

- Route/page like `/prototypes/<slug>` (or framework equivalent).
- One file per variant + small harness that hosts the picker.
- Wire app providers the variants need (theme/preflight already at root; add overlay providers only if Dialog/Toast/etc. are in play).

### No project / static

- Single self-contained HTML file (inline CSS/JS) the user can open in a browser.

## Picker

Markup, styles, keyboard, and placement come from [picker.md](picker.md) — **verbatim**. Load that ref and build exactly that. Do not theme the picker with product tokens.

## Stage rules

- Render **one** variant at a time, full size, in realistic surrounding context (toast needs a page behind it; card needs siblings; button needs a form).
- No side-by-side thumbnails — postage-stamp size lies about spacing.
- **Variant swap is instant** — no transition on the staged UI. Picker highlight may slide (picker.md exception only).
- Switching **re-mounts** the variant so entrances re-run; replay re-mounts without changing selection.

## Verify before handoff

Flip every variant yourself. Interactions work; console clean. Screenshot each if browser tooling exists.

Then present the tradeoff table and **stop** — choice belongs to the user (table shape in hub / [promote.md](promote.md) wait state).

**Done when:** every variant is reachable from the picker; no console errors; URL or file path + keys are stated.
