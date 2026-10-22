# BR-005: "Remove" button does not remove items from the cart (error_user)

- Severity: Medium
- Priority: Medium
- Status: Open (practice finding; demo app seeds this bug intentionally)
- Date found: 2026-10-22
- Author: Abdul Moez

## Environment

- App: https://www.saucedemo.com
- Account: error_user / secret_sauce
- Browser: Chrome (latest), desktop

## Preconditions

Logged in as error_user with Sauce Labs Backpack, Sauce Labs Bike Light and Sauce Labs Onesie already added (cart badge shows 3). On /inventory.html.

## Steps to reproduce

1. Click "Remove" under Sauce Labs Backpack.
2. Check the button label and the cart badge.
3. Click "Remove" under Sauce Labs Bike Light, then check again.
4. Click "Remove" under Sauce Labs Onesie, then check again.

## Expected result

Each click switches the button back to "Add to cart" and lowers the badge by one. After three clicks the badge is empty.

## Actual result

After each click the button still reads "Remove" and the badge still shows 3. No error message is shown. The items cannot be removed from the product list page.

## Additional notes

- error_user is the only account tested for this; not checked against standard_user.
- Combined with BR-004, a user can end up with a cart they cannot correct from the product list.
- Practice report against a demo application; no real users affected.
