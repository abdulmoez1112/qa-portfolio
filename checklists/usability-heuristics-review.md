# Usability heuristics review: Nielsen's 10 mapped to a demo web shop

A structured review of https://www.saucedemo.com (a public demo/practice app by Sauce Labs) against Nielsen's 10 usability heuristics. Unlike the open-ended notes in `usability/usability-heuristics-notes.md`, this is a scored pass: every heuristic gets a status based on evidence actually collected during the 21 Oct - 15 Nov 2026 practice sessions (session logs in `test-cases/saucedemo/`, bug reports BR-001 to BR-010 in `bug-reports/saucedemo/`). Nothing here is hypothetical - every status cites a logged run.

## Status legend

- PASS - checked in a logged session, no problem observed.
- ISSUE - a defect or usability problem was observed and logged; linked where filed.
- PARTIAL - some aspects verified, others untested.
- N/T - not tested in any logged session.

## Score table

| # | Heuristic | Status | Key evidence |
|---|-----------|--------|--------------|
| 1 | Visibility of system status | ISSUE | Badge updates instantly on add (PASS aspect, 15 Nov keyboard run); but cart-page Remove shows false status - BR-008; prices randomize per load for visual_user - BR-006 |
| 2 | Match between system and the real world | PASS | Plain product names and $ prices throughout; minor: "Epic sadface:" joke prefix on login errors (6 Nov login run) |
| 3 | User control and freedom | ISSUE | Checkout Cancel preserves cart (13 Nov, N4 PASS); but BR-008 navigates away unasked, and Cancel from step two lands on inventory, not cart (13 Nov, N5) |
| 4 | Consistency and standards | ISSUE | Uniform card layout and button placement (PASS aspect); but identical Add-to-cart buttons fail per seeded user - BR-001/BR-004; inconsistent Cancel destinations (13 Nov) |
| 5 | Error prevention | ISSUE | Required-field errors fire inline on checkout step one (12 Nov run, PASS aspect); but no checkout state validation - BR-007; whitespace-only names and 1-char postcodes accepted (12 Nov run) |
| 6 | Recognition rather than recall | PASS | Credentials listed on the login page; all four sort options visible; cart contents shown plainly |
| 7 | Flexibility and efficiency of use | ISSUE | Sort works, including by keyboard (15 Nov); but keyboard users cannot reach the cart at all - BR-009; duplicate image+title links double tab stops per product (15 Nov run) |
| 8 | Aesthetic and minimalist design | PASS | Cards carry image, name, description, price, one button; no clutter on any tested page |
| 9 | Help users recognize, diagnose and recover from errors | ISSUE | Inline errors are specific ("Error: First Name is required", 12 Nov); but BR-003 and BR-008 fail silently - the user is never told anything went wrong |
| 10 | Help and documentation | N/T (demo) | No help section exists; acceptable for a demo, would be a finding in production |

Result: 3 PASS, 6 ISSUE, 1 N/T. Five of the six issues map to already-filed bug reports - the heuristic review mostly re-frames functional defects as usability failures, which is expected: a broken function is always also a usability failure.

## Per-heuristic detail

### 1. Visibility of system status - ISSUE
The app does status well in the happy path: the cart badge increments the moment Add to cart succeeds, the button relabels to Remove, and the cart link's accessible name updates ("Cart, 1 items") - all observed 15 Nov. The failures are dishonest status: the cart-page Remove makes the row disappear while the item stays in the cart (BR-008, 14 Nov), and visual_user sees different prices on every load (BR-006, re-tested 9 Nov). Status that lies is worse than no status.

### 2. Match between system and the real world - PASS
Product names, dollar prices, and shopping language are natural throughout. One nit: login errors start with "Epic sadface:" (observed 6 Nov with locked_out_user) - fine for a demo's personality, worth flagging as the kind of voice choice to review in a real product.

### 3. User control and freedom - ISSUE
Good: checkout step one's Cancel returns to the cart with contents intact (13 Nov, N4). Bad: the cart-page Remove navigates the user to the inventory page without being asked (BR-008), and step two's Cancel lands on the inventory page instead of the cart (13 Nov, N5) - two different destinations for the same labelled action. Keyboard users have no freedom at all at the cart icon (BR-009).

### 4. Consistency and standards - ISSUE
Visually the app is admirably consistent: same card, same button position, same relabel behaviour across all six products. The inconsistency is behavioural and invisible until it bites: the same Add-to-cart click does nothing for three products under problem_user (BR-001, re-tested 12 Nov - with the failing set changed) and error_user (BR-004). Identical-looking controls must do identical things.

### 5. Error prevention - ISSUE
The required-field checks on checkout step one are real prevention: First Name, Last Name and Postal Code each produce a specific inline error (12 Nov run). But prevention stops there: a whitespace-only First Name is accepted, a one-character or letter-only postcode passes, an empty cart can be ordered at $0.00, every checkout step is reachable by direct URL, and a finished order can be re-submitted (BR-007, 13 Nov). Prevention exists at the field level and is absent at the flow level.

### 6. Recognition rather than recall - PASS
The accepted usernames and shared password are printed on the login page; the sort control lists its options; the cart shows its contents rather than trusting memory. For a demo this heuristic is fully satisfied.

### 7. Flexibility and efficiency of use - ISSUE
Sorting covers the main efficiency need and is keyboard-operable (15 Nov). The failures: the cart icon is unreachable by keyboard (BR-009), and each product costs two tab stops because the image and title are separate links to the same destination (15 Nov run - 23 stops where 17 would do).

### 8. Aesthetic and minimalist design - PASS
Every tested page carries only what its decision needs. No clutter, no competing calls to action.

### 9. Help users recognize, diagnose and recover from errors - ISSUE
When the app chooses to show an error, it does it well: "Error: First Name is required" is specific and actionable (12 Nov). The problem is the errors it never shows: Last Name keystrokes silently overwrite First Name for problem_user with no message (BR-003, re-tested 12 Nov), and the cart-page Remove pretends success (BR-008). Silent failure is the worst error handling.

### 10. Help and documentation - N/T (demo)
No help section, size guide, or contact path exists; for a practice app that is out of scope. Noted so a production review would not skip it.

## How this review was run

One heuristic at a time against the evidence base, not against fresh intuition: every status above cites a dated session log or bug report. Where a heuristic's verdict rests on a functional defect, the defect report stays the source of truth and this review only re-classifies it. Findings worth acting on are in `usability/heuristic-findings-2026-11-16.md`.
