# Mobile Testing Checklist (Android)

A reusable checklist for manual testing of a web app or mobile app on Android phones. Tick each item per device and note the result in the log at the bottom.

## Test devices

| Device | Notes |
|---|---|
| Realme Note 50 | Low-to-mid range, Realme UI |
| Vivo Y12 | Older, low RAM, good for performance and memory pressure checks |
| Infinix Hot 40 | Mid range, XOS |

Record the Android version, browser or app version and build number for every run.

## 1. Install and launch (apps)

- [ ] App installs from the build or store without errors
- [ ] First launch shows no crash or blank screen
- [ ] Permission prompts (camera, location, notifications, storage) appear at a sensible time with clear wording
- [ ] Denying a permission does not break the app; the user gets a clear message
- [ ] Update over an older version keeps user data and login
- [ ] Uninstall and reinstall behave as expected

## 2. Layout and display

- [ ] Portrait and landscape both render correctly
- [ ] No text cut off, overlapping or unreadable
- [ ] Buttons and links are large enough to tap (about 48 dp)
- [ ] Keyboard opening does not hide the field being typed in or the submit button
- [ ] Notch, status bar and gesture bar do not cover content
- [ ] Font size set to large in Android settings does not break screens
- [ ] Dark mode (if supported) keeps text readable

## 3. Input and gestures

- [ ] Tap, double tap, long press, swipe and pinch behave as designed
- [ ] Scrolling is smooth with no stuck areas
- [ ] Correct keyboard type per field (email, number, phone)
- [ ] Copy and paste work in text fields
- [ ] Autofill and saved passwords do not fill wrong fields

## 4. Interruptions

- [ ] Incoming call during use, then return to the app
- [ ] SMS or notification during use
- [ ] Switch to another app and back (state kept)
- [ ] Lock and unlock the screen mid-flow
- [ ] Rotate the screen mid-form (entered data kept)
- [ ] Press Back at each step; behavior is predictable and does not exit unexpectedly

## 5. Network conditions

- [ ] Wi-Fi and mobile data both work
- [ ] Switch from Wi-Fi to mobile data mid-request
- [ ] Slow connection: loading indicators show, no endless spinner
- [ ] Airplane mode: clear offline message, no crash
- [ ] Connection returns: app recovers without a restart

## 6. Performance and resources

- [ ] Cold start time is acceptable on the Vivo Y12
- [ ] No visible lag when scrolling long lists
- [ ] Battery drain and phone heating are not unusual after 15 minutes of use
- [ ] App works with low storage space
- [ ] No crash after leaving the app in the background for a long time

## 7. Browser checks (mobile web)

- [ ] Chrome and the phone's default browser both load the site
- [ ] Responsive layout switches correctly at phone widths
- [ ] Forms submit correctly with the mobile keyboard
- [ ] File upload from gallery and camera works
- [ ] Links open in the right place (app, browser, dialer, maps)

## 8. Security and privacy basics

- [ ] Sensitive fields are masked
- [ ] Session ends after logout; Back does not show private screens
- [ ] No sensitive data shown in notifications or the app switcher preview (where applicable)

## Result log

| Date | Device | Android version | App or browser version | Items failed | Bug IDs |
|---|---|---|---|---|---|
|  | Realme Note 50 |  |  |  |  |
|  | Vivo Y12 |  |  |  |  |
|  | Infinix Hot 40 |  |  |  |  |
