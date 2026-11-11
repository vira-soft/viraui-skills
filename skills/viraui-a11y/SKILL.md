---
name: viraui-a11y
description: >-
  Use when the user asks for an accessibility audit, APG or ARIA validation,
  screen-reader or keyboard-pattern debug, or WCAG widget review of a ViraUI
  screen. Symptoms include phrases like "audit a11y", "APG review", "is this
  accessible", keyboard trap reports, or deep audit routing from viraui-design
  accessibility.md — not ordinary compose (compose-time a11y stays in
  viraui-design).
license: MIT
metadata:
  author: Vira Software
  version: '2026.10.16'
---

# viraui-a11y

Structured APG audit for `@viraui/react` screens. Load on **explicit audit/debug ask**, or when **viraui-design** [accessibility.md](../viraui-design/accessibility.md) routes here. Portable across Agent Skills hosts — same skill, no host forks.

Compose rules stay in **viraui-design** (compose-time a11y + end-of-work [verify.md](../viraui-design/verify.md)). This skill **audits only**. Do not copy APG sample `role`/`aria-*` onto Vira parts — Base UI already emits widget chrome.

Widget API facts → `@viraui/react/specs` units (index-first). Skills embed no component encyclopedias.

## When to load

- Accessibility audit, APG review, or WCAG widget check
- Screen-reader / keyboard-pattern debug on composed Vira screen
- **viraui-design** `accessibility.md` routes here for structured APG work

## When not to load

- Ordinary compose, prop choice, layout → **viraui-design**
- Compose-time “what aria-label for icon button?” → **viraui-design** [accessibility.md](../viraui-design/accessibility.md)
- Bootstrap, theme, preflight → **viraui-setup**
- Motion tokens on custom CSS → **viraui-motion** (via **viraui-design** compose)

## Action router

| Need | Read |
| --- | --- |
| Run audit + shape report | [audit.md](audit.md) |
| Vira component → APG pattern | [vira-map.md](vira-map.md) |
| DOM `role` → APG pattern | [roles.md](roles.md) |
| `aria-*` → APG pattern | [properties.md](properties.md) |
| Compose fixes without dup ARIA | **viraui-design** [accessibility.md](../viraui-design/accessibility.md) |

Read **one** mapping ref + [audit.md](audit.md) — not whole folder upfront.

## Audit contract

1. Map in-scope widgets via [vira-map.md](vira-map.md) (or [roles.md](roles.md) / [properties.md](properties.md) for unknown DOM).
2. **Never fetch** [APG example-index](https://www.w3.org/WAI/ARIA/apg/example-index/) HTML. Folder tables **are** the index.
3. Fetch only in-scope pattern URLs. Open APG `examples/` only when pattern page insufficient for keyboard Q.
4. Inspect **rendered DOM** + Base UI output — not “ARIA in JSX source.”
5. Verify Vira-added a11y notes in `@viraui/react/specs/components/<id>/a11y.xml` (after index).
6. Separate **page** landmarks/status/focus from **widget** behavior Vira/Base UI owns.
7. Fixes via **viraui-design** (specs units + types) — invent no widget ARIA.

## Red flags — STOP

| Excuse | Reality |
| --- | --- |
| “Fetch example-index to browse patterns” | Forbidden — use [vira-map.md](vira-map.md) |
| “Add role in JSX so audit passes” | Dup/cloak semantics — inspect DOM |
| “Every form field needs viraui-a11y” | Compose → **viraui-design** unless audit asked |
| “Copy APG sample onto ToggleButton” | Specs a11y units + Base UI own widget states |
| “Audit = list generic a11y tips” | Follow [audit.md](audit.md) report shape |

## Rationalization counters

- **“Source has no aria — must be broken”** → check rendered output first.
- **“More ARIA is safer”** → [APG Read Me First](https://www.w3.org/WAI/ARIA/apg/practices/read-me-first/) — omit dup attrs.
- **“I'll audit while building”** → compose with **viraui-design**; audit on ask or router.

## Package specs (supporting)

When verifying Vira-added surface during audit:

- `@viraui/react/specs/index.xml` → `components/<id>/a11y.xml` (+ meta/props as needed)
- **viraui-design** [component-matrix.md](../viraui-design/component-matrix.md) — intent → specs id only

## Out of scope

Monorepo component impl, bootstrap, motion authoring, replacing **viraui-design** compose guidance.

## Next skill

Fixes → **viraui-design** (specs units). Custom CSS motion found in audit → **viraui-motion**.
