# Compatibility spot check: Chrome baseline and cross-browser gaps

Date: 18 Nov 2026, approximately 18:27 PKT. Target: https://www.saucedemo.com/, the public Sauce Labs demo/practice app, not a live store. Account: standard_user. This is a small functional spot check, not a full regression or a cross-browser certification.

## Environment and coverage

| Browser / environment | Execution status | Evidence |
|---|---|---|
| Chrome 156.0.0.0, Linux x86_64, desktop 1920 x 993 CSS pixels | Executed today | Browser-reported version, platform and viewport recorded during the run; results below |
| Firefox | Not run | No Firefox session used |
| Safari / WebKit | Not run | No Safari or WebKit session used |
| Edge | Not run | No Edge session used |
| Mobile browsers / physical devices | Not run | No mobile session used |

Only Chrome was exercised through the available test browser. The other rows are coverage gaps, not passes and not observed failures. Different profiles or viewport sizes in Chrome would still not count as a different browser engine. Cross-browser behavior remains unverified.

## Setup

1. Opened the login page and signed in as standard_user.
2. Found one persisted Backpack from earlier practice. Removed it with the inventory-page Remove button; verified the cart became empty before continuing. This was not a clean-storage launch.
3. Used page controls for interactions and read rendered page data for verification. No checkout submission or order was attempted.

## Results

| ID | Action | Expected | Actual | Result |
|---|---|---|---|---|
| SP-01 | Sign in with the demo standard_user account | Inventory loads | Reached /inventory.html; six products displayed | PASS |
| SP-02 | Select Price (low to high) | Prices are nondecreasing | $7.99, $9.99, $15.99, $15.99, $29.99, $49.99 | PASS |
| SP-03 | Open Backpack detail from inventory | Correct detail page and product | Reached /inventory-item.html?id=4, showing Sauce Labs Backpack at $29.99 | PASS |
| SP-04 | Add Backpack from its detail page | Button changes to Remove; cart count becomes 1 | Both changes observed | PASS |
| SP-05 | Activate the cart icon with a pointer click | Cart lists the added item | Reached /cart.html; one Backpack at $29.99, quantity 1 and badge 1 | PASS |
| SP-06 | Activate Continue Shopping | Return to inventory without losing the cart | Reached /inventory.html; cart count 1 and Backpack button still Remove | PASS |

The Backpack detail navigation in SP-03 happened while targeting its product card; the page transition was checked before continuing. SP-04 was then deliberately executed on the detail page, not on the inventory card.

## Visual check

Inspected a screenshot of the cart at SP-05. The product row, quantity, $29.99 price, badge 1, Remove, Continue Shopping and Checkout controls were readable and did not overlap at this viewport. This is one visual sample on one page, not a site-wide layout verdict. The screenshot is supporting session evidence; this Markdown file does not embed it.

## Interpretation and exclusions

Six checks passed in Chrome in this run. They do not show Firefox, Safari, Edge or mobile compatibility. They also do not close any existing bug report: keyboard access, focus styling, cart-page Remove, negative checkout states and seeded defect accounts were not re-tested here. Pointer access to the cart does not contradict BR-009's earlier keyboard-access finding.

The v2 regression pack remains unexecuted as a complete pack. Today's price-order and detail-link samples overlap parts of it, but do not justify marking the whole pack passed.

## Next execution matrix

When those browsers are available, repeat SP-01 through SP-06 on Firefox and Safari/WebKit with explicit version, OS, viewport and starting cart state. Record actual results separately, then compare failures and layout samples. Do not copy today's PASS values into those rows.
