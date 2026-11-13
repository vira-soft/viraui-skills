# Responsive + direction

**When to read:** viewport / container / breakpoint UI (`@media`, `@container`, aligned `useBreakpoints`) **or** reading direction / RTL (`DirectionProvider`, `useDirection`, `dir` on `html`).

Exact provider/hook API → specs `components/breakpoints/` + `components/direction-provider/` units. Page = **discipline only**.

## Two different `direction`s

| Word        | Surface             | Values               | Meaning                                    |
| ----------- | ------------------- | -------------------- | ------------------------------------------ |
| `direction` | `Stack` (layout)    | `row` / `column` / … | Flex main axis — **not** RTL               |
| `direction` | `DirectionProvider` | `ltr` / `rtl`        | Reading direction for Base UI–backed trees |

Do **not** set `Stack direction="rtl"`. Same-tree flex axis swap at breakpoint = CSS `@media` / `@container` (below). Different React trees or Vira **props** by viewport = `useBreakpoints`.

---

# Breakpoints (mobile-first)

## Hard rule: mobile-first

Always author **narrow** layout as base. Enhance at larger viewports / containers (`min-width` / `min-width` container queries). Do **not** ship desktop-first (`max-width` as primary branch) unless product already owns that pattern and user insists.

```text
Base = mobile / default props / default CSS
  → at breakpoint N: add or change only what wide needs
```

## Hard rule: one shared map

`@media`, `@container`, `useBreakpoints` share **one** threshold map — active `BreakpointsProvider` `breakpoints` prop, or hook defaults when unset. Copy those **exact** CSS lengths (prefer `em` as shipped). Do **not** invent parallel system (`768px` / `1024px`, theme token widths, ad-hoc `matchMedia` hooks).

Defaults (em, mobile-first min-width) when app did not override: `extra-small` 30em, `small` 48em, `medium` 60em, `large` 80em, `extra-large` 100em. Confirm in specs units for installed version. If app set `breakpoints` on provider, CSS **must** use **those** strings — not skill defaults.

## Choose the engine (CSS first — anti-FOUC)

```text
Layout / style only (flex axis, columns, gap via class, visibility, padding) —
same React tree, no Vira prop swap?
  yes → CSS @media (viewport) or @container (parent size)
        lengths = active useBreakpoints / BreakpointsProvider map
        Prefer this so layout does not wait on hydration (FOUC).

Need different React trees, hide/show distinct parts, or change Vira **props**
by viewport?
  yes → BreakpointsProvider + useBreakpoints()  (Client Component)

Container-sized layout (not viewport)?
  → @container — still same em map; not useBreakpoints
```

`useBreakpoints` **not** default layout engine. JS after paint can flash wrong layout. Reach for hook only when structure or React props must change.

## CSS `@media` / `@container` (primary)

When React tree + Vira props stay same:

1. Read active map — app `BreakpointsProvider` `breakpoints` if set, else hook defaults above (or specs units).
2. Write mobile-first **`min-width`** `@media` and/or `@container` queries with those **exact** lengths.
3. Documented exception to “props before CSS”: responsive **layout** values that would FOUC under hydration (e.g. flex-direction, grid columns, show/hide via CSS) may live in `@media` / `@container`. Still do **not** reinvent letter-spacing / tracking / non-responsive spacing props as CSS.

```css
/* Matches default `medium` — or copy the app override string verbatim */
@media (min-width: 60em) {
  .shell {
    flex-direction: row; /* narrow base stays column in the module */
  }
}

/* Parent must establish a containment context */
.panel {
  container-type: inline-size;
}

@container (min-width: 60em) {
  .panelBody {
    /* same medium threshold as useBreakpoints('medium') */
  }
}
```

## `useBreakpoints` (structure / props only)

1. Open specs index → `breakpoints` units (`meta` → `props` → `usage`).
2. Wrap tree that calls hook in `BreakpointsProvider` inside Client Component (`'use client'`). Not Server Component module. Overlay bootstrap (`Dialog` / `Tooltip` / `Toast`) stays separate — don't treat provider as mandatory root chrome.
3. Prefer `useBreakpoints('small')` (one boolean) when only one flag matters; call `useBreakpoints()` once when a branch reads several flags (one subscription, no per-flag hooks).
4. Compose mobile-first: default JSX = narrow; when flag true, swap **trees**, density / other Vira props, or children CSS cannot express.

```tsx
'use client';

import { BreakpointsProvider, Stack, useBreakpoints } from '@viraui/react';

function SettingsShell() {
  const isMedium = useBreakpoints('medium');

  // Different children / props — not a pure flex-direction swap
  return isMedium ? <WideSettings /> : <NarrowSettings />;
}

export function SettingsPage() {
  return (
    <BreakpointsProvider>
      <SettingsShell />
    </BreakpointsProvider>
  );
}
```

Custom map: `breakpoints` on provider **replaces** whole default map (no sparse merge). Align every `@media` / `@container` length to that map.

## Prop override by viewport (typed bag)

Vira has **no** per-breakpoint prop API (no `lg={...}` / `at={...}` on components). Props that must change by viewport = hook + a typed `Partial<Props>` bag spread into the JSX. This keeps prop-only changes in one place without a second responsive system.

```tsx
const wideHeading: Partial<TextProps> = { weight: 'bold', size: 'xl' };

const bp = useBreakpoints();

<Text weight="semibold" size="l" {...(bp.medium && wideHeading)}>
```

- Base props = narrow; the bag carries **only** what the wide viewport changes.
- Spread the bag **after** the base props. Reversed order lets base values win and silently drops the override.
- `false` in a JSX spread is a no-op — no ternary needed.
- `useBreakpoints()` once when the branch reads several flags; `useBreakpoints('medium')` when only one matters.
- Constant bag at module scope (no per-render allocation). Type it with the exported props type (`TextProps`, `StackProps`, …).
- Cumulative mobile-first: at `large`, `small`/`medium`/`large` all match — decide the order of spreads yourself, outermost narrowest.
- Still CSS: flex axis, gap, padding, visibility (anti-FOUC, above). Still conditional JSX: different trees / parts.

## Breakpoint gotchas

- CSS-first for layout; `useBreakpoints` only for structure / React props.
- Responsive bag spread **before** the base props — base wins and the override disappears. Base first, bag last.
- Per-breakpoint prop objects for style-only changes — `@media` / `@container` owns those.
- `@media` / `@container` lengths ≠ active map (drift, px aliases, theme tokens).
- mobile-first `min-width` as main responsive strategy.
- `letter-spacing` / non-responsive spacing reinvented in CSS when public prop covers it.
- Ad-hoc `matchMedia` / `768px` beside existing `BreakpointsProvider` map.
- Calling `useBreakpoints` outside provider.
- Putting provider in Server Component file.
- Using theme design tokens as breakpoint widths (not contract).

---

# Direction (LTR / RTL)

`DirectionProvider` + `useDirection` = **opt-in** transparent Base UI re-export from `@viraui/react`. Not part of Dialog / Tooltip / Toast overlay shell. Setup shell notes → **viraui-setup** [frameworks.md](../viraui-setup/frameworks.md).

Authority: specs `direction-provider` units + https://base-ui.com/react/utils/direction-provider (via `meta` `base_ui`).

## Hard rule: provider + document `dir`

`DirectionProvider` feeds **Base UI context only**. Does **not** set HTML `dir` or CSS `direction`.

For RTL:

1. `DirectionProvider direction="rtl"` around tree needing flipped Base UI behavior (menus, selects, sliders, …).
2. `dir="rtl"` on **portal ancestor** — usually `<html>` — so body-mounted popups inherit CSS direction.
3. Import from `@viraui/react` — never `@base-ui/react/direction-provider` when Vira already re-exports.

```tsx
// app root (Client) — pair with <html dir="rtl"> (or lang-appropriate)
import { DirectionProvider, Slider } from '@viraui/react';

<DirectionProvider direction="rtl">
  <Slider defaultValue={25} aria-label="Volume" />
</DirectionProvider>;
```

Subtree demo (still need `dir` on ancestor covering portals for real apps):

```tsx
<div dir="rtl">
  <DirectionProvider direction="rtl">{/* Menu / Select / Slider */}</DirectionProvider>
</div>
```

## `useDirection`

Use when portaled component must read context direction without relying on DOM `dir`. Confirm in units.

```tsx
const direction = useDirection(); // 'ltr' | 'rtl'
```

## Direction gotchas

- Provider alone (no `dir` on `html` / portal ancestor) — popups stay LTR in CSS.
- `dir="rtl"` only on local wrapper when portals mount on `document.body`.
- Importing Base UI path instead of `@viraui/react`.
- Treating DirectionProvider as required bootstrap.
- Confusing Stack flex `direction` with LTR/RTL.

---

Layout roots / density → [layout.md](layout.md). Props before CSS → [styling.md](styling.md). Discovery → [discovery.md](discovery.md). Compounds / overlays → [composition.md](composition.md) (providers still land here for discipline).
