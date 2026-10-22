# BR-006: Product prices change on every page load (visual_user)

- Severity: High (wrong prices shown to the user)
- Priority: High
- Status: Open (practice finding; demo app seeds this bug intentionally)
- Date found: 2026-10-22
- Author: Abdul Moez

## Environment

- App: https://www.saucedemo.com
- Account: visual_user / secret_sauce
- Browser: Chrome (latest), desktop

## Preconditions

Logged in as visual_user, on /inventory.html.

## Steps to reproduce

1. Note the six product prices after login.
2. Reload /inventory.html and note the prices again.
3. Reload once more and note them a third time.

## Expected result

Prices are the same on every load and match the standard catalog: Backpack $29.99, Bike Light $9.99, Bolt T-Shirt $15.99, Fleece Jacket $49.99.

## Actual result

Prices differ on each load. Backpack, in order of loads: $91.66, $85.29, $21.60. Bike Light: $5.92, $57.67, $30.64. Fleece Jacket: $11.34, $32.04, $84.24. None match the standard catalog.

## Additional notes

- error_user sees the fixed catalog prices on the same page, so the variation is specific to this account.
- A shopper cannot trust any price shown, so this would block purchases in a real shop.
- Practice report against a demo application; no real users affected.
