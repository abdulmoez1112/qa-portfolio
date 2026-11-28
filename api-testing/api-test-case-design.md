# Designing API test cases

Reference notes on how to turn an API endpoint into a set of test cases.
This is a reference document, not a record of a test run.

## Start from the contract, not the UI

For each endpoint write down:

- Method and path (GET /users/{id})
- Required and optional parameters, with types
- Auth requirements (none, token, role)
- Success response: status code and body shape
- Documented error responses

Every test case should map to one row of that contract so coverage is easy to see.

## A minimum case set per endpoint

1. **Happy path** - valid request, expect the documented success code and body.
2. **Each required field missing** - one case per field, expect 400 (or the documented code).
3. **Wrong types** - string where a number is expected, expect rejection.
4. **Boundary values** - min, max, just below min, just above max for numeric params; empty and max-length for strings.
5. **Auth cases** - no token, expired token, valid token with wrong role.
6. **Not found** - valid format id that does not exist, expect 404.
7. **Method not allowed** - POST to a GET-only endpoint, expect 405.

## Checks beyond the status code

- Response body matches the schema (field names, types, no missing keys).
- No extra fields leaking internal data (stack traces, SQL errors, other users' data).
- Headers: Content-Type is correct, caching headers where they matter.
- Side effects: a POST actually created the resource, a DELETE actually removed it. Verify with a follow-up GET, not just the response message.
- Response time within the agreed budget for the endpoint.

## Idempotency and state

- Repeating a GET should return the same result.
- Repeating a PUT with the same body should leave the resource in the same state.
- Repeating a POST should either create duplicates deliberately or be rejected, whichever the contract says. If it is not documented, ask.

## Common mistakes

- Only testing the happy path and one 400 case.
- Asserting on the full response body when only three fields matter, which makes tests brittle.
- Sharing test data between cases so they pass alone but fail in a suite, or the reverse.
- Cleaning up created data in the test itself instead of a teardown step, so a failing assert skips cleanup.

## Quick checklist before calling an endpoint "tested"

- [ ] Happy path with schema validation
- [ ] Each required field missing
- [ ] Wrong types and boundary values
- [ ] Auth: none, wrong, insufficient
- [ ] 404 for missing resources
- [ ] Side effects verified with a follow-up read
- [ ] Test data created and cleaned up reliably
