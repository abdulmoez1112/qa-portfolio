# Week 1 summary: 5-10 Nov 2026 (written 11 Nov)

Six days of the 30-day QA portfolio routine are complete: 12 commits, 4 executed test sessions, 6 documentation artifacts. Everything below links to the committed evidence; session logs are real browser runs, labelled with date and profile.

## Executed test sessions (real runs)

| Date | Session | What was run | Result |
|------|---------|--------------|--------|
| 5 Nov | [sort-cart-session-2026-11-05](../test-cases/saucedemo/sort-cart-session-2026-11-05.md) | Login + all 4 sort options checked against rendered order + cart badge add/remove (7 checks), standard_user | 7/7 PASS |
| 6 Nov | [login-partition-session-2026-11-06](../test-cases/saucedemo/login-partition-session-2026-11-06.md) | 8 login partition/boundary checks: valid, locked-out, empty user, empty pass, unknown user, wrong pass, whitespace-only, 300-char | All behaved; whitespace and 300-char get the generic "do not match" error - no user enumeration |
| 7 Nov | [number-postal-boundary-session-2026-11-07](../test-cases/saucedemo/number-postal-boundary-session-2026-11-07.md) | 8 boundary checks on a live number input + saucedemo postal code with empty/1/5/100 chars | Number input refuses only non-numeric (no bounds); postal code accepts any length/format |
| 9 Nov | [retest-BR-006-BR-002-2026-11-09](../test-cases/saucedemo/retest-BR-006-BR-002-2026-11-09.md) | Re-ran two filed bugs with exact original steps | Both STILL REPRODUCE (details below) |

## Documentation written

- [Combining findings into one bug register](../bug-reports/multi-source-bug-register.md) (5 Nov)
- [Equivalence partitioning examples](../test-design/equivalence-partitioning-examples.md) (6 Nov)
- [Boundary value analysis examples](../test-design/boundary-value-analysis-examples.md) (7 Nov)
- [Severity vs priority guide](../bug-reports/severity-vs-priority-guide.md) + [bug reports index](../bug-reports/README.md) (8 Nov)
- [Defect lifecycle guide](../test-design/defect-lifecycle.md) (9 Nov)
- [Requirements traceability matrix](../test-plans/traceability-matrix-example.md) + [test plans index](../test-plans/README.md) (10 Nov)

## Defect status as of 11 Nov

| Bug | What breaks | Severity | Status |
|-----|-------------|----------|--------|
| [BR-001](../bug-reports/saucedemo/BR-001-add-to-cart-fails-problem-user.md) | Add to cart dead for 3 products (problem_user) | High | Open - re-test pending |
| [BR-002](../bug-reports/saucedemo/BR-002-wrong-product-images-problem-user.md) | All 6 images serve the same sl-404 placeholder (problem_user) | Medium | Open - re-tested 9 Nov, still reproduces; evidence refined with exact file names |
| [BR-003](../bug-reports/saucedemo/BR-003-last-name-field-overwrites-first-name.md) | Last Name overwrites First Name at checkout (problem_user) | High | Open - re-test pending |
| [BR-004](../bug-reports/saucedemo/BR-004-add-to-cart-fails-error-user.md) | Add to cart dead for 3 products (error_user) | High | Open - re-test pending |
| [BR-005](../bug-reports/saucedemo/BR-005-remove-button-fails-error-user.md) | Remove button dead (error_user) | Medium | Open - re-test pending |
| [BR-006](../bug-reports/saucedemo/BR-006-prices-change-on-reload-visual-user.md) | Prices randomize on every load, none match catalog (visual_user) | High | Open - re-tested 9 Nov, still reproduces (3 loads captured) |

## What week 1 showed

- The seeded defects are stable: both re-tested bugs reproduce exactly as filed 18 days earlier, so the practice suite can rely on them for regression training.
- Login error handling is enumeration-safe: every invalid credential class returns the same generic message.
- Form validation on the demo app is thin: the postal code accepts anything, which makes it a good teaching example for boundary analysis.

## Week 2 focus

Re-test BR-001/003/004/005, a checkout form-validation deep pass, a negative-testing session, and the first executed exploratory charter. New regression items from this week are listed in [checklists/week1-regression-additions.md](../checklists/week1-regression-additions.md).
