# viraui-skills

Agent skills for consuming and building with ViraUI. Install with the open [skills](https://github.com/vercel-labs/skills) CLI — no project dependency.

## Install

```bash
npx skills add vira-soft/viraui-skills
```

## Skills

Each skill is a thin `SKILL.md` action hub plus sibling reference markdown files. Skills are **routers**: they teach index-first discovery against the installed package — they do not embed component encyclopedias.

| Skill           | Action    | Purpose                                                                                            |
| --------------- | --------- | -------------------------------------------------------------------------------------------------- |
| `viraui-setup`  | Setup     | Bootstrap imports, theme CSS, tokens, preflight, `@viraui/foundation` presets, framework entry     |
| `viraui-design` | Consume   | Index-first compose via `@viraui/react/specs/*`, layout discipline, consumer `data-*` pointers     |
| `viraui-motion` | Motion    | Duration/easing tokens, functional vs evocative motion, reduced-motion — Vira parts and custom CSS |
| `viraui-a11y`   | APG audit | Structured APG validation when the user asks for an a11y audit or keyboard/SR debug                |

After your app installs `@viraui/react`, agents read package specs from `node_modules`:

- `@viraui/react/specs/PROTOCOL.md`
- `@viraui/react/specs/index.xml` + `activity-hints.xml`
- `@viraui/react/specs/components/<id>/*.xml`
- `@viraui/react/specs/foundation/*.xml`

On disk: `node_modules/@viraui/react/dist/specs/…`. Types/source verify after units — never first discovery via shell-parse of `dist/components/**` or `*.d.ts`.

`viraui-design` auto-loads on UI task fit even when the user never names the skill; when it composes a screen it loads `viraui-motion` (hub, then matching ref). `viraui-setup` loads for setup/bootstrap symptoms only; `viraui-a11y` loads on audit/debug ask (or from `viraui-design` accessibility).

## Docs

Authoring contract (in `vira-ui`): [skills-package.md](https://github.com/vira-soft/vira-ui/blob/main/docs/skills-package.md)
