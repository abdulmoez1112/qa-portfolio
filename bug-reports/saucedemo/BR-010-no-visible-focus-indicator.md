# BR-010: No visible focus indicator on the login, inventory and cart pages - keyboard focus is invisible where it lands

- Date found: 2026-11-15
- Found by: Abdul Moez
- Test user: standard_user / secret_sauce
- Environment: Chrome (cloud browser), desktop viewport, https://www.saucedemo.com - a public demo/practice app maintained by Sauce Labs. Practice finding against a demo environment, not a live store.
- WCAG: 2.4.7 Focus Visible (AA)
- Severity: High (QA judgment - see Impact)
- Priority: High (QA judgment)
- Status: Open

## Summary

Across the login, inventory and cart pages, the focused element shows no visible indicator: the computed `outline-style` is `none` at every tab stop, with no replacement styling (no `box-shadow`, no border or background change). A keyboard user can operate most of the app but cannot see where they are.

## Steps to reproduce

1. Log in as standard_user.
2. On any page, press Tab repeatedly and watch the page: nothing highlights. The login screenshot taken with Password focused shows no ring, border or background change.
3. (Confirmation) Compare computed styles: the focused Add-to-cart button is identical to an unfocused one - `outline: none`, `box-shadow: none`, same 1px dark border, same white background. The same holds for text fields, links, the sort select and the menu button.

## Expected vs actual

- Expected: every focusable element shows a clearly visible focus indicator (browser default ring or a styled replacement).
- Actual (UI/DOM-observable): `outline-style: none` on every focused element observed - 3 stops on the login page, 23 on the inventory page, 6 on the cart page - with no compensating style. Chrome's default focus ring is suppressed by the site's CSS.

## Evidence

- Per-stop computed styles recorded during a full keyboard-only walk; focused-vs-unfocused style comparison of the same control; screenshots taken with focus on form fields and buttons.
- Session log with captures: [keyboard-only session, 15 Nov](../../test-cases/saucedemo/keyboard-only-session-2026-11-15.md).

## Scope of evidence

- Verified in Chrome via computed styles and screenshots for every tab stop on the three core pages.
- Not verified: high-contrast / forced-colours modes, other browsers, mobile viewports.

## Impact (QA judgment in a demo context)

Severity/priority are QA judgment for a flow of this kind, not validated production impact. Keyboard operability exists for most controls (see BR-009 for the one that is not operable), but invisible focus makes keyboard use impractical: the user must guess the focus position or count Tab presses. WCAG 2.4.7 is a Level AA criterion; the failure also undercuts Low Vision usability (2.4.13 Focus Appearance in WCAG 2.2, AAA).

## Notes

- This is a global stylesheet issue (one rule removing outlines without a replacement), so a single CSS fix would resolve every instance; noted for practice completeness, not as prescriptive guidance to the demo's authors.
