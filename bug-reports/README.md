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

## Guides

- [Severity vs priority: how to classify a bug](severity-vs-priority-guide.md) - uses the six reports above as worked examples.
- [Combining findings from repeated test rounds into one bug register](multi-source-bug-register.md) - evidence labelling and dedupe when the same product is tested more than once.

## Related evidence

- Session logs live in `test-cases/saucedemo/` (sort + cart badge, login partitions, number/postal boundaries).
- Issue #1 summarises the 21 Oct - 3 Nov practice routine these reports came from.
