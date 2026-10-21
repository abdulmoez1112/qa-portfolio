# API Testing with Postman - Practical Notes

How I structure a manual API test pass in Postman, using a typical REST product API as the example.

## Collection setup

- One collection per product, one folder per resource (auth, products, cart, orders).
- Environment variables for base_url, auth token, and test user credentials. Never hardcode tokens in requests.
- A health-check request (GET /status or equivalent) runs first in every session.

## What I test per endpoint

1. Happy path: valid request returns 200/201 with the documented schema.
2. Auth: missing or expired token returns 401, not 200 or 500.
3. Validation: missing required fields return 400 with a useful error body.
4. Boundaries: empty strings, very long strings, negative numbers, zero, unicode.
5. Methods: wrong HTTP method returns 405; unknown route returns 404.
6. State: create -> read -> update -> delete in sequence, verifying each step actually persisted.
7. Idempotency where it matters: repeating the same POST must not duplicate records (or must be documented behavior).

## Quick test scripts I keep in Postman

- Status code assertion: `pm.test("status is 200", () => pm.response.to.have.status(200))`
- Response time budget: fail the request if over 1500 ms.
- Schema spot check: assert required keys exist in the JSON body before checking values.

## Bug reporting for API defects

Same template as UI bugs, plus: full request (method, URL, headers, body), full response (status, body), and a cURL export so a developer can reproduce in one paste.
