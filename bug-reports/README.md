# Bug reports index

Practice bug reports from hands-on sessions on https://www.saucedemo.com (a demo app that seeds defects intentionally per test user). Every report includes environment, preconditions, exact steps, expected vs actual, severity and priority.

## Saucedemo reports

| ID | Title | Test user | Severity | Priority | Date found |
|----|-------|-----------|----------|----------|------------|
| [BR-001](saucedemo/BR-001-add-to-cart-fails-problem-user.md) | Add to cart does nothing for three products | problem_user | High | High | 2026-10-21 |
| [BR-002](saucedemo/BR-002-wrong-product-images-problem-user.md) | Product images render as the wrong picture | problem_user | Medium | Medium | 2026-10-21 |
| [BR-003](saucedemo/BR-003-last-name-field-overwrites-first-name.md) | Checkout Last Name overwrites First Name | problem_user | High | High | 2026-10-21 |
| [BR-004](saucedemo/BR-004-add-to-cart-fails-error-user.md) | Add to cart does nothing for three products | error_user | High | High | 2026-10-22 |
| [BR-005](saucedemo/BR-005-remove-button-fails-error-user.md) | Remove button does not remove items | error_user | Medium | Medium | 2026-10-22 |
| [BR-006](saucedemo/BR-006-prices-change-on-reload-visual-user.md) | Prices change on every page load | visual_user | High | High | 2026-10-22 |
| [BR-007](saucedemo/BR-007-checkout-no-state-validation.md) | Checkout has no state validation: empty-cart orders, direct URL access to any step, double submission | standard_user | High | High | 2026-11-13 |

## Re-test status

| ID | Last re-test | Result | Evidence |
|----|--------------|--------|----------|
| BR-001 | 2026-11-12 | Still reproduces, but the failing set changed: Bolt T-Shirt, Fleece Jacket and TATT Red now fail; the original three pass | [12 Nov session](../test-cases/saucedemo/checkout-form-validation-session-2026-11-12.md) |
| BR-002 | 2026-11-09 | Still reproduces; all six images serve the same sl-404 placeholder | [9 Nov re-test](../test-cases/saucedemo/retest-BR-006-BR-002-2026-11-09.md) |
| BR-003 | 2026-11-12 | Still reproduces; keystrokes aimed at Last Name write into First Name, Last Name never fills | [12 Nov session](../test-cases/saucedemo/checkout-form-validation-session-2026-11-12.md) |
| BR-004 | - | Not yet re-tested | - |
| BR-005 | - | Not yet re-tested | - |
| BR-006 | 2026-11-09 | Still reproduces; prices randomize on every load, none match the catalog | [9 Nov re-test](../test-cases/saucedemo/retest-BR-006-BR-002-2026-11-09.md) |
| BR-007 | - | Found 2026-11-13 on standard_user; not yet re-tested | [13 Nov session](../test-cases/saucedemo/negative-checkout-session-2026-11-13.md) |

## Guides

- [Severity vs priority: how to classify a bug](severity-vs-priority-guide.md) - uses the six reports above as worked examples.
- [Combining findings from repeated test rounds into one bug register](multi-source-bug-register.md) - evidence labelling and dedupe when the same product is tested more than once.

## Related evidence

- Session logs live in `test-cases/saucedemo/` (sort + cart badge, login partitions, number/postal boundaries, checkout form validation).
- Issue #1 summarises the 21 Oct - 3 Nov practice routine these reports came from.
