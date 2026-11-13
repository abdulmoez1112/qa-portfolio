# Session log: negative checkout testing (13 Nov 2026)

- Date: 13 Nov 2026, ~18:26-18:28 PKT
- Environment: Chrome (cloud browser), desktop viewport, https://www.saucedemo.com
- Profile: standard_user (fresh login; cart verified empty at start)
- Site context: SauceDemo is a public demo app maintained by Sauce Labs for testing practice; all findings here are against a demo environment, not a live store
- Scope: state and sequence negatives on the checkout flow. Field-level negatives (empty fields, bad postal, long inputs) were covered in the 12 Nov session and are not repeated here.

## Results

| # | Test | Expected | Actual | Verdict |
|---|------|----------|--------|---------|
| N1 | Checkout with empty cart: step one with valid data, Continue, Finish | Flow refuses or warns - an order for nothing should not exist | Reached overview with 0 items, Item total $0, Tax $0.00, Total $0.00; Finish produced "Thank you for your order!" | FAIL |
| N2 | Fresh session, navigate directly to /checkout-step-two.html | Redirect to step one or cart - step two without step one is meaningless | Overview renders with 0 items, Total $0.00, no error, no redirect | FAIL |
| N3 | Fresh session, navigate directly to /checkout-complete.html | No confirmation without an order | "Thank you for your order!" renders in a session where nothing was ever ordered | FAIL |
| N4 | Cancel on checkout step one | Return to cart, cart preserved | Landed on /cart.html, item still in cart (badge 1) | PASS |
| N5 | Cancel on checkout step two | Same as N4 for consistency | Landed on /inventory.html instead of cart; item preserved | PASS with inconsistency note |
| N6 | Revisit step one after cancelling | Data preserved, or explicitly cleared | All three fields empty - silently discarded | Observation (acceptable, but unfriendly) |
| N7 | Complete a real order ($32.39), browser Back from confirmation, click Finish again | Second submission refused - no order exists anymore | Step two re-rendered with Total $0.00 and a live Finish button; clicking it produced a SECOND "Thank you for your order!" confirmation screen | FAIL (frontend guard missing; backend duplicate unverified) |

## Confirmed findings

All four FAILs share one root cause - the checkout flow performs no state validation - and are filed together as [BR-007](../../bug-reports/saucedemo/BR-007-checkout-no-state-validation.md):

1. An order for zero items at $0.00 is accepted and "dispatched" (N1)
2. Any checkout page is reachable directly, in any session state (N2, N3)
3. A phantom confirmation page exists with no order at all (N3)
4. Browser Back after a completed order allows a second submission and a second confirmation screen (N7) - whether the backend records a second order cannot be verified from the UI; there is no order history page in this demo

## Consistency note (not filed)

Cancel returns to the cart from step one but to the inventory page from step two (N4 vs N5). Harmless, but inconsistent; a real product would pick one destination.

## Method notes

- Fresh-session tests (N2, N3) were run after a full logout and re-login; cart badge verified "none" first.
- N7 used a real $32.39 order (1 x Sauce Labs Backpack + tax); the confirmation, badge clear, Back navigation and second Finish were all captured in sequence.
- Nothing here contradicts BR-003 (problem_user field contamination): these runs were all standard_user, so the flow itself, not a seeded profile bug, is what fails.
