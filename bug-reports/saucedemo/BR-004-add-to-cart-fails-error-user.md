# BR-004: "Add to cart" does nothing for three products (error_user)

- Severity: High (items cannot be purchased)
- Priority: High
- Status: Open (practice finding; demo app seeds this bug intentionally)
- Date found: 2026-10-22
- Author: Abdul Moez

## Environment

- App: https://www.saucedemo.com
- Account: error_user / secret_sauce
- Browser: Chrome (latest), desktop

## Preconditions

Logged in as error_user, on the product list (/inventory.html), cart badge empty.

## Steps to reproduce

1. Click "Add to cart" under Sauce Labs Backpack.
2. Click "Add to cart" under Sauce Labs Bike Light.
3. Click "Add to cart" under Sauce Labs Onesie.
4. Click "Add to cart" under Sauce Labs Bolt T-Shirt.
5. Click "Add to cart" under Sauce Labs Fleece Jacket.
6. Click "Add to cart" under Test.allTheThings() T-Shirt (Red).
7. Compare the buttons and the cart badge.

## Expected result

Each click switches the button to "Remove" and raises the cart badge by one. After six clicks the badge shows 6.

## Actual result

Backpack, Bike Light and Onesie switch to "Remove" (badge shows 3). Bolt T-Shirt, Fleece Jacket and Test.allTheThings() T-Shirt stay on "Add to cart" after the click, with no error message. Repeating the click on those three gives the same result.

## Additional notes

- error_user is the only account tested for this; not checked against standard_user.
- No message tells the user the action failed, which makes this worse than a visible error.
- Practice report against a demo application; no real users affected.
