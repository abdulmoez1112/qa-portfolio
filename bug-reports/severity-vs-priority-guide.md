# Severity vs priority: how to classify a bug

Severity and priority answer two different questions, and mixing them up is the most common classification mistake in bug reports.

- **Severity** = how badly the defect hurts the product or the user. It is a property of the bug itself and rarely changes over the bug's life.
- **Priority** = how soon it should be fixed, given impact *plus* context: who is affected, how often, what else is in the queue, and what a workaround costs. Priority is a scheduling decision and can change without the bug changing.

A useful mental check: severity is set by the tester from evidence; priority is agreed with whoever owns the release.

## The four combinations

| | Low priority | High priority |
|---|---|---|
| **High severity** | Rare but real: a crash on an obsolete browser nobody uses yet. Fix, but not this week. | Blocks a core flow for real users. Stop and fix. |
| **Low severity** | Cosmetic in a quiet corner. Backlog. | Tiny fix blocking something bigger, or a trivial typo on the homepage before a launch. Cheap to do, do it now. |

## Worked examples from this repo

All six bugs below are real practice findings in `bug-reports/saucedemo/` (the demo app seeds them intentionally; the classifications are the instructive part).

| Bug | What it does | Severity | Priority | Reasoning |
|-----|--------------|----------|----------|-----------|
| BR-001 | Add to cart does nothing for 3 of 6 products (problem_user) | High | High | Core purchase flow fails for affected items; no workaround inside the app. |
| BR-002 | Wrong product images shown (problem_user) | Medium | Medium | Content is misleading but names and prices are correct and purchase still works. |
| BR-003 | Last Name overwrites First Name at checkout (problem_user) | High | High | Checkout is effectively blocked: the form cannot be completed correctly. |
| BR-004 | Add to cart fails for 3 products (error_user) | High | High | Same core-flow failure as BR-001 on a different profile. |
| BR-005 | Remove button does nothing (error_user) | Medium | Medium | Cart contents cannot be corrected, but the session can be restarted; purchase itself still works for addable items. |
| BR-006 | Prices change on every reload (visual_user) | High | High | Showing wrong prices is a trust and money-integrity issue even before checkout. |

## Judgement calls worth noting

1. **BR-002 is not Low.** A wrong image can sell the wrong product; "cosmetic" would understate it. Medium is honest: the transaction still works, but the user is misinformed.
2. **BR-005 stays Medium despite no in-app workaround for the affected items.** Severity measures damage to the user's goal; they can still complete a purchase of items that add correctly, and a fresh session clears the cart. Compare BR-001/BR-004, where the purchase itself is impossible for those items.
3. **Priority would shift with context.** If 40% of live traffic used the affected profile, every one of these moves up a band; severity would not move at all. That asymmetry is the whole point of keeping the two fields separate.

## A quick checklist for classifying

1. State the severity from evidence: what breaks, for whom, how often, what data or money is at risk.
2. Write the workaround (or "none found") - it is the biggest honest input to priority.
3. Propose priority, but expect it to be negotiated against the release plan.
4. Revisit priority when context changes (launch dates, affected traffic, related fixes); leave severity alone unless the bug itself changes.
