# Test cases index

Two kinds of artifact live here:

- **Scripted case sets** (this folder): reusable test cases with preconditions, steps and expected results. A case is "Not run" until a dated session log records its execution.
- **Session logs** (`saucedemo/` subfolder): dated records of what actually happened in one test session - the evidence behind every bug report.

All against the practice app https://www.saucedemo.com unless stated. Bugs found from these live in `bug-reports/saucedemo/` (BR-001 to BR-010).

## Scripted case sets

| File | Coverage | Case IDs | Notes |
|------|----------|----------|-------|
| [saucedemo-checkout-test-cases.md](saucedemo-checkout-test-cases.md) | Login, catalog, cart, checkout | TC-001..TC-010 | First full set (Oct 2026) |
| [sorting-and-cart-edge-cases.md](sorting-and-cart-edge-cases.md) | Product sorting, cart edge cases | TC-SORT-01..06, TC-CART-01..04 | Two "record the actual behavior" cases; TC-CART-04 answered by BR-007 |
| [checkout-boundary-value-tests.md](checkout-boundary-value-tests.md) | Checkout form boundary values | table format | Design table + results table; ran 7 Nov (see session log) |
| [saucedemo-regression-pack-v2.md](saucedemo-regression-pack-v2.md) | Sorting persistence, images, link/navigation integrity | TC-R2-01..TC-R2-10 | Built from week 1-2 defect learnings; TC-R2-10 guards the BR-009 keyboard fix |

## Session logs (saucedemo/)

| Date | Log | Focus | Key outcomes |
|------|-----|-------|--------------|
| 2026-11-05 | [sort-cart-session-2026-11-05.md](saucedemo/sort-cart-session-2026-11-05.md) | Product sort + cart badge, exploratory | Sort verified; badge tracking verified |
| 2026-11-06 | [login-partition-session-2026-11-06.md](saucedemo/login-partition-session-2026-11-06.md) | Login equivalence partitions | Valid/invalid classes; locked_out_user error observed |
| 2026-11-07 | [number-postal-boundary-session-2026-11-07.md](saucedemo/number-postal-boundary-session-2026-11-07.md) | Number/postal boundary values | Boundary table executed |
| 2026-11-09 | [retest-BR-006-BR-002-2026-11-09.md](saucedemo/retest-BR-006-BR-002-2026-11-09.md) | Re-test of BR-006, BR-002 | Both still reproduce |
| 2026-11-12 | [checkout-form-validation-session-2026-11-12.md](saucedemo/checkout-form-validation-session-2026-11-12.md) | Checkout form validation deep pass + BR-001/BR-003 re-tests | Field errors verified; weak validation logged; both bugs still reproduce (BR-001 failing set changed) |
| 2026-11-13 | [negative-checkout-session-2026-11-13.md](saucedemo/negative-checkout-session-2026-11-13.md) | Negative checkout states and sequences | BR-007 found (no state validation) |
| 2026-11-14 | [exploratory-cart-state-session-2026-11-14.md](saucedemo/exploratory-cart-state-session-2026-11-14.md) | Exploratory charter: cart state | BR-008 found (cart-page Remove visual-only); cart persists across refresh and logout/login |
| 2026-11-15 | [keyboard-only-session-2026-11-15.md](saucedemo/keyboard-only-session-2026-11-15.md) | Keyboard-only login-to-cart | BR-009 (cart icon not keyboard-operable) and BR-010 (no visible focus indicator) found |
