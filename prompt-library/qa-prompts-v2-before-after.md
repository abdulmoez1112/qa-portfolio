# QA Prompts v2: Five Prompts with Before and After

Second version of the prompt library (v1: qa-claude-prompts.md). Each entry shows a weak "before" prompt, the improved "after" prompt, and why the change matters. The improvements follow standard prompt practice: give context, name the output format, set constraints, and say what to leave out. These are written for QA work on a demo web shop such as https://www.saucedemo.com but adapt to any app.

## 1. Generating test cases

Before:
> Write test cases for a login page.

After:
> Write 8 functional test cases for the login page of a web shop. Cover: valid login, wrong password, empty fields, locked account, SQL-injection-style input in the username, password masking, the error message text, and session behavior after login. Output as a table with columns: ID, Title, Preconditions, Steps, Expected result, Priority. Keep each step to one user action. Do not include performance or security test cases beyond the input-handling row.

Why it is better: the before version gets generic cases that mostly repeat "enter valid credentials". The after version fixes the count, the coverage list, the format and the scope, so the output can go straight into a test case document.

## 2. Writing a bug report

Before:
> The checkout is broken, write a bug report.

After:
> Write a bug report for this behavior: on the checkout information page, typing into the Last Name field also overwrites the First Name field with the same text. Include: a one-line title, environment placeholder (browser, OS, date), severity with a one-line justification, exact steps to reproduce from the cart page, actual result, expected result, and a note on which user flows it blocks. Do not invent a root cause; mark unknowns as "not investigated".

Why it is better: the before version has no behavior to describe, so the model invents one. The after version supplies the observed behavior and forces the report to stay factual, which is what makes a bug report usable by a developer.

## 3. Exploratory testing charter

Before:
> Help me test the shopping cart.

After:
> Write a one-hour exploratory testing charter for the shopping cart of a demo web shop. Structure it as: mission (one sentence), areas to explore (cart badge accuracy, item persistence across navigation, quantity handling, remove behavior, checkout handoff), 5 specific test ideas to try first, the oracles to check against (badge count, cart page contents, totals), and what to record during the session. Timebox each area to about 10 minutes.

Why it is better: "help me test" produces a lecture about testing. The after version produces a runnable session plan with a mission, ideas, oracles and a timebox, which is how session-based exploratory testing is actually run.

## 4. API test ideas from an endpoint description

Before:
> What should I test for the /users API?

After:
> Here is an endpoint: GET /users/{id} returns a user object with id, name, email; it returns 404 for unknown ids and requires no authentication. List 10 API test ideas, grouped into: happy path, data validation, negative cases, and boundary values. For each idea give the request, the expected status code, and the one assertion that matters most. Flag any idea that depends on behavior the description does not specify, instead of guessing the behavior.

Why it is better: the before version has no contract, so half the ideas assume behavior that may not exist. The after version anchors every idea to the given description and forces unknowns to be flagged, which keeps the test list honest.

## 5. Reviewing a requirements sentence

Before:
> Check this requirement: the system should be fast and user-friendly.

After:
> Review this requirement for testability: "The system should be fast and user-friendly." Point out exactly which words are not testable and why, then rewrite it as two separate requirements that a tester could verify, with measurable criteria (for example a response-time threshold and a concrete usability criterion such as completing checkout in at most N steps). Keep the rewrite to two sentences.

Why it is better: the before version invites a vague essay. The after version demands the specific defect in the requirement (untestable wording) and a concrete, measurable rewrite, which is the actual skill a QA applies in requirement reviews.

## Notes on use

- Always paste real observed behavior or a real interface description into the prompt; a prompt cannot supply facts about your app.
- Treat generated test cases and checklists as a draft to review against the actual application, not as executed testing.
- Keep prompts in version control with the date, so wording changes are traceable like any other test artifact.
