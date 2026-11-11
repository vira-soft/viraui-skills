# Accessibility

**When to read:** compose-time names, landmarks, typography/semantic hosts, heading outline, icon-only controls, forms, overlays, decorative parts — not full APG audit.

Vira owns widget behavior (Base UI); consumers own page semantics. Structured APG audit / SR-keyboard debug → **viraui-a11y** (don't fetch APG example-index HTML).

Follow [APG Read Me First](https://www.w3.org/WAI/ARIA/apg/practices/read-me-first/): no ARIA better than bad ARIA.

## Before adding `role` or `aria-*`

1. Read surface specs `a11y.xml` (+ `meta` / `props`) + types/source if unsure.
2. Base UI or Vira already emit role/state → **omit** (`role`, `aria-pressed`, `aria-expanded`, `aria-selected`, `aria-checked`, `aria-haspopup`, `aria-controls`, `aria-modal`).
3. Add only consumer-owned names, landmarks, page status.

Don't fake widgets (`role="button"` on `Stack`/`div` — use `Button` / `IconButton`). Don't stamp `aria-label` on control with visible text, `label`, or `title`. Inspect rendered DOM — don't copy APG sample roles into JSX so audit “sees ARIA in source.”

```tsx
// Don't: Base UI already emits tablist + aria-pressed; aria-label cloaks "Save"
<Tabs.List role="tablist" />
<ToggleButton aria-pressed={pinned} aria-label="Pin" restingIcon={<Pin />} />
<Button aria-label="Save">Save</Button>

// Do: consumer-owned name only when there is no visible text
<ToggleButton aria-label="Pin" restingIcon={<Pin />} />
<Button>Save</Button>
```

## Typography + semantic hosts

`Title` / `Text` default `span`. **Size / tone = look. Tag = meaning** — set host via `render`. Prefer **most correct native HTML element** over ARIA or generic `span`/`div`. Table = **examples only** — not closed list (`mark`, `code`, `kbd`, `samp`, `var`, `cite`, `q`, `abbr`, `address`, `small`, `del`/`ins`, `dfn`, `data`, … — pick what content is).

| Meaning (examples) | Host via `render` (examples) |
| --- | --- |
| Document / section heading | `Title` + `h1`…`h6` (never bare `Title` as outline) |
| Block body / paragraph | `Text` + `p` when copy is block |
| Date or time | `Text` + `time` with machine-readable `dateTime` |
| Calculation / form result | `Text` + `output` (wire `htmlFor` / form when applies) |
| Inline prose link | `Text` + `a` (`href` required) |
| Stress / importance in copy | `em` / `strong` when meaning needs it — not weight/CSS alone |

Rule: meaning → correct element → `render` that host. Confirm defaults/don’ts in `title` / `text` `a11y` + `usage` units. Don't use `Text` as heading; don't treat `Title` `size` as HTML level.

```tsx
// Don't: visual size as fake outline; span for a datetime
<Title size="1">Dashboard</Title>
<Text>{publishedAt}</Text>

// Do: native host matches meaning
<Title size="1" render={<h1 />}>Dashboard</Title>
<Text render={<time dateTime="2026-10-09T09:00:00Z" />}>9 Oct 2026, 09:00</Text>
<Text render={<output htmlFor="qty price" />}>{totalLabel}</Text>
```

### Heading outline (no skips)

- One outline per view: levels climb in order (`h1` → `h2` → `h3` …).
- **Never skip level** for styling (no `h2` then `h4` because `size` looked right).
- Nested sections stay in scale: under `h2`, next = `h3`, then `h4` — no jump.
- Pair `size` (visual) with correct `h*` via `render`. Specs: Title `a11y` — hierarchy sequential.

```tsx
// Don't: skip h3
<Title size="2" render={<h2 />}>Settings</Title>
<Title size="4" render={<h4 />}>Notifications</Title>

// Do: sequential nest
<Title size="2" render={<h2 />}>Settings</Title>
<Title size="3" render={<h3 />}>Notifications</Title>
<Title size="4" render={<h4 />}>Email</Title>
```

## Compose checklist

- [ ] Real landmarks + **sequential** heading outline — no skipped `h*` (`Title` size visual; tag via `render`)
- [ ] Semantic host = most correct HTML element for meaning (table above = examples) via `Text`/`Title` `render` — not ARIA / bare `span` fakes
- [ ] DOM / reading / focus order aligned
- [ ] Interactive controls + regions named
- [ ] Loading via `aria-busy` and/or live status; blocking errors via `role="alert"` (or equivalent)
- [ ] Focus visible; color / elevation / motion never sole state signal
- [ ] Custom transitions honor `prefers-reduced-motion` → **viraui-motion**

## Icon-only controls

`IconButton`, `IconButtonLink`, `ToggleButton`, icon-only triggers need `aria-label` or `aria-labelledby`. Use icon props — never `children`. Decorative glyph stays decorative — parent carries name ([icons.md](icons.md)):

```tsx
<IconButton aria-label="Close dialog" icon={<Xmark />} />
```

## Buttons, forms, overlays, decorative

Confirm labels, Field ownership, Dialog/Popover titles, decorative `aria-hidden` in target surface `a11y.xml` / `usage.xml`. Don't invent widget ARIA from APG samples.

## Gotchas

- Dup widget ARIA already emitted by Base UI/Vira.
- `aria-label` cloaks visible text / `label` / `title`.
- `children` on icon-only APIs instead of `icon` / `restingIcon`.
- `Title`/`Text` left on default `span` when more specific semantic element fits (not limited to example table)
- Skipped heading levels (`h2` → `h4`) or `size` used as if it set tag.
- Treating compose-time a11y as substitute for **viraui-a11y** when user asks APG audit.

Prop / part discovery → [discovery.md](discovery.md). Compound assembly → specs `patterns` / `usage` units.
