# Decision table testing

Decision tables list every combination of conditions and the expected action for each. They are useful when business rules depend on several yes/no inputs and a missed combination would be a missed bug.

## When to use it
- Rules with 2 to 5 independent conditions (login, checkout, discounts, permissions).
- Requirements written as "if A and B then C, unless D".
- Any place where testers tend to check only the happy path and one failure.

## Steps
1. List the conditions (inputs) and the actions (outputs).
2. Build one column per combination (2^n columns for n yes/no conditions).
3. Fill in the expected action for each column from the requirement, not from the app.
4. Merge columns where a condition does not change the result.
5. Turn each remaining column into one test case.

## Example: login form (rules written from common expectations, to be checked against a real app)

| Condition / Action            | R1 | R2 | R3 | R4 |
|-------------------------------|----|----|----|----|
| Username is valid             | Y  | Y  | N  | N  |
| Password is valid             | Y  | N  | Y  | N  |
| **Action: log in**            | X  |    |    |    |
| **Action: show error message**|    | X  | X  | X  |
| **Action: stay on login page**|    | X  | X  | X  |

Four columns give four test cases. A good extra check: the error message should not reveal whether the username or the password was wrong.

## Example: checkout with discount code

| Condition / Action        | R1 | R2 | R3 | R4 | R5 |
|---------------------------|----|----|----|----|----|
| Cart has items            | Y  | Y  | Y  | Y  | N  |
| Code is valid             | Y  | Y  | N  | N  | -  |
| Code is not expired       | Y  | N  | -  | -  | -  |
| Customer is logged in     | Y  | Y  | Y  | N  | -  |
| **Discount applied**      | X  |    |    |    |    |
| **Error shown**           |    | X  | X  |    |    |
| **Ask user to log in**    |    |    |    | X  |    |
| **Checkout blocked**      |    |    |    |    | X  |

"-" means the condition does not change the result for that column. Whether the rule for R4 is correct (log in first versus allow guest codes) is a question for the product owner. Record it as an open question, not as a bug.

## Tips
- Write the table before opening the app, so the app does not decide the expected result.
- Count columns before merging, so a merge never hides a missing case.
- Link each column to a test case ID in test-cases/.

## Limits
This guide shows the technique with sample rules. It is not a record of a test run.
