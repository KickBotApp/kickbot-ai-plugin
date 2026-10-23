---
name: kickbot-channel-setup
description: Connect, review, or set up a Kick channel in KickBot. Use when a streamer starts with KickBot, asks what KickBot can do, wants a setup review or suggestions, needs the KickBot moderator check, or asks for channel activity and stats.
---

# KickBot channel setup

Use the KickBot MCP tools available in the current AI service. If the
connection is missing, direct the user to the service's KickBot install or
Connect flow. Do not claim that it is connected until a tool call succeeds.
Never ask the user to put a password, token, or API key in chat.

## Start

Call `get_account_overview`. It shows the selected channel, the user's role
and permissions, the access level of this connection, the plan limits, and
the areas that the connection can use. If the selected channel is not the
user's target, ask them to select the correct channel in the Connect flow
before any write. With read-only access, you can review but not save.

KickBot must be a moderator in the channel for most chat features. If it is
not, ask the streamer to type `/mod KickBot` in their Kick chat, then call
`check_moderator_status`. Use `refresh_kick_data` after the streamer changes
their name, picture, or stream link on Kick.

## Setup review

Call `get_channel_activity` for the last 30 days. It shows which features are
on, use per feature, top commands and TTS voices, the busiest day, when the
TTS widget was last open, and public links. Then read the settings of the
areas that matter to the user.

Give a short list of suggestions, for example:

- Commands such as !discord or !socials, and a timed message for socials.
- Chat alerts that thank new followers and subscribers.
- Text-to-speech, alerts, and overlays that are on but not open in OBS.
- Moderation filters if chat has spam.

A review does not save anything. Make a change only when the user asks.

## Next steps

Use the matching skill for the work:

| Request | Skill |
| --- | --- |
| Commands, timed messages, chat alerts, chat moderation | kickbot-chatbot |
| On-stream alerts and built-in overlays | kickbot-alerts-overlays |
| Text-to-speech and Auto read | kickbot-tts-setup |
| Tip page, tip queue, tip reports | kickbot-tipping |
| AI character and !imagine | kickbot-ai-chat |
| !clip, clip and VOD downloads | kickbot-clips-vods |
| Custom HTML, CSS, and JavaScript widgets | kickbot-widget-builder |

If a tool returns `limit_reached` or `premium_required`, tell the user what is
blocked and do not retry. Changes apply to the live channel at once.

Reference: https://docs.kickbot.com/dashboard/api
