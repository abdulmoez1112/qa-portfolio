# Bug Report Template

Reusable template for writing bug reports a developer can act on without a follow-up conversation. The filled example at the bottom uses a real bug observed on the practice app https://www.saucedemo.com (also filed as BR-003 in bug-reports/saucedemo/).

## Template

```
ID: BR-XXX
Title: [What breaks, where, for whom - one line]

Environment:
- App / version / URL:
- Browser and version:
- OS / device:
- Account or user role used:
- Date observed:

Severity: Blocker | Critical | Major | Minor | Trivial
Priority: High | Medium | Low
(One line justifying each: who is affected and how often.)

Preconditions:
- [State the app must be in before the steps start: logged in as X, cart empty, etc.]

Steps to reproduce:
1. [One user action per step, from a clean start.]
2.
3.

Actual result:
[What the app did. Quote exact error text.]

Expected result:
[What it should have done, and why - spec, common practice, or the app's own consistency.]

Evidence:
- Screenshot / recording / console output / API response (attach or link)

Notes:
- Reproducibility: always | sometimes | once
- Workaround, if any:
- Related bugs:
- NOT included: guesses about root cause. Unknowns are marked "not investigated".
```

## Field guidance

- Title: a stranger should be able to find the bug from the title alone. "Add to cart fails for three products (error_user)" beats "cart broken".
- Severity vs priority: severity is how bad the damage is, priority is how soon it needs fixing. A crash on a rarely used page can be Critical severity, Low priority.
- Steps: start from a state anyone can reach. If the bug needs a specific account or dataset, that goes in Preconditions, not step 1.
- Actual vs expected: both are required. An actual result without an expected result is a complaint, not a report.
- Evidence: attach it or it did not happen. A screenshot of the wrong behavior is worth a paragraph.
- Reproducibility "sometimes" needs a rate ("3 of 5 attempts") so the developer knows what they are chasing.

## Filled example (real observed bug)

```
ID: BR-003
Title: Checkout: typing in the Last Name field overwrites the First Name field (problem_user)

Environment:
- App: saucedemo.com practice shop, checkout information page
- Browser: Chrome (cloud session)
- Account: problem_user / secret_sauce
- Date observed: 21 Oct 2026

Severity: Critical (user cannot enter correct shipping data)
Priority: High (checkout is a core flow; every problem_user order is affected)

Preconditions:
- Logged in as problem_user, one item in the cart, on /checkout-step-one.html

Steps to reproduce:
1. Click into the First Name field and type a first name.
2. Click into the Last Name field and type a last name.
3. Look at the First Name field.

Actual result:
The First Name field now shows the text typed into Last Name. The original first name is gone.

Expected result:
Each field keeps its own value; the form submits the shopper's real name.

Evidence:
- Observed live during exploratory session, 21 Oct 2026 (see bug-reports/saucedemo/)

Notes:
- Reproducibility: always, for problem_user. Not observed for standard_user.
- Workaround: none within the page.
- Root cause: not investigated.
```

## Usage

Copy the template block into a new file under bug-reports/, one file per bug, numbered sequentially. Delete guidance lines that do not apply to the bug at hand; never delete a section just because filling it in takes effort - "not investigated" is a valid entry, an empty field is not.
