# Scope + recon

**When to read:** Phase 1–2 — narrow brief + map Vira ground before naming axes.

## Phase 1 — Scope

One piece per run. If brief spans dashboard or whole page, pick single highest-leverage piece, say which + why, offer rest as follow-up runs.

Restate brief in one sentence: what thing is, where it lives, what it must do.

**Done when:** one shippable UI piece named; multi-piece briefs deferred.

## Phase 2 — Recon

Map ground every variant must stand on:

| Check | Look for |
| --- | --- |
| Stack | Framework + `@viraui/react` import style; CSS modules / app chrome |
| Bootstrap | Preflight + theme already loaded (**viraui-setup** if missing) |
| Tokens | Theme semantics (`--global-*`, `--space-*`, motion `--duration-*` / `--easing-*`) — variants use these |
| Layout habit | **Stack-first**; spacing floor `m` for container gaps/padding |
| Personality | Playful consumer vs crisp tool — bounds boldest direction |
| Context | Background, neighbors, sizes; overlay providers only if variant needs Dialog / Toast / similar |
| Specs | Index-first `@viraui/react/specs` for candidate parts (invent no APIs) |

Empty directory / no project → standalone HTML branch in [harness.md](harness.md); restrained defaults (neutral grays, one accent, system font) until product theme exists.

## Realistic content

No lorem. Plausible names, numbers, timestamps, statuses. Prefer values from **viraui-breakui** [catalog.md](../viraui-breakui/catalog.md) when skill installed; else invent schema-shaped copy.

## Done

Recon notes exist; bootstrap gap escalated to **viraui-setup** if needed; ready for [axes.md](axes.md).
