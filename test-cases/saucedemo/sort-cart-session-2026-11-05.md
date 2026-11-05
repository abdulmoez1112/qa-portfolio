# Exploratory session log: product sort + cart badge (saucedemo.com)

- Date: 5 November 2026
- Environment: Chrome (cloud browser), https://www.saucedemo.com
- Account: standard_user (practice app credentials published on the login page)
- Duration: ~10 minutes
- Charter: verify the product sort control and the shopping-cart badge counter on the inventory page.

## Results

| # | Check | Steps | Expected | Actual | Status |
|---|-------|-------|----------|--------|--------|
| 1 | Login | Enter standard_user / secret_sauce, submit | Redirect to /inventory.html | Redirected to /inventory.html | PASS |
| 2 | Default sort | Land on inventory page | "Name (A to Z)" applied | Sort value `az`; order: Backpack, Bike Light, Bolt T-Shirt, Fleece Jacket, Onesie, Test.allTheThings() T-Shirt (Red) | PASS |
| 3 | Sort Z to A | Select "Name (Z to A)" | Exact reverse of A-Z | Exact reverse observed | PASS |
| 4 | Sort price low to high | Select "Price (low to high)" | Ascending prices | $7.99, $9.99, $15.99, $15.99, $29.99, $49.99 | PASS |
| 5 | Sort price high to low | Select "Price (high to low)" | Descending prices | $49.99, $29.99, $15.99, $15.99, $9.99, $7.99 | PASS |
| 6 | Badge increments | Click "Add to cart" on 2 products | Badge 1 then 2; buttons flip to "Remove" | Badge 1 -> 2; both buttons flipped | PASS |
| 7 | Badge decrements | Click "Remove" on 1 product | Badge back to 1 | Badge back to 1 | PASS |

## Notes

- All 4 sort options were exercised against the rendered list (not just the dropdown label); the full product order and prices were captured for each.
- No defects found in this session. Sort ties ($15.99 x 2) keep a stable relative order between both price directions.
- This log records only what was actually run in this session, per the repo's evidence rule.

## Evidence

Observations captured live from the page DOM during the session (product names, prices, select value, cart badge) plus a full-page screenshot of the final state (sort: Price high to low, badge 1).
