---
name: kickbot-tipping
description: Set up and manage KickBot tips for a Kick stream. Use for the tip page, tip amounts, tip alerts and widget, the tip queue, tip approval, tip moderation filters, and tip history or earnings reports.
---

# KickBot tipping

Start with `get_account_overview` and `get_tipping_status`. Tipping status
shows if the payout account is connected, if tipping is on, and the tip page
URL. If the connection is missing, use the host's KickBot Connect flow. Do not
request credentials or bank details in chat.

## What the integration cannot do

Connecting a payout account, payouts, balance transfers, and refunds are only
in the KickBot dashboard. If the user asks for one of these, explain this and
link them to the dashboard. Do not try a different tool to do it.

## Tip page and widget

- Read `get_tip_page_settings` before `update_tip_page_settings`. Amounts are
  US cents. Keep the suggested amount and presets between the minimum and the
  maximum. Send only the requested fields.
- For a banner, call `create_tip_banner_upload_url`, upload the image with HTTP
  PUT exactly as the response describes, and then finish the step that the
  response names.
- Read `get_tip_widget_settings` before `update_tip_widget_settings`. The tip
  widget URL contains a secret key and is not in the API. Tell the streamer to
  copy it from Tipping > Widget in the dashboard.

## Queue

Read `get_tip_queue` and `get_tip_queue_settings` first.

- `update_tip_queue_settings` changes tipping on/off, automatic or manual
  approval, and the delay between tips.
- `pause_tip_queue` and `resume_tip_queue` stop and start playback.
- `approve_tip` plays a pending tip, and the viewer is charged when it plays.
- `reject_tip` cancels the payment. The streamer does not get that money.
- `clear_tip_queue` rejects every unpaid tip in the queue.

Rejecting and clearing cannot be undone. Do these only when the user asks for
that exact action, and confirm the tip IDs or the full clear first. Never
approve or reject tips in bulk on your own judgment. `replay_tip` plays an
approved tip again without a new charge.

## Moderation and reports

Read `get_tip_moderation_settings` before `update_tip_moderation_settings`.
`blocked_terms` and `regex_patterns` replace the full list, so keep existing
entries. `list_blocked_tip_messages` shows what the filters stopped.

`list_tip_transactions` and `get_tip_earnings_summary` are read only. Give
amounts in dollars, and say that they are before fees when the tool says so.
Do not share tipper names or messages outside the conversation.

Reference: https://docs.kickbot.com/dashboard/api/reference/tipping
