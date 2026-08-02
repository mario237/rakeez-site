# Rakeez marketing site — redesign

**Date:** 2026-08-03
**Repo:** `rakeez-site`
**Status:** design approved, ready to plan
**Supersedes the visual direction of:** `d14b6e8` "Direction SIGNAL: the site follows the product onto carbon and lime"

---

## 1 · Why this exists

Two reasons, and the second is bigger than the first.

**The identity moved.** The site carries Direction SIGNAL (lime `#C7F04A` on carbon,
cloud `#F2F3F0`). The brand is now **SIGNAL GOLD v3.0**, 1 August 2026 — gold `#F5C518`,
warm cloud `#F5F4F0`, a light default rather than a dark one, and a rewritten geometry
section that replaces flat 2px corners with 12–18px radii and two fixed elevations. The
site is the cheapest surface on which to land a new identity and the easiest to revert,
so it goes first; the portal follows when the partner signs off.

**The site sells a product that was cancelled.** On 2026-07-26 Rakeez abandoned
statutory Egyptian payroll calculation — see `rakeez-portal/CLAUDE.md` invariant #3 and
`docs/superpowers/specs/2026-07-26-salary-and-payroll-redesign-design.md`. The landing
page has not been told. It currently promises:

| Location | Claim | Reality |
|---|---|---|
| `index.html:1868` | "Egypt's Labor Law No. 14 of 2025 — insurance, taxes, the 3% increment, training fund, records — all handled automatically, no consultant" | None of it is computed. All of it is forbidden. |
| `index.html:2049` | Payroll table row: **Social insurance** | Not a deduction Rakeez knows about |
| `index.html:2053` | Payroll table row: **Income & martyrs tax** | Same |
| `index.html:2350` | Feature bullet: **Gross-to-net payroll** | Net is entered; gross is optional and derives nothing |
| `index.html:2307` | Payslip figure: **Gross** | Same |
| `index.html:7,11` | "HR & payroll for Egypt's **real estate** teams" | `CLAUDE.md`: horizontal product, not a vertical |

A prospect who books a demo off this page arrives expecting tax computation. That is a
worse problem than an out-of-date colour, and it is why this is a repositioning rather
than a re-skin.

A third, smaller defect found while surveying: **204 elements carry `data-i18n` but the
Arabic dictionary has 135 keys.** Roughly 69 strings silently stay English when a visitor
presses العربية, because `setLang()` skips any key it cannot find. See §7.4.

---

## 2 · Positioning

### 2.1 Audience

**Any Egyptian company.** The page never names an industry. Branches, shifts, field staff
and commission are described as capabilities, so a brokerage, a clinic chain, a retailer
and a logistics operator each recognise themselves without the page choosing for them.

This is not a style preference. `CLAUDE.md`: *"Rakeez serves any Egyptian company. The
first customer (Taylor, a real-estate startup) is customer #1, not the product's scope."*
The current site inverted that.

Taylor appears **once**, low on the page, as a named customer with one real sentence.

### 2.2 The promise

Rakeez is the **system of record** for a company's people, time and money — and it still
holds the record in July when you re-open March.

Three claims carry the page, in order:

1. **Everything about a person, in one place.** Hire to payslip, in Arabic.
2. **You know the net. So do we.** `net − deductions = payable`. Nothing invented.
3. **The past stays the past.** Effective dating, five-year retention.

### 2.3 Payroll, told honestly

The decision: **make the honest model the pitch**, not a caveat.

The market reason is already written down and it is the strongest copy on the page —
when somebody joins an Egyptian company the only figure they know is the net. Demanding
a gross made HR invent one by adding back deductions they do not know, which then read
as a fact. Rakeez takes the figure that is real.

So the payroll section says, in the product's own voice:

- You enter the **net**. Gross is optional and derives nothing.
- Deductions are the ones **you** recorded — advances, penalties, absence.
- `net − deductions = payable`, and that is the whole sheet.
- Your accountant's figures stay your accountant's. Rakeez keeps the record, the
  history and the Excel.
- Re-run March in July and March's figure is what appears.

The brand book already supplies the line, under the Archivo specimen:
**"Your accountant's figures, recorded and paid."** It becomes the hero subhead.

The Arabic equivalent, also from the brand book:
**«نظام الموارد البشرية والأجور للشركات المصرية.»**

### 2.4 What "compliance" is allowed to mean

The word survives, narrowed to **record-keeping**, which is in scope and true:
Arabic contracts printed from the customer's own uploaded `.docx`, employee documents,
and five-year record retention. `CLAUDE.md`: *"Digital Arabic contracts and five-year
record retention stay in scope — they are record-keeping obligations, not
calculations."*

It may never again mean insurance, tax, the 3% increment, the training fund, EOSB, or
net-from-gross.

---

## 3 · Not looking AI-generated

An explicit constraint, recorded so it is designed for rather than hoped for.

The tells of a generated landing page: indigo and violet gradients; blurred floating
blobs; glassmorphic cards; Inter everywhere; three centred icon-cards of equal visual
weight; invented testimonials with generated faces; obviously fake product screenshots;
and every section the same height and rhythm.

The antidote is already written in SIGNAL GOLD. Held literally, the design system
forbids most of the list by itself:

| Invariant | Consequence for this page |
|---|---|
| **I1** — one signal per view | Exactly one gold element per viewport. Every other CTA is carbon or ghost. See §4.2 — the header and the hero would otherwise both claim it. |
| **I2** — gold is a fill taking carbon type, never white | No white-on-gold anywhere. Carbon on gold measures 11.49. |
| **I3** — gold is never text on a light ground | No gold headlines, no gold body copy. Gold on warm cloud is 1.48 and fails. |
| **I5** — figures are mono and tabular | Every EGP figure in IBM Plex Mono with `tabular-nums`, right-aligned. |
| **I6** — one dark tile per view | The eye lands twice per screen, never four times. **This is the rule that kills the equal-weight-card look.** |
| **§9** — four radii, two elevations | No improvised depth. Shadows are neutral carbon at low alpha; never a coloured shadow, never a gold glow. |
| **§9** — one permitted gradient | A single warm radial wash on the canvas, top-right, under 4% opacity. Nothing else. No blobs. |

Three further commitments a generator would not make:

- **The product UI is built in real HTML.** No screenshots, no mockup frames, no
  perspective-tilted browser chrome. The payroll sheet on the page is a real table with
  real type.
- **The data in it is real.** Egyptian names and plausible EGP figures, the same ones
  the brand book uses (Nour Adel 12,000.00 / Kareem Fathy 9,500.00 / Salma Hany
  14,200.00).
- **The Arabic is correct**, not translated-looking — see §5.

Canvas is warm cloud `#F5F4F0`, not white and not dark-violet. That choice alone reads
as designed by a person.

---

## 4 · Page structure

| # | Section | The one thing it does |
|---|---|---|
| 1 | **Header** — pill nav, bilingual toggle, one gold *Book a demo* | Establishes the system's own vocabulary before any copy is read |
| 2 | **Hero** — asymmetric, not centred. Left: claim, subhead, one gold action, one ghost. Right: **the dark tile** — a live payroll sheet, figures counting up once | Claim and proof in one screen |
| 3 | **Trust strip** — Built for Egypt · Arabic and English · Five-year retention · Your data scoped to you. **No logo wall** | Credibility without invention |
| — | ~~**Watch** — the 30-second promo~~ **CUT.** `rakeez-promo.html` still carries the old lime identity and out-of-date product. A stale tour is worse than no tour, so the section, its play button and its three strings are gone. Restoring it is: re-add the section, put `'watch'` back in the gold-owner list, and re-add `w_eye` / `w_h` / `w_play` to the Arabic dictionary | Held until a new promo exists |
| 4 | **The five headaches** — attendance argued over WhatsApp; commission recalculated in a spreadsheet nobody trusts; a contract retyped for every hire; salary history nobody can reconstruct; a month-end that lives in one person's head | Recognition, on general Egyptian pain rather than real-estate pain |
| 5 | **Payroll — the pitch** ⭐ | `net − deductions = payable`, then the **March-in-July demonstration** (§6.3). The section that sells the product's actual philosophy |
| 6 | **Capability bento** — People & org · Attendance, shifts & geo check-in · Leave & requests · Payroll · Commission · Expenses & budget · Contracts from your own `.docx` · Documents · Announcements · Recruitment · Reports & Excel | Breadth, mapped only to what ships (§4.1) |
| 7 | **The employee app** — real phone screens: check-in, my pay, my leave | The surface staff actually touch |
| 8 | **Arabic, properly** — full RTL, Arabic contracts, «أجر» used correctly | The differentiator against imported HR products |
| 9 | **Your data** — row-level tenant scoping, signed expiring document links, five-year retention | Answers the CFO's question |
| 10 | **Tailor Investments** — one real customer, one real sentence | Proof, singular |
| 11 | **CTA** — the existing Formspree demo form, re-skinned | Conversion |
| 12 | **Footer** | |

### 4.1 The capability list is bounded by what exists

Every bento tile must correspond to a shipped Filament resource or employee page. The
authority is `rakeez-portal/app/Models/` and `app/Filament/`:

> Announcement · AttendanceRecord · Branch · CommissionEarning · CommissionPlan ·
> Company · Contract · ContractTemplate · Deduction · Department · Employee ·
> EmployeeDocument · Expense · ExpenseCategory · JobPost · LeaveRequest · LeaveType ·
> MonthlyBudget · Position · ProfileChangeRequest · RecurringBill · SalaryRecord ·
> Shift · Team · TeamMembership · User

Employee panel: Check-in · Home · My Announcements · My Attendance · My Documents ·
My Leave · My Pay · My Profile · Change Password.

**Recruitment is on the `recruitment` branch and not yet merged.** It may appear on the
page only if it has shipped by build time; otherwise it is held back. No tile describes
something that does not exist.

### 4.2 Who holds the gold — resolving I1 against a sticky header

The header carries a *Book a demo* CTA and the hero carries a primary action. Both want
to be gold, and I1 forbids that: two gold elements in one viewport and neither reads as
the action.

The rule: **the gold belongs to whatever is the visitor's next step at that scroll
position.**

- While a section that owns a gold action is in view, that section's action is gold and
  the header's CTA is a **ghost** — carbon type, hairline border, no fill.
- In the gaps between those sections, the header's CTA takes the gold fill.
- They are never both gold at any scroll offset, including mid-transition.

**Implementation note, added after building it.** The first cut compared `scrollY`
against the hero's height. That was wrong, and the browser audit found it: an offset
comparison only knows about the hero, so the armed header CTA ended up sharing viewports
with the play button, the app's check-in button, the demo form's submit, and five gold
rules in the problem cards. The correct version is an `IntersectionObserver` over every
section that owns a gold action; the header arms only when that set is empty.

Two things that scan cannot see, and which must be maintained by hand:

- **Pseudo-elements.** The month scrubber's thumb is gold and is a
  `::-webkit-slider-thumb`, so no sweep of `backgroundColor` will ever find it.
  `#payroll` is in the owner list because of it.
- **Decoration masquerading as signal.** The five 34×2px rules in the problem cards were
  gold. They are decoration, and the brand book is explicit that gold is for actions and
  never decoration — they are carbon now.

Verified by scrolling the whole page in a real browser and counting, not by intention
(§8).

### 4.3 The logo, in both directions

The header shows the **Latin wordmark in both languages**. The brand string is Latin in
`lang/en` and `lang/ar` alike — «ركيز اسم علم», a proper noun — so RTL mirrors the
layout around the wordmark without replacing it. The Arabic logotype and the bilingual
lockups exist in the brand repo but are not used on this page; introducing a second
brand form on a toggle would make the identity read as two identities.

---

## 5 · Bilingual

**Full parity. Every visible string.** No silent English fallback anywhere.

- English loads first, `dir="ltr"`; العربية toggles to `dir="rtl"`. This matches the
  mobile app's 2026-07-28 decision to default to English.
- Latin is **Archivo**, Arabic is **Rubik**, figures are **IBM Plex Mono** — all three
  already loaded, all three the design system's faces. Rubik is swapped by
  `html[dir="rtl"]`, never by locale.
- Arabic line-height **+0.15** over Latin. `letter-spacing: 0` always — never track
  Arabic. Never faux-bold; use a real weight.
- **Full RTL mirroring, except**: numbers, clocks, money columns and charts do not
  mirror. A payroll column stays a payroll column.
- The brand string stays Latin **Rakeez** in both languages — «ركيز اسم علم», a proper
  noun. The Arabic logotype file is a logotype, not a translated string.
- Vocabulary is governed by `rakeez-portal/docs/localisation/GLOSSARY.md`, which is
  non-optional before touching any Arabic string. English says **salary**; Arabic says
  **«أجر»**. Do not drift back to "wage".
- Both directions are opened in a real browser before the work is called done (§8).

---

## 6 · Motion

Every value is taken from §9 of the brand book, so site and product move identically.

### 6.1 The tokens

| Token | Value |
|---|---|
| State change | 120ms |
| Panel | 200ms |
| Section / page | 320ms |
| Ceiling | **400ms** |
| Ease in | `cubic-bezier(0.2, 0, 0, 1)` |
| Ease out | `cubic-bezier(0.4, 0, 1, 1)` |

**No spring, no elastic, no overshoot.** This is a brand-book rule, not a preference.

### 6.2 The inventory

| Element | Motion |
|---|---|
| Hero figures | Count up **once on load**, never re-animate |
| Section reveal | Opacity + 8px rise, 320ms, staggered 60ms within a group, **fires once** — the existing `IntersectionObserver` already `unobserve`s and is kept |
| Payroll sheet | Rows resolve in sequence: net lands, deduction subtracts, payable settles. Once |
| Date scrubber | Figures crossfade at 120ms — tabular, so nothing reflows |
| Pill nav | The dark pill **slides** between items, 200ms |
| Phone screens | Cross-dissolve on a 320ms cycle — **the one looping motion on the page**, see §6.4 |
| Header | Condenses past 60px scroll (already implemented, kept) |

### 6.3 The March-in-July demonstration

The one piece of motion that is an argument rather than decoration.

A month scrubber sits above a two-row salary sheet. Dragging it back to March re-renders
the same employee's figure **as it was in March**, not as it is now — the point being
that `Employee::netSalaryOn()` reads a dated series rather than "the current salary".
A caption states it plainly: *re-run March in July and March is what you get.*

Implemented as a static lookup table of dated values in the page's own JS. It
demonstrates the product's behaviour; it does not call the product.

### 6.4 Never

Parallax. Scroll-jacking. Marquees. Typewriter text. Animated gradients. Auto-playing
video with sound. Anything that moves while the visitor is reading.

**The phone carousel is the single exception**, and it is fenced so it does not become
one: it is the only motion on the page that loops, it advances only while its own
section is in the viewport (the same `IntersectionObserver` that drives reveals pauses
it otherwise), it carries a visible control so a visitor can stop it, and it holds each
screen long enough to be read rather than glimpsed. Under `prefers-reduced-motion` it
does not advance at all — it renders one screen and the control moves between them.

### 6.5 Reduced motion

`@media (prefers-reduced-motion: reduce)` → **opacity only**, per the brand book.
Count-ups jump straight to their final value. The scrubber still works; it simply does
not crossfade. Nothing becomes unusable and nothing becomes invisible.

---

## 7 · Build

### 7.1 Shape

**One static `index.html`.** No framework, no build step, no dependencies, no package
manager. Deploying is copying a file. This is what the site is today and there is no
reason it should become anything else.

The file is **rewritten**, not patched. The current one is 2,703 lines whose token names
mean the opposite of what they say.

### 7.2 Tokens

Named properly this time — `--rk-gold-400`, `--rk-canvas`, `--rk-carbon`, `--rk-t2`.
The current file opens with a comment apologising that `--teal` now means carbon and
`--ochre` means lime, deferring the rename because it touched 159 references. A full
rewrite is the moment that debt costs nothing to clear.

**All eleven gold stops are pasted longhand.** Invariant I4 forbids deriving them:

```
--rk-gold-50 : #FEFBE8    --rk-gold-500: #D4A710
--rk-gold-100: #FDF3BF    --rk-gold-600: #B08A0B
--rk-gold-200: #FBEA93    --rk-gold-700: #8C6D08
--rk-gold-300: #F8DC5C    --rk-gold-800: #6B5306
--rk-gold-400: #F5C518 ←  --rk-gold-900: #4C3B04
   the signal              --rk-gold-950: #2E2302
```

Surfaces — light, the default and the only ground this page uses:

```
--rk-canvas  : #F5F4F0   warm cloud
--rk-card    : #FFFFFF   1.10 on canvas — the shadow is what makes it a card
--rk-raised  : #EFEEE9
--rk-hair    : #E3E1DA
--rk-divider : #CFCDC4
--rk-carbon  : #121212   text and the one dark tile · 17.02 on canvas
--rk-t2      : #595B54   6.26
--rk-t3      : #6A6C64   4.84
--rk-cobalt  : #2A3BE8   links, focus rings · 6.60
```

Dark values are carried for the one dark tile and the hero panel:
`--rk-dark-card #1A1A19` · `--rk-on-dark #F5F4F0` (15.83) ·
`--rk-on-dark-2 #9FA09B` (6.61) · `--rk-on-dark-3 #858680` (4.74) ·
`--rk-cobalt-400 #6B76EF` (4.53 — the floor of the whole system; do not darken it).

States, light twins:

```
--rk-ok   : #177A52   5.33
--rk-warn : #A34A06   5.93
--rk-bad  : #B33023   6.24
```

**`#F2A93B` is never restored.** It sits 10.9° from gold and would read as a dimmer
version of the action. Warn is `#A34A06` on light, `#F08A34` on dark.

A state is a **tinted pill with coloured type and its word written out**; the action is
a **solid gold fill with carbon type**. Different objects, not different shades — colour
alone never carries the distinction. Every state pill carries its word.

### 7.3 Geometry and type

Radius: **18px** card/tile/panel · **12px** button/input · **8px** chip/tag ·
**999px** pill. No other values.

Elevation, two depths only:

```
e1  0 1px 2px rgba(18,18,18,.04), 0 8px 24px rgba(18,18,18,.06)
e2  0 2px 4px rgba(18,18,18,.06), 0 16px 40px rgba(18,18,18,.10)
```

Type scale, 1.25 ratio: Display 64/700/−0.035em · H1 40/700/−0.03em ·
H2 28/600/−0.02em · Body 17/400/1.55 · UI label 14/500 · Eyebrow 11/mono/0.1em.
Tracking is −0.03em above 32px and 0 below.

Icons: **Lucide**, 24px canvas, 20px live area, 1.5px stroke, butt caps, miter joins.
Carbon on light, cloud on dark, **never gold** — gold is for actions, not decoration.
Two sizes only, 20 and 24. Inlined as SVG; no icon font, no icon package.

Focus ring: **2px cobalt at 2px offset**, never gold, because a focus ring is not an
action.

### 7.4 Bilingual mechanism

The existing mechanism is kept unchanged in shape: snapshot the English strings out of
the DOM on load, swap `innerHTML` per `data-i18n` key on toggle. It is the laziest thing
that works and it works.

Two changes:

1. **The dictionary is completed to 100% parity.** Every `data-i18n` and `data-i18n-ph`
   key gets an Arabic entry.
2. **A parity check is added** — a few lines, guarded so it costs nothing in production,
   that walks every `data-i18n` key and logs any without an Arabic entry. The 69-string
   gap that exists today was invisible precisely because `setLang()` silently skips
   missing keys; the check makes a regression loud.

### 7.5 Assets

- **The favicon is replaced.** The current one is an inline data-URI drawing a symbol in
  `#0E5E58` — the *teal* brand, two generations stale — and the brand has no symbol at
  all. It is a wordmark, and the app icon is a crop of its R.
- Copy from `rakeez-portal/docs/brand/logo/`: `rakeez-favicon.svg`,
  `rakeez-appicon-carbon.svg`, `rakeez-wordmark.svg` (the `currentColor` variant,
  inlined into the header so it inherits).
- Logo rules: clear space on all sides equals the cap-height of the R, applied in
  layout because the viewBoxes are cropped tight. Minimum 72px on screen. Never on
  imagery without a solid panel. No outline, shadow, gradient, stretching or
  re-spacing. All caps, always.
- **Fonts stay on the Google Fonts CDN** (Archivo, Rubik, IBM Plex Mono) with the
  existing `preconnect`. Self-hosting is a real improvement for a page whose market has
  slow mobile connections, but it is a separate change with its own testing and it is
  not in this scope.

### 7.6 Files touched

| File | Change |
|---|---|
| `index.html` | Rewritten |
| `rakeez-promo.html` | Re-skinned to gold; content unchanged |
| `rakeez-favicon.svg` | New — copied from brand |
| `rakeez-appicon-carbon.svg` | New — copied from brand |
| `rakeez-wordmark.svg` | New — copied from brand, inlined in header |

Nothing else. No `package.json`, no CI, no CSS build.

---

## 8 · Done means

- [ ] No statutory claim survives anywhere in either language — insurance, tax, the 3%
      increment, training fund, EOSB, gross-to-net. Grep both languages; the Arabic
      strings are not reachable by an English grep.
- [ ] No real-estate framing survives — title, meta description, body, Arabic, and the
      `og:`/social tags.
- [ ] Every bento tile maps to a shipped model or panel page (§4.1).
- [ ] Arabic dictionary parity is 100%, and the parity check reports zero missing.
- [ ] The gold ramp is authored longhand, not derived.
- [ ] One gold element per viewport, and one dark tile per view. Verified by scrolling,
      not by intention.
- [ ] Every EGP figure is Plex Mono, `tabular-nums`, right-aligned.
- [ ] `prefers-reduced-motion` produces a fully usable page with opacity-only
      transitions.
- [ ] Opened in a **real browser** at 375 / 768 / 1440, in **both** directions. A page
      that has only been read as source has not been checked — six bugs in a past
      session were visible only by clicking.
- [ ] The Formspree demo form still submits.

---

## 9 · Deliberately not in scope

- **Pricing.** No numbers exist to publish. The CTA says talk to us.
- **Testimonials beyond Taylor.** Invented social proof is the fastest way to look
  generated, and there is one real customer.
- **Self-hosted fonts** (§7.5).
- **A drawn Arabic logotype.** The current one is typeset in Rubik and correctly shaped
  — ز final, ي medial, ك initial, ر isolated — and usable now. A real Arabic logotype is
  a drawing job for a native reader, and it is tracked as an open item in the brand
  repo, not here.
- **Porting SIGNAL GOLD into the portal.** The site goes first by decision; the portal
  follows on the partner's sign-off.
