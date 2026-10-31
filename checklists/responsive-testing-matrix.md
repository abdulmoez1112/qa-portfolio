# Responsive Testing Matrix (saucedemo.com)

Matrix for checking the practice app https://www.saucedemo.com across viewport sizes. Rows are checks, columns are viewport classes. Every cell starts "Not run" and is only marked when someone actually runs that combination. The performed results at the bottom were executed in a real browser session on 31 Oct 2026.

## Viewport classes

| Class | Widths to test | Example devices |
|-------|----------------|-----------------|
| Phone | 320, 375, 390, 414 px | iPhone SE/14, small Android |
| Tablet | 768, 820, 1024 px | iPad, Android tablets |
| Laptop | 1280, 1366, 1440 px | Common laptops |
| Desktop | 1920 px and up | Monitors |

## Planned matrix

| # | Check | Phone | Tablet | Laptop | Desktop |
|---|-------|-------|--------|--------|---------|
| 1 | Product list: all products reachable, grid adapts, no horizontal scroll | Not run | Not run | Not run | Not run |
| 2 | Header: burger menu and cart icon visible and tappable | Not run | Not run | Not run | Not run |
| 3 | Sort dropdown opens and changes order | Not run | Not run | Not run | Not run |
| 4 | Product detail page: Back to products visible, image scales | Not run | Not run | Not run | Not run |
| 5 | Cart page: item rows readable, Checkout and Continue Shopping tappable | Not run | Not run | Not run | Not run |
| 6 | Checkout form: all fields and Continue reachable without horizontal scroll | Not run | Not run | Not run | Not run |
| 7 | Menu drawer: opens, all links (All Items, About, Logout) reachable | Not run | Not run | Not run | Not run |
| 8 | Text stays readable (no overlap, no clipping) on every page | Not run | Not run | Not run | Not run |
| 9 | Touch targets at phone width: buttons at least about 44px, no mis-taps | Not run | - | - | - |
| 10 | Orientation change (portrait/landscape) keeps state | Not run | Not run | - | - |

## What to record per cell

Viewport width, device or emulation method, browser, date, and Pass/Fail plus a screenshot for any Fail. Emulator results are leads, not proof: layout bugs often only appear on real devices, so failed or borderline emulator cells get retested on hardware before closing.

## Performed results

Executed by me on 31 Oct 2026 in Chrome 155.0.0.0 with viewport emulation, logged in as standard_user. Widths tested: 1280 (laptop), 820 (tablet, iPad UA), 390 (phone, iPhone UA). Only these cells were run.

| # | Check | Result by width | Observed |
|---|-------|-----------------|----------|
| 1 | Product list grid adapts, no horizontal scroll | 1280 Pass / 820 Pass / 390 Pass | 2 products per row at 1280, 1 per row at 820 and 390; scrollWidth never exceeded the viewport |
| 2 | Header controls visible | 1280 Pass / 820 Pass / 390 Pass | Burger menu, cart icon, sort dropdown all visible at every width |
| 5 | Cart page controls | 390 Pass | Checkout and Continue Shopping both visible and tappable; no horizontal scroll |
| 6 | Checkout form | 390 Pass | All three fields and Continue reachable; no horizontal scroll |
| 7 | Menu drawer | 390 Pass | Drawer opened; All Items, About and Logout links all visible |

Cells not listed above remain Not run - including every real-device row, the orientation change check (10), and the touch-target size check (9), which need physical phones or tablets.
