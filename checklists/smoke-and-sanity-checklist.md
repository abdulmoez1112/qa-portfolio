# Smoke and Sanity Testing Checklist (Web Shop)

Two short test passes with different jobs, using https://www.saucedemo.com as the example target. A smoke test answers "is the build alive enough to test at all?" - broad and shallow. A sanity test answers "did the thing we just changed actually get fixed, and nothing right next to it break?" - narrow and quick. Both are checklists you finish in minutes, not hours.

## Smoke test (run on every new build/deploy, before any deeper testing)

| # | Check | Pass looks like | Status |
|---|-------|-----------------|--------|
| 1 | App loads | Home/login page renders, no blank screen, no browser error | Not run |
| 2 | Login works with a valid account | Lands on the main page | Not run |
| 3 | Main page renders its core content | Product list with images, names, prices | Not run |
| 4 | One core action works end to start | Add to cart updates the badge; cart shows the item | Not run |
| 5 | One navigation path works | Open cart, continue shopping, open a product | Not run |
| 6 | Logout works | Returns to the login page | Not run |

Rule: any smoke failure stops testing. Report the build as not testable; running a full regression on a dead build wastes everyone's day.

## Sanity test (run after a specific fix or small change)

1. Name the exact change being verified (bug ID or deploy note) before starting.
2. Re-run the exact steps that reproduced the original bug - it must now pass.
3. Check only the neighboring behavior the change could touch. Examples:
   - Fix in the checkout form -> also try checkout with one wrong field and one empty field, and Cancel back to cart.
   - Fix in the sort dropdown -> try each sort option once, then add to cart from a sorted list.
   - Fix in the cart badge -> add one, add another, remove one, watch the count each time.
4. Stop. Sanity is not regression; if the fix area touches everything, escalate to a regression run instead of stretching the sanity pass.

## Performed example (smoke)

A smoke pass matching the table above was executed on 26 Oct 2026 in Chrome 155.0.0.0 against the live app: login landed on /inventory.html, 6 products rendered with images and prices, sorting low-to-high ordered $7.99 to $49.99, add-to-cart set the badge to 1 and the cart listed the item, logout returned to the login page. All six rows passed (recorded in checklists/cross-browser-checklist-web-app.md).

## Common mistakes

- Calling a full regression "smoke" - a smoke suite that takes an hour is a regression suite with a wrong name.
- Sanity without a named change - if you cannot say which fix you are verifying, you are doing exploratory testing, which is fine, but call it that.
- Skipping smoke because "it worked yesterday" - the whole point is catching the morning where it did not.
