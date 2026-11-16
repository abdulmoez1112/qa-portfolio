# Heuristic findings note - 16 Nov 2026

Findings from applying Nielsen's heuristics to the evidence collected in the 21 Oct - 15 Nov 2026 practice sessions on https://www.saucedemo.com (a public demo/practice app by Sauce Labs). Scored review: `checklists/usability-heuristics-review.md`. Every finding cites a logged run; impact labels are QA judgment in a demo context, not validated production impact. Extends `usability/usability-heuristics-notes.md` with the week-2 evidence (BR-007 to BR-010).

## F1 - False status feedback on the cart-page Remove (filed as BR-008)

- Heuristics: 1 Visibility of system status; 9 Error recovery.
- Observed 14 Nov (exploratory cart-state session): clicking Remove on /cart.html makes the item's row disappear, but the badge keeps its count and the item returns on re-navigation - while also navigating the user to /inventory.html unasked. Reproduced twice with the inventory-page Remove as working control.
- Why it matters (QA judgment): the UI reports a successful removal that never happened. A shopper would buy an item they believe they removed. Status feedback that lies outranks an explicit error as a usability failure.
- Status: filed - [BR-008](../bug-reports/saucedemo/BR-008-cart-page-remove-visual-only.md).

## F2 - Identical controls behave differently for seeded users (filed as BR-001 / BR-004 / BR-005)

- Heuristics: 4 Consistency and standards.
- Observed 21-22 Oct and re-tested 12 Nov: the same Add-to-cart button, visually identical on all six product cards, silently does nothing for three products under problem_user and error_user; the failing product set changed between the 21 Oct and 12 Nov runs.
- Why it matters (QA judgment): users build trust in a control from the first success and transfer it to every identical instance. A control that looks the same but behaves differently breaks the mental model without any signal.
- Status: filed - [BR-001](../bug-reports/saucedemo/BR-001-add-to-cart-fails-problem-user.md), [BR-004](../bug-reports/saucedemo/BR-004-add-to-cart-fails-error-user.md), [BR-005](../bug-reports/saucedemo/BR-005-remove-button-fails-error-user.md).

## F3 - Prevention exists at field level, absent at flow level (filed as BR-007)

- Heuristics: 5 Error prevention.
- Observed 12 Nov (checkout form validation run) and 13 Nov (negative-checkout run): step one blocks empty required fields with specific inline errors (good prevention), yet accepts a whitespace-only First Name and a one-character postcode; and the flow itself has no guards - an empty cart can be ordered at $0.00, every step is reachable by direct URL, and a completed order can be re-submitted.
- Why it matters (QA judgment): prevention that checks format but not meaning teaches users the validation is theatre; the $0.00 empty order and double submission are the expensive failures a flow-level guard exists to stop.
- Status: filed - [BR-007](../bug-reports/saucedemo/BR-007-checkout-no-state-validation.md). The field-level weaknesses are logged in the 12 Nov session, not separately filed.

## F4 - The same Cancel label goes to two different destinations (observation, not filed)

- Heuristics: 3 User control and freedom; 4 Consistency.
- Observed 13 Nov (negative-checkout run, N4/N5): Cancel on checkout step one returns to the cart; Cancel on step two returns to the inventory page. Same word, same style, different outcome.
- Why it matters (QA judgment): users learn one meaning per control. Two destinations for one label means one of them surprises the user every time.
- Status: logged in the [13 Nov session](../test-cases/saucedemo/negative-checkout-session-2026-11-13.md); candidate for a standalone report if it reproduces in a dedicated run.

## F5 - Keyboard users lose the flow twice: reach, then visibility (filed as BR-009 / BR-010)

- Heuristics: 7 Flexibility and efficiency of use; 3 User control and freedom; 1 Visibility of system status (focus position is status too).
- Observed 15 Nov (keyboard-only run): the cart icon cannot receive keyboard focus on the pages tested, so the cart and checkout are unreachable without a mouse; and on the login, inventory and cart pages no focused element shows any visible indicator (computed outline:none, no replacement style, screenshots in the session log).
- Why it matters (QA judgment): efficiency heuristics usually discuss shortcuts; here the base path itself is missing for one user class. Invisible focus additionally removes the "where am I" status that every navigation step depends on.
- Status: filed - [BR-009](../bug-reports/saucedemo/BR-009-cart-link-not-keyboard-operable.md), [BR-010](../bug-reports/saucedemo/BR-010-no-visible-focus-indicator.md).

## F6 - Silent field corruption for problem_user (filed as BR-003)

- Heuristics: 9 Help users recognize, diagnose and recover from errors.
- Observed 21 Oct, re-tested 12 Nov: keystrokes aimed at the Last Name field write into First Name instead, Last Name stays empty, and nothing on screen says anything is wrong - checkout then blocks submission on the "wrong" field.
- Why it matters (QA judgment): the user did nothing wrong and is shown an error they cannot satisfy. Recovery is impossible without understanding a bug the user cannot see.
- Status: filed - [BR-003](../bug-reports/saucedemo/BR-003-last-name-field-overwrites-first-name.md); re-test evidence in the [12 Nov session](../test-cases/saucedemo/checkout-form-validation-session-2026-11-12.md).

## Cross-cutting note

Five of six findings rest on functional defects re-read through a usability lens. That is the expected relationship: heuristics explain WHY a defect hurts, defect reports prove THAT it happens. Keep both labels on the same evidence.
