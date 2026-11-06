# Equivalence partitioning with worked examples

Equivalence partitioning (EP) divides the possible inputs of a field into groups ("partitions") that the application should treat the same way. Testing one representative value per partition gives the same confidence as testing every value in it, at a fraction of the effort. It is usually the first technique I apply to a form, and it pairs naturally with boundary value analysis (see `boundary-value-analysis-examples.md`).

All examples below use the public practice app https://www.saucedemo.com, so anyone can reproduce them.

## Example 1: login form

Fields: Username, Password. Both are free-text; the app accepts a fixed set of known users.

| # | Partition | Representative value | Expected result |
|---|-----------|---------------------|-----------------|
| 1 | Valid, active username + correct password | standard_user / secret_sauce | Login succeeds, inventory page loads |
| 2 | Valid but locked-out username + correct password | locked_out_user / secret_sauce | Login blocked with a lockout message |
| 3 | Unknown username + any password | not_a_real_user / secret_sauce | Generic credentials error |
| 4 | Valid username + wrong password | standard_user / wrong_password | Same generic credentials error |
| 5 | Empty username | (empty) / secret_sauce | Validation: username required |
| 6 | Empty password | standard_user / (empty) | Validation: password required |
| 7 | Whitespace-only username | "   " / secret_sauce | Treated as unknown user or validation error (verify actual behaviour) |

Notes on the choices:

- Partitions 3 and 4 should produce the *same* generic message. If the app distinguishes "unknown user" from "wrong password", that is an information-disclosure finding, not just a cosmetic difference.
- Partition 7 is deliberately ambiguous: the expected result is written as a question to answer in the run log, not assumed.

## Example 2: checkout information form

Fields: First Name, Last Name, Zip/Postal Code (saucedemo checkout step one).

| # | Partition | Representative value | Expected result |
|---|-----------|---------------------|-----------------|
| 1 | Ordinary alphabetic names + plausible postal code | Abdul / Moez / 59250 | Continue to checkout overview |
| 2 | Empty First Name | (empty) | Validation: first name required |
| 3 | Empty Last Name | (empty) | Validation: last name required |
| 4 | Empty Postal Code | (empty) | Validation: postal code required |
| 5 | Names with hyphens/apostrophes | Anne-Marie / O'Brien | Accepted (real-world names) |
| 6 | Names with digits or symbols | Abd7l / M*oez | Verify: accepted or rejected - record actual |
| 7 | Non-postal characters in postal code | ABCDE | Verify actual behaviour (the app is US-flavoured; record what happens) |
| 8 | Very long inputs (300+ chars) | 300 x "a" | Verify: accepted, truncated, or validation error |

## How to write partitions that hold up

1. Partition by *behaviour*, not by data type. "Locked-out user" is its own partition because the app behaves differently, even though it is a valid username.
2. Always include the empty case and at least one malformed case per required field.
3. When the expected result is genuinely unknown, say so and let the run log answer it. Never write an expectation you did not ground.
4. One representative per partition is enough until a partition fails; then investigate within it.
