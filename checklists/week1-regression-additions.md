# Regression additions from week 1 (5-11 Nov 2026)

Additions for the next regression pass on saucedemo.com, each traced to the evidence that motivated it. Run as the affected profile, not just standard_user. Status legend: PENDING = not yet re-run; CONFIRMED OPEN = re-run and still failing.

## A. Defect re-tests (carry into every pass until fixed)

- [ ] BR-001 - add to cart for Backpack, Bike Light, Onesie as problem_user. Source: [report](../bug-reports/saucedemo/BR-001-add-to-cart-fails-problem-user.md). Status: PENDING
- [ ] BR-003 - First Name field contents after typing Last Name, problem_user checkout step 1. Source: [report](../bug-reports/saucedemo/BR-003-last-name-field-overwrites-first-name.md). Status: PENDING
- [ ] BR-004 - add to cart for the same three products as error_user. Source: [report](../bug-reports/saucedemo/BR-004-add-to-cart-fails-error-user.md). Status: PENDING
- [ ] BR-005 - Remove button on cart page as error_user. Source: [report](../bug-reports/saucedemo/BR-005-remove-button-fails-error-user.md). Status: PENDING
- [x] BR-002 - all six product images as problem_user vs standard_user control. Status: CONFIRMED OPEN 9 Nov ([re-test log](../test-cases/saucedemo/retest-BR-006-BR-002-2026-11-09.md)) - keep in pass
- [x] BR-006 - record all six prices across two reloads as visual_user. Status: CONFIRMED OPEN 9 Nov ([re-test log](../test-cases/saucedemo/retest-BR-006-BR-002-2026-11-09.md)) - keep in pass

## B. New functional checks from week-1 sessions

- [ ] Postal code format: submit checkout step 1 with 1, 5 and 100 characters and with letters vs digits; record what is accepted. Motivation: 7 Nov session found no length or format limit - flag any change. Source: [session log](../test-cases/saucedemo/number-postal-boundary-session-2026-11-07.md)
- [ ] Number input bounds (the-internet.herokuapp.com): negative values, 1e3, 21-digit input, arrow-key stepping across zero. Motivation: no bounds enforced on 7 Nov; a future change would be a real finding. Source: same log
- [ ] Login error consistency: whitespace-only and 300-char usernames still return the generic "do not match" message, no account enumeration. Source: [6 Nov session](../test-cases/saucedemo/login-partition-session-2026-11-06.md)

## C. Stable-pass anchors (quick smoke, standard_user)

- [ ] All 4 sort options render in the expected order. Source: [5 Nov session](../test-cases/saucedemo/sort-cart-session-2026-11-05.md) (7/7 PASS)
- [ ] Cart badge increments on add and clears on remove from the inventory page. Source: same session

## Notes

- Items in section A map to requirements REQ-04, REQ-07, REQ-08, REQ-10 and REQ-13 in the [traceability matrix](../test-plans/traceability-matrix-example.md); update the matrix status column when a re-test passes.
- If any CONFIRMED OPEN item stops reproducing, do not close it on one pass - re-run once more on a different day before marking it fixed, because the demo app reseeds state without notice.
