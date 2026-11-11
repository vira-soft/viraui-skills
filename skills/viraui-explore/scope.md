# Scope + recon

**When to read:** Phase 1–2 — narrow the brief and map Vira ground before naming axes.

## Phase 1 — Scope

One piece per run. If the brief spans a dashboard or whole page, pick the single highest-leverage piece, say which and why, and offer the rest as follow-up runs.

Restate the brief in one sentence: what the thing is, where it lives, what it must do.

**Done when:** one shippable UI piece is named; multi-piece briefs are deferred.

## Phase 2 — Recon

Map the ground every variant must stand on:

| Check        | Look for                                                                                               |
| ------------ | ------------------------------------------------------------------------------------------------------ |
| Stack        | Framework + `@viraui/react` import style; CSS modules / app chrome                                     |
| Bootstrap    | Preflight + theme already loaded (**viraui-setup** if missing)                                         |
| Tokens       | Theme semantics (`--global-*`, `--space-*`, motion `--duration-*` / `--easing-*`) — variants use these |
| Layout habit | **Stack-first**; spacing floor `m` for container gaps/padding                                          |
| Personality  | Playful consumer vs crisp tool — bounds the boldest direction                                          |
| Context      | Background, neighbors, sizes; overlay providers only if a variant needs Dialog / Toast / similar       |
| Specs        | Index-first `@viraui/react/specs` for candidate parts (do not invent APIs)                             |

Empty directory / no project → standalone HTML branch in [harness.md](harness.md); restrained defaults (neutral grays, one accent, system font) until a product theme exists.

## Realistic content

No lorem. Plausible names, numbers, timestamps, statuses. Prefer values from **viraui-breakui** [catalog.md](../viraui-breakui/catalog.md) when that skill is installed; otherwise invent schema-shaped copy.

## Done

Recon notes exist; bootstrap gap escalated to **viraui-setup** if needed; ready for [axes.md](axes.md).
