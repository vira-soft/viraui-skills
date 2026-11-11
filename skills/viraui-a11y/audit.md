**When to read:** Structured APG audit or audit-report shape for ViraUI screen.

# APG audit

Audit only. Compose rules + “what aria for this control?” → **viraui-design** [accessibility.md](../viraui-design/accessibility.md). Overlay part trees: `@viraui/react/specs` units (`patterns` / `usage`) after index.

## Checklist

1. Inventory interactive widgets, landmarks, names (source **and** rendered DOM).
2. Map each Vira widget via [vira-map.md](vira-map.md). Unmapped DOM `role` → [roles.md](roles.md). Unmapped `aria-*` → [properties.md](properties.md).
3. Fetch **only** those pattern URLs. Skip patterns with no in-scope widget.
4. Per pattern: keyboard, roles/states, naming, focus. Compare specs `a11y.xml` / `meta.xml` (+ types) — treat primitive-owned chrome as present.
5. Page-level still required: landmarks, heading outline, icon-only names, live status → **viraui-design** [accessibility.md](../viraui-design/accessibility.md).
6. Report with shape below. Fixes → **viraui-design** (no dup widget ARIA).

## Defaults

| Choice | Default |
| --- | --- |
| Mapping entry | [vira-map.md](vira-map.md) for Vira components |
| Unknown DOM | [roles.md](roles.md) / [properties.md](properties.md) |
| APG fetch | Pattern page only; `examples/` only for concrete keyboard Q |
| Missing ARIA in JSX source | Inspect rendered DOM first |
| Widget chrome fail | Fix via specs units / props — stamp no APG sample attrs |

## Gotchas

- **Never fetch** [APG example-index](https://www.w3.org/WAI/ARIA/apg/example-index/) HTML. Folder tables **are** the index.
- Do **not** copy APG sample `role` / `aria-*` onto Vira parts — Base UI already emits widget chrome.
- Prefer [vira-map.md](vira-map.md) over inventing pattern from raw `role`.
- “No aria in source” ≠ broken — inspect rendered output.
- Separate **page** landmarks/status/focus from **widget** behavior Vira/Base UI owns.
- Custom CSS motion in audit → **viraui-motion** (invent no ms/easing here).

## Validation

Stop when any true:

- Example-index fetched or browsed
- Report recommends adding `role` / `aria-*` Base UI already emits
- Audit mixed with ordinary compose without audit ask or design→a11y route
- Fixes invent widget ARIA instead of specs a11y units + types

## Report

```md
## APG audit

Scope: <files or screen>
Patterns fetched: <url list>

| Widget        | APG          | Result            | Note       |
| ------------- | ------------ | ----------------- | ---------- |
| <Vira or DOM> | <pattern id> | pass / fail / n/a | <one line> |

Page: <landmarks / headings / names — pass or gaps>
Do not add: widget `role`/`aria-*` Base UI already emits
```

`n/a` = no APG pattern, or Vira has no primitive (consumer page semantics only).
