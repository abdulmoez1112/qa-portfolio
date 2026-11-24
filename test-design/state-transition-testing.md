# State transition testing

State transition testing checks that a system moves between states correctly in response to events, and that invalid moves are rejected. It fits anything with a lifecycle: orders, accounts, bug tickets, sessions.

## Building blocks
- **States**: the conditions the object can be in.
- **Events**: what triggers a change.
- **Transitions**: state A + event -> state B.
- **Guards**: conditions that must hold for a transition.
- **Invalid transitions**: events that should do nothing or show an error.

## Example: order lifecycle (sample model)

States: Cart, Placed, Paid, Shipped, Delivered, Cancelled.

| From      | Event         | To        | Valid? |
|-----------|---------------|-----------|--------|
| Cart      | place order   | Placed    | Yes    |
| Placed    | pay           | Paid      | Yes    |
| Placed    | cancel        | Cancelled | Yes    |
| Paid      | ship          | Shipped   | Yes    |
| Paid      | cancel        | Cancelled | Yes (refund) |
| Shipped   | deliver       | Delivered | Yes    |
| Shipped   | cancel        | -         | No, reject |
| Delivered | pay           | -         | No, reject |
| Cancelled | ship          | -         | No, reject |

## Coverage levels
1. **All states**: visit each state at least once.
2. **All transitions**: execute every valid transition once.
3. **Invalid transitions**: try every "No" row and confirm nothing changes.
4. **Paths**: chain transitions (Cart -> Placed -> Paid -> Cancelled) to find bugs that only appear after a sequence.

## Sample test cases
- ST-01: Cart -> Placed -> Paid. Expect status Paid and a receipt.
- ST-02: Placed -> Cancelled. Expect no charge.
- ST-03: Shipped, then cancel. Expect rejection and status still Shipped.
- ST-04: Press back or refresh after Paid, then pay again. Expect no second charge.

## What to look for
- Back button, refresh and double click creating a second transition.
- Status shown in the UI differing from the status in the database or email.
- Missing error messages for rejected moves.

## Limits
The order model is a teaching example. Adjust states and rules to the real requirements before using it.
