# Web Regression Checklist (60-minute pass)

A focused manual regression checklist for a typical web application release. Run top to bottom; stop and report on any critical failure.

## Smoke (10 min)

- [ ] App loads without console errors on the landing page
- [ ] Login works with a valid account; invalid login shows the correct error
- [ ] Main navigation links all resolve (no 404/500)
- [ ] Logout works and protected pages redirect to login

## Core user flows (25 min)

- [ ] Primary creation flow (new record/order/item) completes end to end
- [ ] Edit flow saves changes and shows them after refresh
- [ ] Delete flow asks for confirmation and actually removes the record
- [ ] Search/filter returns correct results and handles empty input gracefully
- [ ] Pagination or infinite scroll keeps data consistent (no duplicates/gaps)

## Forms and validation (10 min)

- [ ] Required fields block submit with clear messages
- [ ] Field-level validation (email format, number ranges, date bounds) triggers correctly
- [ ] Form state survives a validation error (entered data is not lost)

## UI and compatibility (10 min)

- [ ] Layout intact at 1920x1080 and 1366x768
- [ ] No overlapping or clipped text after the release's UI changes
- [ ] Quick pass in a second browser (Firefox or Edge) on the main flow
- [ ] Images, icons, and fonts load (no broken assets)

## Wrap-up (5 min)

- [ ] All failures filed as bug reports with repro steps and severity
- [ ] Results summary posted (passed / failed / blocked counts)
- [ ] Blockers flagged to the team immediately, not at the end of the day
