# Claude Prompt Library for QA

Prompts I use to speed up test design and documentation. Every AI output is reviewed and corrected by hand before it goes into real test artifacts. Replace [BRACKETS] with your context.

## 1. Test case generator

> You are a senior QA engineer. Given this feature description: [PASTE FEATURE]. Produce functional test cases in a markdown table with columns: ID, Title, Preconditions, Steps, Expected result, Priority. Cover the happy path, validation failures, and at least 3 edge cases. Write steps so a new tester can execute them without asking questions.

## 2. Edge-case brainstorm

> List edge cases a manual tester should check for [FEATURE], grouped under: Input, State, Timing, Environment, and Permissions. One line each, specific enough to turn into a test case directly.

## 3. Bug report polisher

> Rewrite this rough bug note into a professional bug report with: Title, Severity, Environment, Preconditions, Steps to reproduce, Expected result, Actual result, Additional notes. Keep my facts unchanged; only improve clarity and structure: [PASTE NOTE]

## 4. Regression scoper

> These parts of the app changed in this release: [PASTE CHANGES]. Propose a focused regression checklist for a 60-minute manual pass, ordered by risk. Mark the 5 checks that must pass before release.

## 5. Exploratory charter writer

> Write 3 exploratory testing charters for [AREA OF APP]. Format each as: Explore [target] using [resources] to discover [information]. Add 5 tour ideas per charter (for example: data tour, interruption tour, locale tour).

## 6. Test data ideas

> Suggest test data sets for [FORM/FEATURE]: one valid baseline, plus sets that probe length limits, special characters, unicode/RTL text, HTML/script injection strings (for validation testing only), and boundary numeric values. Format as a table.

## 7. API checklist from endpoints

> Here is a list of REST endpoints: [PASTE LIST]. For each, list the manual API checks I should run in Postman: happy path, auth failure, validation, boundaries, and state changes. Keep it to 5-7 checks per endpoint.

## 8. Mobile-specific checks

> For this web feature: [PASTE FEATURE]. List the extra checks needed on real Android/iOS devices: touch targets, orientation, keyboard behavior, interruptions (call, notification), offline/weak network, and OS-level back behavior.

## 9. Accessibility quick checks

> Give me a 15-minute manual accessibility checklist for [PAGE TYPE]: keyboard-only navigation, focus visibility, form labels, contrast spot checks, alt text, and heading structure. Include the quick keyboard test steps for each.

## 10. Severity triage assistant

> Here is a bug: [PASTE DESCRIPTION]. Propose a severity (Critical/High/Medium/Low) with a one-paragraph justification based on user impact, workaround availability, and affected scope. Then argue for one level lower, so I can sanity-check the call.

## Usage notes

- Paste real app context, not client-confidential data, into any AI tool.
- Treat AI output as a draft: execute or verify every suggested case before relying on it.
- Version prompts here when an edit proves better in practice.
