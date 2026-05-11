# Safe Hookup Plan

This preview is wired to behave like the real product without touching production.

## Current safe behavior

- Launchpad saves draft + completion to browser `localStorage`.
- Mission Control reads local Launchpad context and shows a safe status card.
- Clippy Ron reads local context only.
- Support tickets queue locally as `heyronSupportTickets` with `status: queued_local_only`.
- Billing requests become local supervised support-ticket drafts, never Stripe actions.
- Agent Jam submissions queue locally as `heyronAgentJamEntries`.
- TED Talk questions queue locally as `heyronTedQuestions`.

## Explicitly not enabled

- No prod writes.
- No service-role keys in browser.
- No Stripe actions.
- No container restarts.
- No logs, tokens, secrets, or runtime config shown.
- No public posting from Agent Jam submissions.

## Promote to real APIs in this order

1. Authenticated profile/onboarding save
   - Table/API: profile onboarding payload
   - Required: signed-in user session
   - Safe fields: agent name, use cases, selected tools, comm style, privacy choices, acknowledgement timestamp

2. Support ticket creation
   - Table/API: `tickets`
   - Required: signed-in user or verified email
   - Attach only a safe container snapshot: container id/status, no logs/secrets by default

3. Agent Jam review queue
   - Table/API: review-only submissions table
   - Required: signed-in user or Discord handle
   - Moderation: private queue first, human approval before publishing

4. Clippy Ron read-only context
   - Required: signed-in account context
   - Read-only only: profile, ticket count/status, onboarding state, safe container health summary

## Keep behind stronger auth later

- Billing changes
- Refund/cancel execution
- Container restart
- Log viewing
- Integration/token status
- Moderator tools

## Browser keys used by preview

None. All state is local-only in the browser so Cassie/Robby can test flow safely.

## Generic Clippy app context

Clippy Ron is now shaped like an application-level current-user helper, not a Cassie-only demo.

Preview behavior:
- Known demo users resolve to safe read-only summary cards.
- Unknown emails still work: they get a pending/setup-needed context instead of an error.
- Launchpad completion can fill in a user's pending context locally.

Current demo fixtures:
- `cassie@heyron.ai` -> agent `Ron`, container `c8-0201`, status `online`, read-only preview
- `demo@heyron.ai` -> agent `Nova`, container `demo-0001`, status `online`, read-only preview
- Any other email -> pending context: no assigned container visible yet, safe next actions only

Rules for this lookup:
- Static preview may show container id/status only.
- Do not include host IPs, API keys, bot tokens, gateway tokens, logs, runtime config, private messages, or secrets.
- Real production version should replace fixture maps with an authenticated server endpoint.

Suggested production endpoint:

`GET /api/me/container-summary`

Returns only:
```json
{
  "user": { "email": "user@example.com" },
  "agentName": "Ron",
  "container": "c8-0201",
  "status": "online",
  "channels": ["Discord", "Telegram groups"],
  "safety": "Telegram DMs disabled",
  "ticketCount": 0,
  "launchpadComplete": true
}
```

Do not return logs, tokens, raw config, host IPs, or restart controls from this endpoint.
