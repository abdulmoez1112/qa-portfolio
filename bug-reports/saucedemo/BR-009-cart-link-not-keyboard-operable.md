# BR-009: Shopping cart link is not keyboard-operable - keyboard users cannot reach the cart or checkout

- Date found: 2026-11-15
- Found by: Abdul Moez
- Test user: standard_user / secret_sauce
- Environment: Chrome (cloud browser), desktop viewport, https://www.saucedemo.com - a public demo/practice app maintained by Sauce Labs. Practice finding against a demo environment, not a live store.
- WCAG: 2.1.1 Keyboard (A)
- Severity: High (QA judgment - see Impact)
- Priority: High (QA judgment)
- Status: Open

## Summary

The shopping cart icon in the page header is an `<a>` element with no `href` attribute and no `tabindex`. It never receives keyboard focus, so a keyboard-only user cannot open the cart page from any page of the shop. The cart and the entire checkout flow are mouse-only.

## Steps to reproduce

1. Log in as standard_user using only the keyboard (Tab / Enter work fine on the login form).
2. On /inventory.html, Tab through the page. Focus visits 23 stops: burger menu, sort select, then per product (image link, title link, Add to cart button), then the social links - and never the cart icon.
3. (Confirmation) In the console, `document.querySelector("a.shopping_cart_link").focus()` does not move focus to the element.

## Expected vs actual

- Expected: the cart link is keyboard-focusable (it is a link to /cart.html) and opens on Enter.
- Actual (UI/DOM-observable): the element's markup is `<a class="shopping_cart_link" role="button" aria-label="Cart, empty">` with no `href` and no `tabindex`; it is skipped by Tab navigation and cannot even be focused programmatically. Its `role="button"` and dynamic aria-label ("Cart, 1 items") suggest assistive-technology intent, but the element never receives focus to be announced in context.

## Evidence

- Full Tab walk of the inventory page (25 presses, focus recorded after each): cart link never landed on. Cart page itself, reached by direct URL, Tabs correctly through Remove / Continue Shopping / Checkout - the block is specifically the cart icon.
- Session log with the chronological walk: [keyboard-only session, 15 Nov](../../test-cases/saucedemo/keyboard-only-session-2026-11-15.md).

## Scope of evidence

- Verified from the DOM and keyboard behaviour in Chrome: element markup, focus() failure, complete Tab order.
- Not verified: screen reader announcement behaviour; other browsers (the markup defect is browser-independent, but focus behaviour was only exercised in Chrome).

## Impact (QA judgment in a demo context)

Severity/priority are QA judgment for a flow of this kind, not validated production impact. In a real store this blocks the purchase flow end to end for keyboard-only users (motor impairments, screen reader users): products can be added, but the cart can never be opened and checkout can never start. WCAG 2.1.1 is a Level A failure - the most basic conformance level.

## Notes

- Related: BR-010 (no visible focus indicator) covers the separate problem that focus, where it does land, is invisible.
- A one-attribute fix (`href="/cart.html"` or `tabindex="0"` plus a key handler) would make this operable; noted for practice completeness, not as prescriptive guidance to the demo's authors.
