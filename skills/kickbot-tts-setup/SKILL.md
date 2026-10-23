---
name: kickbot-tts-setup
description: Set up or troubleshoot KickBot text-to-speech for a Kick stream, including voices, command access, moderation, Auto read, and the OBS browser source.
---

# KickBot TTS setup

Read `get_account_overview`, `get_tts_settings`, `list_tts_voices`, and the
settings for the requested TTS feature. Respect the connected channel's
permissions, verification state, and plan limits. If the connection is missing,
use the host's KickBot Connect flow. Do not request credentials in chat.

## Settings and voices

Use `update_tts_settings` to change only the requested fields. Account
verification is required. `global_tts_volume` is from 0 to 1; cooldowns use
seconds from 0 to 120; `global_tts_max_chars` is from 0 to 300; `tts_delay` uses
seconds from 0 to 30. Messages over the length limit are blocked, not cut off.

Use `list_tts_library_voices` and `list_tts_library_filters` to find an existing
voice. `add_tts_voice` starts a new voice enabled for everyone. Add a voice
only when the user asks to make it available. Then use `update_tts_voice` to
apply the requested command and role access. Do not enable all voices as a
shortcut. Premium may be required for a voice or feature.

For automatic chat reading, use `get_auto_read_settings`,
`update_auto_read_settings`, and the Auto read rule tools. Do not use the
deprecated `auto_tts` or `auto_tts_voice` fields in `update_tts_settings`; the
old voice field also turns on reading for everyone.

## Moderation and OBS

Read `get_tts_moderation_settings` before changing filters. List fields replace
the whole list. Keep existing entries that the user did not ask to remove.
Do not clear the live queue, skip a message, or remove a voice unless that is
part of the user's request.

`get_tts_settings` returns the TTS widget URL and information about when it was
last open. Give the URL to the user privately and explain how to add it as an
OBS browser source. Do not put it in a public widget, repository, or example.
A settings change does not prove that OBS is open or that audio played.

Read settings and voices back after changes. Report the saved state and what
the user must check in OBS. If asked to clone a voice, use the dedicated voice
cloning flow and obtain the required consent for that voice. A request to add
a library voice does not grant consent to clone one.

Reference: https://docs.kickbot.com/dashboard/api/reference/tts
