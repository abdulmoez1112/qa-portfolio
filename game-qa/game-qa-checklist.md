# Game QA Checklist

A working checklist for testing a game build, organized by the passes a game QA run actually goes through. Rows are planned coverage to tick during a run - statuses start at "Not run" and get filled in per build, like the other checklists in this repo. Written for PC/mobile game testing; trim rows that do not apply to the title.

## 1. Install and boot (smoke pass first)

| # | Check | Status |
|---|-------|--------|
| 1 | Build installs/copies cleanly, no missing-file errors | Not run |
| 2 | Game boots to the title screen without a crash | Not run |
| 3 | Save file loads; new game starts | Not run |
| 4 | All menus open and back out (main, settings, pause) | Not run |
| 5 | Quit and relaunch - settings and save persist | Not run |

## 2. Core gameplay loop

| # | Check | Status |
|---|-------|--------|
| 6 | Player movement and camera respond in every playable area | Not run |
| 7 | Each core mechanic works once in isolation (jump, attack, pickup - whatever the game has) | Not run |
| 8 | Win/lose/progress conditions trigger correctly | Not run |
| 9 | Score/currency/inventory counts update on gain and spend | Not run |
| 10 | Death/fail state resets the game to a playable state, not a soft-lock | Not run |

## 3. Collision and physics

| # | Check | Status |
|---|-------|--------|
| 11 | Player cannot walk through walls, floors, or closed doors | Not run |
| 12 | Player cannot leave the playable area (map boundaries hold) | Not run |
| 13 | Objects do not fall through the floor or jitter in place | Not run |
| 14 | Projectiles/hits register on targets and stop at obstacles | Not run |

## 4. UI and HUD

| # | Check | Status |
|---|-------|--------|
| 15 | HUD values match the real game state (health, ammo, timer) | Not run |
| 16 | Text fits its boxes at every supported resolution/language, no overflow or clipping | Not run |
| 17 | Buttons have visible hover/press states and every button does something | Not run |
| 18 | UI scales correctly at min and max supported resolutions and aspect ratios | Not run |

## 5. Audio

| # | Check | Status |
|---|-------|--------|
| 19 | Music, effects, and voice each respect their volume sliders, including mute | Not run |
| 20 | Sound effects sync with their visual events | Not run |
| 21 | No crackling/looping glitches when many sounds play at once | Not run |

## 6. Performance soak

| # | Check | Status |
|---|-------|--------|
| 22 | Frame rate stays stable in the busiest scene the game has | Not run |
| 23 | No growing stutter or memory bloat after 30+ minutes of continuous play | Not run |
| 24 | Loading screens complete; no infinite loads on any transition | Not run |

## 7. Edge cases and interruptions (mostly mobile)

| # | Check | Status |
|---|-------|--------|
| 25 | Incoming call / app switch / lock screen mid-game: game pauses and resumes cleanly | Not run |
| 26 | Battery-low and network-loss interruptions do not corrupt the save | Not run |
| 27 | Rapid repeated taps on one button do not double-fire purchases or actions | Not run |
| 28 | Rotating the device (if supported) does not break the layout or crash | Not run |

## Bug-reporting notes for games

- Always attach the build version and platform - game bugs are extremely build-specific.
- For physics/collision bugs, a short video beats paragraphs of description.
- Note repro rate (1/1, ~1 in 5) so triage knows if it is deterministic or a race.
- Reproduce a soft-lock or crash twice before filing; one-off crashes go in as "seen once, watching" rather than a confirmed defect.
