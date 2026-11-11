# Failure signatures + Vira fix ladder

**When to read:** Phase 4 — what broke; fix without reinventing CSS.

## Break pass checklist

With worst-case (+ Empty / One / Huge) active, check:

1. **Real container width** (sidebar ≠ full page), then **320px**, then widest supported layout
2. **Browser zoom 200%** (or raised root font)
3. **Dark** (`data-mode` / theme) + **RTL** if product supports either — wire via **viraui-design** [responsive.md](../viraui-design/responsive.md) + setup theme / `DirectionProvider` + `dir` on `html` (invent no breakpoints)

Screenshot Demo + Worst when tooling allows; else say which findings visual vs inferred from CSS/layout.

## Fix ladder (ordered — stop at first that holds)

1. **Public props / parts** — open `@viraui/react/specs` units (`props.xml` / `usage.xml`) for `Text`, `Title`, `Stack`, Avatar, list/row compounds. Prefer `wrap` / `whiteSpace` / `maxWidth` / `lineHeight` / Stack `fullWidth` / `expandChildren` / `maxWidth` / align props over inventing CSS. Confirm names in units — invent no APIs.
2. **Theme tokens** — spacing/color from theme contract (`--space-*`, semantic colors). No reinvented padding gaps below spacing floor in design [layout.md](../viraui-design/layout.md).
3. **Environment** — RTL / breakpoints / dark via design [responsive.md](../viraui-design/responsive.md) + setup — no ad-hoc media in fix.
4. **App chrome CSS** — only when public props cannot express it. Then **viraui-design** Step 0 CSS rewrite + [verify.md](../viraui-design/verify.md).

Never lead with `min-width: 0` / `flex-shrink: 0` / `overflow-wrap` CSS modules when Vira prop or Stack pattern covers break.

Truncation / overflow without accessible name or hover-only actions → note in report; structured APG audit → **viraui-a11y** on ask.

## Truncate, wrap, or clamp (per field)

| Choice | Use |
| ------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Wrap** | Names, titles user must identify — prefer `Text`/`Title` `wrap`; 2 lines OK; 4 ⇒ column too narrow |
| **Truncate end** | Secondary metadata (role, preview) — pair with `title` / tooltip / detail view |
| **Truncate middle** | Values that differ at end (files, emails, paths, hashes) |
| **Clamp** | Multi-line card previews — `line-clamp` only via public prop if units expose it; else justify chrome CSS after ladder |
| **Never truncate** | Numbers, amounts, dates, compared values — give them room |

Confirm `wrap` / `whiteSpace` / `maxWidth` / `lineHeight` in [typography.md](../viraui-design/typography.md) + text/title units.

## Signature table

| What you see | Likely cause | Vira-first fix |
| --------------------------------------- | -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Avatar/icon squished to oval | Flex child shrinking | Avatar / fixed-size part: let row Stack not shrink it — content-sized sibling + `expandChildren` on text column (Stack [layout.md](../viraui-design/layout.md)); invent no `flex-shrink: 0` first |
| Text overflows box | Text column cannot shrink/wrap | `Text` `wrap` / `whiteSpace` / `maxWidth`; Stack text column with `expandChildren` + measure — [typography.md](../viraui-design/typography.md) |
| Email/URL past the edge | No break opportunities | `Text` wrap/`whiteSpace` props for that node; confirm units before CSS `overflow-wrap` |
| Trailing ••• / button clipped | Middle ate the row | Stack row: text column grows (`expandChildren`), action stays content-sized (`data-grow="false"` if needed) |
| Badge wraps two lines | Badge allowed to shrink | Keep badge content-sized; decide what yields (name wrap vs truncate) |
| Avatar adrift vs multi-line name | Cross-axis center on tall rows | Stack `vAlign` top/start once text wraps — [layout.md](../viraui-design/layout.md) |
| Last row cut mid-glyph | Fixed height, no scroll/fade | Intended overflow + scroll affordance; no silent clip |
| Mid-word breaks in heading | Aggressive break-all | Prefer wrap props that break only when needed |
| Wrong initials / `�` | `.split` / `.charAt` | `Intl.Segmenter` graphemes; first+last; fallback icon — Avatar fallback path in units |
| Orphaned `—` / empty role line | Placeholder for missing optional | Omit line, or reserve height intentionally |
| “1 members” / “0 member” | Hardcoded plural | `Intl.PluralRules` or per-count strings |
| Number jitter / column misalign | Proportional figures | Tabular nums via theme/type props if exposed; else justified chrome |
| Raw `1284` / float / `NaN` | Unformatted number | `Intl.NumberFormat`; null guards |
| Long translated button label overflows | Fixed width | Control `fullWidth` only when intended; else content width + `min` from design — no fixed `width` CSS on Vira roots ([styling.md](../viraui-design/styling.md)) |
| Diacritics / tall scripts clipped | Tight leading + overflow hidden | `Text` `lineHeight`; drop clipping on text boxes |
| Broken-image avatar | No error fallback | Initials fallback; cover fit for media |
| Ellipsis with no way to read full value | Truncate alone | `title` / tooltip / detail; a11y name if interactive |
| 1,000-row scroll jank | All rows mounted | Virtualize or paginate — say which |
| Raw `<b>` / `&amp;` / `**text**` | Wrong escaping | Escape at render; never `dangerouslySetInnerHTML` user data |
| Hover-only ••• on touch | Pointer-fine only affordance | Always-visible or focusable control; design [accessibility.md](../viraui-design/accessibility.md) / **viraui-a11y** if audit asked |

## Gotchas

- Demo data that “looks fine” ≠ proof — flip Worst + Empty/One/Huge.
- Fixing Worst must not regress Demo — re-flip all harness states after fixes.
- CSS rewrite leftovers after chrome fixes → [verify.md](../viraui-design/verify.md) before claiming done.

## Validation

- Every applicable catalog row tried
- Widths + zoom + dark/RTL checked when product supports them
- Each break has signature, cause, ladder-aligned fix
