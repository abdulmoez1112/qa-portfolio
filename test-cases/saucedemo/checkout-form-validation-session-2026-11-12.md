# Session log: checkout form validation + BR-001/BR-003 re-tests (12 Nov 2026)

- Date: 12 Nov 2026, ~18:27-18:32 PKT
- Environment: Chrome (cloud browser), desktop viewport, https://www.saucedemo.com
- Profiles: standard_user (control) and problem_user
- Method: every field filled through the page UI; error text read from the rendered page after clicking Continue

## Part 1 - checkout step 1 validation as standard_user (control)

Cart: 1 x Sauce Labs Backpack. Each row is one submission attempt; after an accepted submission the run returned to step one for the next case.

| # | First Name | Last Name | Postal Code | Result |
|---|-----------|-----------|-------------|--------|
| C1 | (empty) | (empty) | (empty) | Error: First Name is required |
| C2 | John | (empty) | (empty) | Error: Last Name is required |
| C3 | John | Doe | (empty) | Error: Postal Code is required |
| C4 | John | Doe | A (1 char) | ACCEPTED - reached step two |
| C5 | John | Doe | !@#$%^&*() | ACCEPTED - reached step two |
| C6 | John | Doe | ABCDE (letters) | ACCEPTED - reached step two |
| C7 | "   " (whitespace only) | Doe | 12345 | ACCEPTED - reached step two |
| C8 | 300 x "A" | Doe | 12345 | ACCEPTED - reached step two |
| C9 | John123!? | Doe | 12345 | ACCEPTED - reached step two |
| C10 | <script>alert(1)</script> | Doe | 12345 | ACCEPTED - reached step two (name is never re-rendered, so no execution observed; acceptance itself recorded) |

Findings (standard_user):
1. Required-field errors work and are specific and ordered (first, then last, then postal). PASS.
2. Postal Code has NO format or length validation: 1 char, pure letters, and pure symbols all pass. Confirms the 7 Nov observation; unchanged.
3. First Name has no content validation: whitespace-only, 300 chars, digits+symbols, and a script-tag string all pass. Whitespace-only passing the "required" check is the weakest point - a space counts as a name.
4. No field-length cap observed on First Name (300 chars accepted without visible truncation).

## Part 2 - BR-001 re-test: add to cart as problem_user

Original report (21 Oct): add to cart dead for Backpack, Bike Light and Onesie; the other three products worked. Today, each product was clicked fresh from the inventory page with the cart badge checked after each click; failures were retried once.

| Product | 21 Oct | 12 Nov |
|---------|--------|--------|
| Sauce Labs Backpack | FAIL | PASS (badge incremented) |
| Sauce Labs Bike Light | FAIL | PASS |
| Sauce Labs Bolt T-Shirt | PASS | FAIL (2 attempts) |
| Sauce Labs Fleece Jacket | PASS | FAIL (2 attempts) |
| Sauce Labs Onesie | FAIL | PASS |
| Test.allTheThings() T-Shirt (Red) | PASS | FAIL (2 attempts) |

Verdict: STILL REPRODUCES, but the affected set changed. Three products fail today - exactly the complement of the original set. The demo app reseeds state, so the failing set may rotate; the defect class ("some products cannot be added as problem_user") is stable. BR-001's report should be read as a defect class, not a fixed product list. Impact is arguably worse than filed: 3 of 6 failing today, and which three is not predictable.

## Part 3 - BR-003 re-test: name field contamination as problem_user

Original report (21 Oct): typing in Last Name overwrites First Name. Today's characterization, keystroke by keystroke:

1. Typed "Alice" into First Name -> first = "Alice", last = "" (First Name works alone)
2. Typed "Smith" into Last Name -> first = "h", last = "" (every keystroke aimed at Last Name landed in First Name instead, replacing its content; only the final character survived; Last Name received nothing)
3. First pass ("John" / "Doe") showed the same shape: first = "e", last = ""

Verdict: STILL REPRODUCES. Input routed to the Last Name field writes into First Name and the Last Name field never receives a value. Because Last Name is required (C2) and cannot be filled, problem_user cannot complete checkout at all - severity High confirmed.

## Notes

- standard_user checkout remains fully functional; all Part 1 acceptances completed step one normally.
- No new bug filed today: Parts 2 and 3 update existing reports BR-001 and BR-003; the changed product set in Part 2 is recorded here and in the bug register rather than as a new report.
