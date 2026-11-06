# Session log: login boundary and partition checks (saucedemo.com)

- Date: 6 November 2026
- Environment: Chrome (cloud browser), https://www.saucedemo.com login page
- Duration: ~15 minutes
- Charter: execute the login partitions from `test-design/equivalence-partitioning-examples.md` and record exact behaviour, including the two open questions (whitespace-only username, very long username).

## Results

| # | Input | Expected | Actual (verbatim) | Status |
|---|-------|----------|-------------------|--------|
| 1 | standard_user / secret_sauce | Login succeeds | Redirected to /inventory.html | PASS |
| 2 | locked_out_user / secret_sauce | Lockout message | "Epic sadface: Sorry, this user has been locked out." | PASS |
| 3 | (empty) / secret_sauce | Username required | "Epic sadface: Username is required" | PASS |
| 4 | standard_user / (empty) | Password required | "Epic sadface: Password is required" | PASS |
| 5 | not_a_real_user / secret_sauce | Generic credentials error | "Epic sadface: Username and password do not match any user in this service" | PASS |
| 6 | standard_user / wrong_password | Same generic error | Identical message to #5 (no user enumeration) | PASS |
| 7 | "   " (whitespace) / secret_sauce | Open question | Same generic mismatch message; whitespace is NOT trimmed into a validation error, it is treated as an unknown user | ANSWERED |
| 8 | 300-character username / secret_sauce | Open question | Same generic mismatch message; no truncation error, no crash | ANSWERED |

## Notes

- Checks 5 and 6 returning byte-identical messages is good security behaviour: the app does not reveal whether the username exists.
- Each case was run through the real UI (typed into the fields, Login clicked); error text captured from the page after submit.
- No defects found in this session. The two open questions from the partitioning guide are now answered and recorded here.
