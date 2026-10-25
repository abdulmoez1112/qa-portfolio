# API Testing Notes with Worked Postman Examples

Practical API testing notes using the free practice API JSONPlaceholder (https://jsonplaceholder.typicode.com). Examples below were run for real on 25 Oct 2026; the observed responses are quoted next to each one. Postman test snippets go in the request's "Tests" tab.

## What to check on every API test

1. **Status code** - not just 200 vs 404. Check the exact code: 200 (OK), 201 (created), 204 (no content), 400 (bad request), 401 (unauthorized), 404 (not found), 500 (server error).
2. **Response body** - correct fields, correct types, values match the request or the expected data.
3. **Headers** - `Content-Type: application/json` on JSON APIs; caching and rate-limit headers where relevant.
4. **Response time** - a slow endpoint is a defect even when it returns the right data.
5. **Negative cases** - missing fields, wrong types, invalid IDs, unauthorized access. The API should fail cleanly, not crash or leak a stack trace.
6. **Side effects** - after POST/PUT/DELETE, read the resource back with GET to confirm the change (or confirm it is gone).

## Worked example 1: GET an existing resource

Request: `GET https://jsonplaceholder.typicode.com/posts/1`

Observed: `200 OK`, body contains `"userId": 1`, `"id": 1`, plus `title` and `body` strings.

Postman test:

```javascript
pm.test("status is 200", function () {
    pm.response.to.have.status(200);
});
pm.test("id matches the requested post", function () {
    var json = pm.response.json();
    pm.expect(json.id).to.eql(1);
    pm.expect(json).to.have.property("title");
    pm.expect(json.title).to.be.a("string").and.not.empty;
});
pm.test("responds in under 1s", function () {
    pm.expect(pm.response.responseTime).to.be.below(1000);
});
```

## Worked example 2: POST create a resource

Request: `POST https://jsonplaceholder.typicode.com/posts` with header `Content-Type: application/json` and body:

```json
{
  "title": "QA check",
  "body": "created from notes",
  "userId": 1
}
```

Observed: `201 Created`, the response echoes the sent fields and adds a server-generated `"id": 101`.

Postman test:

```javascript
pm.test("status is 201 Created", function () {
    pm.response.to.have.status(201);
});
pm.test("server returns an id and echoes the request", function () {
    var json = pm.response.json();
    pm.expect(json).to.have.property("id");
    pm.expect(json.title).to.eql("QA check");
    pm.expect(json.userId).to.eql(1);
});
```

Note: JSONPlaceholder fakes persistence. A created post appears in the response but is not really stored, so a follow-up GET on `/posts/101` returns 404. On a real API, the create-then-read-back check in step 6 applies.

## Worked example 3: PUT full update

Request: `PUT https://jsonplaceholder.typicode.com/posts/1` with body:

```json
{
  "id": 1,
  "title": "updated",
  "body": "full update",
  "userId": 1
}
```

Observed: `200 OK`, response contains the updated fields with `"id": 1`.

Postman test:

```javascript
pm.test("status is 200", function () {
    pm.response.to.have.status(200);
});
pm.test("fields were updated", function () {
    var json = pm.response.json();
    pm.expect(json.title).to.eql("updated");
    pm.expect(json.id).to.eql(1);
});
```

## Worked example 4: DELETE a resource

Request: `DELETE https://jsonplaceholder.typicode.com/posts/1`

Observed: `200 OK` with an empty JSON object `{}` as the body.

Postman test:

```javascript
pm.test("status is 200 or 204", function () {
    pm.expect(pm.response.code).to.be.oneOf([200, 204]);
});
```

## Worked example 5: negative case - resource that does not exist

Request: `GET https://jsonplaceholder.typicode.com/posts/999`

Observed: `404 Not Found` with body `{}`. This is the correct behavior: a clean 404 with an empty or explanatory body, not a 200 with an error message inside, and not a 500.

Postman test:

```javascript
pm.test("missing post returns 404", function () {
    pm.response.to.have.status(404);
});
pm.test("error body carries no fake data", function () {
    var json = pm.response.json();
    pm.expect(json).to.not.have.property("title");
});
```

## Collection and runner tips

- Put the base URL (`https://jsonplaceholder.typicode.com`) in a collection variable `{{baseUrl}}` so the same collection can point at a staging server later.
- Order the collection: GET list -> GET one -> POST -> PUT -> DELETE -> negative cases. Run it with the Collection Runner to get a pass/fail table for every request.
- Save the observed responses as examples in Postman (Save Response > Save as Example). They double as living documentation of what the API actually returns.
- When a test fails, read the response body first, then the status code, then the request you actually sent (Postman Console). Most "API bugs" in practice are wrong request bodies.
