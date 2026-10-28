# Accessibility Quick-Check Guide (15 minutes per page)

A fast manual accessibility pass for a web page, meant to catch the most common problems before a fuller WCAG audit. Run it on every key page (login, product list, cart, checkout). The checks below are PLANNED steps; the "Performed example run" section at the bottom shows one real execution with its actual findings.

## The 8 checks

### 1. Page language (30 seconds)
View source or run `document.documentElement.lang` in the console. A valid `lang` attribute (for example `en`) must be set so screen readers use the right pronunciation.

### 2. Keyboard only (3 minutes)
Unplug the mouse. Tab through the whole page. Every interactive element (links, buttons, dropdowns, form fields) must be reachable, the focus must be visible at all times, and the order must follow the visual layout. Submit a form with Enter. If anything needs a mouse, that is a failure.

### 3. Form labels (2 minutes)
Every input needs an accessible name: a `<label for>` element, an `aria-label`, or `aria-labelledby`. A placeholder alone is not enough: it disappears when the user types and is not reliably announced. Quick check: click the visible label text - the matching field should receive focus.

### 4. Buttons and links have distinct names (2 minutes)
Every button must have an accessible name that says what it does. If a page repeats the same name ("Add to cart" six times), check whether assistive technology can tell them apart (for example via `aria-label` per product) - identical names with only visual context are a problem.

### 5. Images and alt text (2 minutes)
Every informative image needs meaningful `alt` text. Purely decorative images need `alt=""` so screen readers skip them. Broken or missing alt on a product photo means a blind shopper does not know what is being sold.

### 6. Error messages are announced (2 minutes)
Submit a form with an error. The error must be visible AND programmatically exposed: `role="alert"` or an `aria-live` region, so a screen reader announces it without the user hunting for it. An error that only appears visually is a failure.

### 7. Headings and page structure (2 minutes)
Headings must exist, start at one `h1`, and not skip levels. Landmark regions (header, nav, main, footer) help screen reader users jump around. Quick check: browser devtools accessibility tree, or a headings-outline extension.

### 8. Contrast and zoom (3 minutes)
Text must stay readable at 200% zoom with no overlap or loss of content. Normal text needs a 4.5:1 contrast ratio, large text 3:1 (check with a contrast tool or devtools). Light gray placeholder text on white is a frequent failure.

## Recording results

Mark each check Pass / Fail / Not run per page, with the browser and date. A Fail needs: what you did, what you observed, which check it breaks, and a screenshot if the issue is visual. Never mark a check you did not actually run.

## Performed example run

Executed by me on 28 Oct 2026 in Chrome 155.0.0.0 (Linux x86_64) against the live https://www.saucedemo.com, login and product list pages. Only these checks were run; everything not listed here is Not run.

| Check | Result | Observed |
|-------|--------|----------|
| 1. Page language | Pass | `html lang="en"` is set |
| 2. Keyboard (tab order, login page) | Pass | Tab order follows the layout: Username - Password - Login; Enter submits |
| 3. Form labels (login) | Partial - finding | No `<label>` elements; accessible names come from `aria-label` ("Username", "Password") so screen readers do get a name, but the only visible label is the placeholder, which disappears while typing |
| 4. Distinct button names (product list) | Finding | All six buttons have the identical accessible name "Add to cart" with no `aria-label` to say which product; only visual position links them |
| 5. Image alt text (product list) | Pass | All 6 product images have meaningful alt text (product names) |
| 6. Error announcement (login) | Finding | Submitting empty shows "Epic sadface: Username is required" visually, but the container has no `role="alert"` or `aria-live`, so a screen reader may stay silent |
| Cart link name | Pass | The icon-only cart link has `aria-label="Cart, empty"` |
| Sort dropdown name | Pass | The sort dropdown has `aria-label="Sort products"` |

Findings 3, 4 and 6 are logged as observations from this run; they have not been retested in other browsers or with an actual screen reader, which would be the next step before confirming severity.
