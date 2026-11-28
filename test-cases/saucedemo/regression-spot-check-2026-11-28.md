# Regression spot check - saucedemo.com, 28 Nov 2026

Short regression pass on the core cart flow after a few days away from the app.
Ran in Chrome, desktop viewport, logged in as `standard_user`.

## Scope

- Login
- Cart badge add/remove on the inventory page
- Sort dropdown (Name Z to A)
- Cart page contents and remove-from-cart
- Logout

## Results

| # | Check | Expected | Actual | Status |
|---|-------|----------|--------|--------|
| 1 | Log in as standard_user | Lands on /inventory.html | Landed on /inventory.html | PASS |
| 2 | Cart badge on fresh login | Empty cart for a fresh session | Badge already showed 1 item (Sauce Labs Backpack) left over from a previous session | OBSERVED, see note |
| 3 | Remove Backpack from inventory page | Badge clears | Badge cleared | PASS |
| 4 | Add Sauce Labs Bike Light | Badge shows 1 | Badge showed 1 | PASS |
| 5 | Sort by Name (Z to A) | First item Test.allTheThings() T-Shirt (Red), last Sauce Labs Backpack | Matched | PASS |
| 6 | Open cart page | Bike Light listed, QTY 1, $9.99 | Matched | PASS |
| 7 | Remove item from cart page | Cart empty, badge clears | Matched | PASS |
| 8 | Logout from menu | Returns to login page with login form | Matched | PASS |

## Note: cart state persisted across logins (observation)

On a fresh login the cart badge already showed one Backpack, which must have been
left in the cart during a session from a previous day. After logout and a new
login the item was still there, so the cart survives logout for `standard_user`.

For a demo app this may be intentional, but in a real shop it is a privacy and
correctness risk: a shared machine would show the previous user's cart. Worth a
requirement question: should logout clear the cart, or is persistence per user
the intended behavior? Filing it as an observation rather than a defect until
the intended behavior is confirmed.

## What I would add next time

- Re-check the badge after a full browser restart, not just logout/login.
- Repeat checks 2-4 with `problem_user` and `error_user`, whose add/remove
  buttons have known issues (see BR-001, BR-004, BR-005).
