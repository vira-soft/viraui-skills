# Worst-case catalog

**When to read:** Phase 2 — pick adversarial values for each Phase 1 map field.

Realistic values that break UI. Use applicable rows. Each value = real-user-plausible; note = what it tends to break.

Use `example.com`, `example.org`, or `.test` domains for emails and URLs so fixture never hits real inbox or site.

Hard rule: **plausible or schema-backed, never random.** Prefer actual limit from Zod/Yup/Valibot, DB column, API, or form `maxLength`. If unbounded, say so; still use long but believable value.

---

## People and names

| Value | Breaks |
| -------------------------------------- | -------------------------------------------------------------------- |
| `Aleksandra Wiśniewska-Kowalczyk` | Long hyphenated+diacritics; wraps; hyphen=break point |
| `Christopher Alexander Montgomery III` | Long+suffix; naive first+last initials → `CI` |
| `Konstantin Oberhauser-Wettstein` | Compound; overflows single-line rows |
| `Jo` | Two letters; empty-looking column; initials `J` |
| `J` | One letter; tiny hit target if name=link |
| `Ólafur Darri Ólafsson` | Leading accent; initials `ÓÓ` |
| `Đặng Thị Ngọc Hân` | Vietnamese diacritics; clipped by tight leading + overflow hidden |
| `王秀英` | CJK, no spaces; first/last-word initials fail; breaks anywhere |
| `نور الهدى عبد الرحمن` | RTL; icons/punct wrong without `dir="auto"` / DirectionProvider |
| `Seán O'Brien-Ó Súilleabháin` | Apostrophe+accents; escaping, initials, search |
| `María José de la Cruz y Fernández` | Particles; bad initials / sort |
| `dana` | All lowercase; initials still uppercase |
| `🦊 Fox` | Emoji first; `.charAt(0)` → `�` |
| `👩🏽‍💻 Priya` | ZWJ sequence; `.length` / slice shreds it |
| ` Sam   Lee` | Odd spaces; empty-word initials |
| _(missing)_ | Name absent, email only — must fall back |

## Emails, URLs, identifiers

Unbreakable strings (no spaces).

| Value | Breaks |
| --------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| `bartholomew.fitzgerald@northwind-industries-holdings.example.com` | Classic overflow; pushes siblings off row |
| `a@b.co` | Shortest realistic; length-assuming layouts look empty |
| `first.last+billing-notifications@example.com` | Plus-addressing; bad validation / truncation |
| `ops@sub.department.region.example.co.uk` | Subdomains + two-part TLD |
| `https://example.com/workspaces/acme/projects/q3-launch/docs/9f8e7d6c5b4a?tab=comments&filter=unresolved` | Long URL; end-truncation hides differing part |
| `9f8e7d6c-5b4a-4c3d-8e2f-1a0b9c8d7e6f` | UUID; middle-truncation candidate |
| `Q3 Board Deck — FINAL (revised) v12 [approved by legal].pdf` | File name; end-truncation hides version/ext |
| `IMG_20250914_183022_HDR_portrait_edited_edited.HEIC` | Unbreakable camera name |
| `@a` / `@thisisaverylongusernamethatisallowed` | Handle extremes |

## Labels, titles, and copy from data

| Value | Breaks |
| --------------------------------------------------------- | ------------------------------------- |
| `Senior Product Design Engineer, Platform Infrastructure` | Long title in secondary slot |
| `Invitation expired 12 days ago` | Long status badge squeezes name |
| `Benachrichtigungseinstellungen` | German compound; unbreakable label |
| `Paramètres de confidentialité et de sécurité` | FR expansion ~30% longer |
| Twelve tags on one item | Tag wall — needs `+N` overflow |
| `customer-feedback-from-enterprise-onboarding` | One tag wider than container |
| `Untitled` / empty / `   ` | Collapsed heading / zero-height row |
| `<script>alert(1)</script>` / `&amp;` / `**bold**` | Escaping; must render literal |
| `Line one` + newline + `Line two` | Doubles row height or drops silently |
| 2,000-character pasted description | Clamp / “show more” / textarea growth |

## Numbers and money

| Value | Breaks |
| ---------------------------------- | ----------------------------------------------- |
| `0` | Zero states, empty progress, /0 in percentages |
| `1` | Plurals: “1 members” |
| `1284` | Needs thousands separator |
| `1000000` | Badge width; compact `1M` when precision allows |
| `12345678.9` as currency | `$12,345,678.90` overflows totals |
| `-42.5` | Sign / red / accounting parens |
| `0.1 + 0.2` | Raw float string |
| `142%` / `-3%` | Meters past bounds |
| `null` / `undefined` / `NaN` | Rendered literally |
| `1.284` `de-DE` vs `1,284` `en-US` | Hardcoded separators |
| Live `99` → `100` | Width jump without tabular nums |

Use `Intl.NumberFormat` / `Intl.PluralRules` — no hand-built strings.

## Collections

| Value | Breaks |
| ------------------------------------ | --------------------------------- |
| 0 items | Empty state missing or wrong |
| 1 item | Lone card / “1 of 1” |
| Exactly page size, and page size + 1 | Off-by-one pagination |
| 1,000+ unpaginated | Perf + “Showing 40 of 1,284” copy |
| One item 10× taller | Grid/Masonry stretch |
| Identical names | Name-only distinguishers fail |

## Time

| Value | Breaks |
| --------------------------------- | ----------------------------- |
| Now | “0 seconds ago” vs “just now” |
| 12 days / 11 months / 3 years ago | Relative thresholds |
| Future date | “in 3 days” vs “-3 days ago” |
| `1970-01-01` | Zero timestamp as real date |
| `2025-12-31T23:30:00-08:00` | Day shift across TZ |
| `1,284 hours` duration | Never rolls up to days |

Use `Intl.RelativeTimeFormat` / `Intl.DateTimeFormat`.

## Images and media

| Value | Breaks |
| ------------------------------------ | ---------------------------------------- |
| Avatar URL 404 | Broken icon vs initials fallback |
| No avatar | Fallback size/color parity |
| 4000×200 panorama | Distortion without cover fit |
| 200×4000 tall | Card height blowout |
| Transparent / dark logo on dark mode | Invisible (`data-mode`) |
| Slow image | Layout shift without fixed size / aspect |

## States

| Value | Breaks |
| ------------------------- | ---------------------------------- |
| Loading | Skeleton ≠ final layout |
| API error | Missing state or raw `TypeError…` |
| Partial optional fields | Misaligned rows in one list |
| Every status enum at once | Badge width variance |
| No permission | Disabled actions still need layout |
| Current user in list | “You” + forbidden self-actions |

## Environment

Not data — flip worst case, then change these. Wire RTL/breakpoints/dark → **viraui-design** [responsive.md](../viraui-design/responsive.md) + setup theme / `data-mode` (invent no ad-hoc `768px`).

| Condition | Breaks |
| ----------------------- | ------------------------------------- |
| Container 320px | Every overflow at once |
| Narrow sidebar (~280px) | Full-width designs reused in column |
| 2560px wide | Lines too long; content stranded |
| Zoom 200% / large text | Fixed heights clip growing text |
| Dark mode | Hardcoded colors / invisible borders |
| `dir="rtl"` | Icons, chevrons, trailing actions |
| Touch | Hover-only actions unreachable |
