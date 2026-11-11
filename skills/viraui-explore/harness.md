# Harness

**When to read:** Phase 4 — isolated prototype surface + picker wiring. Never touch production routes here.

## Hard isolation

- Everything under isolated surface. Production code does **not** import from it.
- Integration only on promote ([promote.md](promote.md)), only for chosen variant.

## Branches

### Project with a dev server

- Route/page like `/prototypes/<slug>` (or framework equivalent).
- One file per variant + small harness hosting picker.
- Wire app providers variants need (theme/preflight already at root; add overlay providers only if Dialog/Toast/etc. in play).

### No project / static

- Single self-contained HTML file (inline CSS/JS) user opens in browser.

## Picker

Markup, styles, keyboard, placement from [picker.md](picker.md) — **verbatim**. Load that ref; build exactly that. Theme picker with no product tokens.

## Stage rules

- Render **one** variant at a time, full size, realistic surrounding context (toast needs page behind; card needs siblings; button needs form).
- No side-by-side thumbnails — postage-stamp size lies about spacing.
- **Variant swap is instant** — no transition on staged UI. Picker highlight may slide (picker.md exception only).
- Switching **re-mounts** variant so entrances re-run; replay re-mounts w/o changing selection.

## Verify before handoff

Flip every variant yourself. Interactions work; console clean. Screenshot each if browser tooling exists.

Then present tradeoff table + **stop** — choice belongs to user (table shape in hub / [promote.md](promote.md) wait state).

**Done when:** every variant reachable from picker; no console errors; URL or file path + keys stated.
