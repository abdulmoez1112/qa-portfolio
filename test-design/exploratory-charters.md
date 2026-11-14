# Exploratory testing charters: saucedemo.com set

A charter is one sentence that gives an exploratory session its mission without scripting it. Good charters name an area, a question, and room to follow surprises. Each charter below is timeboxed 30-45 minutes and follows the repo's [exploratory session report template](../templates/exploratory-session-report-template.md).

## Charter 1: cart state (EXECUTED 14 Nov 2026)

**Explore how cart state survives the things users do to it - refresh, logout/login, reset, multiple tabs, and removing items from different pages - as standard_user, to discover where the app's idea of the cart and the user's idea of the cart disagree.**

- Why: the cart is the app's only stateful object; state disagreements turn into wrong orders.
- Starting ideas: refresh mid-flow, logout and re-login, Reset App State, a second browser tab, remove from the cart page vs the inventory page.
- Session log: [exploratory-cart-state-session-2026-11-14](../test-cases/saucedemo/exploratory-cart-state-session-2026-11-14.md) - produced new defect [BR-008](../bug-reports/saucedemo/BR-008-cart-page-remove-visual-only.md).

## Charter 2: seeded-error profile under combined actions

**Explore sorting, pagination-free scrolling and cart actions in combination as error_user, to discover whether the seeded failures (BR-004, BR-005) interact - does a failed add change what sorting shows, or a failed remove change what the badge counts?**

- Why: BR-004 and BR-005 were found with isolated single actions; combined actions are where state machines crack.
- Starting ideas: sort Z-A then add, add then sort price high-low, attempt remove after failed adds, badge vs cart-page comparison after each step.
- Status: not yet executed.

## Charter 3: price integrity downstream

**Explore how far visual_user's unstable prices travel - catalog to cart to checkout overview to confirmation - to discover whether BR-006's randomizing prices are cosmetic (display only) or reach the totals a user would pay.**

- Why: BR-006 re-tests (9 Nov) confirmed catalog prices randomize per load; nobody has yet followed a price into the cart and the checkout math. The answer changes the severity reasoning.
- Starting ideas: record catalog price, add item, compare cart and overview prices against the recorded one, check whether tax computes from the displayed or the catalog price.
- Status: not yet executed.

## Designing your own charters

1. One mission, one sentence. If it needs "and also", split it.
2. Anchor to a risk or a question, not a checklist - the charter guides, the tester decides.
3. Timebox it. When the box ends, write the report even mid-thought; leftovers become the next charter.
4. Note what you deliberately leave out; the scope line is what makes the next charter possible.
