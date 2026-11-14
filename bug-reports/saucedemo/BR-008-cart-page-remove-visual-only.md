# BR-008: Remove button on the cart page is visual-only - the item stays in the cart and returns on re-navigation

- Date found: 2026-11-14
- Found by: Abdul Moez
- Test user: standard_user / secret_sauce
- Environment: Chrome (cloud browser), desktop viewport, https://www.saucedemo.com - a public demo/practice app maintained by Sauce Labs. Practice finding against a demo environment, not a live store.
- Severity: High (QA judgment - see Impact)
- Priority: High (QA judgment)
- Status: Open

## Summary

Clicking Remove on the cart page (/cart.html) makes the item's row disappear, but the item is never removed from cart state: the badge keeps its count, the inventory page still shows the item's button as "Remove", and the item reappears on the cart page after any re-navigation. The same click also navigates the user away to /inventory.html without being asked to. Removing the same item via the inventory-page Remove button works correctly.

## Steps to reproduce

1. Log in as standard_user.
2. Add any product (used Sauce Labs Onesie) from the inventory page. Badge shows 1.
3. Open the cart page (/cart.html). The item is listed.
4. Click the item's Remove button.

## Expected vs actual

- Expected: the item is removed from the cart; badge clears; the cart page stays empty on revisit; the user stays on the cart page.
- Actual (UI-observable): the row disappears briefly; the app navigates to /inventory.html on its own; badge still shows 1; the inventory button for the item still says "Remove"; returning to /cart.html shows the item back in the cart.

## Evidence

- Reproduced twice in the 14 Nov exploratory session, with a control: the inventory-page Remove button for the same item clears the badge and the cart permanently.
- Session log with chronological captures: [exploratory cart state session](../../test-cases/saucedemo/exploratory-cart-state-session-2026-11-14.md).

## Scope of evidence

- Verified from the UI: cart state (badge count, inventory button label, cart-page contents after re-navigation) is unchanged by the cart-page Remove.
- Not verified: any backend cart record - the demo exposes no backend view, so this report covers observable UI state only.

## Impact (QA judgment in a demo context)

Severity/priority are QA judgment for a flow of this kind, not validated production impact. In a real store: users cannot correct an order from the cart page; a shopper who believes they removed an item would buy it. The silent failure mode (visual removal, real retention) is worse than an explicit error because the user acts on a false belief.

## Notes

- Compare BR-005 (remove failure as error_user, filed 22 Oct): same symptom class on a seeded profile; this report is the CLEAN profile (standard_user). A cross-profile comparison session is planned.
