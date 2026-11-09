# The defect lifecycle: states, transitions, and when re-testing happens

A bug report is not a static document - it moves through states, and each transition has an owner and an evidence requirement. This is the lifecycle I use, which matches what most trackers (Jira, GitHub Issues, Azure Boards) implement with different labels.

## States and what each one means

| State | Meaning | Owned by |
|-------|---------|----------|
| New | Reported, not yet reviewed. | Tester |
| Triaged (Open) | Reviewed, accepted as a real defect, classified (severity/priority). | Dev lead / product |
| In progress | A developer is actively fixing it. | Developer |
| Fixed (Ready for re-test) | Developer believes it is fixed; a build contains the fix. | Developer -> back to tester |
| Re-tested / Verified | Tester re-ran the exact reproduction on the new build and the bug is gone. | Tester |
| Closed | Done, or resolved as not-a-bug / duplicate / won't-fix with a recorded reason. | Tester or product |
| Reopened | A verified fix failed again - same build or a later regression. | Tester |

## The transitions that matter

1. **New -> Triaged.** Triage is a decision, not a formality: reproduce or read the evidence, set severity and priority, reject duplicates with a pointer to the original.
2. **Fixed -> Re-tested.** Re-testing is not "trying the app again". It means re-running the *exact steps* from the report, in the *same environment class*, on the *build that claims the fix*, and recording the outcome verbatim. Anything less is an opinion.
3. **Re-tested -> Closed or Reopened.** Pass: close with the build and date. Fail: reopen with fresh evidence (screenshots, exact messages), and say clearly whether it is the same failure or a new related one - a related failure is usually a new bug linked to the old one, not a reopen.
4. **Closed -> Reopened (regression).** A bug that comes back after being closed is a regression. Regression triggers: a fix in the same code area, a dependency upgrade, or a merge. This is why regression suites exist - see the checklists in this repo.

## Re-test vs regression test

- **Re-test** confirms *this* bug is fixed (one report, exact steps).
- **Regression test** confirms the fix did not break *anything else* (a scoped set of checks around the change).
Confusing the two is how teams ship a fix that reopens two other bugs.

## What a good re-test record contains

- The original bug ID and title.
- The build/version and date of the re-test, and the environment.
- The exact steps (copied, not paraphrased) and the observed result, quoted.
- The verdict: verified-fixed, still-reproduces, or partially-fixed (say what remains).
- A link to fresh evidence.

## On this practice repository

Saucedemo's seeded defects never get "fixed" - they are a standing practice environment. The re-test logs here (`test-cases/saucedemo/`) therefore demonstrate the *form* of a re-test: original ID, exact steps re-run on a dated session, verbatim observed behaviour, and an explicit verdict line. The same shape transfers directly to a tracker with real fix builds.
