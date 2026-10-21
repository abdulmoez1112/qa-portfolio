# BR-003: Checkout "Last Name" input overwrites the First Name field (problem_user)

- Severity: High (blocks checkout)
- Priority: High
- Status: Open (practice finding; demo app seeds this bug intentionally)
- Date found: 2026-10-21
- Author: Abdul Moez

## Environment

- App: https://www.saucedemo.com
- Account: problem_user / secret_sauce
- OS/Browser: Windows 11, Chrome (latest), 1920x1080

## Preconditions

Logged in as problem_user with at least one addable product (for example Sauce Labs Backpack) in the cart; on checkout step 1 (/checkout-step-one.html).

## Steps to reproduce

1. Type "John" into First Name.
2. Click into Last Name and type "Doe".
3. Observe both fields while typing.

## Expected result

First Name keeps "John"; Last Name fills with "Doe"; Continue proceeds to the overview step.

## Actual result

Each character typed into Last Name is written into the First Name field instead: First Name changes from "John" to "D", then "o", then "e". Last Name stays empty, so the form cannot be completed correctly and checkout is blocked.

## Additional notes

- Workaround observed in practice: typing the postal code first can make Last Name accept input, but the first-name overwrite still corrupts the order data.
- Not reproducible as standard_user.
- Practice report against a demo application; no real users affected.
