# Exploratory session report: cart state

Session: cart state persistence and removal paths on saucedemo.com
Date: 14 Nov 2026 | Tester: Abdul Moez (daily portfolio session) | Duration: ~45 min planned, ~30 min actual
Environment: saucedemo.com (public demo app by Sauce Labs - findings are against a demo environment, not a live store), Chrome cloud browser, standard_user / secret_sauce

Charter (one sentence):
Explore how cart state survives refresh, logout/login, reset, multiple tabs and different removal paths, to find where the app's idea of the cart and the user's idea of the cart disagree.

Scope:
- In: inventory page, cart page, burger menu (logout, Reset App State), second browser tab
- Out: checkout flow (covered by 12/13 Nov sessions), other seeded profiles

Notes (chronological):
- 18:26 Added Backpack + Bike Light from inventory -> badge 2
- 18:27 Refresh on inventory -> badge still 2; cart survives refresh
- 18:27 Logout, log straight back in -> badge STILL 2; cart survives logout/login in the same browser
- 18:27 Reset App State -> badge cleared, cart page shows 0 items (reset works)
- 18:27 Added Onesie, opened cart page -> 1 item, badge 1
- 18:28 Clicked Remove on the cart page -> the app NAVIGATED to /inventory.html by itself; badge still 1
- 18:28 Back on cart page after re-navigation -> the Onesie is BACK (1 item); inventory shows its button as "Remove"
- 18:28 Repeated cleanly: cart-page Remove again -> same: visual row removal + unexpected navigation, item returns on re-navigation
- 18:28 Control: Remove via the inventory-page button -> badge clears, cart stays empty after navigation (removal works there)
- 18:28 Opened a second browser tab to inventory -> badge 1 in both tabs (cart state is shared browser-wide, not per-tab)

Findings:
- Bugs filed: [BR-008](../bug-reports/saucedemo/BR-008-cart-page-remove-visual-only.md) - cart-page Remove is visual-only (item returns on re-navigation, badge never updates) and navigates to the inventory page; reproduced twice with an inventory-button control that works.
- Behavior worth a product decision: cart survives logout/login (E2). Convenient for the shopper who logs out by accident; on a shared computer it leaks one user's cart to the next login. Not filed - it is a design question, not a broken requirement.
- Questions raised: is the cart-page Remove failure related to BR-005 (error_user remove failure)? Same symptom class, different profile; BR-005's original report predates this session. Left open pending an error_user comparison run.

Coverage vs charter:
- Covered: refresh, logout/login, reset, multi-tab, both removal paths. Skipped: back/forward cache behavior (checkout-side back behavior was already covered 13 Nov) and cart behavior mid-checkout - both noted for Charter 3's session.

Debrief summary:
The cart survives everything EXCEPT the one action that should change it: removing an item from the cart page is visual-only and the item comes back. Removal works from the inventory page. Next session: Charter 3 (follow visual_user's unstable prices into checkout totals).
