# Cross-Browser Testing Checklist (Web App)

Checklist for running the same core user flows across browsers, using the practice app https://www.saucedemo.com as the target. Coverage below is PLANNED: every row starts "Not run" and is only marked Pass/Fail with a date when someone actually runs it in that browser. The only executed results so far are in the "Performed checks" section at the bottom.

## Planned coverage - core flows per browser

Status legend: Not run | Pass | Fail | Blocked. Fill the date and browser version when a row is executed.

| # | Check | Chrome | Firefox | Edge | Safari (macOS) | Chrome (Android) | Safari (iOS) |
|---|-------|--------|---------|------|----------------|------------------|--------------|
| 1 | Login page loads: logo, both fields, Login button, no console errors visible in layout | Not run | Not run | Not run | Not run | Not run | Not run |
| 2 | Valid login (standard_user) lands on /inventory.html | Not run | Not run | Not run | Not run | Not run | Not run |
| 3 | Invalid login shows an error banner and stays on the login page | Not run | Not run | Not run | Not run | Not run | Not run |
| 4 | Product list renders 6 products, each with image, name, price, Add to cart button | Not run | Not run | Not run | Not run | Not run | Not run |
| 5 | Product images load (no broken image icons) | Not run | Not run | Not run | Not run | Not run | Not run |
| 6 | Sort dropdown: all 4 options change the order correctly | Not run | Not run | Not run | Not run | Not run | Not run |
| 7 | Add to cart updates the cart badge; cart page lists the same items | Not run | Not run | Not run | Not run | Not run | Not run |
| 8 | Remove from cart page removes the item and updates the badge | Not run | Not run | Not run | Not run | Not run | Not run |
| 9 | Checkout: form fields accept input, validation errors on empty submit, order completes and shows the confirmation | Not run | Not run | Not run | Not run | Not run | Not run |
| 10 | Menu opens, Logout returns to the login page | Not run | Not run | Not run | Not run | Not run | Not run |
| 11 | Layout: header, cart icon, product grid and buttons aligned, no overlap or clipped text | Not run | Not run | Not run | Not run | Not run | Not run |
| 12 | Links and buttons respond on first click/tap; no dead controls | Not run | Not run | Not run | Not run | Not run | Not run |
| 13 | Mobile browsers only: menu, sort dropdown and cart usable at phone width, no horizontal scrolling | - | - | - | - | Not run | Not run |
| 14 | Zoom to 200% (desktop): content still readable, no overlapping elements | Not run | Not run | Not run | Not run | - | - |

## What differs per browser (watch list)

- Safari (WebKit): date and number inputs render differently; flexbox gaps in older versions; no support for some newer CSS features. Check layout rows 11 and 14 carefully.
- Firefox: form autofill behaves differently; check that the login form does not prefill in a way that hides the labels.
- Mobile browsers: the burger menu and sort dropdown are the most fragile controls at small widths; row 13 is the mobile priority.
- Font rendering differs across engines, so compare text wrapping on product names, not pixel-perfect matches.

## Performed checks (actually executed)

Executed by me on 26 Oct 2026 in Chrome 155.0.0.0 (Linux x86_64, desktop viewport) against the live https://www.saucedemo.com. Only these rows were run; everything in the planned table above remains Not run.

| Check | Browser / date | Result | Observed |
|-------|----------------|--------|----------|
| Valid login (standard_user / secret_sauce) | Chrome 155, 26 Oct 2026 | Pass | Redirected to /inventory.html |
| Product list renders with images, names, prices | Chrome 155, 26 Oct 2026 | Pass | 6 products, all with images; default sort "Name (A to Z)"; prices $7.99-$49.99 |
| Sort "Price (low to high)" | Chrome 155, 26 Oct 2026 | Pass | Order became $7.99, $9.99, $15.99, $15.99, $29.99, $49.99 (Onesie first, Fleece Jacket last) |
| Add to cart badge and cart contents | Chrome 155, 26 Oct 2026 | Pass | Badge showed 1 after adding; cart page listed the added item |
| Logout from menu | Chrome 155, 26 Oct 2026 | Pass | Returned to the login page |

Remaining coverage needs real runs in Firefox, Edge, Safari and on physical Android/iOS devices before those columns can be marked.
