# BR-001: "Add to cart" does nothing for three products when logged in as problem_user

- Severity: High
- Priority: High
- Status: Open (practice finding; demo app seeds this bug intentionally)
- Date found: 2026-10-21
- Author: Abdul Moez

## Environment

- App: https://www.saucedemo.com
- Account: problem_user / secret_sauce
- OS/Browser: Windows 11, Chrome (latest), 1920x1080

## Preconditions

Logged in as problem_user, on /inventory.html.

## Steps to reproduce

1. Locate "Sauce Labs Bolt T-Shirt" and click "Add to cart".
2. Repeat for "Sauce Labs Fleece Jacket".
3. Repeat for "Test.allTheThings() T-Shirt (Red)".
4. Observe the cart badge in the header.

## Expected result

Each click adds the product: cart badge increments and the button changes to "Remove" (as it does for standard_user).

## Actual result

Nothing happens for these three products: badge stays unchanged and the button does not switch to "Remove". Other products (for example Sauce Labs Backpack) add correctly. The defect is product-specific, not account-wide.

## Additional notes

- Not reproducible as standard_user on the same products, so this is account-specific data handling, not a general cart failure.
- Related behavior as problem_user: some products that CAN be added (Backpack, Bike Light, Onesie) cannot be removed afterwards via "Remove".
- Practice report against a demo application; no real users affected.
