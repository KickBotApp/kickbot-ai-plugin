---
name: kickbot-alerts-overlays
description: Set up Kick stream alerts and OBS overlays with KickBot. Use for follower, subscriber, and gifted sub alerts on stream, alert sounds, images, and videos, test alerts, and the chat box, pinned message, emote spawner, viewer count, follower count, and last subscriber overlays.
---

# KickBot alerts and overlays

Read `get_account_overview` first. If the connection is missing, use the
host's KickBot Connect flow. Do not request credentials in chat.

This skill is for alerts on stream: an animation with text, media, and sound
in OBS. If the user means messages that KickBot posts in Kick chat, use the
chat alerts part of the chatbot skill. Ask when the request is not clear.

## Alert overlay

Read `get_alert_overlay_settings`. It returns one overlay URL for all alert
types and one URL for each type. Use `update_alert_overlay_settings` for one
alert type at a time.

For a custom image, video, or sound, call `create_alert_media_upload`, upload
the file with HTTP PUT exactly as the response describes, then set `file_url`
as `media_url` or `audio_url`. Do not invent file URLs.

`test_overlay_alert` plays on the live overlay. Viewers see it if the overlay
is in the stream. Ask before you test while the streamer is live.

## Other overlays

Use `list_overlays` to find the chat box, pinned message, emote spawner,
viewer count, follower count, and last subscriber overlays. Each has a
`get_*_overlay_settings` and `update_*_overlay_settings` pair (the emote
spawner uses `get_emote_spawner_settings`). They work with defaults before any
change. For a custom design, use the widget builder skill.

## OBS

Tell the user to add the overlay URL as a Browser Source in OBS, Streamlabs, or
another streaming app. Settings show after the browser source reloads. Treat
overlay URLs as private. Do not post them in public places.

Read the settings back after each change and report the saved state. A saved
setting does not prove that OBS shows the overlay.

Reference: https://docs.kickbot.com/dashboard/api/reference/overlays
