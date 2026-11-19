# Responsive / mobile web checklist

A working checklist for manual responsive testing of a web app. Built during the
30-day QA routine and applied to saucedemo.com on 2026-11-19 (see
`test-cases/saucedemo/responsive-viewport-session-2026-11-19.md` for the run log).

Scope note: browser viewport emulation changes layout and UA, but it is not a
physical device. Treat emulation results as leads; confirm real defects on real
hardware before calling them device-confirmed.

## 1. Layout and overflow

- [ ] No horizontal scroll at any target width (`document.documentElement.scrollWidth <= window.innerWidth`).
- [ ] No content clipped, overlapping or unreachable at each breakpoint.
- [ ] Multi-column grids collapse to a readable single column on narrow screens.
- [ ] No large unexplained empty areas inside components (check spacing inside cards/containers, not just around them).
- [ ] Sticky/fixed headers do not cover content when scrolling.

## 2. Navigation

- [ ] Desktop nav collapses into a reachable menu control (burger/icon) at small widths.
- [ ] Menu opens, lists every destination, and each entry is tappable/clickable.
- [ ] Menu closes via its close control and via the expected dismiss gesture.
- [ ] Menu entries match desktop destinations (nothing lost at small widths).

## 3. Controls and tap targets

- [ ] Every interactive element stays visible and operable at each width.
- [ ] Tap target sizes recorded in CSS pixels; compare against WCAG 2.2 SC 2.5.8 (24x24 minimum, AA) and SC 2.5.5 (44x44, AAA).
- [ ] Controls that collapse into icons (e.g. a sort dropdown rendered as a funnel icon) still expose their function to assistive tech (accessible name present).
- [ ] Full-width buttons do not stretch so far they look like static banners.

## 4. Text and images

- [ ] Text wraps without truncation or overlap at each width.
- [ ] Font sizes stay readable without zooming.
- [ ] Images scale proportionally, no distortion, no cropping of meaningful content.
- [ ] Icon-only controls still render their icon visibly.

## 5. Functionality at each width

- [ ] Core flows (login, browse, sort/filter, add to cart, cart, checkout start) complete at the smallest target width.
- [ ] Sort/filter controls still change results (verify actual ordering, not just UI state).
- [ ] Forms remain fillable; labels stay associated with fields.

## 6. Evidence discipline

- [ ] Record exact viewport size, UA string, devicePixelRatio and browser/engine for every run.
- [ ] Label every result "emulated" or "physical device" explicitly.
- [ ] Screenshot anything you call a defect, at the size it occurred.
- [ ] State what was NOT covered (orientations, browsers, physical devices, gestures).
