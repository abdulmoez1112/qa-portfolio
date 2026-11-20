# Game testing session template

A one-page session sheet for manual game QA. Fill every field; if a section does
not apply, write "not applicable" and why, never leave it blank. For a filled
example see `game-qa/2048-session-2026-11-20.md`.

## 1. Session header

| Field | Entry |
|-------|-------|
| Game + version/build | |
| Platform / browser / device (exact, incl. viewport or emulation) | |
| Date + tester | |
| Charter (one sentence: what this session is for) | |
| Time box | |
| Starting state (fresh profile? saved game? seeded data?) | |

## 2. Coverage areas (tick what the session actually covers)

- [ ] Controls / input: every listed input does what the game says it does
- [ ] Rules / scoring: score, win, lose and merge/spawn rules behave as documented
- [ ] State / persistence: save, reload, new game, best score, pause/resume
- [ ] UI / visual: layout, HUD readability, animations complete, no overlap
- [ ] Audio: sounds/music present, mute works (write "not checked" if audio off)
- [ ] Edge cases: refresh mid-game, rapid input, invalid moves, resize/orientation
- [ ] Platform notes: anything specific to browser/OS/device observed

## 3. Running log

Record actions and observations as they happen, not from memory afterwards.

| Time | Action | Observed result | Status (PASS/FAIL/NOTE) |
|------|--------|-----------------|--------------------------|

## 4. Defects and suspicions

For each: title, steps to reproduce, expected vs actual, evidence (screenshot,
measurement), and whether it is a CONFIRMED defect (reproduced) or a SUSPICION
(seen once, needs re-test). State the game's documented behavior you compared
against, or say "no spec available - judged against genre convention".

## 5. Evidence and honesty rules

- Record exact game version/URL, browser, OS, viewport and emulation state.
- Label every result as physical device, emulation, or desktop browser.
- Screenshot every defect at the moment it occurred.
- End the sheet with a "NOT covered" list: inputs, levels, modes, platforms,
  and paths the session did not reach.

## 6. Exit summary

3-5 lines: what was covered, overall result, defects filed/raised, and what the
next session should pick up.
