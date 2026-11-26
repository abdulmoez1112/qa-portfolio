# Writing good bug titles and steps

## Title
Say what happens and where. Compare:
- Weak: "Button not working"
- Better: "Checkout: Place Order button does nothing after entering a valid postal code"

## Steps
1. Start from a known state (account, page, data).
2. One action per numbered step.
3. Use exact values.
4. End with the point where the problem shows.

## Expected vs actual
- Expected: what the requirement or common sense says should happen.
- Actual: what happened, in plain words.

## Evidence
- Screenshot or short recording
- Browser, OS, device, build
- Console or network error if visible

## Rating
- Severity: how bad the impact is.
- Priority: how soon it should be fixed.
- Reproducibility: always, sometimes, once.

## Avoid
- Several bugs in one report
- Opinions such as "bad design" without a reason
- Guessing the cause when only the symptom is known

This is a writing guide, not a record of a test run.
