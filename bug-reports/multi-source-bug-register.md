# Combining findings from repeated test rounds into one bug register

Practice note from real QA work. When the same product gets tested more than once (a fresh session, plus findings carried in an older document or from a teammate), the output should be a single register - not two lists stapled together. This is the structure I use.

## 1. Label every finding by evidence source

Each row names where the evidence came from and when:

- **Verified this round** - seen and reproduced in the current session, with date and environment recorded.
- **Historical** - reported in an older document or earlier round, not re-run this time. Never silently promote these to "confirmed".
- **Unverified claims** - mentioned but not reproduced or evidenced yet. Keep them in a separate list so nobody mistakes them for proven bugs.

## 2. Merge duplicates before numbering

The same root cause appearing in two sources is one bug, not two. Cross-reference both evidence sources in the single record. If two findings only look similar, keep them separate and note the relationship instead of merging on a guess.

## 3. One-line register plus detail blocks

- **Register:** ID, title, source, severity, area, status - one line per bug so the whole list fits on a screen.
- **Detail per bug:** evidence (verbatim quotes where they exist), expected vs actual, reproduction steps, suggested fix, and cross-references to related bugs.

## 4. Keep passed checks visible

A short list of what was verified working stops a reader assuming everything is broken, and shows the actual coverage of the round.

## 5. State the method up front

A short "read me" section: what was tested, when, for how long, what the ground-truth checks were, and what was deliberately left out.

## Why it matters

- Prevents double-counting when a client or developer sizes the work.
- Keeps old findings honest instead of quietly becoming "confirmed".
- Gives the developer one document to work from instead of two overlapping ones.
