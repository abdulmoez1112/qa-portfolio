# Usability Heuristics Notes (Nielsen's 10, applied to a web shop)

Working notes for reviewing a web app against Nielsen's 10 usability heuristics. Each heuristic has what to look for and a concrete example from the practice app https://www.saucedemo.com. Examples marked with a date were actually observed in a live session; the rest are review prompts for future passes. Related bug reports: bug-reports/saucedemo/ (BR-001 to BR-006).

## 1. Visibility of system status
Look for: the app always telling the user what is going on - cart counts, loading indicators, current step in checkout.
Observed 29 Oct 2026: adding the Sauce Labs Backpack sets the cart badge to 1 and the cart page lists that same item. The badge is the status cue; it updates immediately without a page reload. Checkout shows its step in the page title (Your Information, Overview).

## 2. Match between system and the real world
Look for: language the user understands, in a logical order - product names and prices a shopper recognizes, not internal codes.
Observed in earlier sessions: product list uses plain names and dollar prices ($7.99 to $49.99), sorted by name or price in ways that match how people shop. Contrast: the login error text starts with "Epic sadface:" - a joke prefix a first-time user may not expect in an error.

## 3. User control and freedom
Look for: an obvious way out of every flow - cancel, back, undo.
Observed 29 Oct 2026: the checkout information page has a Cancel button that returns to the cart (/checkout-step-one.html back to /cart.html) without losing the cart contents. Remove buttons on the cart page act as undo for add-to-cart.

## 4. Consistency and standards
Look for: the same action looking and behaving the same everywhere - buttons, navigation, terminology.
Observed in earlier sessions: all six products use the same card layout and the same "Add to cart" button position, which is consistent; the button flips to "Remove" after adding, keeping the action in the same place. (The identical accessible name on all six is an accessibility issue - see accessibility/a11y-quick-check-guide.md - even though the visual consistency is good.)

## 5. Error prevention
Look for: stopping mistakes before they happen - validation before submit, disabled next steps until required data exists.
Observed 29 Oct 2026: continuing checkout with an empty form is blocked inline with "Error: First Name is required" before any data is sent onward. That is prevention at the right point.

## 6. Recognition rather than recall
Look for: options visible instead of memorized - visible sort choices, prefilled known data, instructions where needed.
Observed in earlier sessions: the sort dropdown shows all four options when opened; the login page lists the accepted usernames and the shared password directly on the page (fine for a demo app, notable as a deliberate recognition-over-recall choice).

## 7. Flexibility and efficiency of use
Look for: shortcuts for repeat users - sorting, filtering, direct links to deep pages.
Observed in earlier sessions: sorting by price and name covers the main efficiency need on a six-item catalog. There is no search or category filter; acceptable at this size, a finding if the catalog grows.

## 8. Aesthetic and minimalist design
Look for: screens carrying only what the decision needs - no competing clutter.
Observed in earlier sessions: the product card shows image, name, short description, price, one button. Nothing extra. The cart page keeps the same restraint.

## 9. Help users recognize, diagnose and recover from errors
Look for: plain-language error messages that say what went wrong and what to do next.
Observed 29 Oct 2026: "Error: First Name is required" is specific and actionable. Weaker example observed 21 Oct (BR-003): when the Last Name field overwrites First Name for problem_user, no message tells the user anything is wrong - the error is invisible, the worst kind.
Observed 28 Oct 2026: the login error appears visually but is not announced to screen readers (no role="alert"/aria-live) - recovery depends on seeing the page.

## 10. Help and documentation
Look for: help where the task needs it, searchable and task-focused.
Observed in earlier sessions: the demo app has no help section; the on-page credential list partly covers it. In a real shop this heuristic would flag missing size guides, return policy links and contact options at the decision points.

## How to use these notes
Run one heuristic at a time against one page, write down concrete evidence (what you saw, where, when), and log anything user-visible as a bug report with severity. A heuristic pass finds usability problems; it does not replace functional testing - BR-001 to BR-006 were found by functional exploration, not by this checklist.
