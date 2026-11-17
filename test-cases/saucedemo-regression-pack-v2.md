# Regression pack v2: sorting, images, links (saucedemo.com)

Second scripted regression set for the practice app https://www.saucedemo.com, built from what weeks 1-2 of testing taught: the cases v1 did not cover. Account unless stated: standard_user / secret_sauce. Status of every case: Not run (design committed 17 Nov 2026; run results get logged in a dated session log under `test-cases/saucedemo/` and the status column updated then).

Complements: `sorting-and-cart-edge-cases.md` (v1 sorting + cart, TC-SORT/TC-CART), `saucedemo-checkout-test-cases.md` (checkout, TC-001..010), `checkout-boundary-value-tests.md` (checkout form boundaries). Known defects these cases exercise are linked per case (BR-001..010 in `bug-reports/saucedemo/`).

## Sorting (extends v1 with persistence and exact-value checks)

| ID | Title | Preconditions | Steps | Expected result | Priority | Status |
|---|---|---|---|---|---|---|
| TC-R2-01 | Sort selection survives a page refresh | Logged in, on /inventory.html | 1. Sort by "Price (high to low)". 2. Refresh the page. 3. Read the dropdown and the product order. | Record the actual behavior. Expected: either the selection persists (dropdown and order agree) or the app resets to "Name (A to Z)" - log a bug if the dropdown label and the displayed order disagree. | Medium | Not run |
| TC-R2-02 | Price sort low-to-high is exactly correct, including the $15.99 tie | On product list | 1. Sort by "Price (low to high)". 2. Read every price top to bottom. | Order is exactly: $7.99 (Onesie), $9.99 (Bike Light), $15.99 (Bolt T-Shirt), $15.99 (TATT Red), $29.99 (Backpack), $49.99 (Fleece Jacket). The two $15.99 items are adjacent; record their relative order. | High | Not run |
| TC-R2-03 | Sort resets to default after logout/login | Sorted by "Name (Z to A)" | 1. Log out via the burger menu. 2. Log back in. 3. Read the dropdown and product order. | Dropdown shows "Name (A to Z)" and the list is in ascending alphabetical order. (Cart contents persisting across logout/login is expected product behavior per the 14 Nov exploratory session; sort is view state and should reset.) | Medium | Not run |

## Images (motivated by BR-002, wrong images for problem_user)

| ID | Title | Preconditions | Steps | Expected result | Priority | Status |
|---|---|---|---|---|---|---|
| TC-R2-04 | Every product image loads and is distinct | On product list | 1. For each of the six products, check the image rendered (not broken, not a placeholder). 2. Compare the six images. | Six distinct product photos, each matching its product name. No two products share an image; no sl-404 placeholder (the BR-002 symptom). | High | Not run |
| TC-R2-05 | Image alt text matches the product name | On product list | 1. Inspect each product image's alt attribute (DevTools). | Each alt equals its product name exactly, e.g. "Sauce Labs Backpack" (true in the 15 Nov DOM audit - this case guards it staying so). | Medium | Not run |
| TC-R2-06 | Image link and title link reach the same detail page | On product list | 1. For one product, open the image link; note the URL. 2. Go back; open the title link; note the URL. | Both URLs are identical (/inventory-item.html?id=N with the same id). (Two tab stops for one destination is a usability note from the 15 Nov keyboard run, not a failure of this case.) | Low | Not run |

## Links (navigation integrity, incl. the keyboard dimension of BR-009)

| ID | Title | Preconditions | Steps | Expected result | Priority | Status |
|---|---|---|---|---|---|---|
| TC-R2-07 | All six product detail links open the right item | On product list | 1. For each product, click its name. 2. Check the detail page title and the id in the URL. | Detail page shows the same product; the id is stable for that product across runs (Backpack id=4, Bike Light id=0, Bolt id=1, Fleece id=5, Onesie id=2, TATT Red id=3, as in the 15 Nov DOM audit). | High | Not run |
| TC-R2-08 | Footer social links point to official Sauce Labs profiles | On product list | 1. Read the href of the X, Facebook and LinkedIn footer links (do not follow them mid-test; record the targets). | Each href points to a Sauce Labs profile on its network. Record the actual targets on first run; investigate any non-Sauce-Labs or dead target. | Low | Not run |
| TC-R2-09 | Burger menu items navigate where they say | On product list | 1. Open the burger menu. 2. For each item (All Items, Dynamic Catalog, About, Logout, Reset App State), activate it and record the destination; log back in after Logout. | All Items -> /inventory.html; About -> a Sauce Labs page; Logout -> the login page; Reset App State clears the cart badge (true 14 Nov). Dynamic Catalog: record the actual destination (item first seen 15 Nov). | High | Not run |
| TC-R2-10 | Cart link is reachable and operable by mouse AND keyboard | On product list, one item in cart | 1. Click the cart icon; check /cart.html opens with the item. 2. Return; Tab from the top of the page and count stops until the cart icon receives focus; press Enter. | Mouse: /cart.html opens, item listed. Keyboard: the icon receives focus and Enter opens the cart. KNOWN ISSUE: keyboard half currently fails - BR-009 (icon has no href/tabindex; focus() fails). This case is the regression guard for the fix. | High | Not run (blocked by BR-009) |

## Notes

- Cases marked "record the actual behavior" follow the v1 convention (TC-SORT-06, TC-CART-04): first run establishes the baseline, then Expected is tightened and any divergence becomes a bug report.
- Re-run this pack for problem_user, error_user and visual_user where it makes sense (images especially - BR-002 was a problem_user symptom), and compare against standard_user.
- v1's TC-CART-04 (checkout with an empty cart) now has its answer: the app allows it - BR-007.
