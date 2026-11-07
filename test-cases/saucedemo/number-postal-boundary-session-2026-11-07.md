# Session log: number input and postal code boundaries (7 Nov 2026)

- Date: 7 November 2026
- Environment: Chrome (cloud browser)
- Sites: the-internet.herokuapp.com/inputs (number input), saucedemo.com checkout step one (postal code)
- Duration: ~20 minutes
- Charter: run the boundary pattern from `test-design/boundary-value-analysis-examples.md` against a live number input and a live postal code field; record exactly what each edge does.

## Part A: number input (the-internet.herokuapp.com/inputs)

The page documents no min/max. Each value was typed into the field and the resulting field value read back.

| # | Input | Field value after typing | Observation |
|---|-------|--------------------------|-------------|
| 1 | 5 | "5" | Plain integer accepted |
| 2 | -5 | "-5" | Negatives accepted; no lower bound |
| 3 | abc | "" (empty) | Non-numeric input is refused - the field stays empty rather than holding bad text |
| 4 | 1e3 | "1e3" | Exponent notation held as typed; numerically parses as 1000 |
| 5 | 999999999999999999999 (21 digits) | full 21 digits | No length cap observed |
| 6 | 3.75 | "3.75" | Decimals accepted; step behaviour still moves by 1 |
| 7 | arrows: 1 -> Up | "2" | Step up works from a typed value |
| 8 | arrows: 2 -> Down x3 | "-1" | Stepping crosses zero with no floor |

Conclusion: this widget has no documented or enforced numeric boundaries at all - every edge is "accepted", and the only real boundary behaviour is the refusal of non-numeric text. A good demonstration that BVA's first job on an undocumented field is to *find* the boundaries.

## Part B: postal code length boundaries (saucedemo checkout step one)

First/Last name filled with ordinary values each time; only the postal code varied; Continue clicked; result read from the page.

| # | Postal code | Expected (open) | Actual | Status |
|---|-------------|-----------------|--------|--------|
| 1 | (empty) | Required error | "Error: Postal Code is required" | Confirmed |
| 2 | "5" (1 char) | Record actual | Accepted - checkout step two loaded | Recorded |
| 3 | "59250" (5 chars) | Accepted | Accepted | Confirmed |
| 4 | 100 x "9" (100 chars) | Record actual | Accepted - no length limit, no truncation, no format check | Recorded |

Finding (minor, documented not assumed): the postal code field enforces only non-emptiness. There is no minimum length, maximum length, or format validation - a 1-character and a 100-character value both pass. On a real checkout this would be reported as a data-quality gap; here it is recorded as observed behaviour of the practice app.

## Notes

- Every result above was produced through the real UI in this session (typed, clicked, read back). Nothing is copied from documentation.
- The cart was left with one item; no order was submitted.
