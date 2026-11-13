---
name: viraui-design
description: >-
  Use when building, editing, debugging, or styling any UI in a ViraUI /
  @viraui/react consumer app — forms, overlays, page or shell layout, spacing,
  typography, icons, charts / graphs / plots / data visualization / KPI series /
  dashboards that need charts (@viraui/charts + @visx/visx peer), responsive or
  RTL, compounds, or visual polish — even if the user never names Vira,
  @viraui/react, @viraui/charts, or this skill. Also use when tempted to invent
  CSS modules, Tailwind utilities, raw HTML flex/grid, caption/logo-strip
  classes, packaged LineChart / BarChart / PieChart wrappers, or restyle
  controls instead of public Vira props and parts — including before the first
  JSX/CSS edit (coverage plan) and when a first pass already shipped replaceable
  CSS and needs a CSS rewrite pass before done. Load for login/settings/dashboard
  screens, Dialog/Menu/Toast compose, Stack/Surface/Grid/Masonry, icon-only
  controls, missing or unstyled Vira after bootstrap, or props-vs-CSS questions.
license: MIT
metadata:
  author: Vira Software
  version: '2026.11.13'
---

# viraui-design

Thin router for `@viraui/react` (+ charts → `@viraui/charts`). When UI/task fit is ~1%+, **read this hub before JSX, CSS, or invented props.** Durable API → package specs; skill pages = discipline only. Any Agent Skills host — same hub, same gates.

## Step 0 — coverage plan before code + CSS rewrite (hard)

**Do not edit JSX/CSS yet.** Emit a **coverage plan** in chat first (need → Vira prop/part/pattern | CSS?). Template + traps → [styling.md](styling.md). Then per row: open `props.xml` + `usage.xml` → use prop/part if covered → else `--vui-*` → else minimal CSS only for uncovered app-chrome / express ask. Skipping the plan, or opening a CSS module before plan + units = protocol fail. “Caption / logo strip — class is faster” = fail — [red-flags.md](red-flags.md).

**CSS rewrite pass (mid-draft, mandatory):** after any new CSS/utility/`style` on or around Vira roots — inventory every declaration → prop/part/`--vui-*`/justify/**delete**. Replaceable leftovers = critical. No “swap CSS for props later.” Same gate when user never named this skill. Detail → [styling.md](styling.md), [layout.md](layout.md), [verify.md](verify.md).

## Stance: compose WITH the system

Build from Vira **parts + public props**. Index → units before JSX/CSS. Prefer another Vira part/prop when something looks missing; custom CSS = **app chrome** only (or express consumer ask). Missing globals → **viraui-setup**. Vague intent → [symptoms.md](symptoms.md). Excuses → [red-flags.md](red-flags.md) (**read with this hub**).

## Mandatory load

| Signal                                                             | Action                                                                                               |
| ------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------- |
| Any `@viraui/react` compose/edit/debug/style                       | Read this hub first                                                                                  |
| User never said “viraui-design”                                    | Still load — description is discovery only                                                           |
| Any UI compose/edit (JSX or CSS)                                   | **Coverage plan in chat** (Step 0) before first edit — then props/JSX; CSS only for uncovered rows   |
| Any UI CSS/Tailwind/visual `style` edit                            | **CSS rewrite pass** (Step 0) before polish or done — even without naming this skill                 |
| Chart/graph/plot/data viz/KPI series/pie·donut·radar·bar·line·area | [charts.md](charts.md) → install `@viraui/charts` + `@visx/visx` if missing → `@viraui/charts/specs` |
| Screen compose (forms, shell, overlays, chrome)                    | Also [accessibility.md](accessibility.md)                                                            |
| Transitions/hover-press/overlay motion CSS                         | **viraui-motion** hub + one ref                                                                      |
| Missing global styles                                              | **viraui-setup** before CSS workarounds                                                              |
| Explicit APG audit/SR-keyboard debug                               | **viraui-a11y**                                                                                      |
| After JSX/CSS — before claiming done                               | Cite coverage plan + CSS rewrite 0 leftovers → **Read [verify.md](verify.md)**; emit ship report     |

## Action router

| Need                                                                | Read                                                                                 |
| ------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Vague intent/anti-pattern                                           | [symptoms.md](symptoms.md)                                                           |
| Choose component/inspect API                                        | [discovery.md](discovery.md) → specs index + units                                   |
| Intent → component id                                               | [component-matrix.md](component-matrix.md) — confirm in units                        |
| Forms, Dialog, Popover, Menu, Toast, compounds, custom field labels | [composition.md](composition.md) → specs `patterns`/`usage`/`props`                  |
| Layout/density/Stack·Grid·Masonry/prefer-`safe`                     | [layout.md](layout.md)                                                               |
| Mobile-first/`@media`/`@container`/`useBreakpoints`/RTL             | [responsive.md](responsive.md)                                                       |
| Props, `--vui-*`, elevation, motion **engine**                      | [styling.md](styling.md)                                                             |
| Text measure/leading/`wrap`/`whiteSpace`/align                      | [typography.md](typography.md)                                                       |
| Bare HTML lists/prose/tables/link chrome                            | [preflight-baseline.md](preflight-baseline.md)                                       |
| Compose-time a11y (not full audit)                                  | [accessibility.md](accessibility.md)                                                 |
| Motion tokens/reduced-motion                                        | **viraui-motion**; engine → [styling.md](styling.md)                                 |
| APG audit/keyboard or SR debug                                      | **viraui-a11y**                                                                      |
| Consumer `data-*`/vibrancy/elevation                                | [custom-attributes.md](custom-attributes.md)                                         |
| Icons/glyph slots                                                   | [icons.md](icons.md)                                                                 |
| Charts/graph/plot/data viz/`@viraui/charts`                         | [charts.md](charts.md) → install if missing → `@viraui/charts/specs`; no `LineChart` |
| Excuses/STOP                                                        | [red-flags.md](red-flags.md)                                                         |
| End of work                                                         | [verify.md](verify.md) — rewrite inventory + ship report; 0 critical                 |

## Authority (in order)

1. **Package specs** — `index.xml` + `activity-hints.xml` + scoped units (`@viraui/react/specs` UI; `@viraui/charts/specs` charts).
2. **Base UI API** — when `meta.xml` has `<base_ui href>`, after Vira props. Still unsure → ask.
3. **Types/source** — verify after units. Charts: upstream visx docs after units.
4. **Stories** — examples only.
5. **Skills** — routers only; never second props encyclopedia.

## Filesystem recipe

`@viraui/react/specs/*` → `node_modules/@viraui/react/dist/specs/`. Charts → `@viraui/charts/specs/*` → `node_modules/@viraui/charts/dist/specs/` — [charts.md](charts.md).

## FORBIDDEN discovery

No `ls`/`rg`/`grep` on `dist/components/**` or `*.d.ts` **before** specs index + target units. No monorepo clone/skills prose as charts API when `@viraui/charts` is installed.

## Consumer contract

1. Compose with public parts + props from units. Custom CSS reshape **only** when consumer expressly asks.
2. Import from `@viraui/react`. Icon slots: any `ReactNode`.
3. Index-first; omit equals-default props (incl. color) — [styling.md](styling.md). Base UI via `meta` after Vira props.
4. **Coverage plan → props before CSS** — Step 0 (emit plan before first edit).
5. Layout → [layout.md](layout.md). Responsive/RTL → [responsive.md](responsive.md). Ladder → [styling.md](styling.md). Measure → [typography.md](typography.md).
6. Icon-only: slots + accessible name; omit glyph `size`/width/height — [icons.md](icons.md).
7. Documented consumer `data-*` — [custom-attributes.md](custom-attributes.md).
8. Bare HTML lists/prose/tables/links — [preflight-baseline.md](preflight-baseline.md).
9. Landmarks, heading outline, semantic `render`; no duplicate Base UI widget ARIA — [accessibility.md](accessibility.md).

## Before done (non-optional)

1. **Coverage plan** was emitted before first JSX/CSS edit (cite in ship report).
2. **CSS rewrite pass** — reinvented props-as-CSS = **0** (no “clean later” handoff).
3. **Read [verify.md](verify.md)**; adversarial checklist on **final** diff.
4. **Emit ship report**. Silent mental checklist = fail.
5. Fix criticals → re-run → done only at **0 critical** with `adversarial verify: pass`.

## Out of scope

Monorepo authoring, npm release, APG structured audit (→ **viraui-a11y**), first-time bootstrap (→ **viraui-setup**).

## Next skill

APG audit → **viraui-a11y**. Screen motion → **viraui-motion**.
