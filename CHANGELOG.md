# viraui-skills

## Unreleased

### Patch

- `viraui-design`: add layout **scale floor** — `m` (16px) is the baseline for container gaps and insets; `s` is for tight in-row clusters, `xs`/`2xs` for optical micro pairs only. Fixes agents shipping cramped layouts with `xs`/`2xs` container spacing. Touches `layout.md` (floor table + rules), `verify.md`, `red-flags.md`, `discovery.md`, hub router row, and evals.

### Major

- Consumer install is `npx skills add vira-soft/viraui-skills` (GitHub). skills.sh pack URL is no longer documented.
- Move out of `@viraui/skills` npm package; install via open skills CLI.

## 2026.1.10

### Patch Changes

- [`b95f025`](https://github.com/vira-soft/vira-ui/commit/b95f02531c43c96d074f1d5c851fb2d02a6c995a) - Refactorin skills

## 2026.1.9

### Patch Changes

- [`72a3eee`](https://github.com/vira-soft/vira-ui/commit/72a3eee052bb62bcdce57783bf4c5d23fe62e06f) - Update skills about providers

## 2026.1.8

## 2026.1.7

## 2026.1.6

### Patch Changes

- [`70766ed`](https://github.com/vira-soft/vira-ui/commit/70766edcd0515cc162f7fb1d612d96afa8326207) - Add new toggle effect-shadows to disable shadows

## 2026.1.5

### Patch Changes

- [`3bef879`](https://github.com/vira-soft/vira-ui/commit/3bef8794a77c3b04e63fa6109e7a66d2ca67eb0d) - Rename token corner-shape-squircle into corner-shape to allows different values

## 2026.1.4

### Patch Changes

- [`d2f0986`](https://github.com/vira-soft/vira-ui/commit/d2f09864f9b1f8b6e3d4865625192f7c5c932b7a) - Add `viraui-a11y` for on-demand APG audits (split index files, fetch matching pattern pages only) and route deep a11y debug from `viraui-design`.

- [`b9e034a`](https://github.com/vira-soft/vira-ui/commit/b9e034abb838501b290b0daa144c05f8183798d9) - Add global reduce-motion into preflight

- [`828757d`](https://github.com/vira-soft/vira-ui/commit/828757d531c985d6af55dcb0641d25b316c5d4b6) - Update skills with elevations info

- [`d8e9ac1`](https://github.com/vira-soft/vira-ui/commit/d8e9ac1bc2be6c34ad5df48e58d0a95c902ab25e) - Add new motion skill

- [`37e32b3`](https://github.com/vira-soft/vira-ui/commit/37e32b3080dad92851ace55e5926c9fc15dc05ef) - Add new viraui-a11y skill

- [`d8e9ac1`](https://github.com/vira-soft/vira-ui/commit/d8e9ac1bc2be6c34ad5df48e58d0a95c902ab25e) - Add viraui-motion skill for interface micro-interactions

## 2026.1.0

## 2026.0.39

## 2026.0.38

### Patch Changes

- [`7a76337`](https://github.com/vira-soft/vira-ui/commit/7a76337a45cf6c96f01c288a0999a2d776a2b7a1) - Update container type for Stack and Surface

- [`85ff97c`](https://github.com/vira-soft/vira-ui/commit/85ff97ce4faa15128ca049ccced1ff91b4a75151) - Update Grid to allow fixed width declared columns

- [`85ff97c`](https://github.com/vira-soft/vira-ui/commit/85ff97ce4faa15128ca049ccced1ff91b4a75151) - Opt Grid into fixed-breadth column tracks when `columns` is paired with an explicit `colMinWidth`, so a parent with `overflow: auto` can scroll without shrinking tracks.

## 2026.0.37

## 2026.0.36

## 2026.0.35

## 2026.0.34

## 2026.0.33

## 2026.0.32

### Patch Changes

- [`d12ef13`](https://github.com/vira-soft/vira-ui/commit/d12ef1341bbdd0d5f345fecb3633e0ce02010bb3) - Fix Typewriter effect

## 2026.0.31

## 2026.0.30

## 2026.0.29

## 2026.0.28

### Patch Changes

- [`e74f04a`](https://github.com/vira-soft/vira-ui/commit/e74f04a8b9bf7dd17ca7913909cc030c22c05c97) - Fix slider renderLabel

## 2026.0.27

## 2026.0.26

## 2026.0.25

## 2026.0.24

## 2026.0.23

## 2026.0.22

### Patch Changes

- [`f994d09`](https://github.com/vira-soft/vira-ui/commit/f994d09a03ce4e5d87caaeb5e68e9385639b40b5) - Trim brand color ramps to steps 0–70 by tens (drop 5/20/80/90)

- [`1190cb4`](https://github.com/vira-soft/vira-ui/commit/1190cb48ec26f11ed8dc25fd4a98927540521f86) - Init Grid component

## 2026.0.21

### Patch Changes

- [`3c2cc48`](https://github.com/vira-soft/vira-ui/commit/3c2cc482ab3e0efd09c5e1d7f44d7a09bfde1c8d) - update skills

- [`3c2cc48`](https://github.com/vira-soft/vira-ui/commit/3c2cc482ab3e0efd09c5e1d7f44d7a09bfde1c8d) - Teach `renderValue` (not `showValue`) for Slider, Meter, and LinearProgress in viraui-design skills.

## 2026.0.20

## 2026.0.19

## 2026.0.18

## 2026.0.17

## 2026.0.16

### Patch Changes

- [`3dda040`](https://github.com/vira-soft/vira-ui/commit/3dda040c1a50d0ddf8827f4de1cb60fd85a05547) - Inline brand `global.json` `{base.*}` refs to literal base color values

## 2026.0.15

### Patch Changes

- [`ab7b515`](https://github.com/vira-soft/vira-ui/commit/ab7b515b720836292e23a05a0d4ddbf4935663a9) - Align `viraui-design` with the full public component surface (matrix, composition, a11y, layout) and document same-change public surface sync for guides, stories, and skills.

## 2026.0.14

## 2026.0.13

## 2026.0.12

### Patch Changes

- [`0c7be88`](https://github.com/vira-soft/vira-ui/commit/0c7be88431cb4e42e8128ba06cc81ca1a4698f92) - Add new holofoil effect

## 2026.0.11

## 2026.0.10

## 2026.0.9

## 2026.0.8

### Patch Changes

- [`bbc6d46`](https://github.com/vira-soft/vira-ui/commit/bbc6d467d27bcec37053ef577f0526c3989f040b) - Rename viraui-foundation to viraui-setup

## 2026.0.7

## 2026.0.6

## 2026.0.5

## 2026.0.4

## 2026.0.3

## 2026.0.2

## 2026.0.1
