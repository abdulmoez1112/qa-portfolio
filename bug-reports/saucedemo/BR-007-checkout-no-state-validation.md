# BR-007: Checkout flow has no state validation - empty-cart orders, direct URL access to any step, double submission

- Date found: 2026-11-13
- Found by: Abdul Moez
- Test user: standard_user / secret_sauce
- Environment: Chrome (cloud browser), desktop viewport, https://www.saucedemo.com - a public demo/practice app maintained by Sauce Labs for testing training. This is a practice finding against a demo environment, not a live store.
- Severity: High (QA judgment - see Scope of evidence and Impact)
- Priority: High (QA judgment)
- Status: Open

## Summary

The checkout flow never checks that an order actually exists. An empty cart can be checked out and "dispatched" at $0.00, every checkout page is reachable directly in any session state including a fresh one, and the browser Back button after a completed order allows a second submission that is also accepted with a second confirmation screen.

## Evidence (all captured 13 Nov 2026, standard_user)

| # | Steps | Observed result |
|---|-------|-----------------|
| 1 | Empty cart -> /checkout-step-one.html -> valid data -> Continue -> Finish | "Thank you for your order!" with Item total $0, Tax $0.00, Total $0.00 |
| 2 | Fresh login, open /checkout-step-two.html directly | Overview renders, 0 items, Total $0.00, no error or redirect |
| 3 | Fresh login, open /checkout-complete.html directly | "Thank you for your order!" with no order in the session at all |
| 4 | Real $32.39 order -> confirmation -> browser Back -> Finish again | Second "Thank you for your order!" confirmation screen (Total $0.00 the second time) |

## Scope of evidence (what is and is not verified)

- Verified from the UI: the client-side guards are missing - every checkout page renders without any cart or order state, and the Finish action is accepted repeatedly.
- Not verified: what the backend records. There is no order history page or API access in this demo, so a second confirmation screen does NOT by itself prove a second order record was created. Rows 1 and 4 establish accepted submissions and rendered confirmations, not confirmed duplicate order rows.

## Expected vs actual

- Expected: checkout requires at least one cart item; step two requires completed step one data; the confirmation page requires a completed order; a submitted order cannot be resubmitted.
- Actual (UI-observable): none of these are enforced anywhere in the flow.

## Impact (QA judgment in a demo context)

Severity and priority are my QA judgment for a flow of this kind, not a validated production impact - this is a demo app with no real money or inventory. If this pattern existed in a real store: money integrity ($0.00 orders reaching "dispatched"), data integrity (order analytics polluted by phantom confirmations), and user trust (a confirmation page that does not necessarily mean an order exists).

## Notes

- Root cause is shared, so the symptoms are filed as one report (see the bug-register methodology note on merging duplicates).
- Related evidence: [negative checkout session log](../../test-cases/saucedemo/negative-checkout-session-2026-11-13.md).
- This is a flow-level observation on the CLEAN profile (standard_user); it is unrelated to the seeded problem_user/error_user/visual_user bugs BR-001..006.
