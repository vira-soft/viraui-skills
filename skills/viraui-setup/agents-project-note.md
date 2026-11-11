# Project agent note (portable)

**When to read:** after installing publishable skills from `vira-soft/viraui-skills`. Paste this into consumer `AGENTS.md` (or host-equivalent) by **default** on skills install so the CSS→props gate fires even when the agent never opens **viraui-design** by name.

Primary triggers remain skill `description` fields + hub gates. This note is the host-agnostic belt — do **not** invent Cursor-only `.cursor/rules` as the source of truth. Mirror this note into a host-native format only if needed.

## Install skills (same source, all hosts)

```bash
npx skills add vira-soft/viraui-skills
```

## Copy into consumer `AGENTS.md` (or host-equivalent)

Paste near the top of the project agent instructions file (default on skills install / refresh):

```markdown
## ViraUI (agent skills)

This app uses `@viraui/react`. Publishable skills install via:
`npx skills add vira-soft/viraui-skills`

- **UI build / edit / style** → load **viraui-design** before JSX or custom CSS (even if nobody named the skill). Props, parts, and layout roots before CSS modules/Tailwind/`style` on Vira roots.
- **CSS rewrite pass (mandatory, mid-draft):** after any new CSS/utility/visual `style` on or around Vira roots, inventory every declaration → public prop / part / `--vui-*` / justify (app chrome or explicit ask) / delete. Do **not** claim done while reinvented props-as-CSS remains. Do not leave a user second pass (“ricontrolla CSS → props”).
- **Charts / graphs / data viz** → **viraui-design** `charts.md` → installed `@viraui/charts/specs` (index-first). Missing packages → install `@viraui/charts` + `@visx/visx` first. No packaged `LineChart`.
- **Transitions / hover-press / overlay motion / motion tokens** → **viraui-motion** (hub + one ref).
- **Explicit APG / a11y audit** → **viraui-a11y**. Ordinary compose-time a11y stays in viraui-design `accessibility.md`.
- **Stress-test / worst-case data / Demo·Worst harness** → **viraui-breakui** (not ordinary compose).
- **Bootstrap / theme / preflight / providers** → **viraui-setup** (ask charts intent early; yes → `@viraui/charts` + `@visx/visx`).
- **Before claiming UI done:** CSS rewrite leftovers = 0, then follow viraui-design `verify.md` — emit the adversarial ship report (CSS rewrite inventory, reinvented props-as-CSS: 0, compose a11y, `adversarial verify: pass`). Do not hand off with open criticals.
```

Same wording for every host. No per-host skill forks.
