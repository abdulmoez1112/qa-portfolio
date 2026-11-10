# Requirements traceability matrix (RTM): saucedemo.com worked example

A requirements traceability matrix links every requirement to the test cases that cover it and the defects found against it. It answers two questions fast:

- **Forward trace:** if a requirement matters, where is it tested?
- **Backward trace:** if a test or bug exists, which requirement justifies it?

This example is built entirely from real artifacts already in this repo. Requirements are keyed to the scope section of the [saucedemo test plan](saucedemo-test-plan.md); test coverage links to the designed case set and dated session logs; defects link to the verified bug reports. REQ-13 is an implicit requirement the matrix surfaced from BR-006 - surfacing missing requirements is one of the things an RTM is for.

## Matrix

| Req | Requirement (test plan scope) | Test coverage | Defects | Status |
|-----|-------------------------------|---------------|---------|--------|
| REQ-01 | Login with valid credentials | [TC-001](../test-cases/saucedemo-checkout-test-cases.md) | - | Covered |
| REQ-02 | Locked-out user is rejected with a clear error | [TC-002](../test-cases/saucedemo-checkout-test-cases.md) | - | Covered |
| REQ-03 | Invalid username/password combinations are rejected | [login-partition-session-2026-11-06](../test-cases/saucedemo/login-partition-session-2026-11-06.md) | - | Covered (executed 6 Nov) |
| REQ-04 | Catalog shows 6 products with correct name, price and image | TC-001 postcondition | [BR-002](../bug-reports/saucedemo/BR-002-wrong-product-images-problem-user.md), [BR-006](../bug-reports/saucedemo/BR-006-prices-change-on-reload-visual-user.md) | Defects open - both still reproduce (re-tested 9 Nov) |
| REQ-05 | Sort products by name A-Z and Z-A | [TC-005](../test-cases/saucedemo-checkout-test-cases.md), [sort-cart-session-2026-11-05](../test-cases/saucedemo/sort-cart-session-2026-11-05.md) | - | Covered (executed 5 Nov) |
| REQ-06 | Sort products by price low-high and high-low | [TC-006](../test-cases/saucedemo-checkout-test-cases.md), [sort-cart-session-2026-11-05](../test-cases/saucedemo/sort-cart-session-2026-11-05.md) | - | Covered (executed 5 Nov) |
| REQ-07 | Add to cart from the inventory page | [TC-003](../test-cases/saucedemo-checkout-test-cases.md) | [BR-001](../bug-reports/saucedemo/BR-001-add-to-cart-fails-problem-user.md), [BR-004](../bug-reports/saucedemo/BR-004-add-to-cart-fails-error-user.md) | Defects open (problem_user, error_user) |
| REQ-08 | Remove item from cart | [TC-004](../test-cases/saucedemo-checkout-test-cases.md) | [BR-005](../bug-reports/saucedemo/BR-005-remove-button-fails-error-user.md) | Defect open (error_user) |
| REQ-09 | Cart page lists items with correct price; badge count accurate | [TC-007](../test-cases/saucedemo-checkout-test-cases.md), [sort-cart-session-2026-11-05](../test-cases/saucedemo/sort-cart-session-2026-11-05.md) | - | Covered (executed 5 Nov) |
| REQ-10 | Checkout step 1 validates required fields | [TC-009](../test-cases/saucedemo-checkout-test-cases.md), [checkout-boundary-value-tests](../test-cases/checkout-boundary-value-tests.md), [number-postal-boundary-session-2026-11-07](../test-cases/saucedemo/number-postal-boundary-session-2026-11-07.md) | [BR-003](../bug-reports/saucedemo/BR-003-last-name-field-overwrites-first-name.md) | Defect open (problem_user) |
| REQ-11 | Checkout happy path through order confirmation | [TC-008](../test-cases/saucedemo-checkout-test-cases.md) | - | Covered |
| REQ-12 | Logout returns to login and blocks direct URL access | [TC-010](../test-cases/saucedemo-checkout-test-cases.md) | - | Covered |
| REQ-13 | Prices stay stable and match the catalog across reloads (implicit, surfaced by BR-006) | [retest-BR-006-BR-002-2026-11-09](../test-cases/saucedemo/retest-BR-006-BR-002-2026-11-09.md) | [BR-006](../bug-reports/saucedemo/BR-006-prices-change-on-reload-visual-user.md) | Defect open - still reproduces (re-tested 9 Nov) |

## Coverage summary

- 13 requirements, all with at least one linked test artifact. No orphan tests: every dated session log maps to a requirement.
- 6 open defects across 5 requirements (REQ-04, REQ-07, REQ-08, REQ-10, REQ-13), all affecting the seeded problem/error/visual users; the standard_user flow stays clean.
- Re-test debt: BR-001, BR-003, BR-004, BR-005 have not been re-run since they were filed (21-22 Oct). BR-002 and BR-006 were re-tested 9 Nov and still reproduce. Open re-tests are tracked in the [bug reports index](../bug-reports/README.md).

## Gaps this matrix makes visible

- Performance, load and security testing are out of scope per the test plan - the RTM records that as a deliberate exclusion, not an oversight.
- Mobile native coverage is deferred to a later cycle (also per the plan).
- Login coverage rests on one partition session; a second browser/OS pass would harden REQ-01 to REQ-03.

## Maintaining the matrix

1. One row per requirement; add a row before writing the test, not after.
2. When a new session log or bug lands, link it in the same commit that adds the artifact.
3. When a defect is re-tested and fixed, update the Status column and date it - the matrix is a living record, not a snapshot.
4. Use it for impact analysis: a fix touching checkout validation means re-running everything on the REQ-10 and REQ-11 rows.
