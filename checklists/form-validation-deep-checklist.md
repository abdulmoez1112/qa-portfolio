# Form validation: the deep checklist

Beyond "required field is required". Run every category against every input; a form that passes required-only testing is usually still broken.

## 1. Required vs optional
- [ ] Each required field, left empty alone, produces its own specific error (not a generic one)
- [ ] Submitting with everything empty names the FIRST required field, not all at once or none
- [ ] Optional fields truly accept empty
- [ ] Whitespace-only input is treated as empty (or explicitly trimmed and rejected)

## 2. Length bounds
- [ ] Minimum length - 1: rejected if a minimum exists
- [ ] Minimum length: accepted
- [ ] Maximum length: accepted
- [ ] Maximum length + 1: rejected or visibly truncated (silent truncation is a finding)
- [ ] Absurd length (300+ chars): handled gracefully, no layout break, no silent data loss

## 3. Character classes
- [ ] Digits in a name field: accepted or rejected *deliberately* (record which)
- [ ] Letters in a numeric field: rejected with a clear message
- [ ] Special characters typical for the field (apostrophes and hyphens in names: O'Brien, Mary-Jane)
- [ ] Symbols with no business in the field (!@#$%) : rejected or accepted deliberately
- [ ] Unicode: accented names (Jose, Renee), non-Latin scripts, emoji
- [ ] Leading/trailing spaces: trimmed or preserved - record which, check for downstream display issues

## 4. Format patterns (where a format exists)
- [ ] Postal/ZIP: country-appropriate patterns; letters vs digits; too short / too long
- [ ] Email: missing @, missing domain, double dots, plus-addressing
- [ ] Phone: separators, country code, alpha characters

## 5. Injection and safety
- [ ] HTML/JS string (<script>alert(1)</script>): accepted or rejected - and if accepted, confirm it never renders as markup anywhere the value reappears
- [ ] SQL-flavoured input (' OR 1=1 --): treated as plain text
- Record acceptance honestly; only claim execution if you actually observe it

## 6. Field interaction
- [ ] Typing in field B never alters field A (cross-field contamination - saucedemo's problem_user BR-003 is the textbook case)
- [ ] Autofill/paste fills only the intended field
- [ ] Tab order follows the visual order
- [ ] Error clearing: fixing a field clears its error without re-validating unrelated fields

## 7. Error message quality
- [ ] Messages name the field and the problem ("Postal Code is required", not "Invalid input")
- [ ] No account/data enumeration through differing messages (see login partition session, 6 Nov)
- [ ] Errors survive a round trip: navigate away and back - state is either cleanly reset or cleanly preserved, never half-filled

## 8. Submission integrity
- [ ] Double-clicking submit sends once
- [ ] Browser back after a successful step does not resurrect a stale form state
- [ ] A rejected submission preserves the valid fields the user already typed

Evidence template: record field, input, expected, actual, and exact error text - as in the 12 Nov saucedemo session log in test-cases/saucedemo/.
