# Checkout Boundary-Value Tests (saucedemo.com)

Boundary value analysis for the checkout information form of the practice app https://www.saucedemo.com (standard_user / secret_sauce). The design table lists the boundary classes to cover; the results table at the bottom records what actually happened when I ran them. Status is "Not run" until executed.

## Boundary classes to design around

For each text field (First Name, Last Name, Zip/Postal Code) the meaningful boundaries are:

| Class | Boundaries to test | Expected in a typical web shop |
|-------|--------------------|--------------------------------|
| Empty | "" (submit without touching) | Blocked with a field-specific error |
| Minimum length | 1 character | Usually accepted for names; postal codes have a format-dependent minimum |
| Typical | "Abdul", "Moez", "54000" | Accepted |
| Upper length | Just under / at / over any maxlength (if none set: 100+ and 1000+ characters) | Accepted up to a sane documented limit, or blocked with a clear message |
| Character set | Letters, apostrophes, hyphens, digits, spaces, HTML/script metacharacters | Names: letters plus ' and - accepted, metacharacters rejected or safely escaped |
| Zip format | All digits, all letters, mixed, wrong length for the country | Format validated with a clear error |
| Totals | Price boundaries: cheapest cart, most expensive cart, tax rounding at the cent | Subtotal + tax = total, rounding consistent |

## How to run

One boundary per pass: cart -> Checkout -> fill only the values under test -> Continue -> record error text or the page reached. Check the overview page totals on every pass that gets through. Log deviations as bugs.

## Performed results

Executed by me on 30 Oct 2026 in Chrome 155.0.0.0 (Linux x86_64) against the live app, one Backpack ($29.99) in the cart. Only these rows were run.

| # | Boundary tested | Input | Observed result | Assessment |
|---|-----------------|-------|-----------------|------------|
| 1 | Empty form | (nothing) | Blocked: "Error: First Name is required" | Pass - validation fires |
| 2 | Minimum length, all fields | First "A", Last "B", Zip "1" | Accepted, reached the overview page | Finding - 1-character names and a 1-digit zip pass |
| 3 | Upper length | First name: 101 characters (field has no maxlength attribute) | Accepted, reached the overview | Finding - no upper bound |
| 4 | Script metacharacters | Last name: O'Brien<script>alert(1)</script> | Accepted; no script element rendered in the overview DOM (framework escaped it) | Pass for escaping; the value is accepted without complaint |
| 5 | Zip format | Zip: "ABCDE" (letters) | Accepted, order flow continued | Finding - no zip format validation at all |
| 6 | Totals math | 1 x Backpack | Item total $29.99, Tax $2.40, Total $32.39 | Pass - 8% tax, cent rounding correct |
| 7 | Order completion with boundary junk | Rows 2-5 values left in place | Order completed: "Thank you for your order!" | Finding - an order can be placed with a 101-character first name, a script-tag last name and a letter-only zip |
| 8 | HTML constraints | Inspected the three fields | No maxlength and no required attribute on any field; all validation is on-submit | Note - client-side prevention is absent by design here |

## Notes

- The empty-field check (row 1) is the only gate: anything non-empty, of any length or character set, goes through. In a real shop rows 2, 3, 5 and 7 would be logged as bugs with a product decision on limits.
- The escaping observed in row 4 covers the overview page; any other place that later displays the name (emails, admin views) would need the same check.
- Remaining classes not yet run: 1000+ character input, cheapest-cart and most-expensive-cart total boundaries, tax rounding on prices like $15.97. Status: Not run.
