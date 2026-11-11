# Report format + fix invoke

**When to read:** Phase 5–6 — shape the reply; apply fixes only when asked.

## Phase 5 — Report and stop

Leave the harness toggle running. User flips, looks, decides. **Do not fix yet.**

Tone: matter-of-fact, never smug. Name the break, show the value, give the fix. Short report on a sturdy component is a good result.

### Part 1 — What broke

One row per break, worst first.

Severity:

| Severity    | Meaning                                                            |
| ----------- | ------------------------------------------------------------------ |
| **Broken**  | Unreadable, action unreachable, wrong data shown                   |
| **Ugly**    | Readable but visibly wrong (squished avatar, wrapped badge)        |
| **Fragile** | Fine now; one realistic step from breaking (no limit, no fallback) |

| #   | Severity | Field   | Worst-case value                                                   | What happens                     | Fix                                                                                              |
| --- | -------- | ------- | ------------------------------------------------------------------ | -------------------------------- | ------------------------------------------------------------------------------------------------ |
| 1   | Broken   | `email` | `bartholomew.fitzgerald@northwind-industries-holdings.example.com` | Pushes ••• off the row at ~400px | Stack text column + `Text` wrap props; action content-sized — see [signatures.md](signatures.md) |
| 2   | Ugly     | avatar  | long email sibling                                                 | Avatar squishes                  | Keep avatar content-sized in Stack row                                                           |
| 3   | Ugly     | `count` | `1`                                                                | “1 members”                      | `Intl.PluralRules`                                                                               |
| 4   | Fragile  | `name`  | —                                                                  | No max length in schema/form     | Add matching limit both sides                                                                    |

Every row: `file:line` for the fix location in the Fix cell or under the table.

### Part 2 — Decisions for you

Breaks with more than one right answer (truncate vs wrap, empty role, paginate vs virtualize). One line each: recommendation + why.

### Part 3 — What held up

Worst cases the component already handles — proves the test was real; tells the user what not to touch.

Close with:

- Toggle location (URL or file path) and states
- “Say `fix all` or `fix 1, 3` and I’ll apply them.”

## Phase 6 — Fix on request

| Invoke                       | Behavior                                                     |
| ---------------------------- | ------------------------------------------------------------ |
| `fix all` / `fix 1, 3`       | Apply named fixes from the last report                       |
| Earlier ask included `+ fix` | After report, apply every fix **not** listed under Decisions |

Apply via **viraui-design** (specs units, Stack/Text props, CSS rewrite). Then:

1. Flip harness through **every** state including Demo
2. Confirm each fixed break is gone and Demo did not regress
3. Keep worst-case fixture unless user says otherwise
4. End with [verify.md](../viraui-design/verify.md) ship checklist when UI changed

Toggle stays **dev-only**.
