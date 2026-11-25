# Test data checklist

Bad test data hides bugs and makes failures hard to repeat. Use this list before a test session.

## Per field
- Valid typical value
- Minimum and maximum length
- Empty, spaces only
- Special characters and quotes
- Very long text
- Non-English text (Urdu, Arabic, emoji)
- Leading and trailing spaces

## Numbers and dates
- Zero, negative, decimal, very large
- Leap day, month end, year change
- Past, today, future dates
- Different time zones

## Accounts and state
- New user with no data
- User with lots of data
- Locked, expired or unverified account
- Two users acting on the same record

## Files
- Allowed type, wrong type, renamed extension
- Empty file, file at the size limit, over the limit

## Handling
- Never use real customer data. Use fake or synthetic values.
- Note the data used in each test result so it can be repeated.
- Reset or clean data after the session.

This is a reference checklist. It does not claim any test was run.
