**When to read:** Map Vira `@viraui/react` component → APG pattern URL before fetch.

# Vira → APG pattern

Fetch pattern URL, not example-index. No row = no APG widget pattern; audit page semantics only (**viraui-design** [accessibility.md](../viraui-design/accessibility.md)).

**Same-change:** new/renamed/removed public `@viraui/react` component updates this file same change — APG pattern URL, or n/a / layout / decorative footnote. Rewrite not [roles.md](roles.md) / [properties.md](properties.md) for Vira add/remove (W3C index, not Vira surface). Matrix sync: **viraui-design** [component-matrix.md](../viraui-design/component-matrix.md).

## Checklist

1. Identify public Vira export (not raw DOM role).
2. Look up row below; fetch that pattern URL only.
3. No row → page semantics / specs a11y units only — invent no pattern from APG samples.
4. Layout + decorative components never APG widgets.

## Gotchas

- **Never fetch** [APG example-index](https://www.w3.org/WAI/ARIA/apg/example-index/). This table + [roles.md](roles.md) / [properties.md](properties.md) replace it.
- Do **not** copy APG sample markup onto Vira — map → fetch pattern → compare rendered DOM.
- Prefer this file over [roles.md](roles.md) for known Vira component.
- `LinearProgress`, `Stack`, `Surface`, `Grid`, `Prose`, `SROnly`, decorative effects = no widget pattern — force no Accordion/Button/etc. onto them.
- Decorative effects include `StaticNoise`, `ProgressiveBlur`, `Glow`, `Beam`, `Shimmer`, `Typewriter`, similar non-widget visuals.
- `Interpolator` = effect / composition shell (n/a APG) — inactive face inert; moves no focus.

Base: `https://www.w3.org/WAI/ARIA/apg/patterns/<id>/`

| Vira | Pattern | URL |
| --- | --- | --- |
| `Accordion` | Accordion | https://www.w3.org/WAI/ARIA/apg/patterns/accordion/ |
| `Autocomplete` | Combobox | https://www.w3.org/WAI/ARIA/apg/patterns/combobox/ |
| `Button` / `IconButton` / `ToggleButton` / `ToggleTextButton` | Button | https://www.w3.org/WAI/ARIA/apg/patterns/button/ |
| `ButtonLink` / `IconButtonLink` | Link | https://www.w3.org/WAI/ARIA/apg/patterns/link/ |
| `Checkbox` / `CheckboxGroup` | Checkbox | https://www.w3.org/WAI/ARIA/apg/patterns/checkbox/ |
| `Dialog` | Dialog (Modal) | https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/ |
| `Disclosure` | Disclosure | https://www.w3.org/WAI/ARIA/apg/patterns/disclosure/ |
| `Menu` | Menu Button | https://www.w3.org/WAI/ARIA/apg/patterns/menu-button/ |
| `OTPField` | n/a (Base UI OTP labeling) | — |
| `NumberField` | n/a (Base UI Number Field labeling) | — |
| `Meter` | Meter | https://www.w3.org/WAI/ARIA/apg/patterns/meter/ |
| `IconMeter` | Meter | https://www.w3.org/WAI/ARIA/apg/patterns/meter/ |
| `Gauge` | Meter | https://www.w3.org/WAI/ARIA/apg/patterns/meter/ |
| `GaugeControl` | Slider | https://www.w3.org/WAI/ARIA/apg/patterns/slider/ |
| `Popover` | Disclosure | https://www.w3.org/WAI/ARIA/apg/patterns/disclosure/ |
| `Radio` / `RadioGroup` | Radio Group | https://www.w3.org/WAI/ARIA/apg/patterns/radio/ |
| `Select` | Combobox | https://www.w3.org/WAI/ARIA/apg/patterns/combobox/ |
| `Slider` | Slider | https://www.w3.org/WAI/ARIA/apg/patterns/slider/ |
| `Switch` | Switch | https://www.w3.org/WAI/ARIA/apg/patterns/switch/ |
| `Tabs` | Tabs | https://www.w3.org/WAI/ARIA/apg/patterns/tabs/ |
| `Toast` | Alert | https://www.w3.org/WAI/ARIA/apg/patterns/alert/ |
| `ToggleGroup` | Toolbar | https://www.w3.org/WAI/ARIA/apg/patterns/toolbar/ |
| `Tooltip` | Tooltip | https://www.w3.org/WAI/ARIA/apg/patterns/tooltip/ |
| `Fieldset` | Radio Group / Checkbox (group name) | https://www.w3.org/WAI/ARIA/apg/patterns/radio/ |
| Page landmarks | Landmarks | https://www.w3.org/WAI/ARIA/apg/patterns/landmarks/ |

`LinearProgress` — no APG widget row; determinate vs `value={null}` stays in **viraui-design** [accessibility.md](../viraui-design/accessibility.md). `Interpolator` — no APG widget row; two-face morph shell; faces own semantics; no auto-focus (`components/interpolator/a11y.xml`). `OTPField` — no APG widget row; first slot uses field label; later slots Base UI `Character N of {length}` names (see `components/otp-field/a11y.xml`). `NumberField` — no APG widget row; visible `label` names control; steppers use Decrement/Increment names; optional label scrub (see `components/number-field/a11y.xml`). Layout (`Stack`, `Surface`, `Grid`, `Prose`, `SROnly`, …), `BreakpointsProvider` / `useBreakpoints`, `DirectionProvider` / `useDirection`, decorative effects = not APG widgets.
