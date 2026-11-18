# Week 2 QA summary: 12-18 Nov 2026

Days 8-14 of the 30-day practice plan. Target: https://www.saucedemo.com/, a public demo/practice app maintained by Sauce Labs, not a live store. This summary separates executed checks from test design and historical findings. Severity and priority in linked reports are QA judgments, not validated production impact.

## Work completed

| Date | Work | Evidence |
|---|---|---|
| 12 Nov | Checkout field validation; re-tests of BR-001 and BR-003; validation checklist | [Form-validation session](../test-cases/saucedemo/checkout-form-validation-session-2026-11-12.md), [checklist](../checklists/form-validation-deep-checklist.md) |
| 13 Nov | Negative checkout states and sequences; BR-007 filed | [Negative session](../test-cases/saucedemo/negative-checkout-session-2026-11-13.md), [negative-testing guide](../checklists/negative-testing-guide.md) |
| 14 Nov | Exploratory cart-state charter executed; BR-008 filed | [Charters](../test-design/exploratory-charters.md), [session](../test-cases/saucedemo/exploratory-cart-state-session-2026-11-14.md) |
| 15 Nov | Keyboard navigation of login, inventory and cart; BR-009 and BR-010 filed | [Walkthrough](../accessibility/keyboard-only-walkthrough.md), [session](../test-cases/saucedemo/keyboard-only-session-2026-11-15.md) |
| 16 Nov | Documentation review of prior evidence against usability heuristics; no new app run | [Review](../checklists/usability-heuristics-review.md), [findings](../usability/heuristic-findings-2026-11-16.md) |
| 17 Nov | Ten new regression cases designed; no execution claimed | [Regression pack v2](../test-cases/saucedemo-regression-pack-v2.md), [case index](../test-cases/README.md) |
| 18 Nov | Six Chrome functional spot checks; explicit cross-browser coverage gaps | [Compatibility baseline and gaps](../test-cases/saucedemo/compatibility-spot-check-2026-11-18.md) |

## Findings and their limits

### Checkout: field errors are not flow guards

The 12 Nov run observed the expected required-field messages in order. It also observed acceptance of whitespace-only names, long names and several postal-code shapes. Acceptance is an observation, not proof of code execution or a universal rule about valid international postal formats.

The 13 Nov run found missing UI state guards: empty-cart checkout, direct access to later pages and a repeat confirmation after Back then Finish. These are grouped in [BR-007](../bug-reports/saucedemo/BR-007-checkout-no-state-validation.md). A repeated confirmation screen does not prove a second backend order. No backend order history was verified.

### Cart: visual removal was not persistent removal

The 14 Nov run reproduced a cart-page Remove failure twice: the row disappeared but the badge and later page contents still reflected the item, with unexpected navigation. The inventory-page Remove was a working control. [BR-008](../bug-reports/saucedemo/BR-008-cart-page-remove-visual-only.md) records the UI evidence only.

Cart persistence across refresh and logout/login was also observed. No approved retention requirement was available, so persistence is a product-decision question, not a confirmed defect or a newly established expected behavior.

### Keyboard: distinguish reachability, focus and activation

The 15 Nov run found the cart icon absent from the keyboard path and filed [BR-009](../bug-reports/saucedemo/BR-009-cart-link-not-keyboard-operable.md). The cart page was inspected using a direct URL workaround. Reaching a control with Tab is not itself proof that its action was activated successfully.

[BR-010](../bug-reports/saucedemo/BR-010-no-visible-focus-indicator.md) covers the focus-visibility finding on the tested login, inventory and cart pages. It is not a claim about all pages, screen-reader output or every browser. Today's pointer-based cart check does not re-test either keyboard finding.

### Existing defects re-tested

BR-001 still reproduced on 12 Nov, but the failing product set differed from the original report. BR-003 still reproduced: keystrokes intended for Last Name altered First Name while Last Name stayed empty. These are re-tests of existing reports, not new bugs. The observed change in the product set does not establish why the demo changed.

## Test-design progress

The heuristic review connects existing functional failures to usability concerns; it is an interpretation of prior evidence, not another test run. The ten-case v2 pack adds sorting-state, image and link checks. Its cases remain Not run until their exact steps are executed and dated results recorded. Known defects should not be treated as evidence that a newly written case has already run.

## Coverage and next priorities

- Today's Chrome 156/Linux sample passed login, price sorting, Backpack details, detail-page add, pointer cart navigation and Continue Shopping. No checkout order was attempted.
- Firefox, Safari/WebKit, Edge and mobile browsers were not exercised today. Cross-browser compatibility is still unverified.
- New reports this week are BR-007 through BR-010. See the [bug index](../bug-reports/README.md) for their historical evidence and status, not a claim of a fresh re-test today.
- Next planned practice: responsive viewport checks, then game QA and API testing. Emulated viewports must be labelled as emulated, not physical-device coverage.

The main lesson is evidence discipline: separate what the UI showed from backend effects, a design expectation from a product requirement, a case written from a case run, and one-browser success from compatibility coverage.
