# End-of-work adversarial verify

**When to read:** after JSX/CSS edits for any task that loaded **viraui-design**; **before** claiming done, shipping, or saying UI is finished.

**Tone:** attack your own output. Hunt rationalizations. Friendly skim ≠ pass.

Compose-time loops in sibling refs stay in place. This file = **ship-time** gate over whole diff. Same requirements on every Agent Skills host.

## Hard gate

1. Run **CSS rewrite inventory** (below) on **final** diff first.
2. Copy checklist below into working notes.
3. Mark each item against **final** output (not plan).
4. Any fail = critical → fix → re-run this file from top.
5. **Emit ship report** (below) in **final reply**. Silent mental checklist = fail.
6. Claim done only at **0 critical** with `adversarial verify: pass`.
7. Never hand off with “looks fine — swap CSS for props later.”

## CSS rewrite inventory (required)

Before rest of checklist: scan **every** new CSS module rule, Tailwind utility, and visual `style` key in final diff (on or around Vira roots).

For each declaration, write one line:

| Declaration | Maps to | Action |
| ------------------------------------- | -------------------------------- | ---------------------------- |
| e.g. `gap: 1rem` | Stack `rowGap` / `columnGap` | **delete** CSS; use prop |
| e.g. `letter-spacing` | Text `tracking` | **delete** CSS; use prop |
| e.g. page backdrop blur | app chrome (system doesn't own) | keep — justify |
| e.g. mock-matched Button radius tweak | consumer **expressly asked** | keep — cite ask; units first |

Rules:

- Public prop / part / layout pattern covers it → **delete** CSS; apply prop/part. Leftover = **critical**.
- Documented `--vui-*` covers it → set hook; drop reinvented raw CSS.
- Else keep only as **app chrome** or **explicit consumer ask** — name which in ship report.
- Empty inventory (`none`) is fine when no custom CSS was added.
- Skipping this table (mental skim) = fail — same as skipping ship report.

## Checklist

### Discovery / authority

- [ ] Specs **index-first** for every Vira surface touched (`index.xml` / `@viraui/react/specs` → scoped units). Charts / data viz → `@viraui/charts/specs` via [charts.md](charts.md) (install `@viraui/charts` + `@visx/visx` first if missing). No first discovery via `ls` / `rg` / `grep` on `dist/components/**` or `*.d.ts` trees.
- [ ] **Compose-with:** `props.xml` + `usage.xml` opened **before** any CSS module / utility / size-fill `className` on those Vira roots. No “I already know this control — style first.” Unsolicited reshape CSS forbidden; consumer-requested overrides still need units first.
- [ ] No invented props, parts, hooks, or CSS prefixes. Stories are examples only — never API authority.
- [ ] Surfaces with `meta.xml` `<base_ui>`: Base UI API checked after Vira `props` — no invented pass-through; no assumed 1:1 wrap/regroup; ask if still unsure.
- [ ] `usage.xml` **do/dont** read for each touched surface — no CSS that listed dont forbids.
- [ ] Types/source opened only to **verify** after units, not to browse API.

Depth → [discovery.md](discovery.md).

### API hygiene

- [ ] Every equals-default prop **omitted** — including **color**: no part / `variant` / `tone` / accent set to value it already defaults to. Paint appears only where it carries meaning (zone, severity, status) — [styling.md](styling.md).
- [ ] Icon-only controls use icon slots + accessible name — never `children` on `IconButton` / `IconButtonLink` / `ToggleButton`.
- [ ] Icons in slots omit `size` / `width` / `height` unless expressly overriding host/library default ([icons.md](icons.md)).
- [ ] Imports from `@viraui/react` root (icons: any `ReactNode` in slots — [icons.md](icons.md)).
- [ ] No custom CSS reinventing public prop on same root (`letter-spacing`→`tracking`, `text-transform`→`transform`, gap/padding→layout props, etc.) — `props.xml` opened first.

### Layout

- [ ] Flex framing → `Stack` (semantic tags via `render`). Tracks → `Grid`. Ragged pack → `Masonry`. No raw HTML/`div` + `display:flex` / `display:grid` / CSS columns glue.
- [ ] No noop `render` that restates component default root (e.g. Stack `render={<div />}`) — omit unless host changes ([layout.md](layout.md) / PROTOCOL).
- [ ] Every used layout root has spacing props set (unset gap/padding = 0 — not “omit defaults”).
- [ ] **Scale floor:** container gap/padding is `m` or larger (sections `l`/`xl`, fields & cards `m`). `s` only for tight in-row clusters, `xs`/`2xs` only for optical micro pairs — never as container gap/padding ([layout.md](layout.md)). Scan every `rowGap`/`columnGap`/`hPadding`/`vPadding`/Masonry `gap` in diff.
- [ ] No CSS `gap`/`padding` on Stack / Surface / Grid / Masonry / Bleed roots.
- [ ] **No** `style` / CSS `paddingBlock*` / `paddingInline*` / side paddings on roots that own `hPadding`/`vPadding` — one-sided inset → tuples (`vPadding={[0, 'l']}`, …) with space tokens, not raw `1rem` ([layout.md](layout.md)).
- [ ] Stack content-position align uses **`safe …`** by default (`hAlign`/`vAlign` e.g. `safe center`, `safe end`) — not bare `center`/`end` when centering/ending. **No** `style`/`justifyContent`/`alignItems` / CSS module whose only job is `safe` flex alignment ([layout.md](layout.md)). `stretch` / `space-*` / `initial` stay bare.
- [ ] **No** invented `width` / `height` / `inline-size` / `block-size: 100%` / `w-full` / size-fill `className` (`.Social`, `.Submit`, `.fullWidth`, …) on Stack or **any** Vira control — including fixed-size `IconButton` where it would do nothing. Both-axes fill → Stack `fullWidth` / `fullHeight` / `expandChildren` + `hAlign`/`vAlign="stretch"` (Stack `patterns.xml`) or control’s own `fullWidth` ([layout.md](layout.md)). Scan CSS modules / inline `style` in diff for this.

Depth → [layout.md](layout.md).

### Responsive / direction (if viewport, breakpoint, or RTL work)

- [ ] Mobile-first base; enhance at larger viewports / containers.
- [ ] Layout / style-only (same tree) → CSS `@media` / `@container` first (anti-FOUC) — not `useBreakpoints`.
- [ ] Structure or Vira prop branches → `BreakpointsProvider` + `useBreakpoints` (not ad-hoc `matchMedia`).
- [ ] Every `@media` / `@container` length = active `useBreakpoints` / provider map (override or defaults) — no px drift.
- [ ] RTL → `DirectionProvider` from `@viraui/react` **and** `dir="rtl"` on portal ancestor (`html`); not Stack flex `direction`.

Depth → [responsive.md](responsive.md).

### Styling / attributes — useless custom CSS = critical

- [ ] **CSS rewrite inventory** completed for final diff (table above) — not mental skim.
- [ ] **No useless custom CSS** on Vira roots: every new module/utility either () sets documented `--vui-*` after units proved gap, (b) is **app chrome** system doesn't own, or (c) is override consumer **expressly asked** for. Otherwise delete and use props.
- [ ] Reinvented props-as-CSS count = **0** (gap/padding/width/height/letter-spacing/text-transform/line-height/max-width/list-style/…).
- [ ] No invented `--vui-*`; no consumer `--__*`. Confirm `shared_contract` before any public CSS hook.
- [ ] No hand-rolled elevation/`box-shadow` when Elevator / documented elevation applies; no `z-index` > 4 for app UI.
- [ ] Consumer `data-*` only from [custom-attributes.md](custom-attributes.md) / foundation attributes units.
- [ ] No reinvent of preflight typography/list/table chrome unless consumer expressly asked — [preflight-baseline.md](preflight-baseline.md).

Depth → [styling.md](styling.md), [preflight-baseline.md](preflight-baseline.md).

### Typography (if Text / Title / Prose / wrapping copy)

- [ ] UI short copy capped ~10–12 words/line via `maxWidth` / Stack **scaled to `size`** (smaller → narrower) — not full-bleed; no one fixed ch for every size; no CSS `max-width` / `line-height` on Text/Title when props cover it.
- [ ] `lineHeight` matched to size/context (Title in Prose → `s`); default `wrap` is `pretty`; short even-rag blocks use `wrap="balance"`; metrics use `whiteSpace="nowrap"`.
- [ ] Text walls (docs/privacy/long article) → `Prose` + reading column sized for body `size` — not Stack-for-rhythm; region `align` once.

Depth → [typography.md](typography.md).

### Accessibility (compose-time) — must run

- [ ] **Compose a11y checked** via [accessibility.md](accessibility.md) (not skipped). Full APG audit is separate → **viraui-a11y**.
- [ ] No duplicate widget `role` / `aria-*` Base UI already emits.
- [ ] Page landmarks, status, focus order, names owned by consumer app.
- [ ] Heading outline sequential — no skipped `h*`; `Title` `size` ≠ tag (`render` sets `h1`–`h6`).
- [ ] Text/Title `render` uses most correct semantic HTML host for meaning (e.g. `time`/`output`/`p`/…) — examples in accessibility.md, not exhaustive list; no span/ARIA fakes.
- [ ] Icon-only controls have accessible names; labeled fields wired correctly.

Depth → [accessibility.md](accessibility.md).

### Motion / setup

- [ ] Interactive custom CSS uses `--duration-*` / `--easing-*` and `prefers-reduced-motion` → **viraui-motion**.
- [ ] Missing / unstyled surfaces → **viraui-setup** bootstrap — not per-component CSS imports.

### Compounds (if touched)

- [ ] Parts match specs `meta` / `patterns` — no invented compound names.
- [ ] Field ownership correct; overlays have required titles/names.

Depth → [composition.md](composition.md).

### Charts (if graph / plot / data viz / `@viraui/charts`)

- [ ] [charts.md](charts.md) loaded; `@viraui/charts` + `@visx/visx` present (installed this task if missing).
- [ ] Authority = installed `@viraui/charts/specs` index → activity-hints → units — not skill encyclopedia / monorepo clone / `*.d.ts` first.
- [ ] No packaged `LineChart` / `BarChart` / `PieChart` / `DonutChart` / `RadarChart` / `ResponsiveChart`; no `--vui-charts-*` / `ChartRoot`.
- [ ] Name collisions (`Text` / `Stack` / `Grid`) aliased vs `@viraui/react` when both appear.
- [ ] Parent-fill charts use `ParentSize` / `useParentSize` when brief requires resize — not hard-coded svg only.

Depth → [charts.md](charts.md).

## Ship report (required in final reply)

Copy + fill. Omit = fail (don't claim done).

```markdown
## Adversarial verify

- specs/units: …
- CSS rewrite inventory: none | declaration → prop/part/--vui-*/justify/delete (every new CSS/utility/style)
- custom CSS on Vira roots kept: none | list + why (app chrome / explicit ask only)
- reinvented props-as-CSS: 0
- compose a11y (accessibility.md): pass | findings…
- motion tokens if custom CSS: … / n/a
- critical: 0
  adversarial verify: pass
```

## Pass criteria

- **Pass:** ship report present (with rewrite inventory) + `adversarial verify: pass` (0 critical).
- **Fail:** list each critical finding + fix applied; re-run until pass.
- **Never** claim done, ship, or hand off with open critical items, replaceable CSS left for user second pass, or without ship report.
