# Boundary value analysis with worked examples

Boundary value analysis (BVA) concentrates testing on the edges of an input domain, because defects cluster where behaviour changes: exactly at the minimum, exactly at the maximum, and one step either side. It is the natural partner of equivalence partitioning (see `equivalence-partitioning-examples.md`): EP picks the groups, BVA picks the riskiest representatives inside and around them.

## The standard pattern

For a numeric range **min..max**, test:

| Point | Value | Why |
|-------|-------|-----|
| min - 1 | just below | should be rejected |
| min | lower edge | should be accepted |
| min + 1 | just above | should be accepted |
| nominal | a comfortable middle value | normal operation |
| max - 1 | just below top | should be accepted |
| max | upper edge | should be accepted |
| max + 1 | just above | should be rejected |

For a **length** limit (characters), the same idea applies to length: 0, 1, max-1, max, max+1.

## Example 1: quantity field, valid range 1-10

| Input | Partition/edge | Expected |
|-------|---------------|----------|
| 0 | min - 1 | Rejected (validation message, no silent clamp) |
| 1 | min | Accepted |
| 2 | min + 1 | Accepted |
| 5 | nominal | Accepted |
| 9 | max - 1 | Accepted |
| 10 | max | Accepted |
| 11 | max + 1 | Rejected |

Watch for off-by-one defects: accepting 11, or rejecting 10, are the classic BVA catches. Also record *how* rejection happens - a visible message, a silent clamp to the nearest valid value, or a spin button that refuses to move. Silent clamping is a usability finding worth reporting even when the data stays valid.

## Example 2: name field, required, 1-50 characters

| Input length | Edge | Expected |
|--------------|------|----------|
| 0 | below min | "Required" validation |
| 1 | min | Accepted |
| 2 | min + 1 | Accepted |
| 49 | max - 1 | Accepted |
| 50 | max | Accepted |
| 51 | max + 1 | Rejected or truncated - record which |

Truncation without a message loses user data silently; that is reportable.

## Example 3: number input widgets (spinner arrows)

HTML number inputs add their own boundaries: typed vs stepped input can behave differently, exponent notation (1e3) may parse as 1000, and non-numeric keystrokes may be dropped or clear the field. A boundary run should cover:

- typing below/above the range,
- stepping with the arrows across min and max,
- non-numeric input (what happens to the field value),
- exponent and decimal input.

## Writing it up

1. State the domain (range or length) and where it comes from - requirement, or observed behaviour labelled as observed.
2. One row per edge, exact input, exact observed result.
3. Distinguish "rejected with a message" from "silently changed" - both can be correct, only one is visible to the user.
4. When the app has no documented limits, the run log is where the real boundaries get discovered; record them as findings, not assumptions.
