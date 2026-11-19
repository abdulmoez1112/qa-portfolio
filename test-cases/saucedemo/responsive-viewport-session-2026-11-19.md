# Responsive viewport session - 2026-11-19 (saucedemo.com, emulated sizes)

## Environment (record exactly)

- Site: https://www.saucedemo.com/ as `standard_user` (public demo credentials).
- Browser: cloud Chrome 156.0.0.0, Linux x86_64.
- Emulation: browser viewport override (DevTools-style emulation), devicePixelRatio 1.
- Size A: 390x844 CSS px, iPhone 17.0 Safari UA, mobile emulation ON.
- Size B: 820x1180 CSS px, iPad OS 17.0 Safari UA, mobile emulation ON.
- This is EMULATION. No physical device was used. Touch gestures, landscape
  orientation, Android, real Safari, and the checkout form pages were NOT tested.
- Starting state: cart already contained 1 Sauce Labs Backpack carried over from
  the 2026-11-18 session. Cart persistence across sessions was previously observed
  on 14 Nov; whether persistence is intended product behavior is UNCONFIRMED (no
  requirements source exists for this demo app).

## Results at 390x844 (emulated mobile)

| # | Check | Result | Evidence |
|---|-------|--------|----------|
| M1 | No horizontal overflow on inventory page | PASS | scrollWidth 390 = innerWidth 390 |
| M2 | Products render single-column, images scale | PASS | 6 items, images ~340px wide, no distortion |
| M3 | Burger menu opens, all entries visible and operable | PASS | All Items, Dynamic Catalog, About, Logout, Reset App State; Close control works (screenshot) |
| M4 | Sort control works at mobile width | PASS | Native select rendered as 40x30 icon; selected "Price (low to high)", verified exact order $7.99, $9.99, $15.99, $15.99, $29.99, $49.99 |
| M5 | Cart page layout at mobile | PASS | No overflow; QTY/description readable; Continue Shopping (360x34) and Checkout (360x32) full-width; footer social icons render in a row |
| M6 | Inventory product card internal spacing | OBSERVATION O1 | ~256px of empty vertical space between description and price inside each card (measured: card height 767px, gap 256px); price and Add/Remove button pushed far below content. Visually confirmed in screenshot. Not seen on the cart page item (compact). |
| M7 | Tap target sizes (measurement only) | OBSERVATION O2 | Measured CSS px: burger menu button 20x20, sort select 40x30, Add/Remove 306x34, Checkout 360x32. Measurements only, NOT nonconformance findings: WCAG 2.2 SC 2.5.8 (AA, 24x24) has spacing/equivalent/inline/user-agent/essential exceptions that this session did not evaluate, and SC 2.5.5 (44x44) is AAA, not an AA requirement |

## Results at 820x1180 (emulated tablet)

| # | Check | Result | Evidence |
|---|-------|--------|----------|
| T1 | No horizontal overflow on inventory page | PASS | scrollWidth 820 = innerWidth 820 |
| T2 | Layout switches to list style (image left, details right) | PASS | visually confirmed (screenshot) |
| T3 | Card internal spacing | PASS with note | gap reduced to ~86px (card height 240px) |
| T4 | Sort control | PASS with note | still rendered as collapsed 40x30 icon at 820px; combobox accessible name "Sort products" present |

## Observations (not filed as bug reports)

- O1 and O2 are emulation results on a demo app. Before filing O1 as a layout
  defect or O2 as an accessibility defect, re-test on a physical device: emulation
  can misrepresent rendering, and SC 2.5.8's documented exceptions need evaluation
  against the real layout.
- The burger-menu 20x20 measurement (O2) sits in the target-size area (WCAG 2.2
  SC 2.5.8), distinct from BR-010's focus-visibility criterion (SC 2.4.7). Whether
  2.5.8 is met depends on its exceptions (spacing, equivalent, inline, user agent
  control, essential), which were not evaluated here.

## What was NOT covered

Physical devices, touch gestures, landscape orientation, Android emulation, real
Safari/Firefox/Edge, the login page at small widths, checkout form pages at small
widths, Dynamic Catalog submenu behaviour.
