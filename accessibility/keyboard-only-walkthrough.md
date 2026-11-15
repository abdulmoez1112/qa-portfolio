# Keyboard-only walkthrough: how to test a web app without a mouse

Keyboard-only testing means putting the mouse aside and driving the whole flow with the keyboard. It is the cheapest accessibility test with the highest defect yield: it covers users with motor impairments, screen reader users (who navigate by keyboard), and power users. If a flow cannot be completed, or focus cannot be seen, nothing else about the page's accessibility matters for those users.

Relevant WCAG 2.1 criteria: 2.1.1 Keyboard (A), 2.1.2 No Keyboard Trap (A), 2.4.3 Focus Order (A), 2.4.7 Focus Visible (AA).

## Setup

1. Decide the scope: one complete user flow, start to finish (example below: login -> add to cart -> cart page).
2. Put the mouse out of reach. Every action must be a key press.
3. Keys you need: Tab / Shift+Tab (move focus), Enter (activate links and buttons), Space (buttons, checkboxes), arrow keys (selects, radios, menus), Escape (close dialogs and menus).
4. Open the browser's developer tools console. After each Tab, reading `document.activeElement` tells you exactly what has focus - more reliable than looking, especially when the site hides the focus ring.
5. Record as you go: the focus order, what you pressed, what happened, and anything you could not reach or could not see.

## What to check, in order

### 1. Tab order vs visual order

Tab through the whole page once without interacting. Write down the stop sequence. It should follow the visual reading order (usually top-left to bottom-right). Surprises - jumping columns, skipping a control, landing on hidden elements - are focus-order defects.

### 2. Every control is reachable and operable

Every interactive element must be reachable by keyboard and activatable with Enter or Space. Common failures:

- Fake links/buttons: an `<a>` without `href`, or a `<div>` with a click handler, is invisible to the keyboard. In the console, `element.focus()` not moving focus, or a missing `href`/`tabindex`, confirms it.
- Custom widgets (menus, autocompletes, modals) that open on click only.

### 3. Focus is always visible

At every stop, the user must be able to SEE where focus is. Check the focused element's computed style (`outline`, `box-shadow`, `border`, `background`) against its unfocused state, and confirm with a screenshot. `outline: none` with no replacement style is a WCAG 2.4.7 failure - keyboard operability without visible focus is useless in practice.

### 4. No keyboard traps

You must be able to Tab INTO and OUT OF every component. If focus gets stuck (classic offenders: embedded widgets, modal dialogs, menus that only close on click), that is 2.1.2. Menus and modals should also close with Escape.

### 5. Focus management on dynamic changes

Modern apps re-render constantly. Two patterns to test explicitly:

- Opening a menu/dialog should move focus INTO it; closing it (especially with Escape) should return focus to the trigger. If `document.activeElement` becomes `<body>` after close, focus was dropped.
- When a control you just used is replaced by a re-render (e.g. "Add to cart" morphing into "Remove"), focus should survive or move somewhere sensible. If it drops to the page background, the user must re-tab from the top.

### 6. Supporting DOM audit (not keyboard behaviour - label it separately)

- Form fields have an accessible name (`<label>`, `aria-label`, or `aria-labelledby`) - placeholder alone is not enough.
- Images that carry meaning have `alt` text.
- Headings exist and reflect structure (a page title that is not a heading element gives screen reader users no landmark).
- The page has `lang` and a `<title>`.

## A worked example: saucedemo login-to-cart, 15 Nov 2026

Full log: [keyboard-only session, 15 Nov](../test-cases/saucedemo/keyboard-only-session-2026-11-15.md) (against https://www.saucedemo.com, a public demo app by Sauce Labs).

What a 30-minute run produced:

- PASS: login completable by keyboard; sort select, burger menu, Add to cart, Remove, Checkout all keyboard-operable; product images have alt text.
- FAIL, filed as [BR-009](../bug-reports/saucedemo/BR-009-cart-link-not-keyboard-operable.md): the shopping cart link is an `<a>` with no `href` and no `tabindex` - the entire cart/checkout flow is unreachable without a mouse.
- FAIL, filed as [BR-010](../bug-reports/saucedemo/BR-010-no-visible-focus-indicator.md): no visible focus indicator on any of the 30+ tab stops (`outline: none`, no replacement style).
- Observations recorded for follow-up: focus dropped to the page background when the burger menu closes with Escape, and again when Add-to-cart re-renders as Remove; no headings on the inventory page; duplicate image+title links double the tab stops per product.

## Session checklist

- [ ] Flow scoped and completed (or the blocking point documented)
- [ ] Tab order written down, compared to visual order
- [ ] Every control reached and activated by keyboard
- [ ] Focus visibility checked at each stop (computed style + screenshot)
- [ ] Trap test: into and out of every component, Escape where expected
- [ ] Focus behaviour on open/close and on re-render checked
- [ ] DOM audit (names, alt, headings, lang, title) recorded separately from keyboard behaviour
- [ ] Each failure filed with: the key presses, the element's markup, expected vs actual, WCAG criterion
