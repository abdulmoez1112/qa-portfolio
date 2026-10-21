# Test Cases - saucedemo.com Login, Catalog, Cart, Checkout

- Author: Abdul Moez
- Date: 2026-10-21
- Covered by test plan: test-plans/saucedemo-test-plan.md
- Account for TC-003 to TC-010: standard_user / secret_sauce

| ID | Title | Preconditions | Steps | Expected result | Priority |
|----|-------|---------------|-------|-----------------|----------|
| TC-001 | Valid login as standard_user | On login page | 1. Enter username standard_user 2. Enter password secret_sauce 3. Click Login | Redirected to /inventory.html, 6 products visible, no error | Critical |
| TC-002 | Locked-out user sees error | On login page | 1. Enter locked_out_user 2. Enter secret_sauce 3. Click Login | Stays on login page; error "Epic sadface: Sorry, this user has been locked out." shown | High |
| TC-003 | Add single item to cart | Logged in, on inventory | 1. Click "Add to cart" on Sauce Labs Backpack | Cart badge shows 1; button changes to "Remove" | Critical |
| TC-004 | Remove item from inventory page | TC-003 done | 1. Click "Remove" on Sauce Labs Backpack | Cart badge clears; button returns to "Add to cart" | High |
| TC-005 | Sort products Z to A | Logged in | 1. Open sort dropdown 2. Select "Name (Z to A)" | First product is "Test.allTheThings() T-Shirt (Red)"; order fully reversed | Medium |
| TC-006 | Sort price low to high | Logged in | 1. Select "Price (low to high)" | First product is "Sauce Labs Onesie" at $7.99; prices ascend | Medium |
| TC-007 | Cart page shows added items | TC-003 done | 1. Click cart icon | /cart.html lists Sauce Labs Backpack with correct name and $29.99 price | Critical |
| TC-008 | Checkout happy path | TC-003 done | 1. Cart > Checkout 2. Enter First/Last name and postal code 3. Continue 4. Finish | Overview shows item, tax, total; "Thank you for your order!" confirmation shown | Critical |
| TC-009 | Checkout rejects empty first name | TC-003 done, on checkout step 1 | 1. Leave First Name empty 2. Fill Last Name and Postal Code 3. Click Continue | Error "Error: First Name is required"; stays on step 1 | High |
| TC-010 | Logout returns to login page | Logged in | 1. Open burger menu 2. Click Logout | Back on login page; visiting /inventory.html directly is blocked with error | High |

## Execution notes

- Each case should be run in a fresh session (logout or incognito) unless preconditions chain them.
- Record actual result, status (Pass/Fail/Blocked), build/date, and evidence link for every execution.
