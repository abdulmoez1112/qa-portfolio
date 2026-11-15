# Keyboard-only session: login to cart, 15 Nov 2026

- Date: 2026-11-15
- Tester: Abdul Moez
- Test user: standard_user / secret_sauce
- Environment: Chrome (cloud browser), desktop viewport ~1905x993, https://www.saucedemo.com - a public demo/practice app maintained by Sauce Labs. Practice findings against a demo environment, not a live store.
- Input method: keyboard only (Tab, Enter, arrow keys, Escape). No mouse, no clicks. Focus position and focus styling recorded after each key press.

## Scope and method

Cover the core flow login -> inventory -> add one product -> cart page using only the keyboard, recording:

1. Tab order (does it match the visual order, are all controls reached).
2. Focus visibility (computed `outline`/`box-shadow`/`border` of the focused element, plus screenshots).
3. Operability (can each control be activated with Enter / arrows / Escape).
4. Focus management on dynamic changes (menu open/close, button re-render).

DOM facts (aria attributes, alt text, headings) were read from the live page and are labelled as DOM audit, not as keyboard behaviour.

## Chronological log

### Login page (/)

- Tab walk, 8 presses: Username -> Password -> Login -> (page background) -> cycle repeats. 3 stops, matches visual order. PASS.
- Username filled with per-character keyboard input, Tab, Password filled the same way, Tab to Login, Enter. Reached /inventory.html. Login is fully keyboard-operable. PASS.
- Focus visibility at every stop: computed `outline-style: none`, no `box-shadow`. Screenshot with Password focused shows no visible ring or border change. FAIL (see BR-010).
- DOM audit: both fields carry `aria-label` ("Username", "Password"); no `<label>` elements. Page has `lang="en"`, a title, and only H4 headings (no H1). OBS.

### Inventory page (/inventory.html)

- Full Tab walk, 25 presses. 23 stops: burger menu button -> sort select -> per product (image link, title link, Add to cart button) x6 -> X / Facebook / LinkedIn. Order matches visual order. PASS for the 23 stops.
- The shopping cart link is never landed on. DOM check: `<a class="shopping_cart_link" role="button" aria-label="Cart, empty">` has NO `href` and NO `tabindex`; a programmatic `focus()` call does not move focus to it. Keyboard users cannot open the cart from this page. FAIL (see BR-009).
- Sort select: focused via Tab; ArrowDown changed the selection az -> za and the list re-sorted immediately (first product became "Test.allTheThings() T-Shirt (Red)"). Native select is keyboard-operable. PASS.
- Burger menu: Enter on the button opens it and focus MOVES INTO the menu (lands on "All Items"); Tab walks the menu items (All Items, Dynamic Catalog, About, Logout, Reset App State). PASS on open.
- Escape closes the menu, but focus is lost to the page background instead of returning to the burger button. FAIL (focus management; recorded as finding F3, not yet filed).
- After that focus loss, the next Tab resumed from the sort select (the position AFTER the last focused element) - Chrome's sequential focus starting point; behaviour varies by browser. OBS.
- Add to cart: Tab to "Add to cart" (Sauce Labs Backpack), Enter. Badge becomes 1, the cart link's aria-label updates to "Cart, 1 items", and the button morphs to "Remove". PASS for operability.
- Focus after that re-render: `document.activeElement` is the page background. The button node was swapped and focus was dropped; a keyboard user must re-tab to their place. FAIL (focus management; recorded as finding F4, not yet filed).
- Deviation (recorded for honesty): during one walk, Enter was pressed one stop late and activated the Bike Light image link, navigating to the product detail page. Confirms links activate with Enter; the flow was restarted from /inventory.html.
- Focused Add-to-cart button style vs an unfocused one: identical (1px dark border, white background, no outline, no shadow). No visible focus indicator anywhere on the page. FAIL (BR-010).
- DOM audit: all six product images have descriptive `alt` text; the sort select has `aria-label="Sort products"`; the cart link's aria-label is dynamic ("Cart, empty" / "Cart, 1 items"). No headings at all on the page - the "Products" title is not a heading element. Each product has two adjacent links to the same destination (image + title), doubling tab stops: 21 stops before the footer. OBS.

### Cart page (/cart.html)

- Reached by direct URL, because the cart icon is not keyboard-reachable (BR-009). This workaround is itself the evidence for BR-009.
- Cart contents persisted (badge 1, Backpack listed).
- Tab walk, 6+ presses: burger menu -> item title link -> Remove -> Continue Shopping -> Checkout -> social links. All key controls reachable and in visual order. PASS.
- `outline-style: none` on every stop here too. FAIL (BR-010).

## Results summary

| # | Check | Result |
|---|-------|--------|
| 1 | Login completable by keyboard only | PASS |
| 2 | Tab order matches visual order (login, inventory, cart) | PASS |
| 3 | Sort select operable with arrow keys | PASS |
| 4 | Burger menu opens with Enter, focus enters menu | PASS |
| 5 | Add to cart operable with Enter; badge + aria-label update | PASS |
| 6 | Cart icon reachable by keyboard | FAIL - BR-009 |
| 7 | Visible focus indicator on interactive elements | FAIL - BR-010 |
| 8 | Focus returned/kept after burger-menu close (Escape) | FAIL - observation F3 |
| 9 | Focus kept when Add-to-cart re-renders to Remove | FAIL - observation F4 |
| 10 | Product images have alt text; dynamic cart aria-label | PASS (DOM audit) |
| 11 | Heading structure (H1 present, page title as heading) | FAIL - observation: no headings on inventory page |

## Findings

- Filed: [BR-009 - cart link not keyboard-operable](../../bug-reports/saucedemo/BR-009-cart-link-not-keyboard-operable.md)
- Filed: [BR-010 - no visible focus indicator](../../bug-reports/saucedemo/BR-010-no-visible-focus-indicator.md)
- F3 (focus lost on menu close) and F4 (focus lost on button re-render) recorded here as observations; candidates for promotion to reports after a repeat run.

## Limitations

- Single browser (Chrome, server-side cloud instance); other browsers' focus behaviour not covered.
- No screen reader run; assistive-technology notes come from DOM attributes (aria-label, alt, roles), not from announced output.
- One test user (standard_user) on a demo app; findings describe this demo environment.
