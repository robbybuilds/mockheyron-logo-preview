# MockHeyron logo preview

Temporary preserved-copy preview of Catherine's MockHeyron work with the Heyron Launchpad celestial crest and Cassie's latest onboarding direction incorporated.

Source preserved from: https://github.com/catherinebb272/MockHeyron

## Robby review links

- Preview: https://robbybuilds.github.io/mockheyron-logo-preview/?v=bc6691e
- Support: https://robbybuilds.github.io/mockheyron-logo-preview/support.html?v=bc6691e
- Launchpad onboarding entry: https://robbybuilds.github.io/mockheyron-logo-preview/launchpad-onboarding.html?v=bc6691e
- Direct functional Launchpad flow: https://robbybuilds.github.io/mockheyron-logo-preview/launchpad-flow.html?path=beginner&v=bc6691e

## Onboarding order

1. Mission Control `Open` on the Launchpad card goes to `launchpad-onboarding.html`.
2. First screen is the full Ron welcome art with the “Welcome cadet” card.
3. The card/hotspot continues to the Launchpad path screen.
4. Beginner, Expert, and Remix buttons hand off into `launchpad-flow.html`.
5. `launchpad-flow.html?path=beginner` is the working guided setup flow with real validation/buttons.

## Button check

- Mission Control -> `index.html`
- Skip to demo dashboard -> `launchpad-flow.html?path=dashboard`
- First art continue hotspot -> shows path choice screen
- Beginner -> `launchpad-flow.html?path=beginner`
- Expert -> `launchpad-flow.html?path=expert`
- Remix -> `launchpad-flow.html?path=beginner&template=remix`

## Changes in this preview

- Added `assets/launchpad-crest.png`
- Kept raccoon logo as primary Heyron mark
- Added celestial crest as secondary Mission Control / Launchpad badge in the header and hero scene
- Added the onboarding intro shell before the older working Launchpad flow
- Normalized the Ron assistant artwork into a cleaner Clippy/widget icon after the Discord CDN source was already 404
- Did not edit Catherine's original repository

## Desktop/mobile responsive pass

Cassie flagged mobile Safari/phone layout risk. Added responsive safety CSS across:

- `index.html`
- `support.html`
- `launchpad-onboarding.html`
- `launchpad-flow.html`

What changed:

- Adds iOS/Android safe-area bottom padding so buttons/cards do not sit under browser chrome.
- Tightens mobile grids and card heights on Mission Control.
- Keeps tap targets at least 44px.
- Moves support/Clippy floating widgets above mobile browser bars.
- Uses `100svh`/`100dvh` where needed so onboarding does not get clipped.

Verification done locally: all four pages return 200 from a local static server and include the responsive safety pass. Playwright screenshot could not run because browsers are not installed in this environment.
