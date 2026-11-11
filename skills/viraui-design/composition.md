# High-risk composition

**When to read:** Field ownership, Dialog / Popover / Menu / Toast / ToggleGroup / Select / Autocomplete / OTPField / NumberField trees, or any compound assembly before inventing parts.

Canonical **shapes** only. Full props/defaults → specs `components/<id>/` (`meta` → `props` → `usage` → `patterns`) + types verify. Prefer high-level parts (`Sheet`, `Popup`, `Banner`) over reimplementing Portal/Positioner.

Lower-risk (`Accordion`, `Disclosure`, `Grid`, `Masonry`, `Skeleton`, `Tabs`, `Tooltip`, `Gauge`): follow surface units (`Tooltip.Provider` shared delay; grouped adjacent triggers → `Tooltip.createHandle` + payload so Content morphs, no close/reopen flash; `Skeleton.Overlay` child-sized placeholders; `Disclosure` = `Trigger` + `Panel` one section — not Accordion; `Gauge` = round domain root + SVG parts, optional `GaugeControl` — linear ranges stay `Slider`). Overlay enter/exit → **viraui-motion**.

`BreakpointsProvider` / `DirectionProvider` **opt-in**, not Dialog/Tooltip/Toast overlay shell. Discipline (CSS `@media`/`@container` first + shared em map, `useBreakpoints` structure/props, RTL + `dir` on `html`, Stack flex vs LTR/RTL) → [responsive.md](responsive.md) → specs `breakpoints` / `direction-provider` units.

## Field ownership

`Field` from `@base-ui/react`, not `@viraui/react`. `Textfield` (unless `controlOnly`), `Textarea`, `Select`, `Autocomplete`, `OTPField`, `NumberField` own `Field.Root` — never double-wrap.

Standalone `Checkbox` validation needs Base UI Field:

```tsx
import { Field } from '@base-ui/react';
import { Checkbox } from '@viraui/react';

<Field.Root name="terms">
  <Checkbox label="Accept terms" />
</Field.Root>;
```

`Fieldset` only when choice group needs shared legend, description, or error. No shared group copy → `RadioGroup` / `CheckboxGroup` may sit in `Field.Root` directly.

### Custom field labels

`Textfield`, `Textarea`, `Select`, `Autocomplete` render `label` via internal `FieldLabel` (`Text` `size="s"` `weight="semibold"`). Prefer string for plain text.

Side action / badge / rich row (e.g. “Forgot password?”)? Pass ReactNode. Match plain-label title with public `Text` `size="s"` `weight="semibold"`. Extra bits own size/tone (link → `size="xs"`). Layout: `Stack` row + `hAlign="space-between"` + cluster gap `s`. Do **not** import `FieldLabel`. No label CSS. Confirm in surface `patterns` / `usage` / `props`.

```tsx
<Textfield
  type="password"
  label={
    <Stack render={<span />} direction="row" hAlign="space-between" columnGap="s" vAlign="center">
      <Text size="s" weight="semibold">
        Password
      </Text>
      <Text render={<a href="#forgot" />} size="xs">
        Forgot password?
      </Text>
    </Stack>
  }
/>
```

## Dialog

Root indent shell = bootstrap — **viraui-setup** [bootstrap.md](../viraui-setup/bootstrap.md) / [frameworks.md](../viraui-setup/frameworks.md). Exact parts → `components/dialog/patterns.xml` + `usage.xml`.

```tsx
<Dialog.Provider>
  <Dialog.IndentBackground />
  <Dialog.Indent>
    <main>
      <Dialog>
        <Dialog.Trigger render={<Button>Open settings</Button>} />
        <Dialog.Sheet title="Settings" description="Manage preferences">
          {/* body */}
          <Dialog.Close render={<Button variant="secondary">Done</Button>} />
        </Dialog.Sheet>
      </Dialog>
    </main>
  </Dialog.Indent>
</Dialog.Provider>
```

Indent optional. Without effect: `Dialog`, `Trigger`, required-title `Sheet`, optional `Close`. Nested `Dialog` inside `Sheet` = drill-down. Non-modal: confirm props in units (no invented `showBackdrop`).

## Popover

Styled sheet:

```tsx
<Popover>
  <Popover.Trigger render={<Button>Options</Button>} />
  <Popover.Sheet title="Options" description="Choose an action">
    {/* body */}
    <Popover.Close render={<Button variant="secondary">Close</Button>} />
  </Popover.Sheet>
</Popover>
```

Unstyled sheet owns chrome + accessible heading — `components/popover` units. Detached/multiple triggers: `Popover.createHandle()` when documented. Don't invent non-public parts (e.g. `Popover.Arrow`).

## Menu

```tsx
<Menu>
  <Menu.Trigger render={<Button>Sort</Button>} />
  <Menu.Popup>
    <Menu.RadioGroup defaultValue="asc" label="Order">
      <Menu.RadioItem value="asc">Ascending</Menu.RadioItem>
      <Menu.RadioItem value="desc">Descending</Menu.RadioItem>
    </Menu.RadioGroup>
  </Menu.Popup>
</Menu>
```

Don't wrap `Menu` in `Popover` — Menu owns portal, positioning, keyboard. Confirm parts in `components/menu` units.

## Toast

Root `Toast.Provider` + viewport mapping = bootstrap — **viraui-setup**. Manager / Banner shapes:

```tsx
const toastManager = Toast.createToastManager();

function ToastRegion() {
  const { toasts } = Toast.useToastManager();
  return (
    <Toast.Portal>
      <Toast.Viewport>
        {toasts.map((toast) => (
          <Toast.Banner key={toast.id} description={toast.description} toast={toast} />
        ))}
      </Toast.Viewport>
    </Toast.Portal>
  );
}

<Toast.Provider toastManager={toastManager}>
  <App />
  <ToastRegion />
</Toast.Provider>;

toastManager.add({ title: 'Saved', description: 'Changes stored.' });
```

Anchored / action children → `components/toast` units. Viewport alone renders nothing — map manager toasts → `Toast.Banner`.

## ToggleGroup

```tsx
<ToggleGroup aria-label="Editor options">
  <ToggleButton aria-label="Pin" restingIcon={<Pin />} value="pin" />
  <ToggleButton aria-label="Mute" restingIcon={<Mute />} value="mute" />
</ToggleGroup>
```

Each item: distinct `value`, icon slot, accessible name. Never `ToggleButton` children.

## OTPField

Compound `OTPField` / `Input` / `Separator` (no public `.Root`). One Field for label/helper. Exactly `length` Inputs — no auto-spawn. Default slots = Textfield `controlOnly`; host always native `input` (no Input `render`). Group via Stack + `Separator`. Equal-grow via `fullWidth`. Invalid+dirty (and `onValueInvalid`) = built-in one-shot slot wiggle — keep error copy. Remaining-slot names → `components/otp-field` units.

```tsx
<OTPField length={6} label="Verification code">
  <OTPField.Input />
  <OTPField.Input />
  <OTPField.Input />
  <OTPField.Input />
  <OTPField.Input />
  <OTPField.Input />
</OTPField>
```

## NumberField

Single public `NumberField` (no `.Root` / `.Input`). Owns Base UI value/bounds/`name`, Field chrome, steppers, scrub, width. Don't export Group/Decrement/Increment/ScrubArea. Placement / scrub / `fullWidth` (input grows, steppers compact) → `components/number-field` units.

```tsx
<NumberField defaultValue={100} name="amount" label="Amount" description="Local currency." />
```

## Select and Autocomplete

Both own field + popup chrome. Don't add `Field.Root`. Confirm `Option` / `Group` / `Item` / `empty` / `modal` in units — don't invent parts.

```tsx
<Select label="Status">
  <Select.Option value="open">Open</Select.Option>
</Select>

<Autocomplete label="Tag" empty="No tags found">
  <Autocomplete.Item value="feature">feature</Autocomplete.Item>
</Autocomplete>
```

## Validation loop

1. Open specs `patterns` / `usage` + types for compound.
2. Diff planned parts vs units — stop on undocumented names.
3. `meta` has `<base_ui>` → open Base UI API for pass-through (Vira may wrap/regroup) — [discovery.md](discovery.md). Unsure → ask.
4. Confirm Field ownership (no double-wrap; Base UI `Field` when required).
5. Confirm overlay titles / names; omit dup widget ARIA — [accessibility.md](accessibility.md).
6. Enter/exit motion → **viraui-motion** hub + one ref.

## Gotchas

- Invented parts (`Dialog.Body`, `Popover.Arrow`, `showBackdrop`).
- Double-wrapping Textfield/Select/Autocomplete/OTPField/NumberField in `Field.Root`.
- Importing `Field` from `@viraui/react`.
- Importing internal `FieldLabel` or inventing label CSS for rich labels — ReactNode `label` + `Text` matching FieldLabel (`s` / `semibold`).
- Wrapping `Menu` in `Popover`.
- `ToggleButton` / icon-only controls with `children`.
- Toast viewport without mapping toasts → `Banner`.
- Copying APG sample roles onto Dialog/Popover parts.
- Skipping required styled `Sheet` `title` when units require it.

Routing → [component-matrix.md](component-matrix.md). Props → [discovery.md](discovery.md) → specs units.
