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
