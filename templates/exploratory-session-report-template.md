# Exploratory Session Report Template

Template for reporting a timeboxed exploratory testing session, in the spirit of session-based test management: one charter, one timebox, a written record someone else can review. A filled example from a real session follows the template.

## Template

```
Session: [short name, e.g. "checkout form boundaries"]
Date: | Tester: | Duration planned vs actual: [e.g. 45 min planned, 40 min actual]
Environment: [app/URL, browser and version, account used]

Charter (one sentence):
[What this session set out to explore, and why.]

Scope:
- In: [pages/flows/features covered]
- Out: [what was deliberately left for other sessions]

Notes (chronological, brief):
- [time] [what I tried] -> [what happened]
- ...

Findings:
- Bugs filed: [BR IDs, or "none"]
- Behavior worth a product decision: [things that are not clearly bugs but need an answer]
- Questions raised: [what I could not determine in this session]

Coverage vs charter:
- [Did the session cover the charter? What was skipped and why?]

Debrief summary (3 lines max):
[The one thing a reviewer should take away. Risks remaining. Suggested next session.]
```

## Guidance

- Write notes DURING the session, not after; memory edits details.
- A finding without a bug report needs a reason: out of scope, already filed, or needs a product answer first.
- "Planned vs actual" duration matters: big overruns usually mean the charter was too wide.
- The debrief summary is for someone who will not read the notes. If they only read three lines, what must those lines say?

## Filled example (real session)

```
Session: checkout form boundaries on saucedemo.com
Date: 30 Oct 2026 | Tester: (this portfolio's daily session) | Duration: ~25 min
Environment: saucedemo.com, Chrome 155.0.0.0 (Linux x86_64), standard_user / secret_sauce

Charter:
Probe the checkout information form (First Name, Last Name, Zip/Postal Code) at its
boundaries - empty, minimum, extreme length, odd character sets - and check the
totals math on the overview page.

Scope:
- In: checkout step one validation, overview totals, order completion with boundary data
- Out: payment/shipping steps (the demo app has none), performance, other accounts

Notes (abridged):
- Empty submit -> blocked, "Error: First Name is required"
- "A"/"B"/"1" (1 char each) -> accepted, reached overview
- 101-character first name -> accepted; fields have no maxlength attribute
- Last name "O'Brien<script>alert(1)</script>" -> accepted; overview DOM contains no
  script element (framework escaped it)
- Zip "ABCDE" -> accepted, no format validation
- Totals with 1 x Backpack: $29.99 + $2.40 tax = $32.39 (8%, correct rounding)
- Finish with the boundary values still in place -> "Thank you for your order!"

Findings:
- Bugs filed: none in-session; recorded as results in test-cases/checkout-boundary-value-tests.md
- Behavior worth a product decision: any non-empty value of any length or character
  set is accepted end-to-end; only empty fields are blocked
- Questions raised: does any downstream view (email, admin) display the name fields,
  and is escaping applied there too?

Coverage vs charter:
- Covered. Skipped: 1000+ character input and cheapest/most-expensive cart totals
  (listed as Not run in the test document).

Debrief summary:
The only working gate is non-emptiness. Length, character set and zip format are all
unchecked, and an order completes with junk data. Next session: repeat with
problem_user and error_user to compare validation behavior across accounts.
```
