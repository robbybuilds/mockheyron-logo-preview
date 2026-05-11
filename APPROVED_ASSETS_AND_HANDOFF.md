# Approved Assets + Handoff Notes

Final preview commit: `c6dd61a`

## Live links

- Main Mission Control preview: https://robbybuilds.github.io/mockheyron-logo-preview/?v=c6dd61a
- Launchpad flow: https://robbybuilds.github.io/mockheyron-logo-preview/launchpad-flow.html?path=beginner&v=c6dd61a
- Launchpad start screen: https://robbybuilds.github.io/mockheyron-logo-preview/launchpad-start.html?v=c6dd61a
- Support page: https://robbybuilds.github.io/mockheyron-logo-preview/support.html?v=c6dd61a
- Safe hookup plan: https://robbybuilds.github.io/mockheyron-logo-preview/SAFE_HOOKUP_PLAN.md?v=c6dd61a

## Approved/used images in this preview

### Ron / Clippy

- `assets/ron/interstellar-ron-portrait.png`
  - Premium interstellar Ron portrait from Cassie’s latest reference.
  - Use for larger Ron moments, hero/card/profile contexts.
- `assets/ron/interstellar-ron-avatar.png`
  - Cropped circular version of the premium Ron portrait.
  - Wired into Mission Control Clippy Ron and Support Clippy Ron.
- `assets/clippy/clippy-ron-avatar.png`
  - Filled circular raccoon avatar.
  - Still kept for smaller/tighter Launchpad widget contexts where the detailed portrait may get muddy.

### Mission Control / Agent Jam

- `assets/agent-jam/agent-jam-command-bridge.png`
  - Approved Agent Jam command bridge artwork.
  - Used inside the Agent Jam modal/drawer.
- `assets/mission-control-floating-spaceship-transparent.png`
  - Mission Control ship/hero scene support asset.
- `assets/ron-cinematic-astronaut-transparent.png`
  - Floating astronaut Ron asset for Mission Control hero scene.
- `assets/launchpad-crest.png`
  - Celestial Launchpad crest/badge.

### Launchpad onboarding

- `assets/onboarding/launchpad-start-confirmed.png`
  - First Launchpad entry image.
  - Important: this was explicitly preserved and should not be replaced unless Cassie/Robby asks.
- `assets/onboarding/final/welcome.png`
  - In-flow welcome artwork.
- `assets/onboarding/final/names.png`
  - Name/setup artwork.
- `assets/onboarding/define-agent.png`
  - “Define your agent” use-case artwork.
- `assets/onboarding/final/connect-tools.png`
  - Tool connection artwork.
- `assets/onboarding/final/working-style.png`
  - Final approved clean working-style art.
  - Weird face overlays were removed. It now uses clean style panels only.
- `assets/onboarding/final/comm-style.png`
  - Communication verbosity/style artwork.
- `assets/onboarding/final/origins-preferences.png`
  - Origins/preferences artwork.
- `assets/onboarding/final/agent-crew.png`
  - Crew overview artwork/reference.
- `assets/onboarding/final/crew-handshake.png`
  - Crew/handshake artwork.
- `assets/onboarding/onboarding-complete.png`
  - Final congrats/onboarding-complete artwork.
  - Restored after regression and used on the final preview screen.
- `assets/onboarding/final/final-mission-control-card.png`
  - Earlier final card asset kept in repo as reference, but not the current final-screen source of truth.

### Support

- `assets/support/robby-cassie-support-hero.png`
  - Support page hero artwork with Robby/Cassie command center framing.

## Product/UX decisions preserved

- This repo is the separate preview lane: `robbybuilds/mockheyron-logo-preview`.
- Catherine/Cassie’s original dashboard repo/work was not edited.
- Mission Control and Launchpad are distinct surfaces.
- Launchpad completion returns to Mission Control.
- Final onboarding requires the safety acknowledgement before `Finish in Mission Control` is enabled.
- The working-style onboarding step is behavior-first, not character-first:
  - Direct & strategic
  - Warm & encouraging
  - Technical & precise
  - Creative & playful
  - Executive & polished
  - Gentle & organized
  - Bright & community-minded
  - Protective & careful
- Ron/Eloise/etc are “inspired by” references, not hard persona locks.
- Working-style optional tone notes are capped at 300 characters.
- Weird face badges in the working-style art were removed by request.

## Safe hookup state

Implemented as preview-only/local-only behavior:

- Launchpad saves draft/completion locally in browser storage.
- Mission Control reads local Launchpad context.
- Clippy Ron reads local context and supports generic current-user shape.
- Clippy demo fixtures are not product hardcoding:
  - `cassie@heyron.ai` -> Ron / `c8-0201` / read-only preview
  - `demo@heyron.ai` -> Nova / `demo-0001` / read-only preview
  - unknown emails -> pending/setup-needed context
- Support tickets queue locally.
- Billing requests queue locally as supervised support-ticket drafts.
- Agent Jam entries queue locally for review.
- TED questions queue locally.

Explicitly not enabled:

- No production writes.
- No service-role keys in browser.
- No Stripe actions.
- No container restarts.
- No logs, tokens, secrets, runtime config, host IPs, or private messages exposed.

Production endpoint shape Robby can implement later:

- `GET /api/me/container-summary`
  - Returns only safe per-user summary: agent name, container id, status, channels, safety notes, ticket count, Launchpad state.
  - Should not return logs, tokens, raw config, host IPs, or restart controls.

## Current source-of-truth files

- `index.html` — Mission Control preview and Clippy Ron current-user context pattern.
- `launchpad-start.html` — preserved Launchpad entry screen.
- `launchpad-flow.html` — updated onboarding flow, working-style step, final safety acknowledgement.
- `support.html` — safe local support/billing/TED queue patterns.
- `SAFE_HOOKUP_PLAN.md` — safe-to-real API promotion plan.
- `APPROVED_ASSETS_AND_HANDOFF.md` — this handoff file.

## Known future polish, not blockers

- Glow Cloud and Spencer card style in the crew image set can be polished later for stronger consistency.
- The safe local hooks should be replaced with authenticated backend endpoints before production use.
- Clippy should use the real signed-in session rather than email input once auth is ready.
