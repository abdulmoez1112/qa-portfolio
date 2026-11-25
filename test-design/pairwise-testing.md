# Pairwise (all-pairs) testing

Most bugs are caused by one input or the interaction of two inputs. Pairwise testing covers every pair of values across parameters with far fewer tests than the full combination set.

## Why use it
Full combinations grow fast. Browser (3) x OS (3) x language (3) x payment (3) = 81 tests. Every pair of values can be covered in about 9.

## Steps
1. List parameters and their values (keep to equivalence classes).
2. Generate a pair-covering set with a tool (for example PICT or an online all-pairs generator).
3. Add known risky triples by hand.
4. Add constraints, for example Safari does not run on Windows.
5. Run the tests and record results per row.

## Example: 3 parameters x 3 values (sample)

| # | Browser | OS      | Payment |
|---|---------|---------|---------|
| 1 | Chrome  | Windows | Card    |
| 2 | Chrome  | Android | Wallet  |
| 3 | Chrome  | macOS   | COD     |
| 4 | Firefox | Windows | Wallet  |
| 5 | Firefox | Android | COD     |
| 6 | Firefox | macOS   | Card    |
| 7 | Safari  | Windows | COD     |
| 8 | Safari  | Android | Card    |
| 9 | Safari  | macOS   | Wallet  |

Every browser/OS, browser/payment and OS/payment pair appears at least once. Row 7 breaks the Safari/Windows constraint above, so a real set must replace it.

## Limits
- It will miss bugs that need three or more values together.
- Results are only as good as the chosen values.
- This is a technique guide with sample data, not a record of a test run.
