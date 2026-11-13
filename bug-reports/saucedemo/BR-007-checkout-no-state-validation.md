# BR-007: Checkout flow has no state validation - empty-cart orders, direct URL access to any step, double submission

- Date found: 2026-11-13
- Found by: Abdul Moez
- Test user: standard_user / secret_sauce
- Environment: Chrome (cloud browser), desktop viewport, https://www.saucedemo.com
- Severity: High
- Priority: High
- Status: Open

## Summary

The checkout flow never checks that an order actually exists. An empty cart can be checked out and "dispatched" at $0.00, every checkout page is reachable directly in any session state including a fresh one, and the browser Back button after a completed order allows a second, empty submission that is also accepted.

## Evidence (all captured 13 Nov 2026, standard_user)

| # | Steps | Result |
|---|-------|--------|
| 1 | Empty cart -> /checkout-step-one.html -> valid data -> Continue -> Finish | "Thank you for your order!" with Item total $0, Tax $0.00, Total $0.00 |
| 2 | Fresh login, open /checkout-step-two.html directly | Overview renders, 0 items, Total $0.00, no error or redirect |
| 3 | Fresh login, open /checkout-complete.html directly | "Thank you for your order!" with no order in the session at all |
| 4 | Real $32.39 order -> confirmation -> browser Back -> Finish again | Second "Thank you for your order!" (Total $0.00 the second time) |

## Expected vs actual

- Expected: checkout requires at least one cart item; step two requires completed step one data; the confirmation page requires a completed order; a submitted order cannot be resubmitted.
- Actual: none of these are enforced anywhere in the flow.

## Impact

- Money integrity: $0.00 orders enter the same "dispatched" state as paid ones.
- Data integrity: order counts and confirmation analytics are polluted by phantom orders.
- User trust: a confirmation page that does not mean an order exists.

## Notes

- Root cause is shared, so the four symptoms are filed as one report (see the bug-register methodology note on merging duplicates).
- Related evidence: [negative checkout session log](../../test-cases/saucedemo/negative-checkout-session-2026-11-13.md).
- This is a flow-level defect and reproduces on the CLEAN profile (standard_user); it is unrelated to the seeded problem_user/error_user/visual_user bugs BR-001..006.
