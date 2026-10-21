# Test Plan - saucedemo.com Core E-Commerce Flows

- Author: Abdul Moez
- Date: 2026-10-21
- Application: https://www.saucedemo.com (public demo e-commerce app)
- Test accounts: standard_user, locked_out_user, problem_user (password: secret_sauce, published by the app)

## 1. Objective

Verify the core purchase flow of saucedemo.com for the standard user on desktop: login, product catalog, sorting, cart, and checkout through order confirmation. Identify and document defects in the seeded problem_user account for practice bug reporting.

## 2. Scope

In scope:
- Login (valid, invalid, locked-out user)
- Product catalog display and sorting (Name A-Z, Z-A, Price low-high, high-low)
- Add to cart / remove from cart
- Cart page contents and badge count
- Checkout step 1 (customer info), step 2 (overview), confirmation
- Logout

Out of scope:
- Performance and load testing
- Security testing
- Payment processing (demo app has none)
- Mobile native apps (responsive web only, later cycle)

## 3. Approach

- Scripted functional testing: execute the test case set in test-cases/saucedemo-checkout-test-cases.md as standard_user.
- Exploratory testing: 30 minutes per session, chartered around cart state and checkout validation.
- Negative testing: empty and invalid checkout form inputs, locked-out login.
- Defect hunt: repeat key flows as problem_user and document differences in bug-reports/saucedemo/.

## 4. Environment

- OS: Windows 11
- Browser: Chrome (latest), 1920x1080
- Network: broadband, no throttling
- Test data: demo app's seeded users and products

## 5. Entry criteria

- saucedemo.com reachable, login page loads
- Demo credentials available

## 6. Exit criteria

- All planned test cases executed and marked pass/fail
- All critical and high severity defects reported with repro steps
- Test summary written (executed, passed, failed, blocked)

## 7. Risks

- The demo app resets state without notice; test data is not persistent.
- Seeded bugs in problem_user are intentional; reports label them as practice findings.

## 8. Deliverables

- Executed test case set with results
- Bug reports BR-001 to BR-003+ in bug-reports/saucedemo/
- Regression checklist for future passes (checklists/web-regression-checklist.md)
