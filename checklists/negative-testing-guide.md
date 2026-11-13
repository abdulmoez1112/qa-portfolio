# Negative testing: a practical guide

Positive testing proves the product works when everyone behaves. Negative testing proves it fails safely when they don't. Most production incidents live in the second category.

## What makes a test "negative"

A negative test feeds the system input, state or sequences it should reject or survive, and checks that it:

1. Rejects with a clear, specific message, or
2. Degrades gracefully (no crash, no corruption, no silent acceptance).

Silent acceptance is the worst outcome: the system says nothing and does the wrong thing. That is a defect even when no error appears.

## The five categories

### 1. Invalid input
Wrong types, formats, characters. Letters in numeric fields, symbols in names, malformed emails, script strings. (See the 12 Nov checkout form session: postal code accepted `!@#$%^&*()`.)

### 2. Missing data
Empty required fields, whitespace-only input, null-equivalents. Remember: whitespace-only is NOT empty to most naive validators - always test it separately. Record it as an observation against implicit requirements, not a confirmed defect, unless a spec says otherwise.

### 3. Boundary violations
One below minimum, one above maximum, absurd lengths (300+ chars), negative numbers, zero. Boundaries are where off-by-one errors live.

### 4. State and sequence violations
The most neglected category and the most productive:
- Steps out of order: jump to step 2 of a wizard without step 1 (direct URL)
- Missing prerequisites: checkout with an empty cart
- Repeated actions: submit twice, double-click, browser Back then re-submit
- Stale state: back/refresh mid-flow, session expired mid-action

### 5. Permission violations
Accessing pages or actions without the required role or login. (Saucedemo handles this one correctly: logged-out users hitting /inventory.html get bounced with an error - a good control example.)

## Designing negative cases

1. Start from each requirement and ask "what if this is absent, wrong, or repeated?"
2. Walk the state machine of the flow: every transition should have a "what if I arrive here without the previous state?" case.
3. Mine past defects: every historical bug suggests a family of negatives (BR-003's field contamination suggests testing every pair of adjacent fields).

## Reporting negative findings

- State expected vs actual even when "expected" is implicit: "any sane checkout rejects an empty cart" is defensible; phrase it as the expected behavior.
- Distinguish severity honestly: a missing nice-to-have validation is not the same as a $0 order being accepted.
- One root cause per report: three symptoms of "no state validation" are one bug, not three (see BR-007).

## Evidence from this portfolio

- 12 Nov: [checkout form validation session](../test-cases/saucedemo/checkout-form-validation-session-2026-11-12.md) - input-level negatives
- 13 Nov: [negative checkout session](../test-cases/saucedemo/negative-checkout-session-2026-11-13.md) - state and sequence negatives, three confirmed failures
