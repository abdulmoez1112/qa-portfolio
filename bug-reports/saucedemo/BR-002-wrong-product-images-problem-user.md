# BR-002: Product images render as the wrong picture when logged in as problem_user

- Severity: Medium
- Priority: Medium
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

1. View the product images in the catalog grid.
2. Compare with the same page logged in as standard_user (second session or incognito).

## Expected result

Each product shows its own product photo, identical to what standard_user sees.

## Actual result

Several products show an incorrect placeholder image (a dog photo) instead of the product photo. Product names and prices are unaffected, so the defect is limited to image rendering/mapping.

## Additional notes

- Wrong images can hide stock or variant problems from shoppers and erode trust in the catalog.
- Practice report against a demo application; no real users affected.
