# Regression testing checklist

Run this after any fix or change to confirm old behaviour still works.

## Before the run
- Note the build or version under test.
- List what changed and which areas it touches.
- Pick the test set: smoke tests, then tests for changed areas, then high-risk older tests.

## Core flows
- Sign up, log in, log out, password reset
- Main user journey from start to finish
- Search, filter, sort
- Create, edit and delete a record
- Payment or checkout, if present

## After a bug fix
- Re-run the exact steps from the bug report.
- Try nearby inputs and a different user role.
- Check related screens that share the same code.

## Recording
- Pass or fail per test, with the build number.
- Link failures to bug reports.
- Mark tests that were skipped and why.

## Exit
- No open critical or high bugs in the tested areas.
- Failures either fixed, or accepted with a note.

This is a reference checklist. It does not claim any test was run.
